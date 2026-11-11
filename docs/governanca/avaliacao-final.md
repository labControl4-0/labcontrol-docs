# LabControl 4.0 - Avaliação Final de Governança e Preparação da Defesa Individual

**Identificador da Entrega:** `[S4][GOV-09]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/governanca/avaliacao-final.md`  
**Disciplina / Área:** Governança de TI  
**Responsável:** Victor Geroto (@victorgeroto)  
**Issue de Referência:** [#17](https://github.com/labControl4-0/labcontrol-docs/issues/17)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  
**Status:** **Esqueleto (v0.1, 2026-11-11)** — a avaliação só pode ser preenchida **depois** dos marcos finais; resultados em branco são intencionais

> Este documento prepara a estrutura e a linha de base. Nenhum resultado, demonstração ou resposta de defesa foi registrado, porque ainda não ocorreram. Preencher apenas com evidência real.

---

## 1. Comparação de Metas × Resultados

Metas vêm do termo de abertura (`docs/gestao/termo-abertura.md`, GP-01) e do plano (`docs/plano-governanca-ti.md`, GOV-01). A coluna "Linha de base" é o estado verificado em 2026-11-11.

| Meta | Indicador | Linha de base (2026-11-11) | **Resultado final** | Evidência (PR/commit/teste) | Meta atingida? |
| :--- | :--- | :--- | :--- | :--- | :---: |
| O1 Backend migrado | BE-01 a BE-10 concluídas com paridade de rotas | 0 de 10 | *a preencher* | | ☐ |
| O2 Mobile offline-first | Registro offline sincronizado sem duplicidade; push abre a ocorrência | 0 de 9; PRs #11–#16 abertos | *a preencher* | | ☐ |
| O3 Web com dashboard | WEB-02 e WEB-05 concluídas; testes úteis | 0 de 8 | *a preencher* | | ☐ |
| O4 Broker protegido | Conexão anônima recusada (teste reproduzível) | `allow_anonymous true` | *a preencher* | | ☐ |
| O5 Governança rastreável | PRs com revisão; proteção de branch; CI | 0 de 3 PRs revisados; 0 de 5 repositórios protegidos; 1 de 5 com CI | *a preencher* | | ☐ |
| O6 Segurança verificável | Zero segredos reais versionados; achados corrigidos e retestados | Inventário SEC-01 em aberto | *a preencher* | | ☐ |
| O7 Entrega integrada | Fluxo ponta a ponta homologado (REL-01) | Não executada | *a preencher* | | ☐ |
| Recuperação | RPO/RTO acordados e medidos (GOV-07) | Não testado | *a preencher* | | ☐ |
| Valor para o usuário | MTTA, localização do ativo, esforço administrativo (NEG-02) | Reportado em NEG-02; dados brutos não versionados | *a preencher* | | ☐ |

---

## 2. Maturidade por Critério da Rubrica

Níveis de 0 a 4; pontuação = nível ÷ 4 × peso. **Autoavaliação preenchida pela equipe ao final.**

| Critério | Peso | Nível (0–4) | Justificativa com evidência | Lacunas |
| :--- | :---: | :---: | :--- | :--- |
| Alinhamento e valor | 20% | *—* | | |
| Responsabilidades e decisões | 15% | *—* | | |
| Riscos, conformidade e ética | 20% | *—* | | |
| Controles no repositório | 25% | *—* | | |
| Indicadores e serviço | 10% | *—* | | |
| Plano e apresentação | 10% | *—* | | |

---

## 3. Cadeia Necessidade → Decisão → Risco → Controle → Evidência → Resultado

Cada integrante deve conseguir explicar ao menos uma cadeia completa. Candidatas (a completar com o que realmente aconteceu):

| Necessidade | Decisão | Risco | Controle | Evidência | Resultado |
| :--- | :--- | :---: | :--- | :--- | :--- |
| Segredos fora do repositório | `.env.example`, rotação e varredura no CI | R-02 | SEC-01, política P-05 | *a preencher* | *a preencher* |
| Mudanças revisadas | Proteção de `main` com 1 aprovação e CI | R-03 | GOV-04 | *a preencher* | *a preencher* |
| Broker confiável | Autenticação e ACL | R-04 | IOT-02 | *a preencher* | *a preencher* |
| Recuperar dados | Backup e restauração testados | R-08 | GOV-07 | *a preencher* | *a preencher* |
| Migração sob controle | Decisão formal e paridade de rotas | R-01 | MUD-001, BE-01 a BE-10 | *a preencher* | *a preencher* |

---

## 4. Demonstração: uma Mudança, uma Falha e uma Recuperação

Roteiro proposto (a ensaiar antes da banca; **só registrar como feito depois de executar**):

| Parte | Proposta | Evidência a anexar | Executada? |
| :--- | :--- | :--- | :---: |
| **Mudança** | Uma mudança real percorrendo solicitação → análise de impacto → aprovação → verificação (`docs/gestao/mudancas.md`, MUD-001 ou MUD-002) | Link do PR/ata e da aprovação | ☐ |
| **Falha** | Simular a perda do container do banco ou a queda do broker em ambiente de teste | Logs sanitizados, horário e impacto | ☐ |
| **Recuperação** | Restaurar a partir do backup e verificar integridade (`docs/rollback.md`) | Tempo medido, contagens, hash do backup | ☐ |

---

## 5. Preparação Individual

Cada integrante explica: sua contribuição, decisões que tomou, controles que operou, **um risco tratado** e **um risco residual aceito**. Os temas abaixo vêm do [RACI](partes-interessadas-raci.md); completar com evidência.

| Integrante | Contribuição (base: RACI) | Decisões que explica | Risco tratado | Risco residual aceito |
| :--- | :--- | :--- | :--- | :--- |
| Giovani Miamoto | Governança, EAP/Kanban, STRIDE/DAST | *a preencher* | *a preencher* | *a preencher* |
| Victor Geroto | Planejamento, riscos, políticas, pentest prático, homologação | *a preencher* | *a preencher* | *a preencher* |
| Carlos Eduardo Oliveira | Backend / migração Spring | *a preencher* | *a preencher* | *a preencher* |
| André Fernandes | Web | *a preencher* | *a preencher* | *a preencher* |
| Gustavo Silveira | Mobile e IoT | *a preencher* | *a preencher* | *a preencher* |

---

## 6. Perguntas Prováveis e Onde Está a Resposta

| Pergunta | Resposta apoiada em |
| :--- | :--- |
| Quais controles existem de fato e quais são planejados? | `docs/plano-governanca-ti.md` §5 e `docs/riscos.md` §4 |
| Como vocês sabem que um controle funciona? | Evidência vinculada na matriz controle-evidência |
| Qual foi a mudança mais importante e como foi aprovada? | `docs/gestao/mudancas.md` |
| Que risco vocês trataram e qual aceitaram? | `docs/riscos.md` §5 |
| O que acontece se o banco for perdido? | `docs/rollback.md` e os testes REC-01 a REC-03 |
| Que dados pessoais o sistema coleta e por quê? | `docs/governanca/conformidade.md` §2–3 |
| O que ficou de fora e por quê? | `docs/gestao/termo-abertura.md` §7 e `docs/plano-governanca-ti.md` Anexo A |

---

## 7. Melhorias Propostas

*(Preencher após a comparação de metas e resultados: ações, responsáveis, prazos.)*

---

## 8. Critérios de Aceite (issue #17) — Situação

| Critério | Situação |
| :--- | :--- |
| Equipe demonstra uma mudança, uma falha e uma recuperação | **Pendente** (seção 4) |
| Cada integrante explica sua contribuição e riscos relevantes | **Pendente** (seção 5) |
| Comparar metas e resultados e propor melhorias | **Pendente** (seções 1 e 7) |

**Dependências da issue:** GOV-08 (#16) e NEG-02 (#26), ambas concluídas; a avaliação ainda depende dos resultados de GOV-07, SEC-01, REL-01 e das frentes de código.

---

## 9. Histórico de Alterações

| Versão | Data | Autor | Alteração |
| :--- | :--- | :--- | :--- |
| 0.1 | 2026-11-11 | @victorgeroto | Esqueleto com linha de base, roteiro de demonstração e preparação individual |
