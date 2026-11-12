# LabControl 4.0 - Acompanhamento de Sprints (Planning, Review, Retrospectiva)

**Identificador da Entrega:** `[S4][GP-07]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/gestao/sprints/README.md`  
**Disciplina / Área:** Gestão de Projetos  
**Responsável:** Victor Geroto (@victorgeroto)  
**Issue de Referência:** [#7](https://github.com/labControl4-0/labcontrol-docs/issues/7)  
**Status:** **Estrutura pronta; atas de Sprint 4 ainda não realizadas** — nada aqui comprova execução de cerimônias que não ocorreram.

---

## 1. Como usar esta pasta

1. A cada sprint, copiar o modelo da seção 4 para `sprint-NN.md` **no dia do evento** (planning, review, retrospectiva), preenchendo o que realmente ocorreu.
2. Atualizar o quadro de acompanhamento (seção 2) ao final de cada sprint com dados do GitHub Project 3.
3. Mudanças de escopo, prazo, custo ou qualidade vão para [`../mudancas.md`](../mudancas.md), com link para a ata onde foram discutidas.
4. Não apagar linhas de base: replanejamentos entram como nova linha com data.

Metodologia, cadência e papéis propostos: `docs/gestao/metodologia.md` (GP-05).

---

## 2. Quadro de Acompanhamento — Realizado × Planejado (Sprint 4)

Linha de base lida em 2026-11-11 (fonte: issues S4; detalhes em `docs/gestao/cronograma-custos.md`, GP-03).

| Data do registro | Issues concluídas / total | Horas concluídas / total | % de horas | Observações |
| :--- | :---: | :---: | :---: | :--- |
| 2026-11-11 (linha de base) | 14 / 60 | 89 h / 425 h | 21% | Concluídas: 14 issues de `labcontrol-docs` (Giovani). Nenhuma issue de BE, WEB, MOB ou IOT concluída |
| *próximo registro* | | | | |

Como coletar: `gh issue list -R labControl4-0/<repo> --state all --search "[S4] in:title" --json number,title,state`, somando as estimativas de cada corpo de issue.

---

## 3. Sprints Registradas

| Sprint | Período | Meta | Ata | Situação |
| :--- | :--- | :--- | :--- | :--- |
| Sprint 1 | semestre anterior | Fundação: backend, banco, arquitetura, design e documentação | [`entregaSprint01.md`](../../../Sprints/entrega01/entregaSprint01.md) (Review, Retrospectiva e Planning) | Registrada |
| Sprint 2 | semestre anterior | Arquitetura em nuvem e MVP | [`arquiteturaAws.md`](../../../Sprints/entrega02/arquiteturaAws.md) | Sem ata de cerimônias no repositório |
| Sprint 4 | *a definir (depende do prazo docente)* | Marcos M1–M6 de GP-03 | *a criar* | **Planning ainda não registrado** |

---

## 4. Modelo de Ata de Sprint

```markdown
# Sprint NN — Ata (planning | review | retrospectiva)

- Data / duração real:
- Participantes (presentes / ausentes):
- Meta da sprint:

## Planning
- Issues selecionadas (ID, responsável, horas):
- Capacidade informada por integrante (h):
- Riscos e dependências identificados:

## Review
- Incrementos demonstrados (link de PR/commit/evidência):
- Issues aceitas / não aceitas e motivo:
- Realizado × planejado (horas, issues):

## Retrospectiva
- O que funcionou:
- O que não funcionou:
- Ações (máx. 3) com responsável e prazo:

## Bloqueios e decisões
- Bloqueio | causa | responsável | situação
- Decisão | nível (1, 2 ou 3) | quem decidiu

## Mudanças geradas
- IDs em docs/gestao/mudancas.md:
```

---

## 5. Critérios de Aceite (issue #7) — Situação

| Critério | Situação |
| :--- | :--- |
| Uma mudança real percorre solicitação, análise de impacto, aprovação e verificação | **Em andamento** — ver MUD-001 em [`../mudancas.md`](../mudancas.md): análise de impacto preenchida, aprovação e verificação pendentes |
| Atas cobrem os marcos executados | **Pendente** — só a Sprint 1 tem ata; Sprint 4 ainda não executou cerimônias |
| Monitorar realizado × planejado | Estrutura pronta (seção 2); atualizar a cada sprint |
