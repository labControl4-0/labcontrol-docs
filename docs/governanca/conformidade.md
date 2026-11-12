# LabControl 4.0 - Políticas de Dados, Acesso, Credenciais e Licenças

**Identificador da Entrega:** `[S4][GOV-05]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/governanca/conformidade.md` + `docs/governanca/.env.example`  
**Disciplina / Área:** Governança de TI  
**Responsável:** Victor Geroto (@victorgeroto)  
**Issue de Referência:** [#13](https://github.com/labControl4-0/labcontrol-docs/issues/13)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  
**Status:** Rascunho v0.1 (2026-11-11) — retenções e responsáveis são **propostas**; depende de SEC-01 (#18) para a parte de segredos versionados

---

## 1. Princípios

1. **Minimização:** coletar apenas o que uma funcionalidade realmente usa.
2. **Finalidade explícita:** todo dado tem origem, propósito e prazo de guarda registrados.
3. **Menor privilégio:** cada pessoa/serviço acessa só o necessário.
4. **Nenhum segredo no repositório**, nem no plano nem em evidências.
5. **Dados de demonstração e de teste são sintéticos.**

Estado verificado em 2026-11-11 nas `main` (docs `1a2a30e`, api `84da384`, web `6b2e6b6`, mobile `ff07943`, iot `56c166e`).

---

## 2. Inventário e Classificação de Dados

Classificação: **Segredo** (compromete o sistema se vazar), **Pessoal** (identifica alguém), **Interno** (operacional), **Público**.

| Dado | Onde fica | Origem | Finalidade | Classe | Proteção atual / necessária |
| :--- | :--- | :--- | :--- | :---: | :--- |
| Nome, e-mail e hash de senha do usuário | PostgreSQL (`Users`) | Cadastro | Autenticação e identificação | **Pessoal** | Hash da senha; hoje o login em uso usa SHA-256 sem salt — ver risco R-05; BCrypt previsto no novo backend (BE-04) |
| Token de sessão (JWT, 2 h) | Cliente (web: `localStorage`; mobile: `AsyncStorage`, `expo-secure-store` em PR #12) | Login | Sessão | **Segredo** | Expiração curta; armazenamento seguro no mobile (MOB-02, PR aberto) |
| Chave de assinatura do JWT | Configuração da API | Equipe | Assinar tokens | **Segredo** | Somente variável de ambiente; **valor de desenvolvimento versionado hoje** — trocar (ver 5) |
| Chave da API de IA e credenciais de banco/broker | Variáveis de ambiente | Equipe | Integrações | **Segredo** | Somente variáveis de ambiente ou *secret store*; ver 5 |
| Estrutura da planta (plantas, setores, máquinas) | PostgreSQL | Usuário | Planta baixa | Interno | Isolamento por usuário na API |
| Telemetria (temperatura, vibração, rpm, energia) | MQTT → PostgreSQL | Sensores / simulador | Monitoramento | Interno | Sintética em demonstração; broker sem autenticação hoje (IOT-02) |
| Eventos e alertas de máquinas | PostgreSQL | Sistema / usuário | Histórico | Interno | — |
| Pergunta do chat + contexto (plantas, máquinas, eventos abertos) | Enviado a provedor externo (Google Gemini) | Usuário / banco | Respostas do assistente | Interno (pode conter dados que o usuário digitar) | Orientar a não digitar dados pessoais; ver P-09 |
| Dados da pesquisa com usuários (NEG-02) | `docs/negocio/validacao.md` | Participantes | Validação de valor | Pessoal (anonimizado) | Codificação por perfil; TCLE simplificado; sem identificação |
| Dump de banco para demonstração | Repositório da API (arquivo de dump) | Equipe | Reproduzir ambiente | A classificar | **Deve ser sintético**; conteúdo será verificado em SEC-01 |
| Logs | Contêineres | Sistema | Diagnóstico | Interno | Sem senhas, tokens ou dados pessoais (padrão em `operacao/servico.md` §3.2) |
| Backups | Local controlado (ver `docs/rollback.md`, GOV-07) | Equipe | Recuperação | Herda a classe da origem | Fora do Git; descarte conforme retenção |

---

## 3. Avaliação do CPF Citado no SAGA

| Pergunta | Resposta |
| :--- | :--- |
| O que o SAGA prevê? | Cadastro com "CPF ou identificador institucional", cargo e função ([`documentoSAGA.md`](../../Sprints/entrega01/documentoSAGA.md) §3.2) |
| O que o sistema coleta hoje? | A API de cadastro recebe **nome, e-mail e senha**; **CPF e cargo não são coletados** |
| Alguma funcionalidade implementada precisa de CPF? | **Não** |
| Decisão proposta | **Não coletar CPF** (necessidade não demonstrada). Se houver identificação institucional, usar um campo opcional sem valor documental. Registrar uma nota no SAGA de que o campo foi removido do escopo |
| Base | Princípios de necessidade e minimização da LGPD (Lei 13.709/2018) |
| Pendência | Aprovação da equipe e eventual nota no SAGA |

---

## 4. Políticas

| ID | Política | Objetivo | Responsável (proposto) | Verificação | Evidência esperada |
| :---: | :--- | :--- | :--- | :--- | :--- |
| P-01 | **Minimização** de dados pessoais | Coletar somente nome, e-mail e senha | Victor Geroto | Revisar DTOs/formulários a cada mudança de cadastro | Contratos de API e telas sem CPF/cargo |
| P-02 | **Origem e finalidade** documentadas | Todo dado do inventário (seção 2) com origem e propósito | Victor Geroto | Revisão do inventário a cada marco | Seção 2 atualizada |
| P-03 | **Retenção e descarte** | Não guardar além do necessário | Victor Geroto | Conferir descarte no fim do semestre | Registro de descarte |
| P-04 | **Acesso por menor privilégio** | Cada recurso acessível somente ao titular/perfil autorizado | Carlos Eduardo | Testes de autorização (BE-04/05; SEC-05) | Testes automatizados verdes |
| P-05 | **Credenciais e segredos** fora do Git | Zero segredos reais versionados | Victor Geroto + Carlos Eduardo | Varredura de segredos no CI de todos os repositórios | CI verde; relatório SEC-01 |
| P-06 | **Dados sintéticos** em demonstração | Nada de dados reais em dumps, evidências ou vídeos | Equipe | Revisão de dumps e evidências antes de mesclar | Checklist de PR marcado |
| P-07 | **Dependências e licenças** | Conhecer e respeitar as licenças | Victor Geroto | Inventário (seção 6) atualizado a cada marco | Seção 6 + ferramenta de licenças |
| P-08 | **Acessibilidade** | Interface legível por quem usa luvas ou luz forte | André Fernandes / Gustavo Silveira | Contraste mínimo WCAG AA (4,5:1 para texto) e alvos de toque ≥ 48×48 dp | Checagem em WEB-06 e MOB-08 (decisões de NEG-02) |
| P-09 | **Terceiros** (IA) | Saber o que sai do sistema | Carlos Eduardo | Revisar o conteúdo enviado ao provedor | Descrição do contexto do chat (seção 2) |

**Retenção proposta (a validar):** dados de demonstração apagados ao fim do semestre; logs por até 30 dias; backups por até 7 dias (alinhado ao RPO de `docs/rollback.md`); conta de usuário de teste removida junto com os dados do ambiente.

---

## 5. Credenciais e Segredos

### 5.1 Regras

1. Segredos entram **somente por variáveis de ambiente** (ou *secret store*/GitHub Actions Secrets).
2. O arquivo `.env` **nunca** é versionado; cada repositório que o use deve ter `.env` no `.gitignore` e um **`.env.example`** com valores fictícios. O modelo está em [`.env.example`](.env.example).
3. **Remover um arquivo do repositório não revoga a credencial.** Se um segredo real foi versionado, ele deve ser **revogado e substituído**, e o histórico do Git deve ser considerado comprometido (SEC-01).
4. Chaves de desenvolvimento nunca são reutilizadas em demonstração ou produção.
5. Evidências (logs, capturas, relatórios) são sanitizadas: tokens, IPs reais e senhas mascarados ([`acordos-equipe.md`](../gestao/acordos-equipe.md) §3.2).

### 5.2 Verificação automática

- **Existe hoje:** step de varredura em `docs/` no CI de documentação (padrões de senha literal, token `ghp_` e chave privada).
- **Falta:** varredura de segredos em api, web, mobile e iot (hoje sem CI). Proposta: ferramenta de varredura (por exemplo `gitleaks`) como etapa obrigatória do CI de cada repositório e como *pre-commit* opcional.

### 5.3 Resposta a um segredo exposto

1. Revogar/rotacionar a credencial no provedor (não apenas apagar o arquivo).
2. Avaliar uso indevido (cota, acessos) e registrar o incidente (SEV conforme `operacao/servico.md`).
3. Remover do rastreamento e corrigir `.gitignore`; decidir sobre reescrita de histórico.
4. Atualizar o inventário (seção 2) e o relatório SEC-01.

---

## 6. Dependências e Licenças

Fonte: `package-lock.json` (campo `license`) das dependências diretas de web e mobile; demais itens pelos manifestos do repositório. O que está marcado "a confirmar" deve ser checado com ferramenta antes do fechamento.

| Componente | Dependências diretas | Licenças | Situação |
| :--- | :---: | :--- | :--- |
| `labcontrol-web` | 71 | MIT (67); Apache-2.0 (`@playwright/test`, `typescript`); **2 sem campo no lockfile** (`class-variance-authority`, `lucide-react`) | **A confirmar** os 2 sem licença no lockfile |
| `labcontrol-mobile` | 33 | MIT (32); Apache-2.0 (`typescript`) | Verificado no lockfile |
| `labcontrol-api` (NuGet) | 8 pacotes (ex.: BCrypt.Net-Next, Npgsql EF Core, MQTTnet, Swashbuckle, JwtBearer, EF Core Design) | Não consta no repositório | **A confirmar** (`nuget.org` ou ferramenta de licenças do .NET) |
| `labcontrol-iot` | Eclipse Mosquitto, Node-RED, `paho-mqtt` 1.6.1 | Não consta no repositório | **A confirmar** na documentação de cada projeto |
| Imagens base | PostgreSQL 15, `eclipse-mosquitto:2.0`, `nodered/node-red`, Node, nginx, .NET | Definidas pelos provedores | **A confirmar** |

**Licença do próprio projeto:** há arquivo `LICENSE` em `labcontrol-docs`, `labcontrol-api` e `labcontrol-mobile`; **não há** em `labcontrol-web` e `labcontrol-iot`. Ação proposta: adicionar a mesma licença aos dois.

**Obrigações a respeitar:** manter os avisos de copyright e o texto da licença das dependências redistribuídas (MIT/Apache-2.0); preservar `NOTICE` quando existir. **Nenhuma restrição incompatível foi identificada nas licenças já verificadas.**

Comandos de apoio (a executar pela equipe):

```bash
# web e mobile: licenças de todas as dependências
npx license-checker --summary
# api: licenças dos pacotes NuGet
dotnet tool install --global dotnet-project-licenses
dotnet-project-licenses -i .
```

---

## 7. Dados de Demonstração

- Contas de teste usam o domínio reservado `example.test` (ex.: `operador01@example.test`).
- Máquinas, plantas e telemetria são geradas por simulador; nenhuma medição real de cliente.
- Antes de mesclar qualquer dump/evidência, marcar a caixa "Nenhum segredo, token, senha ou dado sensível exposto" do checklist de PR ([`mudancas-ci.md`](mudancas-ci.md) §2.1).

---

## 8. Critérios de Aceite (issue #13)

| Critério | Situação |
| :--- | :--- |
| Políticas possuem objetivo, responsável, verificação e evidência | Atendido na estrutura (seção 4); **responsáveis a validar** e evidências a coletar |
| Dados de demonstração são sintéticos | **Regra definida** (seção 7); verificação do dump existente depende de SEC-01 |
| Coleta dispensável é removida ou justificada | **Proposta**: CPF não coletado (seção 3) — falta aprovação e nota no SAGA |
| Documentar origem, finalidade, necessidade, retenção e proteção; avaliar minimização e licenças | Atendido (seções 2, 3, 4 e 6); licenças marcadas "a confirmar" |
| Nenhuma credencial real ou dado sigiloso no repositório ou no plano | Atendido **neste documento**; a situação dos demais repositórios é objeto de SEC-01 |

---

## 9. Histórico de Alterações

| Versão | Data | Autor | Alteração |
| :--- | :--- | :--- | :--- |
| 0.1 | 2026-11-11 | @victorgeroto | Inventário de dados, políticas P-01 a P-09, avaliação do CPF, inventário de licenças e `.env.example` |
