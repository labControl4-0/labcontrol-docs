# LabControl 4.0 - Registro e Controle de Mudanças

**Identificador da Entrega:** `[S4][GP-07]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/gestao/mudancas.md`  
**Disciplina / Área:** Gestão de Projetos  
**Responsável:** Victor Geroto (@victorgeroto)  
**Issue de Referência:** [#7](https://github.com/labControl4-0/labcontrol-docs/issues/7)  
**Status:** Rascunho v0.1 (2026-11-11) — **MUD-001 e MUD-002 aguardam aprovação; nenhuma está verificada**

---

## 1. Fluxo de uma Mudança

```
 Solicitação -> Análise de impacto -> Aprovação -> Execução -> Verificação -> Encerramento
 (quem pede)    (escopo, prazo,       (nível 1/2/3   (issue/PR)  (evidência)    (registro aqui)
                 custo, recursos,      conforme RACI)
                 riscos, qualidade)
```

Quem aprova (conforme [`partes-interessadas-raci.md`](../governanca/partes-interessadas-raci.md) §3 e [`mudancas-ci.md`](../governanca/mudancas-ci.md) §1.1):

| Tipo de mudança | Decisão | Aprovação |
| :--- | :--- | :--- |
| Ajuste interno, documentação | Nível 1 | Revisão no PR (1 aprovação de outra pessoa) |
| Contrato de API, schema, protocolo, arquitetura | Nível 2 | Documentada na issue, aprovação de 2 membros envolvidos |
| Datas de entrega, inclusão/exclusão de pacotes da EAP, infraestrutura | Nível 3 | Consenso da equipe + alinhamento com o docente |

---

## 2. Índice de Mudanças

| ID | Título | Tipo | Nível | Situação | Solicitada em | Aprovada em | Verificada em |
| :--- | :--- | :--- | :---: | :--- | :--- | :--- | :--- |
| MUD-001 | Migração do backend de .NET 9 para Java 21 / Spring Boot 3 | Arquitetura / escopo | 3 | **Análise de impacto preenchida; decisão pendente (BE-01 aberta)** | semestre atual (objetivo estratégico no EAP) | *pendente* | *pendente* |
| MUD-002 | Alinhar caminhos de entregáveis entre EAP e issues | Documentação | 1 | **Proposta** | 2026-11-11 | *pendente* | *pendente* |

---

## 3. MUD-001 — Migração do Backend para Spring Boot

**Solicitação.** O EAP (§1.1) estabelece como objetivo do semestre a transição da API legada (.NET 9) para Java 21 / Spring Boot 3, com JPA e PostgreSQL. A decisão de *como* migrar é a issue BE-01 (`labcontrol-api#67`), ainda aberta.

**Análise de impacto** (dados de 2026-11-11):

| Dimensão | Impacto |
| :--- | :--- |
| **Escopo** | 10 issues (BE-01 a BE-10), de entidades JPA a autenticação, CRUD, sincronização, push, ingestão MQTT e corte de API. Funcionalidades hoje em .NET precisam de paridade ou exclusão explícita |
| **Prazo** | 94 h em um único responsável; 86 h são P0. É o provável caminho crítico: BE-10 bloqueia REL-01 e BE-02 bloqueia GOV-07 e SEC-03 |
| **Custo / recursos** | Sem custo financeiro direto; consome 94 h de uma pessoa e exige JDK 21 e ambiente de testes |
| **Riscos** | Regressão de contratos de API usados por web e mobile; perda ou inconsistência de dados na troca; atraso em cascata (ver riscos R-01, R-06 em GOV-03) |
| **Qualidade** | Exige testes de compatibilidade (BE-10) e revalidação de segurança sobre o novo backend (SEC-03/SEC-05) |
| **Alternativa** | Manter o .NET e endurecê-lo, liberando 94 h para outras frentes — **não avaliada formalmente; deve ser registrada em BE-01** |

**Aprovação.** Pendente. Por ser mudança de arquitetura de API (Nível 2) com impacto em prazo (Nível 3), registrar: decisão, quem aprovou, data e alinhamento com o docente.

| Decisão | Responsável | Data | Evidência |
| :--- | :--- | :--- | :--- |
| ☐ Aprovada  ☐ Rejeitada  ☐ Adiada | *a preencher* | __/__/____ | link da issue/ata |

**Verificação (após a execução).** Paridade de rotas documentada; testes de compatibilidade (BE-10) verdes; REL-01 executada sobre o backend novo. **Pendente.**

---

## 4. MUD-002 — Alinhar Caminhos de Entregáveis (EAP × Issues)

**Solicitação (2026-11-11, @victorgeroto).** A tabela do [`escopo-eap.md`](escopo-eap.md) §3 indica caminhos de entregáveis diferentes dos que as issues S4 definem em "Entregáveis e evidências". Exemplos:

| Card | Caminho no EAP | Caminho na issue |
| :--- | :--- | :--- |
| GP-05 | `docs/gestao/metodologia-agil.md` | `docs/gestao/metodologia.md` |
| GP-07 | `docs/gestao/controle-sprints.md` | `docs/gestao/sprints/` + `docs/gestao/mudancas.md` |
| GOV-01 | `docs/governanca/plano-base.md` | `docs/plano-governanca-ti.md` |
| GOV-03 | `docs/governanca/riscos-respostas.md` | `docs/riscos.md` |
| GOV-05 | `docs/governanca/politicas-acesso-dados.md` | `docs/governanca/conformidade.md` + `.env.example` |
| GOV-07 | `docs/governanca/backup-rollback.md` | `docs/rollback.md` + `docs/evidencias/recuperacao/` |
| SEC-03 | `docs/seguranca/escopo-pentest.md` | `docs/seguranca/escopo-metodologia.md` |

**Análise de impacto.** Escopo: nenhum. Prazo e custo: ~15 min. Risco: avaliadores não encontrarem o artefato pelo caminho do EAP. Qualidade: melhora a rastreabilidade.

**Proposta.** Tratar os caminhos das **issues** como oficiais (são o critério de aceite) e atualizar a tabela do EAP em um PR de documentação (Nível 1). **Aprovação e verificação pendentes.**

---

## 5. Modelo para Novas Mudanças

```markdown
## MUD-NNN — Título
**Solicitação:** quem, quando, motivo
**Análise de impacto:** escopo | prazo | custo | recursos | riscos | qualidade
**Alternativas consideradas:**
**Decisão (nível 1/2/3):** aprovada / rejeitada / adiada — por quem, quando, evidência
**Execução:** issue/PR
**Verificação:** evidência de que o resultado foi alcançado
**Encerramento:** data e lições
```

---

## 6. Critérios de Aceite (issue #7) — Situação

| Critério | Situação |
| :--- | :--- |
| Uma mudança real percorre solicitação, análise de impacto, aprovação e verificação | **Parcial** — MUD-001 e MUD-002 têm solicitação e análise; **aprovação e verificação pendentes** |
| Registrar mudança real com impacto em escopo, prazo, custos, recursos, riscos e qualidade | Atendido para MUD-001 (seção 3) |
| Monitorar realizado × planejado e manter decisões, revisões e retrospectivas | Ver [`sprints/README.md`](sprints/README.md); atas da Sprint 4 pendentes |

---

## 7. Histórico de Alterações

| Versão | Data | Autor | Alteração |
| :--- | :--- | :--- | :--- |
| 0.1 | 2026-11-11 | @victorgeroto | Fluxo, MUD-001 (migração Spring) e MUD-002 (caminhos EAP × issues) |
