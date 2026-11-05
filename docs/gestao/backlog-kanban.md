# LabControl 4.0 - Organização do Backlog e Diretrizes do Quadro Kanban

**Identificador da Entrega:** `[S4][GP-04]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/gestao/backlog-kanban.md`  
**Disciplina / Área:** Gestão de Projetos  
**Responsável:** Giovani Miamoto (@giovanimiamotob)  
**Issue de Referência:** [#4](https://github.com/labControl4-0/labcontrol-docs/issues/4)  
**Projeto Centralizado:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  

---

## 1. Visão do Fluxo de Trabalho (Kanban Multi-Repositório)

O LabControl 4.0 é composto por múltiplos repositórios (`labcontrol-api`, `labcontrol-web`, `labcontrol-mobile`, `labcontrol-iot`, `labcontrol-docs`). Para garantir visibilidade integral e controle de gargalos, todo o trabalho é centralizado no **GitHub Project 3** no nível da organização `labControl4-0`.

### 1.1 Estados e Colunas do Fluxo de Valor

```
+----------------+      +---------------+      +-------------------+      +-----------------+      +------------+
| 1. Product     |  ->  | 2. Ready for  |  ->  | 3. In Progress    |  ->  | 4. In Review    |  ->  | 5. Done    |
|    Backlog     |      |    Dev        |      |    (WIP Limit: 5) |      |    (WIP: 3)     |      |            |
+----------------+      +---------------+      +-------------------+      +-----------------+      +------------+
        ^                                                                          |                     |
        |                                                                          v                     |
        +---------------------------- [ Bloqueado / Devolução ] <------------------+                     v
                                                                                           [ Evidência Validada ]
```

---

## 2. Políticas Explícitas por Etapa (Critérios de Entrada e Saída)

### Coluna 1: Product Backlog
- **Critério de Entrada:** Ideia ou requisito catalogado com título claro, descrição de escopo preliminar e estimativa de prioridade (`P0`, `P1`, `P2`).
- **Política de Saída:** Passa por refinamento técnico da equipe para validar dependências e decomposição em critérios verificáveis.

### Coluna 2: Ready for Dev (Pronto para Iniciar / DoR)
- **Definição de Pronto para Iniciar (DoR):**
  1. A issue possui responsável explicitamente atribuído (`Assignee`).
  2. As dependências técnicas diretas foram sanadas ou identificadas como mocks/stubs acordados.
  3. Há critérios de aceite objetivos expressos em checkboxes Markdown (`- [ ]`).
  4. Há definição clara do artefato final (caminho do arquivo, endpoint REST, PR de código ou documento).

### Coluna 3: In Progress (Em Desenvolvimento)
- **Limite de Trabalho em Andamento (WIP Limit):** **Máximo de 1 a 2 tarefas simultâneas por integrante (total máximo = 5 a 7 tarefas em andamento)**.
- **Regras:**
  - Criação obrigatória de branch vinculada seguindo o padrão de nomenclatura (ex: `feature/BE-04-autenticacao`, `docs/GOV-02-raci`).
  - Commits incrementais com mensagens descritivas no padrão [Conventional Commits](https://www.conventionalcommits.org/).

### Coluna 4: In Review / Quality Assurance (Revisão e Teste)
- **Limite de WIP:** Máximo de 3 itens simultâneos.
- **Regras:**
  - Pull Request formal aberto apontando para a branch base (`develop` ou `main`).
  - Passagem verde nos testes automatizados e builds de CI (GitHub Actions).
  - Revisão técnica obrigatória por pelo menos 1 outro membro da equipe (`Approved`).
  - Para artefatos de documentação: verificação ortográfica, checagem de links e conformidade de formatação.

### Coluna 5: Done (Concluído / DoD)
- **Definição de Concluído (DoD):**
  1. Todos os critérios de aceite do card estão checados (`- [x]`).
  2. O código ou documento foi mergeado na branch base e está no repositório oficial.
  3. As evidências (screenshots de testes, logs de execução sanitizados ou links de arquivos) estão anexadas como comentário de encerramento na issue.
  4. Nenhuma credencial ou segredo foi exposto nos commits.

---

## 3. Classificação e Taxonomia de Rastreabilidade

### Prioridades Padronizadas
- `prioridade: P0` - **Crítico / Caminho Crítico:** Bloqueia outras entregas ou é requisito mandatório da avaliação acadêmica (ex: Autenticação, CI, Governança Base, EAP).
- `prioridade: P1` - **Alto Valor:** Funcionalidades principais do sistema (ex: Fila offline mobile, telemetria MQTT, observabilidade).
- `prioridade: P2` - **Desejável / Melhoria:** Refinamentos de UX, animações secundárias e otimizações adicionais.

### Tipos de Atividade
- `tipo: planejamento` - EAP, Termo de Abertura, Backlog, Metodologia.
- `tipo: documentação` - Planos, runbooks, catálogos de risco e relatórios em PDF.
- `tipo: infraestrutura` - Docker Compose, pipelines de CI, configurações de rede e broker.
- `tipo: segurança` - Modelagem de ameaças, varreduras DAST/SAST, pentest e remediação.
- `tipo: integração` - Conexões entre frontends, mobile, broker MQTT e backend.
- `tipo: teste` - Testes automatizados unitários, e2e, usabilidade e carga.

---

## 4. Rastreabilidade Inter-Repositórios e Convenções Git

Para manter o histórico rastreável entre repositórios:
1. **Branch Naming:** `<tipo>/<ID-CARD>-<descricao-curta>`  
   *Exemplo:* `feature/MOB-03-sqlite-fila-offline`, `fix/BE-08-mqtt-payload`, `docs/GP-02-escopo-eap`.
2. **Commit Message:** `<tipo>(<escopo>): <descrição no imperativo>`  
   *Exemplo:* `feat(mobile): implement offline sync queue using SQLite (MOB-03)`.
3. **Fechamento de Issues:** No corpo do Pull Request, vincular a issue explicitamente:  
   `Closes labControl4-0/labcontrol-docs#2` ou `Resolves #4`.
