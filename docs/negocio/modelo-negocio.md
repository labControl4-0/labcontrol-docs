# LabControl 4.0 - Proposta de Valor e Modelo de Negócio

**Identificador da Entrega:** `[S4][NEG-01]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/negocio/modelo-negocio.md`  
**Disciplina / Área:** Empreendedorismo / Inovação — *rubrica específica ainda a confirmar*  
**Responsável:** Victor Geroto (@victorgeroto)  
**Issue de Referência:** [#25](https://github.com/labControl4-0/labcontrol-docs/issues/25)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  
**Status:** Rascunho v0.1 (2026-11-11) — modelo de **hipóteses**; nenhuma venda, preço ou mercado foi comprovado

---

## 1. Como Ler Este Documento

Todo item recebe um rótulo, para não misturar hipótese com fato:

| Rótulo | Significado |
| :---: | :--- |
| **[H]** | **Hipótese de mercado** — ainda não validada |
| **[E]** | **Evidência observada** — com fonte no repositório (inclusive relatos de validação, citados como tal) |
| **[M]** | **Existe na `main`** — funcionalidade implementada, **não homologada** (REL-01) |
| **[P]** | **Previsto** — issue aberta ou PR não mesclado |

Estado do produto verificado em 2026-11-11 (api `84da384`, web `6b2e6b6`, mobile `ff07943`, iot `56c166e`).

---

## 2. Usuários, Dor e Solução

### 2.1 Personas

| Persona | Quem é | Dor principal | Rótulo |
| :--- | :--- | :--- | :---: |
| **Operador / técnico de manutenção** | Trabalha no chão de fábrica ou laboratório | Perceber a falha tarde; localizar o equipamento; registrar ocorrências onde não há rede | [H] / [E: relatos em `negocio/validacao.md`] |
| **Supervisor / gestor** | Coordena a equipe e responde pela planta | Falta de visão consolidada do estado das máquinas e do histórico de eventos | [H] |
| **Responsável por energia / custos** | Gestor da instalação | Consumo energético sem visibilidade | [H] |

### 2.2 Problema

Máquinas são acompanhadas por inspeção presencial e registros manuais; falhas são percebidas tarde, o equipamento é difícil de localizar e o consumo energético não é monitorado. **[H]** *Tamanho do problema e perda financeira não foram medidos.*

### 2.3 Solução

Plataforma única com **planta baixa interativa**, **telemetria por MQTT**, **alertas/eventos** e **aplicativo mobile** (com operação offline planejada), mais um **assistente de chat** que responde com base nos dados do usuário.

### 2.4 Diferencial

| Diferencial | Rótulo |
| :--- | :---: |
| Planta baixa editável que posiciona máquinas por setor, ligada à telemetria | [M] |
| Mesma API para web e mobile | [M] |
| Assistente de chat que consulta o contexto real da planta do usuário | [M] |
| Operação offline com sincronização | [P] |
| Stack aberta e reproduzível por Docker (baixo custo de adoção em ambiente de teste) | [M] |

---

## 3. Proposta de Valor ↔ Funcionalidades Entregues

Conecta cada benefício prometido (redução de desperdício e do tempo de reação) ao que de fato existe:

| Benefício prometido | Funcionalidade | Situação real | Rótulo |
| :--- | :--- | :--- | :---: |
| **Reagir mais rápido a falhas** | Eventos e alertas de máquinas | API de eventos existe (criar, listar, resolver); **central de alertas no web é previsão (WEB-05)** | [M] API / [P] UI |
| **Reagir mais rápido a falhas** | Notificação push ao operador | MOB-05 e MOB-06 em PR aberto; BE-07 (registro de dispositivo e envio) aberta | [P] |
| **Localizar o equipamento rapidamente** | Planta baixa interativa (web: editor; mobile: visualização) | Implementada, sem homologação | [M] |
| **Reduzir desperdício de energia** | Métrica de consumo + dashboard | A API aceita a métrica de energia; **não há painel de consumo no web** (`Dashboard.tsx` vazio) e o dashboard mobile usa **dados simulados**; dashboard real é WEB-02/BE-09 | [P] |
| **Operar sem rede** | Fila offline e sincronização | MOB-03 e MOB-04 em PR aberto; BE-06 aberta | [P] |
| **Reduzir esforço de registro** | Ocorrências digitais | Eventos na API; registro offline depende de MOB-03/04 | [M] parcial / [P] |
| **Consultar dados por linguagem natural** | Chat com IA | Implementado na API e no mobile | [M] |

> Conclusão honesta do vínculo: **hoje a planta baixa e a base de eventos/telemetria são o que existe; o ganho de tempo de reação e de energia depende de itens ainda previstos** (alertas na web, push, dashboard, offline).

---

## 4. Modelo de Negócio (Canvas)

| Bloco | Conteúdo | Rótulo |
| :--- | :--- | :---: |
| **Segmentos de clientes** | Laboratórios e plantas industriais de pequeno/médio porte; instituições de ensino técnico com laboratórios | [H] |
| **Proposta de valor** | Visão única de plantas, máquinas e alertas; menor tempo para localizar e reagir; operação móvel, inclusive offline | [H] / ver seção 3 |
| **Canais** | Demonstração em laboratórios da própria instituição; parcerias com integradores de automação; documentação e repositório abertos | [H] |
| **Relacionamento** | Piloto acompanhado, suporte por canal digital, material de treinamento | [H] |
| **Fontes de receita** | Assinatura por planta/mês; serviço de implantação e integração de sensores; suporte | [H] — **sem preço, sem venda comprovada** |
| **Recursos-chave** | Equipe de desenvolvimento, repositórios e CI, ambiente Docker/nuvem, simulador de telemetria, API de IA | [M] |
| **Atividades-chave** | Evoluir a plataforma, integrar sensores, hospedar e operar, suportar o cliente | [H] |
| **Parcerias-chave** | Fornecedores de sensores/gateways, integradores de automação, a instituição de ensino (piloto), provedor de nuvem | [H] |
| **Estrutura de custos** | Horas da equipe (336 h abertas — ver `docs/gestao/cronograma-custos.md`), nuvem, API de IA, dispositivos Android, suporte | [E] para horas; demais a levantar |

---

## 5. Hipóteses a Validar

| ID | Hipótese | Como validar | Métrica de sucesso | Situação |
| :---: | :--- | :--- | :--- | :--- |
| H-01 | Operadores perdem tempo relevante procurando equipamento e percebendo falhas | Observação e entrevistas com mais participantes além dos 3 de NEG-02; medir tempos antes/depois com a mesma versão | Redução de tempo medida com dado bruto anexado | **Não validada** |
| H-02 | Gestores pagariam por uma visão consolidada | Entrevistas de descoberta; piloto | Intenção de uso/pagamento registrada | **Não validada** |
| H-03 | Operar offline é requisito do chão de fábrica | Levantar condições de rede dos ambientes-alvo | % de ambientes com falhas de conectividade | **Não validada** |
| H-04 | Monitorar consumo gera economia | Piloto com medição de energia | Variação de consumo medida | **Não validada** |
| H-05 | Sensores/gateways existentes integram-se por MQTT sem esforço excessivo | Prova de integração com um dispositivo | Horas de integração por tipo de sensor | **Não validada** |
| H-06 | Modelo por assinatura é viável frente ao custo de nuvem e IA | Estimar custo por planta e comparar | Margem estimada > 0 | **Não validada** |

---

## 6. Premissas Financeiras (modelo, sem números comprovados)

| Variável | Fórmula / uso | Valor | Fonte |
| :--- | :--- | :---: | :--- |
| Preço por planta/mês (P) | Receita = N × P | *a definir* | Hipótese H-02 |
| Plantas atendidas (N) | — | *a definir* | Hipótese H-02 |
| Custo de nuvem por planta (Cn) | Custo = N × Cn | *a levantar* | Levantamento de custos (GP-03) |
| Custo de IA por planta (Ci) | Custo = N × Ci | *a levantar* | Levantamento de custos (GP-03) |
| Custo de suporte (Cs) | — | *a estimar* | — |
| Margem estimada | N × (P − Cn − Ci − Cs) | *a calcular* | **Premissa, não resultado** |

**Nenhum valor acima é venda comprovada.** Os campos serão preenchidos somente com dados do levantamento de custos e das entrevistas.

---

## 7. Critérios de Aceite (issue #25)

| Critério | Situação |
| :--- | :--- |
| O canvas conecta redução de desperdício e tempo de reação com funcionalidades entregues | Atendido (seção 3), com a ressalva de que parte é **prevista** |
| Premissas financeiras não são vendas comprovadas | Atendido (seção 6; rótulos [H]) |
| Descrever personas, problema, valor, parceiros, canais, recursos, custos e receita | Atendido (seções 2 e 4) |
| Separar hipóteses de mercado, evidências e capacidades implementadas | Atendido (rótulos [H], [E], [M], [P]) |

---

## 8. Histórico de Alterações

| Versão | Data | Autor | Alteração |
| :--- | :--- | :--- | :--- |
| 0.1 | 2026-11-11 | @victorgeroto | Canvas, vínculo benefício × funcionalidade e hipóteses |
