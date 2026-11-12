# LabControl 4.0 - Escolha de Metodologia e Comparativo de Ferramentas Ágeis

**Identificador da Entrega:** `[S4][GP-05]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/gestao/metodologia.md`  
**Disciplina / Área:** Gestão de Projetos  
**Responsável:** Victor Geroto (@victorgeroto)  
**Issue de Referência:** [#5](https://github.com/labControl4-0/labcontrol-docs/issues/5)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  
**Status:** Rascunho v0.1 (2026-11-11) — **proposta sujeita à concordância da equipe**
**Continuidade:** atividade do semestre anterior em [`labcontrol-api#29`](https://github.com/labControl4-0/labcontrol-api/issues/29) (estrutura Scrum), mantida; este documento detalha a evolução do 4º semestre.

---

## 1. Contexto de Decisão

| Fator | Situação do LabControl 4.0 (PI-IV) |
| :--- | :--- |
| Equipe | 5 integrantes, com frentes separadas (backend, web, mobile + IoT, governança/segurança, planejamento) |
| Trabalho | 60 issues em 5 repositórios; 336 h abertas em 2026-11-11 (ver `docs/gestao/cronograma-custos.md`, GP-03) |
| Requisitos | Relativamente estáveis (EAP e rubricas docentes), mas com **dependências em cadeia** (migração do backend → homologação) |
| Entrega | Incrementos verificáveis por evidência e demonstração integrada (REL-01/02) |
| Prazo | Banca ainda não confirmada; precisa de replanejamento barato |
| Já em uso | Quadro Kanban no GitHub Project 3 com limites de WIP ([`backlog-kanban.md`](backlog-kanban.md)), acordos e ritos ([`acordos-equipe.md`](acordos-equipe.md)), Sprint Review/Retrospective/Planning na Sprint 1 ([`entregaSprint01.md`](../../Sprints/entrega01/entregaSprint01.md)) |

---

## 2. Comparativo das Seis Abordagens

Escala de adequação: **Alta**, **Média**, **Baixa** (julgamento do autor para este contexto; deve ser discutido com a equipe).

| Abordagem | Ideia central | Adequação ao projeto | Custo de adoção | Limitações para este projeto |
| :--- | :--- | :---: | :--- | :--- |
| **Scrum** | Sprints com planning, daily, review e retrospectiva; papéis PO, SM e time | **Alta** | Médio: exige cerimônias e papéis | Cerimônias podem pesar numa equipe pequena com horário limitado; sem prática de engenharia prescrita |
| **Kanban** | Fluxo contínuo, limites de WIP, políticas explícitas | **Alta** | Baixo: o quadro e os limites já existem | Sem cadência/meta de iteração; exige disciplina para não acumular itens |
| **XP (Extreme Programming)** | Práticas de engenharia: integração contínua, revisão/pareamento, testes, refatoração, entregas pequenas | **Alta (como práticas complementares)** | Médio: exige CI e testes | Pouco prescreve sobre gestão e planejamento; hoje **não há CI nos repositórios de código** |
| **FDD (Feature-Driven Development)** | Desenvolvimento por funcionalidades com modelo global e listas de features | **Média** | Médio-alto: modelagem global e papéis específicos (chief programmers) | Pensado para equipes maiores; o escopo já está decomposto em EAP/issues |
| **MSF (Microsoft Solutions Framework)** | Modelos de equipe e de processo com governança e gestão de riscos | **Média** | Alto: vocabulário e artefatos próprios | Peso documental alto; sobrepõe o que a Governança de TI já cobre |
| **DSDM (Dynamic Systems Development Method)** | Prazo fixo, escopo flexível (MoSCoW), envolvimento do usuário | **Média-alta (como técnica)** | Médio | O MoSCoW já aparece como prioridades P0/P1/P2; framework completo é excessivo |

---

## 3. Decisão Proposta

**Scrum como estrutura de cadência, Kanban como sistema visual de fluxo e práticas de XP como disciplina de engenharia**, usando MoSCoW (via P0/P1/P2) para definir o que cortar se o prazo apertar.

| Elemento | Origem | Como se aplica ao LabControl |
| :--- | :--- | :--- |
| Sprint com meta e revisão | Scrum | Metas por marco (M1–M6 em GP-03); review e retrospectiva registradas em `docs/gestao/sprints/` (GP-07) |
| Quadro com colunas e WIP | Kanban | GitHub Project 3: *Product Backlog → Ready for Dev → In Progress → In Review → Done* |
| Integração contínua e revisão por par | XP | PR obrigatório com revisão; CI nos repositórios (ver 5) |
| Entregas pequenas, testes | XP | Branches por card; testes automatizados em WEB-08, BE-05 e MOB-09 |
| Prioridade `P0/P1/P2` | DSDM (MoSCoW) | P0 = obrigatório; P1 = importante; P2 = desejável (corte primeiro) |

**Por que não as demais por inteiro:** FDD e MSF acrescentam papéis e artefatos que a equipe não tem capacidade de sustentar; DSDM completo é redundante com o que Scrum + Kanban + prioridades já entregam. O critério de aceite não exige executar as seis metodologias.

---

## 4. Cerimônias, Papéis e Duração das Sprints

> Valores abaixo são **proposta**. A duração depende do calendário docente (a confirmar) e os papéis dependem da concordância da equipe.

### 4.1 Cadência

| Item | Proposta | Observação |
| :--- | :--- | :--- |
| Duração da sprint | **2 semanas** | Se restarem menos de 6 semanas até a banca, usar sprints de 1 semana |
| Planning | Início da sprint, até 1 h | Seleciona issues, confirma DoR e estimativas; define a meta |
| Check-in assíncrono | Diário ou bidiário | Já previsto em [`acordos-equipe.md`](acordos-equipe.md) §2.2 |
| Alinhamento semanal | 30–45 min | Já previsto; inspeciona o quadro, bloqueios e riscos |
| Review | Fim da sprint, até 45 min | Demonstra o incremento e coleta evidências |
| Retrospectiva | Fim da sprint, até 30 min | Gera até 3 ações, registradas na ata |

### 4.2 Papéis

| Papel | Responsabilidade | Atribuição |
| :--- | :--- | :--- |
| **Product Owner** | Prioriza o backlog e valida aceite em nome do usuário | *a definir pela equipe* |
| **Scrum Master / facilitador** | Conduz cerimônias, remove bloqueios, cuida do quadro | *a definir pela equipe (a Sprint 1 já adicionou um Scrum Master ao quadro)* |
| **Time de desenvolvimento** | Entrega as issues com evidência | Os 5 integrantes |
| **Docente orientador** | Valida escopo e prazo (decisões de Nível 3) | Docentes do PI-IV |

### 4.3 Limites de WIP

Conforme [`backlog-kanban.md`](backlog-kanban.md): máximo de 1 a 2 tarefas por integrante em *In Progress* (5 a 7 no total) e 3 em *In Review*.

---

## 5. Práticas de Engenharia Adotadas (XP) e Estado Atual

| Prática | Estado verificado em 2026-11-11 | Ação |
| :--- | :--- | :--- |
| Integração contínua | Existe CI apenas em `labcontrol-docs`; **não há workflows em api, web, mobile e iot** | Criar pipelines mínimos (build, lint, testes) — alinhado a GOV-04 |
| Revisão por par | Política documentada; **proteção de branch desativada nos 5 repositórios** e os PRs #30–32 de docs foram mesclados sem revisão | Habilitar proteção de `main` com 1 aprovação obrigatória |
| Testes automatizados | Web tem só um teste de exemplo; WEB-08 prevê testes úteis | Cumprir WEB-08, BE-05, MOB-09 |
| Entregas pequenas | Branches por card (`<tipo>/<ID>-<descricao>`) e PR com `Closes #N` | Manter |

---

## 6. Tratamento de Mudanças, Bloqueios e Evidências

| Situação | Regra |
| :--- | :--- |
| **Mudança de escopo/prazo** | Registrar em `docs/gestao/mudancas.md` (GP-07), com análise de impacto, aprovação conforme o nível de decisão do [RACI](../governanca/partes-interessadas-raci.md) e verificação |
| **Bloqueio** | Comentar na issue com a causa e o responsável; escalonamento conforme RACI §4 (12 h → weekly → docente) |
| **Evidência** | Comentário de encerramento com links de PR/commit, testes e demonstração sanitizada (DoD de [`acordos-equipe.md`](acordos-equipe.md) §4.2) |
| **Replanejamento** | Atualizar a linha de base de `docs/gestao/cronograma-custos.md` (GP-03) sem apagar o histórico |

---

## 7. Registro de Uso Real e Trabalho Colaborativo

Evidências já existentes (a ampliar a cada sprint):

| Evidência | Onde |
| :--- | :--- |
| Sprint Review, Retrospectiva e Planning da Sprint 1 | [`Sprints/entrega01/entregaSprint01.md`](../../Sprints/entrega01/entregaSprint01.md) |
| Quadro Kanban com prioridades e responsáveis | [GitHub Project 3](https://github.com/orgs/labControl4-0/projects/3) |
| Issues com critérios de aceite, dependências e refinamento | `labcontrol-docs`, `-api`, `-web`, `-mobile`, `-iot` |
| PRs de documentação | `labcontrol-docs` #30, #31, #32 (autoria e merge pela mesma pessoa; sem revisão registrada) |
| PRs de mobile abertos aguardando revisão | `labcontrol-mobile` #11 a #16 |

**A registrar nas próximas sprints:** atas de planning/review/retrospectiva em `docs/gestao/sprints/`, revisões cruzadas nos PRs e a redução do tempo em *In Review*.

---

## 8. Critérios de Aceite (issue #5)

| Critério | Situação |
| :--- | :--- |
| Justificativa compara as seis abordagens | Atendido (seção 2) |
| Cerimônias, papéis e duração das sprints definidos | **Proposto** — pendente de confirmação da equipe (seção 4) |
| Registrar uso real e trabalho colaborativo | Parcial (seção 7); evolui a cada sprint |

---

## 9. Histórico de Alterações

| Versão | Data | Autor | Alteração |
| :--- | :--- | :--- | :--- |
| 0.1 | 2026-11-11 | @victorgeroto | Comparativo, proposta de metodologia e práticas |
