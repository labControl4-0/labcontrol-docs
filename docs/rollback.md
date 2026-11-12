# LabControl 4.0 - Backup, Recuperação e Rollback

**Identificador da Entrega:** `[S4][GOV-07]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/rollback.md` + `docs/evidencias/recuperacao/`  
**Disciplina / Área:** Governança de TI  
**Responsável:** Victor Geroto (@victorgeroto)  
**Issue de Referência:** [#15](https://github.com/labControl4-0/labcontrol-docs/issues/15)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  
**Status:** Procedimento **proposto**; **nenhum teste de restauração ou rollback foi executado** — os números de RPO/RTO abaixo são metas a acordar, não resultados medidos

---

## 1. Escopo e Dependências

| Item | Situação |
| :--- | :--- |
| Dados a proteger | Banco PostgreSQL do LabControl (usuários, plantas, setores, máquinas, métricas e eventos) |
| Configuração a proteger | `docker-compose.yml` de cada módulo, `mosquitto.conf`, fluxos do Node-RED, variáveis de ambiente (fora do Git) |
| Dependências da issue | **BE-02** (aplicação Spring reproduzível — ainda aberta) e **GOV-04** (CI/mudanças — concluída) |
| Ambiente de teste | Apenas dados sintéticos; nunca o ambiente real do docente ou de terceiros |

**Ponto de atenção verificado (2026-11-11):** no `docker-compose.yml` da API (commit `84da384`) o serviço do PostgreSQL **não declara volume**. Os dados vivem na camada do container: remover ou recriar o container (`docker compose down`, troca de imagem) **apaga o banco**. Antes de qualquer demonstração, definir um volume nomeado ou garantir backup recente.

---

## 2. Objetivos de Recuperação (a acordar com a equipe e o docente)

| Objetivo | Proposta | Justificativa | Acordado em |
| :--- | :--- | :--- | :--- |
| **RPO** (perda máxima de dados) | **≤ 24 h** em ambiente de demonstração; backup **antes** de cada deploy/migração | Dados são sintéticos e recriáveis; custo baixo | *pendente* |
| **RTO** (tempo máximo para voltar) | **≤ 60 min** para restaurar o banco e subir a versão identificada | Procedimento manual com Docker em ambiente único | *pendente* |
| Retenção de backups | 7 dias (ver `docs/governanca/conformidade.md`) | Coerente com o RPO e a minimização | *pendente* |

---

## 3. Backup

> Substitua `<usuario-db>` pelo usuário do banco (variável `POSTGRES_USER`/connection string do `.env` local). Nomes de container e banco vêm do compose da API: container `labcontrol_db`, banco `labcontroldb`.

```bash
# 1. Identificar a versão em execução (registrar no relatório do teste)
git -C labcontrol-api rev-parse --short HEAD

# 2. Gerar o backup em formato custom do pg_dump
STAMP=$(date +%Y%m%d_%H%M)
docker exec labcontrol_db pg_dump -U <usuario-db> -Fc -f /tmp/labcontrol_$STAMP.dump labcontroldb

# 3. Copiar para fora do container (pasta fora do Git: backups/)
mkdir -p backups && docker cp labcontrol_db:/tmp/labcontrol_$STAMP.dump backups/

# 4. Registrar o hash de integridade do arquivo
sha256sum backups/labcontrol_$STAMP.dump        # PowerShell: Get-FileHash <arquivo> -Algorithm SHA256
```

Regras: a pasta `backups/` **não vai para o Git** (adicionar ao `.gitignore`); arquivos com dados nunca entram em `docs/evidencias/`; só tempos, contagens e hashes.

---

## 4. Restauração em Banco de Teste

```bash
T0=$(date +%s)

# 1. Criar um banco vazio para o teste (não sobrescrever o original)
docker exec labcontrol_db createdb -U <usuario-db> labcontroldb_restore

# 2. Restaurar
docker cp backups/labcontrol_<STAMP>.dump labcontrol_db:/tmp/restore.dump
docker exec labcontrol_db pg_restore -U <usuario-db> -d labcontroldb_restore --no-owner /tmp/restore.dump

T1=$(date +%s); echo "RTO do banco (s): $((T1-T0))"
```

### 4.1 Verificação de integridade

Rodar **no original e no restaurado** e comparar:

```sql
SELECT 'Users' AS tabela, count(*) FROM "Users"
UNION ALL SELECT 'Plants', count(*) FROM "Plants"
UNION ALL SELECT 'Sectors', count(*) FROM "Sectors"
UNION ALL SELECT 'Machines', count(*) FROM "Machines"
UNION ALL SELECT 'MachineMetrics', count(*) FROM "MachineMetrics"
UNION ALL SELECT 'MachineEvents', count(*) FROM "MachineEvents";

-- Registros órfãos (devem retornar 0)
SELECT count(*) FROM "Machines" m LEFT JOIN "Plants" p ON p."Id" = m."PlantId" WHERE p."Id" IS NULL;
SELECT count(*) FROM "MachineMetrics" x LEFT JOIN "Machines" m ON m."Id" = x."MachineId" WHERE m."Id" IS NULL;
SELECT count(*) FROM "MachineEvents" x LEFT JOIN "Machines" m ON m."Id" = x."MachineId" WHERE m."Id" IS NULL;
```

Execução: `docker exec labcontrol_db psql -U <usuario-db> -d <banco> -c "<consulta>"`.

**Verificação funcional:** apontar uma instância da API para o banco restaurado (`ConnectionStrings__DefaultConnection`), autenticar com a conta de teste e listar plantas/máquinas.

**RPO medido:** horário da falha simulada − horário do registro mais recente presente no banco restaurado.

---

## 5. Rollback de Versão

### 5.1 Identificação da versão

Toda versão implantada deve ser identificável por **tag Git ou SHA** e pela **imagem** usada (`git describe --tags` ou `git rev-parse --short HEAD`; `docker image ls`). Registrar a versão *antes* e *depois* de cada mudança.

### 5.2 Procedimento (código e contêineres)

```bash
# Voltar a versão anterior identificada
git -C labcontrol-api checkout <tag-ou-sha-anterior>
docker compose -f labcontrol-api/docker-compose.yml up -d --build
```

Repetir para web, mobile (build) e iot quando a mudança envolver esses módulos.

### 5.3 Compatibilidade de schema (regra obrigatória)

- **Voltar o código não reverte automaticamente as migrações do banco.** A API aplica migrações ao iniciar (`Database.Migrate()`); hoje existe uma única migração (`InitialCreate`).
- Antes de qualquer deploy que altere o schema: **backup (seção 3)**.
- Para reverter o schema há duas opções, escolhidas por mudança: **restaurar o backup pré-deploy** (perde dados gravados depois) ou **migração reversa** testada (`dotnet ef database update <migração-anterior>` no .NET; mecanismo equivalente a definir no Spring em BE-02/BE-03).
- Preferir mudanças **expandir e depois contrair** (adicionar colunas antes de remover), mantendo as versões N e N−1 compatíveis com o mesmo schema.

---

## 6. Protocolo de Teste e Registro (preencher na execução)

Cada teste gera um arquivo em `docs/evidencias/recuperacao/` (ver o README da pasta) e uma linha aqui.

| ID | Cenário | Versão (SHA/tag) | Executor | Backup (hash) | RTO medido | RPO medido | Integridade (contagens e órfãos) | Resultado |
| :--- | :--- | :--- | :--- | :--- | :---: | :---: | :--- | :--- |
| REC-01 | Restaurar banco em base de teste | *—* | *—* | *—* | *—* | *—* | *—* | **NÃO EXECUTADO** |
| REC-02 | Perda do container do banco e recuperação a partir do backup | *—* | *—* | *—* | *—* | *—* | *—* | **NÃO EXECUTADO** |
| REC-03 | Rollback de versão com compatibilidade de schema | *—* | *—* | *—* | *—* | *—* | *—* | **NÃO EXECUTADO** |

---

## 7. Critérios de Aceite (issue #15)

| Critério | Situação |
| :--- | :--- |
| Recuperação executada com tempo medido e integridade verificada | **Pendente** — procedimento e gabarito prontos; falta executar (REC-01 a REC-03) |
| Voltar código não é declarado como reversão automática de migração | Atendido (seção 5.3) |
| Demonstrar restore/rollback com versão identificável, responsáveis, tempos e verificação | **Pendente** — depende da execução; a parte do Spring depende de BE-02 |
| RPO/RTO acordados | **Pendente** — metas propostas na seção 2 |

---

## 8. Histórico de Alterações

| Versão | Data | Autor | Alteração |
| :--- | :--- | :--- | :--- |
| 0.1 | 2026-11-11 | @victorgeroto | Procedimento de backup/restauração/rollback, metas propostas e gabarito de testes |
