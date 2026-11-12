# Homologação Integrada — Plano, Roteiro e Registro (REL-01)

**Identificador da Entrega:** `[S4][REL-01]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/evidencias/homologacao/`  
**Disciplina / Área:** Entrega integrada  
**Responsável:** Victor Geroto (@victorgeroto) — com Giovani Miamoto (RACI: REL-01/02)  
**Issue de Referência:** [#28](https://github.com/labControl4-0/labcontrol-docs/issues/28)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  
**Status:** **Plano e roteiro prontos; homologação NÃO executada** (2026-11-11). Nenhum resultado abaixo foi obtido — todas as etapas estão como "Não executada".

---

## 1. Pré-requisitos (bloqueios)

A homologação só deve começar quando as dependências da issue estiverem concluídas e integradas na mesma versão:

| Dependência | Issue | Situação em 2026-11-11 |
| :--- | :--- | :--- |
| Corte de API / compatibilidade | BE-10 (`labcontrol-api#76`) | **Aberta** |
| Fluxo mobile completo | MOB-09 (`labcontrol-mobile#10`) | **Aberta** |
| Testes úteis do web | WEB-08 (`labcontrol-web#8`) | **Aberta** |
| Ambiente Docker e docs IoT unificados | IOT-04 (`labcontrol-iot#4`) | **Aberta** |
| Correção e reteste de segurança | SEC-06 (`labcontrol-docs#23`) | Concluída |

**Estado atual:** a `main` ainda não contém várias capacidades que o roteiro exercita (fila offline, push, sincronização, central de alertas). O roteiro abaixo é o **alvo**; não execute etapas cujo recurso ainda não esteja mesclado.

---

## 2. Ambiente e Versões (preencher na execução)

| Item | Valor |
| :--- | :--- |
| Data / executores | *a preencher* |
| Ambiente | Docker Compose único (mesma rede `labcontrol-network`), dados sintéticos |
| Versão API | *SHA/tag* |
| Versão Web | *SHA/tag* |
| Versão Mobile (build) | *SHA/tag + tipo de build* |
| Versão IoT | *SHA/tag* |
| Dispositivo Android | *modelo e versão do sistema* |
| Contas de teste | ao menos **dois usuários sintéticos** (`usuario-a@example.test`, `usuario-b@example.test`); credenciais fora do Git |
| Backup pré-teste | hash do arquivo (ver `docs/rollback.md`) |

**Critério:** os quatro componentes testados **na mesma versão de ambiente** — registrar o SHA/tag de cada um; trocar qualquer versão invalida a execução.

---

## 3. Roteiro Ponta a Ponta

Fluxo: login → planta → máquina → telemetria → alerta → web → push → clique → ocorrência offline → sincronização; depois isolamento e recuperação.

| # | Etapa | Ação | Resultado esperado | Componentes | Evidência a anexar | Status |
| :---: | :--- | :--- | :--- | :--- | :--- | :---: |
| 1 | Login | Entrar no web e no mobile com `usuario-a` | Sessão iniciada nos dois clientes | web, mobile, API | Captura sanitizada; log sem token | Não executada |
| 2 | Planta | Criar uma planta no web | Planta aparece no web e no mobile | web, API, mobile | Capturas | Não executada |
| 3 | Máquina | Criar setor e máquina no editor | Máquina listada na planta e no mobile | web, API, mobile | Capturas | Não executada |
| 4 | Telemetria | Publicar mensagem no tópico/payload padronizados (IOT-01) para o GUID da máquina | API grava a métrica; valor visível no web | iot, API, web | Mensagem enviada (sem segredos) e consulta resultante | Não executada |
| 5 | Alerta | Publicar valor que ultrapasse o limite (BE-08) | Evento de alerta criado e visível na central de alertas (WEB-05) | iot, API, web | Capturas; registro do evento | Não executada |
| 6 | Push | Aguardar a notificação no dispositivo Android | Push recebido (MOB-05/06) | API, mobile | Foto/captura da notificação | Não executada |
| 7 | Clique | Tocar na notificação | App abre a ocorrência **correta** (payload) | mobile | Vídeo curto ou capturas | Não executada |
| 8 | Ocorrência offline | Ativar modo avião; registrar uma ocorrência no mobile | Registro fica na fila local (MOB-03) | mobile | Capturas | Não executada |
| 9 | Reinício | Reiniciar o app (e a API) com o registro pendente | Registro continua na fila; nada se perde | mobile, API | Capturas/logs sanitizados | Não executada |
| 10 | Sincronização | Reativar a rede | Registro sincroniza **sem duplicidade**; conflitos tratados (MOB-04/BE-06) | mobile, API | Contagem antes/depois | Não executada |
| 11 | Estados | Observar status de telemetria, cache e erro nos clientes | Estados **coerentes** entre web, mobile e API (conectado, sem dados, erro, desatualizado) | web, mobile | Tabela de coerência (seção 4) | Não executada |
| 12 | Isolamento | Entrar com `usuario-b` e tentar ver/alterar dados de `usuario-a` | Acesso negado ou lista vazia; nenhum dado de A vaza | API, web, mobile | Resultado de cada tentativa | Não executada |
| 13 | Recuperação | Restaurar o backup pré-teste e repetir o *smoke* (etapas 1 a 3) | Ambiente volta ao estado anterior e funciona (REC-01 de `docs/rollback.md`) | API, banco | Tempo medido e contagens | Não executada |

---

## 4. Coerência de Status (telemetria, cache, erro)

| Situação | Web | Mobile | API/Banco | Coerente? |
| :--- | :--- | :--- | :--- | :---: |
| Telemetria recente | *—* | *—* | *—* | ☐ |
| Sem telemetria / sensor parado | *—* | *—* | *—* | ☐ |
| API indisponível | *—* | *—* | *—* | ☐ |
| Dado em cache/offline desatualizado | *—* | *—* | *—* | ☐ |
| Erro de autenticação (token expirado) | *—* | *—* | *—* | ☐ |

---

## 5. Registro de Defeitos

Toda falha vira **issue** no repositório do componente, com impacto e responsável:

```markdown
Título: [REL-01][DEF-NN] <resumo>
Etapa do roteiro / execução:
Versões (API / Web / Mobile / IoT):
Resultado esperado × observado:
Impacto (SEV 1 a 4, conforme docs/operacao/servico.md):
Evidência sanitizada:
Responsável sugerido:
```

| Defeito | Etapa | Issue | Impacto (SEV) | Responsável | Situação |
| :--- | :---: | :--- | :---: | :--- | :--- |
| *nenhum registrado — a homologação não foi executada* | | | | | |

---

## 6. Registro de Execuções

| Execução | Data | Versões | Etapas OK / total | Defeitos abertos | Resultado |
| :---: | :--- | :--- | :---: | :---: | :--- |
| *—* | *—* | *—* | *—* | *—* | **Não executada** |

Cada execução gera um arquivo `AAAA-MM-DD-execucao-NN.md` nesta pasta, com o ambiente da seção 2 preenchido, o status de cada etapa e os links das evidências sanitizadas. **Reexecutar após correções**, mantendo o histórico (não sobrescrever execuções anteriores).

---

## 7. Regras de Evidência

- Somente dados sintéticos; capturas e logs **sanitizados** (sem tokens, senhas, IPs reais ou dados de usuários).
- Não versionar bancos, dumps nem arquivos brutos de ferramentas.
- Vincular PRs/commits das versões testadas.
- Concluir a issue **somente** após os critérios abaixo estarem verificados com evidência.

---

## 8. Critérios de Aceite (issue #28)

| Critério | Situação |
| :--- | :--- |
| Teste usa o mesmo ambiente e versão entre repositórios | **Pendente** — registrar na seção 2 |
| Status de telemetria/cache/erro é coerente | **Pendente** — seção 4 |
| Falhas têm issue e impacto | **Pendente** — seção 5 |
| Percorrer login → planta → máquina → telemetria → alerta → web → push → clique → ocorrência offline → sincronização; testar isolamento e recuperação | **Pendente** — roteiro na seção 3 |

---

## 9. Histórico de Alterações

| Versão | Data | Autor | Alteração |
| :--- | :--- | :--- | :--- |
| 0.1 | 2026-11-11 | @victorgeroto | Plano, roteiro de 13 etapas e gabaritos de registro (sem execução) |
