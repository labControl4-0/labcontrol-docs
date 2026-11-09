# LabControl 4.0 - Relatório de Encerramento do Projeto e Registro de Aprendizados

**Identificador da Entrega:** `[S4][GP-08]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/gestao/encerramento.md`  
**Disciplina / Área:** Gestão de Projetos  
**Responsável:** Giovani Miamoto (@giovanimiamotob)  
**Issue de Referência:** [#8](https://github.com/labControl4-0/labcontrol-docs/issues/8)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  

---

## 1. Visão Geral do Encerramento do 4º Semestre (PI-IV)

Este documento formaliza o encerramento das atividades do **Projeto Integrador IV** da equipe LabControl 4.0, consolidando a comparação entre a linha de base de escopo planejada e o produto efetivamente entregue, o balanço de esforço, a gestão de débitos técnicos residuais e a síntese das lições aprendidas.

---

## 2. Comparativo Linha de Base Planejada vs. Realizada

| Macro-Pacote EAP | Escopo Planejado Inicialmente | Entregável Realizado | Status Final | Justificativa de Desvios |
| :--- | :--- | :--- | :---: | :--- |
| **1.1 Gestão de Projetos (GP)** | Termo de abertura, EAP, acordos, Kanban e encerramento. | EAP formalizada, Kanban ativo no GitHub Projects 3, Working Agreements e Encerramento. | **100% Concluído** | Sem desvios relevantes de cronograma. |
| **1.2 Governança de TI (GOV)** | RACI, CI, Observabilidade, Runbooks e PDF Consolidado. | Matriz RACI, CI no GitHub Actions, Runbooks SEV 1-4, Matriz Controle e PDF compilado. | **100% Concluído** | Pipeline de CI automatizou checagens manuais. |
| **1.3 Cibersegurança (SEC)** | STRIDE, DAST ZAP, PoC de 2 falhas, correções e PDF. | Modelagem STRIDE, DAST ZAP, PoC BOLA/Rate Limit, Reteste Antes/Depois e PDF Pentest. | **100% Concluído** | Avaliação ofensiva e defensiva completa. |
| **1.4 Backend & APIs (BE)** | Transição .NET para Spring Boot, JPA, Auth e Sync. | Rotas essenciais documentadas, migração Spring Boot mapeada e APIs REST operacionais. | **Concluído / Em Transição** | Coexistência controlada entre .NET 9 e Spring Boot 3. |
| **1.5 Frontend Web (WEB)** | Dashboard industrial, planta baixa e acessibilidade. | Editor de planta baixa, visualização em tempo real e consumo unificado da API. | **100% Concluído** | Layout responsivo e acessível. |
| **1.6 Mobile (MOB)** | Armazenamento seguro, SQLite offline e push. | SQLite operacional com fila offline, SecureStore e integração com API. | **100% Concluído** | Validação bem-sucedida em modo avião. |
| **1.7 IoT & Mensageria (IOT)**| Docker Compose unificado com Mosquitto e Node-RED. | Ambiente conteinerizado reproduzível com telemetria padronizada. | **100% Concluído** | Simuladores reproduzíveis sem dependência de hardware. |
| **1.8 Negócios e Release (NEG/REL)**| Validação de negócio, roteiro de banca e manifesto. | Teste com operadores (redução MTTA 94%), manifesto v4.0.0 e roteiro de defesa. | **100% Concluído** | Métricas industriais validadas com usuários. |

---

## 3. Gestão de Dívidas Técnicas e Recomendações para o 5º Semestre

| ID Débito | Descrição da Dívida Técnica | Responsável Atribuído | Prioridade Futura | Impacto / Mitigação Recomendada |
| :---: | :--- | :--- | :---: | :--- |
| **DEBT-01** | Conclusão do corte total de 100% dos endpoints .NET para Spring Boot | Carlos Eduardo | Alta | Manter testes de compatibilidade de contrato Swagger ativos durante a migração. |
| **DEBT-02** | Suporte a TLS mútuo (mTLS) no tráfego MQTT entre sensores e broker | Gustavo Silveira | Média | Geração de certificados X.509 para dispositivos quando implantados em hardware físico. |
| **DEBT-03** | Expansão da suíte de testes E2E automatizados Web com Playwright | André Fernandes | Média | Aumentar cobertura de cenários de drag-and-drop de máquinas na planta baixa. |

---

## 4. Lições Aprendidas e Melhores Práticas Consolidadas

1. **Governança Automatizada Supera Burocracia Manual:** A configuração de workflows no GitHub Actions validando diretórios, links e integridade eliminou revisões manuais demoradas e assegurou que todo commit fosse auditável.
2. **Segurança Ofensiva Alavanca Qualidade Defensiva:** Executar o pentest e a varredura DAST em ambiente próprio revelou vulnerabilidades arquiteturais (como BOLA/IDOR) que não teriam sido capturadas por simples testes de unidade.
3. **Resiliência Offline é Requisito Primário na Indústria:** A implementação do SQLite local no mobile transformou a percepção de valor dos operadores fabris, permitindo trabalho ininterrupto em zonas de sombra de conectividade.

---

## 5. Critérios de Avaliação e Autoavaliação Acadêmica

A distribuição formal de notas do UniSENAI diferencia claramente as disciplinas e componentes:
- **Avaliação Docente das Disciplinas (55%):** Cumprimento rigoroso do programa, qualidade dos PDFs versionados no GitHub e fundamentação conceitual.
- **Avaliação do Projeto Integrador Integrado (35%):** Funcionamento integrado ponta a ponta entre hardware simulado, broker, API, web e mobile em demonstração ao vivo.
- **Autoavaliação e Avaliação Interpares (10%):** Assiduidade, cumprimento dos acordos de trabalho (Working Agreements), ausência de tarefas represadas no Kanban e cooperação técnica mútua.
- **Rubrica Específica de Cibersegurança:** Avaliação ponderada 20/30/30/15/5 (Testes automatizados 20 pontos, Pentest prático 30 pontos, Relatório técnico 30 pontos, Discussão e conclusões 15 pontos, Referências 5 pontos) atendida integralmente no relatório [relatorio-vulnerabilidades-pentest.pdf](../relatorio-vulnerabilidades-pentest.pdf).
