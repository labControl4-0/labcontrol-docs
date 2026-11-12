# LabControl 4.0 - Registro de Riscos e Planos de Resposta

**Identificador da Entrega:** `[S4][GOV-03]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/riscos.md`  
**Disciplina / Área:** Governança de TI  
**Responsável:** Victor Geroto (@victorgeroto)  
**Issue de Referência:** [#11](https://github.com/labControl4-0/labcontrol-docs/issues/11)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  
**Status:** Rascunho v0.1 (2026-11-11) — **donos e prazos são propostas; aceite de risco residual pendente**

---

## 1. Método

- **Probabilidade (P)** e **Impacto (I)** de 1 a 5. **Score = P × I**.
- **Nível:** Alto (≥ 15), Médio (8 a 14), Baixo (≤ 7).
- **Estratégias:** Eliminar, Mitigar, Transferir, Aceitar.
- **Risco residual:** estimativa após a resposta. Só é considerado **aceito** com registro formal (seção 5); só é considerado **tratado** com evidência real vinculada.
- **Prazos** usam os marcos M1–M6 de `docs/gestao/cronograma-custos.md` (GP-03); datas de calendário dependem da confirmação do prazo docente.
- Ameaças técnicas detalhadas (STRIDE/DREAD) ficam em [`seguranca/modelagem-ameacas.md`](seguranca/modelagem-ameacas.md); este registro as conecta ao ciclo de gestão do projeto.
- Estado verificado em 2026-11-11 nas `main` dos 5 repositórios (docs `1a2a30e`, api `84da384`, web `6b2e6b6`, mobile `ff07943`, iot `56c166e`).

---

## 2. Registro de Riscos

| ID | Risco | Causa | P | I | Score | Nível |
| :---: | :--- | :--- | :---: | :---: | :---: | :---: |
| R-01 | Atraso ou falha na migração do backend (.NET → Spring Boot) | 10 issues (94 h) em um único responsável; nenhuma branch Spring iniciada; BE-10 bloqueia a homologação | 4 | 5 | 20 | **Alto** |
| R-02 | Credenciais e dados sensíveis versionados em repositório público | Arquivos de configuração e de dados rastreados no repositório de API (inventário em SEC-01); histórico do Git pode reter valores mesmo após remoção | 5 | 5 | 25 | **Alto** |
| R-03 | Mudanças sem revisão e sem verificação automática nos repositórios | Proteção de branch desativada nos 5 repositórios; só `labcontrol-docs` tem workflow de CI | 5 | 3 | 15 | **Alto** |
| R-04 | Telemetria falsificada ou broker explorado por acesso anônimo | Mosquitto com `allow_anonymous true` na `main` (IOT-02 aberta) | 4 | 4 | 16 | **Alto** |
| R-05 | Controle de acesso incompleto em parte dos endpoints da API atual | Rotas sem exigência de autenticação ou sem checagem de titularidade (ver SEC-02/THR-01) | 4 | 4 | 16 | **Alto** |
| R-06 | Perda ou duplicidade de dados na troca de backend e na sincronização offline | Mudança de modelo/ORM, sincronização idempotente ainda não implementada (BE-06, MOB-04) | 3 | 4 | 12 | Médio |
| R-07 | Push notification inviável a tempo | Depende de Android físico, *development build* e serviço externo (MOB-05/06) | 3 | 3 | 9 | Médio |
| R-08 | Ambiente de demonstração sem backup e recuperação comprovados | GOV-07 aberta; sem teste de restauração registrado | 3 | 4 | 12 | Médio |
| R-09 | Estouro de cronograma | 76% das horas abertas são P0; capacidade não confirmada; cadeia de dependências até REL-01 | 4 | 4 | 16 | **Alto** |
| R-10 | Custo ou cota de serviços externos (IA, nuvem) fora de controle | Chave de API exposta (R-02) ou uso sem limite; titularidade/custo do host de nuvem não levantados | 3 | 3 | 9 | Médio |
| R-11 | Status declarados nos documentos divergem do estado real dos repositórios | Controles descritos como implementados antes do PR/commit mesclado; ver seção 4 | 4 | 4 | 16 | **Alto** |
| R-12 | Dependência de pessoa única por frente | Backend (94 h) com 1 pessoa; mobile + IoT (88 h) com 1 pessoa | 3 | 4 | 12 | Médio |
| R-13 | Coleta de dados pessoais além do necessário (LGPD) | O SAGA cita CPF e cargo no cadastro; a API atual não os coleta | 2 | 3 | 6 | Baixo |
| R-14 | Prazo da banca, rubrica de Negócios/eletiva e escopo dos testes de segurança sem confirmação | Informações docentes pendentes (EAP §5; NEG-01/03) | 3 | 3 | 9 | Médio |
| R-15 | Teste de segurança executado fora de ambiente autorizado | Escopo e ambiente ainda não formalizados (SEC-03 aberta) | 2 | 5 | 10 | Médio |
| R-16 | Credenciais em documentos do repositório de docs | Cópia acidental de tokens/senhas em evidências | 2 | 4 | 8 | Médio |

---

## 3. Respostas, Donos e Situação

| ID | Estratégia | Ação de resposta | Gatilho / contingência | Dono (proposto) | Prazo | Situação | Residual esperado |
| :---: | :---: | :--- | :--- | :--- | :---: | :--- | :---: |
| R-01 | Mitigar | Decidir BE-01 cedo (registrar em MUD-001); definir paridade mínima de rotas; congelar BE-09 (P1); revisão cruzada de PRs | Sem branch Spring com BE-02 até o fim de M1 → manter .NET na demonstração e registrar a alternativa | Carlos Eduardo | M1 | Aberto | 3 × 4 = 12 |
| R-02 | Eliminar / Mitigar | SEC-01: inventariar e classificar sem reproduzir valores; remover do rastreamento; **revogar/rotacionar** credenciais confirmadas (remover arquivo não revoga); `.env.example`; varredura de segredos nos repositórios de código | Qualquer credencial confirmada → tratar como comprometida e rotacionar imediatamente | Victor Geroto (SEC-01) + Carlos Eduardo | M1 | Aberto | 1 × 5 = 5 |
| R-03 | Mitigar | Habilitar proteção de `main` com 1 aprovação; workflows mínimos (build, lint, testes) em api, web, mobile, iot | PR mesclado sem revisão → registrar em mudanças e revisar a posteriori | Giovani Miamoto (GOV-04) | M1 | Aberto | 2 × 3 = 6 |
| R-04 | Mitigar | IOT-02: autenticação e ACL no Mosquitto; credenciais por variável de ambiente; teste que prova a recusa de conexão anônima | Mensagem inesperada no tópico → revisar o broker | Gustavo Silveira | M2 | Aberto | 2 × 4 = 8 |
| R-05 | Mitigar | Revisar rotas e exigir autenticação/titularidade (BE-04 no Spring ou correção no .NET); teste automatizado de autorização | Achado confirmado em SEC-05 → mudança emergencial | Carlos Eduardo | M2 | Aberto | 2 × 4 = 8 |
| R-06 | Mitigar | Sincronização idempotente (BE-06) e política de conflitos (MOB-04); backup e restauração testados (R-08); dados sintéticos | Duplicidade detectada em REL-01 → issue P0 | Carlos Eduardo / Gustavo Silveira | M3 | Aberto | 2 × 3 = 6 |
| R-07 | Mitigar / Aceitar | Confirmar o dispositivo Android cedo; plano B: demonstrar com notificação simulada, registrando a limitação | Sem dispositivo ao fim de M2 → ativar plano B | Gustavo Silveira | M2 | Aberto | 2 × 2 = 4 |
| R-08 | Mitigar | Executar e medir restauração e *rollback* (GOV-07, `docs/rollback.md`) | Falha no teste → corrigir procedimento e repetir | Victor Geroto | M4 | Aberto | 2 × 3 = 6 |
| R-09 | Mitigar | Capacidade e estimativas revisadas (GP-03); ordem de corte P2 → P1; replanejamento em `docs/gestao/mudancas.md` | % de horas concluídas abaixo do esperado em duas sprints | Victor Geroto | contínuo | Aberto | 3 × 3 = 9 |
| R-10 | Mitigar | Rotacionar chaves (R-02); definir limite de cota; levantar custo e titularidade do host de nuvem (GP-03) | Consumo acima do limite → desativar chave | Victor Geroto | M1 | Aberto | 2 × 2 = 4 |
| R-11 | Mitigar | Reconciliar "declarado × verificado" (seção 4); vincular cada controle a PR/commit mesclado; adotar a regra "planejamento não comprova implementação" | Novo documento afirmando implementação sem link verificável → bloquear no review | Giovani Miamoto (GOV-08) + Victor Geroto | M1 | Aberto | 2 × 3 = 6 |
| R-12 | Mitigar | Revisão cruzada obrigatória; documentar decisões; usar capacidade disponível (hoje sem issues abertas para Giovani) | Bloqueio > 12 h → escalar (RACI §4) | Equipe / facilitador | contínuo | Aberto | 2 × 3 = 6 |
| R-13 | Eliminar | Decisão: **não coletar CPF** nem dados dispensáveis (GOV-05); dados de demonstração sintéticos | Nova exigência de campo pessoal → reavaliar necessidade | Victor Geroto | M1 | Aberto | 1 × 3 = 3 |
| R-14 | Mitigar | Confirmar prazo e rubricas com o docente; manter itens pendentes explícitos | Resposta tardia → replanejar via mudança | Victor Geroto | M1 | Aberto | 2 × 2 = 4 |
| R-15 | Eliminar | SEC-03: autorização formal do grupo, ambiente próprio, lista de exclusões e critérios de interrupção antes de qualquer teste | Alvo fora da lista → interromper | Victor Geroto | M1 | Aberto | 1 × 5 = 5 |
| R-16 | Mitigar | Verificação automática de segredos em `docs/` no CI; regra de sanitização de evidências | Falha do workflow → bloquear o PR | Giovani Miamoto | — | **Tratado (parcial)** | 1 × 4 = 4 |

---

## 4. Reconciliação: Status Declarado × Verificado (origem do risco R-11)

Esta tabela **não atribui responsabilidade**: corrige o registro para que os documentos reflitam o estado real. Verificação em 2026-11-11 (API do GitHub e leitura das `main`).

| Item | Onde está declarado | Declarado | Verificado |
| :--- | :--- | :--- | :--- |
| Proteção da branch `main` | `governanca/mudancas-ci.md` §2; matriz CTL-03 | Implementado | **Desativada** nos 5 repositórios (`protected=false`) |
| Revisão obrigatória por outra pessoa | `governanca/mudancas-ci.md` §2 | Implementado | PRs #30, #31 e #32 de docs: **0 revisões**; autor e quem mesclou são a mesma pessoa |
| CI padronizado por repositório | `governanca/mudancas-ci.md` §3.2–3.4 | Descrito como padrão | **Só `labcontrol-docs` tem workflow**; api, web, mobile e iot não |
| Armazenamento seguro no mobile (CTL-09) | `governanca/matriz-controle-evidencia.md` | Implementado (PR #12) | **PR #12 aberto**; MOB-02 aberta |
| Fila offline SQLite (CTL-10) | idem | Implementado (PR #13) | **PR #13 aberto**; MOB-03 aberta |
| Broker sem acesso anônimo e com ACL | Plano consolidado (HTML) §5 | Controle implementado | **`allow_anonymous true`**; IOT-02 aberta |
| RBAC com Spring Security | Plano consolidado (HTML) §5; `seguranca/modelagem-ameacas.md` | Implementado | BE-04 aberta; **sem código Spring** nos repositórios |
| Logs JSON com mascaramento (CTL-07) | `operacao/servico.md` §3 | Implementado | Padrão **apenas documentado**; a API usa o log padrão do ASP.NET |
| Endpoints do runbook (`/health`, `/api/v1/sync`) | `operacao/servico.md` §4 | Em procedimento | **Inexistentes** na API da `main` (previstos para a nova versão) |
| Metas de disponibilidade e latência | `operacao/servico.md` §1 | SLA | **Metas**, sem medição registrada |
| Plano consolidado (CTL-12) | matriz | Implementado | PDF/HTML existem; **fonte Markdown** é entregue em GOV-01 |

**Ação proposta:** atualizar a matriz (GOV-08) e o plano consolidado com uma coluna **"Evidência verificada (PR/commit mesclado)"** e usar os rótulos *Existe na main*, *Em PR aberto* e *Planejado*.

---

## 5. Evidência de Tratamento e Aceite de Risco Residual

### 5.1 Risco tratado com evidência real — R-16

- **Controle:** step `Secret Leak Prevention Scan` em `.github/workflows/ci.yml` (`grep` por senhas literais, tokens `ghp_` e chaves privadas em `docs/`).
- **Evidência:** workflow *CI - Docs Quality & Compliance* com **6 execuções bem-sucedidas** entre 2026-11-05 e 2026-11-09 (3 em `main` e 3 em branches de PR).
- **Limitação (motivo do residual):** cobre apenas `docs/` e poucos padrões; não vale para os demais repositórios.

### 5.2 Aceite de risco residual — **pendente**

Nenhum risco residual foi aceito formalmente até agora. Registrar abaixo quando a equipe decidir:

| Risco | Residual aceito | Justificativa | Quem aceitou | Data | Evidência |
| :--- | :--- | :--- | :--- | :--- | :--- |
| *ex.: R-16* | 1 × 4 = 4 | Cobertura do scan limitada a `docs/`; demais repositórios tratados em R-02 | *a preencher* | __/__/____ | link da issue/ata |

---

## 6. Revisão do Registro

- **Quando:** no início de cada sprint (planning) e sempre que um gatilho ocorrer.
- **Como:** atualizar P/I/situação, registrar a data e, se o risco se materializar, abrir uma mudança em `docs/gestao/mudancas.md` (GP-07).
- **Quem:** dono do risco propõe; a equipe valida no alinhamento semanal.

---

## 7. Critérios de Aceite (issue #11)

| Critério | Situação |
| :--- | :--- |
| Cada risco tem causa, impacto, probabilidade, resposta, responsável, situação e risco residual | Atendido neste rascunho (donos e prazos a validar) |
| Ao menos um risco tratado e um residual aceito possuem evidência real | **Parcial** — R-16 tratado com evidência (5.1); **nenhum residual aceito ainda** (5.2) |
| Incluir migração, perda de dados, sincronização, push, credenciais, MQTT, custos, indisponibilidade e atraso | Atendido (R-01, R-06, R-07, R-02, R-04, R-10, R-08, R-09) |

---

## 8. Histórico de Alterações

| Versão | Data | Autor | Alteração |
| :--- | :--- | :--- | :--- |
| 0.1 | 2026-11-11 | @victorgeroto | Registro inicial com 16 riscos, reconciliação de status e evidência de R-16 |
