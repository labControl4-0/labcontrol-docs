# LabControl 4.0 - Plano de Governança de TI (Fonte Editável)

**Identificador da Entrega:** `[S4][GOV-01]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/plano-governanca-ti.md`  
**Disciplina / Área:** Governança de TI  
**Responsável (fonte):** Victor Geroto (@victorgeroto) — Responsável pela governança: Giovani Miamoto (@giovanimiamotob)  
**Issue de Referência:** [#9](https://github.com/labControl4-0/labcontrol-docs/issues/9)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  
**Status:** Rascunho v0.1 (2026-11-11) — fonte Markdown do plano; **não substitui o PDF até a equipe validar e o PDF ser regenerado (GOV-08)**

> Este arquivo é a **fonte editável** do plano. Ele parte do conteúdo do [`plano-governanca-ti.html`](plano-governanca-ti.html) (origem do [PDF](plano-governanca-ti.pdf)) e dos documentos de governança, gestão e segurança existentes, e reorganiza tudo nas **12 seções exigidas**. Onde o HTML descrevia um controle como implementado sem evidência verificável, esta fonte usa os rótulos de status da seção 5.1.

---

## 1. Identificação e Versionamento

| Campo | Valor |
| :--- | :--- |
| Título | Plano de Governança de TI — LabControl 4.0 |
| Instituição / curso | UniSENAI Sorocaba — CST em Análise e Desenvolvimento de Sistemas, PI-IV (4º semestre) |
| Equipe | Giovani Miamoto, Victor Geroto, Carlos Eduardo Oliveira, André Fernandes, Gustavo Silveira |
| Versão atual | 0.1 (rascunho) |
| Data | 2026-11-11 |
| Estado verificado | `main` de cada repositório: docs `1a2a30e`, api `84da384`, web `6b2e6b6`, mobile `ff07943`, iot `56c166e` |
| Artefatos derivados | `docs/plano-governanca-ti.html` e `docs/plano-governanca-ti.pdf` (versão consolidada) |

**Regra de versionamento:** esta fonte é atualizada a cada marco (M1–M6 de GP-03); cada mudança entra na tabela da seção 13 e o PDF é regenerado a partir dela. O processo de geração do PDF (hoje feito a partir do HTML) deve ser documentado em GOV-08.

---

## 2. Contexto, Problema e Valor

O LabControl 4.0 é uma plataforma de monitoramento de máquinas, planta baixa interativa, telemetria e alertas para laboratórios e plantas industriais. No PI-IV o projeto entra em continuidade: migração do backend para Spring Boot, mobile offline-first, web com dashboard, broker protegido e governança com evidências.

- Termo de abertura (problema, valor, objetivos mensuráveis e escopo existente × previsto): `docs/gestao/termo-abertura.md` (GP-01).
- Escopo, EAP e catálogo de entregas: [`gestao/escopo-eap.md`](gestao/escopo-eap.md).

**Objetivos de governança do semestre** (do plano original):

1. **Confiabilidade do serviço:** catálogo de serviços, metas de disponibilidade e runbooks.
2. **Rastreabilidade de mudanças:** alterações por Pull Request, com revisão e verificação automática.
3. **Higiene e proteção de dados:** sem segredos versionados; logs sem dados sensíveis.
4. **Responsabilidades claras:** RACI para todas as frentes.

---

## 3. Partes Interessadas

Mapeamento de stakeholders, influência e interesse: [`governanca/partes-interessadas-raci.md`](governanca/partes-interessadas-raci.md) §1. Resumo: docentes avaliadores, operadores industriais, supervisores/gestores de manutenção, equipe de desenvolvimento, auditoria e cibersegurança.

---

## 4. Papéis e Decisões

- **RACI por frente de trabalho:** [`governanca/partes-interessadas-raci.md`](governanca/partes-interessadas-raci.md) §2.
- **Três níveis de decisão:** operacional (desenvolvedor + code review), arquitetura (consenso no PR com 2 membros) e escopo/crítica (equipe + docente) — mesmo documento, §3.
- **Escalonamento:** 12 h entre as partes → votação na weekly → mediação docente — §4.
- **Mudanças:** fluxo e registro em `docs/gestao/mudancas.md` (GP-07).

---

## 5. Políticas e Controles

### 5.1 Rótulos de status usados neste plano

| Rótulo | Significado |
| :--- | :--- |
| **Existe na main** | Há arquivo/configuração mesclado na `main` que comprova o controle (não implica que foi testado em operação) |
| **Em PR aberto** | Implementação existe em PR ainda não mesclado |
| **Planejado** | Há issue/decisão, mas nenhum código mesclado |
| **Não verificado** | Não foi possível confirmar |

### 5.2 Controles e evidências (com reconciliação)

| Controle | Política / objetivo | Dono | Declarado antes | **Status verificado (2026-11-11)** | Evidência |
| :--- | :--- | :--- | :--- | :--- | :--- |
| CTL-01 Escopo e EAP | Escopo rastreável por pacote | Giovani | Implementado | **Existe na main** | [`gestao/escopo-eap.md`](gestao/escopo-eap.md) |
| CTL-02 RACI | Responsabilidades e decisões | Giovani | Implementado | **Existe na main** | [`governanca/partes-interessadas-raci.md`](governanca/partes-interessadas-raci.md) |
| CTL-03 Mudanças e PRs | Branch protegida, 1 revisão, checklist de PR | Giovani | Implementado | Política **existe na main**; **proteção de branch desativada** nos 5 repositórios e PRs #30–32 sem revisão | [`governanca/mudancas-ci.md`](governanca/mudancas-ci.md) |
| CTL-04 CI | Validação automática por commit/PR | Giovani | Implementado | **Existe na main** só em `labcontrol-docs` (6 execuções com sucesso); **api, web, mobile e iot sem workflow** | [`../.github/workflows/ci.yml`](../.github/workflows/ci.yml) |
| CTL-05 Anti-vazamento de segredos | Proibir segredos versionados | Giovani / Victor | Implementado | **Existe na main** para `docs/` (regex); demais repositórios **não cobertos**; inventário em SEC-01 | `ci.yml` (step *Secret Leak Prevention Scan*) |
| CTL-06 Catálogo de serviços e SLA | 4 serviços, severidades e runbooks | Giovani | Implementado | Documento **existe na main**; SLOs são **metas sem medição**; runbook cita rotas inexistentes na API atual | [`operacao/servico.md`](operacao/servico.md) |
| CTL-07 Logs sanitizados | JSON com mascaramento | Giovani | Implementado | **Planejado** (padrão documentado; API usa log padrão do ASP.NET) | [`operacao/servico.md`](operacao/servico.md) §3 |
| CTL-08 Modelagem de ameaças | STRIDE/DREAD | Giovani | Implementado | **Existe na main** (análise); mitigações listadas são **planejadas** | [`seguranca/modelagem-ameacas.md`](seguranca/modelagem-ameacas.md) |
| CTL-09 Armazenamento seguro mobile | Credenciais em armazenamento seguro | Gustavo | Implementado (PR #12) | **Em PR aberto** (PR #12, MOB-02) | `labcontrol-mobile` PR #12 |
| CTL-10 Fila offline SQLite | Operar sem rede | Gustavo | Implementado (PR #13) | **Em PR aberto** (PR #13, MOB-03) | `labcontrol-mobile` PR #13 |
| CTL-11 Rede IoT dedicada | Broker e Node-RED em rede Docker própria | Gustavo | Implementado | Rede **existe na main** (compose); broker aceita conexão anônima (`allow_anonymous true`) — **hardening planejado** (IOT-02) | `labcontrol-iot/docker-compose.yml`, `mosquitto.conf` |
| CTL-12 Plano consolidado | PDF para avaliação | Giovani | Implementado | PDF/HTML **existem na main**; esta **fonte Markdown** é nova | [`plano-governanca-ti.pdf`](plano-governanca-ti.pdf) |
| CTL-13 Controle de acesso na API | Autenticação/autorização por rota | Carlos | Implementado (RBAC Spring) | **Planejado** (BE-04); API atual com cobertura parcial | `labcontrol-api` #70; riscos R-05 |
| CTL-14 Broker autenticado com ACL | Sem acesso anônimo | Gustavo | Implementado | **Planejado** (IOT-02) | `labcontrol-iot` #2; risco R-04 |

**Políticas de dados, acesso, credenciais e licenças** (GOV-05): `docs/governanca/conformidade.md` e `.env.example`.

---

## 6. Riscos

- **Registro de riscos, respostas, donos e reconciliação de status:** `docs/riscos.md` (GOV-03) — 16 riscos; 7 de nível alto.
- **Ameaças técnicas (STRIDE/DREAD):** [`seguranca/modelagem-ameacas.md`](seguranca/modelagem-ameacas.md).
- **Principais:** migração do backend (R-01), segredos versionados (R-02), ausência de CI/proteção de branch (R-03), broker anônimo (R-04), controle de acesso parcial (R-05), cronograma (R-09), divergência entre status declarado e real (R-11).

---

## 7. Serviço de TI

Catálogo de serviços, severidades e runbooks: [`operacao/servico.md`](operacao/servico.md).

| Serviço | Protocolo / porta | Meta de disponibilidade | Meta de resposta | Situação da medição |
| :--- | :--- | :---: | :--- | :--- |
| Telemetria e mensageria IoT | MQTT 1883 / WS 9001 | 99,0% | < 500 ms fim a fim | **Meta; não medida** |
| API central e sincronização | REST 8080 | 99,5% | < 300 ms | **Meta; não medida** |
| Portal web | HTTP 80 | 99,0% | < 1,5 s | **Meta; não medida** |
| App mobile | Expo / SQLite | Autônomo offline até 8 h | — | **Meta; depende de MOB-03/04 (PRs abertos)** |

Severidades: SEV 1 (30 min), SEV 2 (2 h), SEV 3 (8 h), SEV 4 (24 h). **Pendência:** o runbook usa rotas como `/health` e `/api/v1/sync`, ainda inexistentes na API da `main`; alinhar após a migração (BE-10).

---

## 8. Indicadores

| Indicador | Meta | Fonte | Valor em 2026-11-11 |
| :--- | :--- | :--- | :--- |
| Issues P0 com evidência vinculada | 100% | Quadro / issues | A medir (14 de 60 issues concluídas; ver GP-03) |
| PRs com revisão de outra pessoa | 100% | GitHub | **0 de 3** PRs de documentação (#30–32) |
| Repositórios com CI | 5 de 5 | `.github/workflows` | **1 de 5** |
| Repositórios com proteção de `main` | 5 de 5 | API do GitHub | **0 de 5** |
| Taxa de sucesso do CI de documentação | 100% | Actions | **6 de 6** execuções (2026-11-05 a 2026-11-09) |
| Segredos reais versionados | 0 | SEC-01 | **A confirmar** (inventário em andamento; ver R-02) |
| Disponibilidade e latência dos serviços | metas da seção 7 | Observabilidade | **Não medido** |
| RPO / RTO | a acordar (GOV-07) | Teste de restauração | **Não testado** |
| Tempo de reconhecimento de falha (MTTA) | < 2 min | NEG-02 | **Reportado em NEG-02**; dados brutos não versionados — tratar como indicativo até a evidência ser anexada |

---

## 9. Continuidade e Recuperação

Procedimentos de backup, restauração e *rollback*, com RPO/RTO propostos e registro de testes: `docs/rollback.md` e `docs/evidencias/recuperacao/` (GOV-07).

**Situação:** procedimento **proposto**, **nenhum teste de recuperação executado**. Princípio: voltar o código para uma versão anterior **não reverte automaticamente** migrações de banco; a compatibilidade de schema deve ser verificada.

---

## 10. Conformidade e Ética

- **LGPD:** minimização de dados; avaliação de CPF e cargo citados no SAGA (decisão proposta: não coletar); dados de demonstração sintéticos — `docs/governanca/conformidade.md` (GOV-05).
- **Pesquisa com usuários:** [`negocio/validacao.md`](negocio/validacao.md) descreve anonimização e termo de consentimento simplificado.
- **Licenças:** inventário das dependências diretas em `docs/governanca/conformidade.md`.
- **Segurança:** testes somente em ambiente próprio e autorizado — `docs/seguranca/escopo-metodologia.md` (SEC-03).

---

## 11. Evidências (rastreabilidade seção → issue → artefato)

| Seção do plano | Issues | Artefato |
| :--- | :--- | :--- |
| 1, 13 Identificação e histórico | GOV-01 (#9) | este arquivo |
| 2 Contexto e valor | GP-01 (#1), GP-02 (#2) | `gestao/termo-abertura.md`, `gestao/escopo-eap.md` |
| 3, 4 Stakeholders, papéis e decisões | GOV-02 (#10), GP-07 (#7) | `governanca/partes-interessadas-raci.md`, `gestao/mudancas.md` |
| 5 Políticas e controles | GOV-04 (#12), GOV-05 (#13), GOV-08 (#16) | `governanca/mudancas-ci.md`, `governanca/conformidade.md`, `governanca/matriz-controle-evidencia.md` |
| 6 Riscos | GOV-03 (#11), SEC-02 (#19) | `riscos.md`, `seguranca/modelagem-ameacas.md` |
| 7 Serviço | GOV-06 (#14) | `operacao/servico.md` |
| 8 Indicadores | GP-03 (#3), GOV-06 (#14), NEG-02 (#26) | `gestao/cronograma-custos.md`, `negocio/validacao.md` |
| 9 Continuidade | GOV-07 (#15) | `rollback.md`, `evidencias/recuperacao/` |
| 10 Conformidade e ética | GOV-05 (#13), SEC-01 (#18), SEC-03 (#20) | `governanca/conformidade.md`, `seguranca/escopo-metodologia.md` |
| 12 Avaliação final | GOV-09 (#17) | `governanca/avaliacao-final.md` |

Matriz de controle e evidências existente: [`governanca/matriz-controle-evidencia.md`](governanca/matriz-controle-evidencia.md) (deve receber a coluna "evidência verificada", conforme `docs/riscos.md` §4).

---

## 12. Avaliação Final

Comparação entre metas e resultados, demonstração de mudança/falha/recuperação e preparação da defesa individual: `docs/governanca/avaliacao-final.md` (GOV-09). **Ainda não executada.**

### 12.1 Rubrica docente e onde cada critério é atendido

| Critério | Peso | Seções deste plano |
| :--- | :---: | :--- |
| Alinhamento e valor | 20% | 2, 3 |
| Responsabilidades e decisões | 15% | 4 |
| Riscos, conformidade e ética | 20% | 6, 10 |
| Controles no repositório | 25% | 5, 11 |
| Indicadores e serviço | 10% | 7, 8 |
| Plano e apresentação | 10% | 1, 12 |

Pontuação do critério = nível (0–4) ÷ 4 × peso.

---

## Anexo A. Itens Não Executados (explícitos)

- Teste de restauração/*rollback* e medição de RPO/RTO (GOV-07).
- Medição de disponibilidade, latência e MTTA em operação.
- Hardening do broker (IOT-02), RBAC no novo backend (BE-04), armazenamento seguro e fila offline no mobile (PRs abertos).
- Proteção de branch, revisão obrigatória e CI nos repositórios de código.
- Inventário e rotação de segredos (SEC-01), exploração controlada de vulnerabilidades (SEC-05) e homologação integrada (REL-01).
- Avaliação final e defesa individual (GOV-09).

---

## 13. Histórico de Alterações

| Versão | Data | Autor | Alteração |
| :--- | :--- | :--- | :--- |
| 0.1 | 2026-11-11 | @victorgeroto | Fonte em Markdown criada a partir do HTML/PDF e dos documentos existentes; status reconciliados; 12 seções |
