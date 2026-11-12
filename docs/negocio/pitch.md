# LabControl 4.0 - Pitch Executivo e Revisão de Critérios Restantes

**Identificador da Entrega:** `[S4][NEG-03]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/negocio/pitch.md`  
**Disciplina / Área:** Empreendedorismo / Inovação — *rubrica específica ainda a confirmar*  
**Responsável:** Victor Geroto (@victorgeroto)  
**Issue de Referência:** [#27](https://github.com/labControl4-0/labcontrol-docs/issues/27)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  
**Status:** Rascunho v0.1 (2026-11-11) — **roteiro provisório**; revisar quando as frentes previstas forem mescladas e a rubrica for recebida

---

## 1. Regras do Pitch

1. Cada afirmação sobre o produto tem **evidência** (tabela da seção 3) ou é apresentada como **hipótese/plano**.
2. Números só entram com fonte; **resultado reportado ≠ resultado comprovado**.
3. O que está em PR aberto ou em issue é dito como **"em desenvolvimento"**, nunca como pronto.
4. Dados de exemplo são sintéticos.

Complementos já existentes: [`apresentacao.md`](../apresentacao.md) (roteiro de demonstração) e [`validacao.md`](validacao.md) (validação com usuários, NEG-02). Base do canvas: `docs/negocio/modelo-negocio.md` (NEG-01).

---

## 2. Roteiro (≈ 3 a 5 minutos)

| # | Bloco | Mensagem | Base |
| :---: | :--- | :--- | :--- |
| 1 | **Problema** | Em laboratórios e plantas, falhas de máquina são percebidas tarde, o equipamento é difícil de localizar e o consumo não é monitorado. *(hipótese — a dimensão do problema ainda não foi medida)* | NEG-01 §2 |
| 2 | **Solução** | Uma plataforma com planta baixa interativa, telemetria por MQTT, alertas/eventos, app mobile e assistente de chat | NEG-01 §2.3 |
| 3 | **Demonstração** | Entrar → criar planta → desenhar setor e máquina → ver a planta no mobile → telemetria chegando (*só mostrar etapas homologadas em REL-01*) | `apresentacao.md`, REL-01 |
| 4 | **Benefício** | Menos tempo para localizar e reagir; operação móvel. Relato de testes de usabilidade: ver tabela da seção 3 (linha de MTTA) | NEG-02 |
| 5 | **Viabilidade e custos** | Stack aberta e reproduzível; custos principais: horas, nuvem, API de IA, dispositivos | `gestao/cronograma-custos.md` (GP-03) |
| 6 | **Evolução** | Backend em Spring Boot, mobile offline com push, dashboard web, broker protegido | Termo de abertura (GP-01) |
| 7 | **Próximos passos / pedido** | Piloto em um laboratório; validar hipóteses H-01 a H-06 | NEG-01 §5 |

---

## 3. Afirmações × Evidências

Estado verificado em 2026-11-11 (api `84da384`, web `6b2e6b6`, mobile `ff07943`, iot `56c166e`).

| Afirmação possível | Evidência | Pode ser dita como… |
| :--- | :--- | :--- |
| "Desenhamos setores e posicionamos máquinas na planta" | Editor de planta baixa na `main` do web | **Implementado** (não homologado) |
| "Máquinas enviam métricas por MQTT e a API grava" | Assinante MQTT na API (`main`) | **Implementado**; o simulador atual precisa de ajuste (IOT-01, IOT-03) para gerar mensagens válidas |
| "Há um assistente de chat que usa os dados da planta" | Endpoint de chat e tela mobile na `main` | **Implementado**; a leitura do código do mobile indica um possível problema de autenticação na tela de chat (não executado) — **confirmar e corrigir antes da demonstração** |
| "O app funciona sem rede" | MOB-03/04 em **PR aberto** (#13, #14) | **Em desenvolvimento** |
| "Recebemos alerta no celular" | MOB-05/06 em **PR aberto** (#15, #16); BE-07 aberta | **Em desenvolvimento** |
| "Dashboard com consumo e alertas em tempo real" | `Dashboard.tsx` vazio; dashboard mobile simulado; WEB-02/05 abertas | **Previsto** |
| "O backend foi migrado para Spring Boot" | Nenhuma branch Spring; BE-01 a BE-10 abertas | **Previsto** |
| "Tempo de reconhecimento de falha caiu para 1 min 12 s (vs. 18–25 min)" | [`validacao.md`](validacao.md) (NEG-02): sessão com 3 participantes | **Reportado em teste de usabilidade**; **dados brutos não versionados** e o cenário usa recursos (fila offline, alertas) que **ainda não estão mesclados** — dizer "em teste com 3 participantes, o tempo reportado foi…" e **confirmar a versão testada** antes de usar como resultado |
| "Economizamos 35 min/dia por operador" | NEG-02 | **Reportado**; mesma ressalva — tratar como indicativo, não como resultado comprovado |
| "O sistema é seguro" | Modelagem de ameaças e relatório de segurança existem; correções dependem de SEC-01/03/05 e de outras issues | **Não afirmar**; dizer que há análise de ameaças e plano de correção em andamento |

---

## 4. Texto-Base Provisório (para ensaio)

> "Em laboratórios e plantas industriais, uma máquina pode falhar sem ninguém perceber, e achar o equipamento certo leva tempo. O **LabControl 4.0** reúne, em um só lugar, a **planta baixa interativa**, a **telemetria das máquinas** e os **alertas**, com um **app mobile** e um **assistente** que responde com base nos dados da planta.
> Hoje já é possível desenhar a planta, posicionar máquinas e receber métricas pela API. Estamos concluindo a **operação offline com sincronização**, os **alertas por push** e o **dashboard** — e migrando o backend para Spring Boot.
> Em um teste de usabilidade com três participantes, o tempo reportado para reconhecer uma falha foi de pouco mais de um minuto, contra uma referência manual de 18 a 25 minutos; vamos repetir essa medição com a versão integrada, com dados anexados.
> Queremos validar o valor em um piloto: o que falta é medir ganho de tempo e de energia em um laboratório real."

*(Ajustar os números e as frases "estamos concluindo" conforme o estado real dos PRs na data da apresentação.)*

---

## 5. Revisão dos Critérios Restantes

| Item | Situação |
| :--- | :--- |
| Rubrica de **Empreendedorismo/Inovação** | **Não recebida** — permanece pendente; cobrir somente o que a rubrica pedir |
| Rubrica/tema da **unidade eletiva** | **Não recebida** — pendente (EAP §5) |
| Critérios de Governança, Segurança e Gestão | Cobertos pelas demais entregas (GOV, SEC, GP) |
| Promessa de cobrir todas as disciplinas | **Não feita** — critérios não recebidos ficam explicitamente pendentes |

**Ação:** solicitar ao docente as rubricas pendentes e registrar a resposta e a data aqui.

---

## 6. Critérios de Aceite (issue #27)

| Critério | Situação |
| :--- | :--- |
| Pitch usa evidências do produto | Atendido (seção 3), com classificação de cada afirmação |
| Critérios não recebidos permanecem pendentes, sem promessa de cobertura | Atendido (seção 5) |
| Consolidar problema, solução, benefício, custos e evolução | Atendido (seções 2 e 4) |

**Dependência:** NEG-02 (#26), concluída; a revisão do número de MTTA depende de a equipe anexar os dados brutos e a versão testada.

---

## 7. Histórico de Alterações

| Versão | Data | Autor | Alteração |
| :--- | :--- | :--- | :--- |
| 0.1 | 2026-11-11 | @victorgeroto | Roteiro, tabela afirmação × evidência e texto-base |
