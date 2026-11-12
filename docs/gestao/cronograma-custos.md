# LabControl 4.0 - Estimativas, Cronograma, Custos e Recursos

**Identificador da Entrega:** `[S4][GP-03]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/gestao/cronograma-custos.md`  
**Disciplina / Área:** Gestão de Projetos  
**Responsável:** Victor Geroto (@victorgeroto)  
**Issue de Referência:** [#3](https://github.com/labControl4-0/labcontrol-docs/issues/3)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  
**Status:** Rascunho v0.1 (2026-11-11) — **datas e capacidades pendentes de confirmação** (ver seção 7)

---

## 1. Fonte dos Dados e Premissas

- As horas vêm do campo **"Estimativa inicial"** do corpo de cada issue da Sprint 4 (60 issues nos 5 repositórios), lido em 2026-11-11. As issues indicam "revisar com a equipe": **os números são a linha de base inicial, não uma estimativa já revisada**.
- O **realizado em horas não é registrado** nas issues; a coluna "realizado" abaixo permanece em branco até a equipe adotar um registro (proposta na seção 6).
- **Nenhuma data de calendário é fixada neste documento.** O critério de aceite da issue exige confirmar antes o prazo docente; o [EAP](escopo-eap.md) (§5) prevê a homologação integrada **duas semanas antes** do encerramento.

---

## 2. Linha de Base de Esforço (Previsto)

### 2.1 Por frente e situação

| Frente | Issues | Horas previstas | Concluídas (h) | Abertas (h) | Responsável |
| :--- | :---: | :---: | :---: | :---: | :--- |
| Gestão (GP) | 8 | 39 | 17 (GP-02, 04, 06, 08) | 22 | Giovani / Victor |
| Governança (GOV) | 9 | 60 | 28 (GOV-02, 04, 06, 08) | 32 | Giovani / Victor |
| Segurança (SEC) | 7 | 52 | 32 (SEC-02, 04, 06, 07) | 20 | Giovani / Victor |
| Negócios (NEG) | 3 | 14 | 6 (NEG-02) | 8 | Giovani / Victor |
| Entrega (REL) | 2 | 14 | 6 (REL-02) | 8 | Giovani / Victor |
| Backend (BE) | 10 | 94 | 0 | 94 | Carlos Eduardo |
| Web (WEB) | 8 | 64 | 0 | 64 | André |
| Mobile (MOB) | 9 | 64 | 0 | 64 | Gustavo |
| IoT (IOT) | 4 | 24 | 0 | 24 | Gustavo |
| **Total** | **60** | **425** | **89** | **336** | |

### 2.2 Carga aberta por responsável

| Responsável | Issues abertas | Horas abertas | P0 (h) | P1 (h) | P2 (h) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| Victor Geroto | 15 | 90 | 66 | 21 | 3 |
| Carlos Eduardo Oliveira | 10 | 94 | 86 | 8 | 0 |
| Gustavo Silveira | 13 | 88 | 71 | 17 | 0 |
| André Fernandes | 8 | 64 | 32 | 32 | 0 |
| Giovani Miamoto | 0 | 0 | 0 | 0 | 0 |
| **Total** | **46** | **336** | **255** | **78** | **3** |

Leituras úteis: **76% das horas abertas são P0** (255 de 336 h); a carga está concentrada em Carlos e Gustavo; Giovani não tem issues abertas atribuídas (capacidade possível para revisão cruzada — *a confirmar com a equipe*).

---

## 3. Capacidade e Cenários (a preencher)

A capacidade real de cada integrante **não está registrada**. Para visualizar a viabilidade, a tabela mostra quantas semanas cada carga aberta exige conforme as horas semanais dedicadas ao projeto. **São cenários ilustrativos, não capacidade confirmada.**

| Responsável | Horas abertas | 6 h/sem | 8 h/sem | 10 h/sem | Capacidade confirmada (h/sem) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| Victor Geroto | 90 | 15 sem | 12 sem | 9 sem | *a preencher* |
| Carlos Eduardo Oliveira | 94 | 16 sem | 12 sem | 10 sem | *a preencher* |
| Gustavo Silveira | 88 | 15 sem | 11 sem | 9 sem | *a preencher* |
| André Fernandes | 64 | 11 sem | 8 sem | 7 sem | *a preencher* |

*(semanas = horas ÷ capacidade, arredondado para cima)*

**Contingência proposta:** reservar **15%** sobre as horas abertas (≈ 50 h) para retrabalho, bloqueios e revisão — *percentual a validar com a equipe*.

---

## 4. Dependências e Caminho Crítico

Dependências declaradas nas issues (as dependências internas entre BE-01 e BE-10 não foram verificadas aqui):

```
BE-01 -> BE-02 -> ... -> BE-10 ---+
                                  |
MOB-09 --------------------------+--> REL-01 (homologação integrada)
WEB-08 --------------------------+          ^
IOT-04 --------------------------+          |
SEC-06 (concluída) --------------+          |
                                             
BE-02 ---> GOV-07 (backup/rollback)         GP-01 ---> GOV-01, NEG-01
BE-02 ---> SEC-03 (escopo de testes)        GOV-03 ---> SEC-03
```

- **Caminho crítico provável:** migração do backend (BE-01 → BE-02 → … → BE-10) → REL-01. São 94 h em uma única pessoa e 10 issues P0/P1; qualquer atraso aqui atrasa a homologação, GOV-07 e SEC-03.
- **Gargalos de planejamento:** REL-01 depende de quatro frentes ainda abertas; GOV-07 e SEC-03 dependem de BE-02.

---

## 5. Cronograma (marcos, sem datas)

As datas ficam em branco até a confirmação do prazo docente. Os marcos usam **T = data de encerramento/banca (a confirmar)**.

| Marco | Conteúdo | Janela proposta | Data |
| :--- | :--- | :--- | :--- |
| M1 — Fundação | BE-01, BE-02, IOT-01, MOB-01, WEB-01; SEC-01, GOV-05, SEC-03 | início do período restante | *a definir* |
| M2 — Núcleo | BE-03 a BE-05; MOB-02 a MOB-04; IOT-02; WEB-02; GOV-03 | meio do período | *a definir* |
| M3 — Integração | BE-06 a BE-09; MOB-05, MOB-06; WEB-05; IOT-03 | após M2 | *a definir* |
| M4 — Corte e testes | BE-10, MOB-09, WEB-08, IOT-04, GOV-07 | antes da homologação | *a definir* |
| M5 — Homologação | REL-01 | **T − 2 semanas** (EAP §5) | *a definir* |
| M6 — Encerramento | GOV-09, NEG-03, SEC-05 (se confirmada), release | T | *a definir* |

**Regra de replanejamento:** mudar uma data ou o escopo é decisão de Nível 3 (RACI) e deve ser registrada em `docs/gestao/mudancas.md` (GP-07), sem apagar esta linha de base.

---

## 6. Custos e Recursos

### 6.1 Recursos necessários

| Recurso | Para quê | Situação | Custo previsto | Custo realizado |
| :--- | :--- | :--- | :---: | :---: |
| Horas da equipe | Execução das 336 h abertas | Trabalho acadêmico; custo de oportunidade = horas × valor/hora *a definir* | R$ *a definir* | R$ *a registrar* |
| Android físico | *Development build* e push (MOB-05/06) | Disponibilidade *a confirmar* (quem fornece, qual modelo) | R$ *a levantar* | — |
| Nuvem (host da API/banco) | Ambiente de homologação e demonstração | O app mobile referencia um host em nuvem; **titularidade, custo e prazo de vida a confirmar** | R$ *a levantar* | — |
| API de IA (Gemini) | Chat com IA | Uso depende de chave e cota; **a chave deve ser tratada como segredo** (GOV-05) | R$ *a levantar* | — |
| Estações de desenvolvimento | Docker, Node, JDK 21, .NET 9 | Já utilizadas | R$ 0 adicional | — |
| GitHub | Repositórios, Actions, Project | Plano da organização *a confirmar* | R$ *a levantar* | — |

### 6.2 Previsto × realizado

| Indicador | Previsto | Realizado em 2026-11-11 | Observação |
| :--- | :---: | :---: | :--- |
| Issues concluídas | 60 | 14 (23%) | Fonte: quadro |
| Horas concluídas (estimadas) | 425 h | 89 h (21%) | Soma das estimativas das issues fechadas |
| Horas reais gastas | — | *não registrado* | **Proposta:** registrar no comentário de encerramento de cada issue (`Horas reais: N`) |
| Custo financeiro | R$ *a levantar* | R$ *a registrar* | Depende de 6.1 |

---

## 7. Restrição Tripla (Escopo × Prazo × Custo)

```
              ESCOPO
        60 issues / 425 h
          (255 h em P0)
              /\
             /  \
            /    \
        PRAZO ---- CUSTO
   (a confirmar)   (a levantar)
```

- **Escopo fixo, prazo incerto:** com 336 h abertas e capacidade desconhecida, qualquer encurtamento do prazo força corte de escopo.
- **Ordem de corte, se necessário:** primeiro P2 (3 h: NEG-03), depois P1 (78 h: BE-09, MOB-07/08, IOT-04, WEB-03/04/06/07, GP-05/07, GOV-09, NEG-01), **preservando os 255 h de P0** — decisão de Nível 3 com o docente.
- **Custo** tende a ser baixo; o risco financeiro principal é o consumo de serviços externos (nuvem e IA) sem controle de cota.

---

## 8. Critérios de Aceite (issue #3)

| Critério | Situação |
| :--- | :--- |
| Linha de base tem esforço, capacidade, marcos e custos previstos × realizados | **Parcial** — esforço, marcos e previsto × realizado de issues preenchidos; **capacidade e custos aguardam a equipe** |
| Datas são definidas após confirmar o prazo docente | **Pendente** — nenhuma data fixada, de propósito |

**Pendências para concluir a issue:** (1) cada integrante informar capacidade semanal; (2) revisar as estimativas com os responsáveis técnicos; (3) confirmar a data da banca; (4) levantar custos da seção 6.1; (5) validar a contingência de 15%.

---

## 9. Histórico de Alterações

| Versão | Data | Autor | Alteração |
| :--- | :--- | :--- | :--- |
| 0.1 | 2026-11-11 | @victorgeroto | Linha de base de esforço a partir das issues S4; cenários de capacidade; marcos sem datas |
