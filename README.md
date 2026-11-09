# LabControl 4.0 - Documentação Oficial do Projeto (PI-IV)

[![CI - Docs Quality & Compliance](https://github.com/labControl4-0/labcontrol-docs/actions/workflows/ci.yml/badge.svg)](https://github.com/labControl4-0/labcontrol-docs/actions/workflows/ci.yml)
[![Organization](https://img.shields.io/badge/Organization-labControl4--0-blue)](https://github.com/labControl4-0)
[![Project](https://img.shields.io/badge/GitHub_Project-Project_3-green)](https://github.com/orgs/labControl4-0/projects/3)
[![Plano de Governança PDF](https://img.shields.io/badge/Download-Plano_Governança_PDF-red)](docs/plano-governanca-ti.pdf)
[![Relatório Pentest PDF](https://img.shields.io/badge/Download-Relatório_Pentest_PDF-darkred)](docs/relatorio-vulnerabilidades-pentest.pdf)

Repositório central de documentação acadêmica, técnica, de governança de TI, cibersegurança e gestão de projetos do **LabControl 4.0**, desenvolvido no âmbito do **Projeto Integrador IV (PI-IV)** da Faculdade de Tecnologia SENAI (UniSENAI).

---

## 📑 Índice Geral de Evidências e Documentação

### 1. Governança de TI (GOV)
- 📕 **[Plano Consolidado de Governança de TI (PDF)](docs/plano-governanca-ti.pdf)** - Documento oficial consolidado e formatado para avaliação acadêmica.
- [Matriz de Controle e Evidências (GOV-08)](docs/governanca/matriz-controle-evidencia.md) - Rastreabilidade integral entre diretrizes, controles implementados e links no repositório.
- [Mapeamento de Stakeholders e Matriz RACI (GOV-02)](docs/governanca/partes-interessadas-raci.md) - Mapeamento de partes interessadas, matriz RACI integral de papéis e fóruns de tomada de decisão.
- [Política de Gestão de Mudanças e CI (GOV-04)](docs/governanca/mudancas-ci.md) - Classificação de mudanças, proteção de branch `main`, checklist padrão de PR e automações de integração contínua.
- [Catálogo de Serviços, Observabilidade e Incidentes (GOV-06)](docs/operacao/servico.md) - Catálogo dos 4 serviços de TI, matriz de resposta a incidentes SEV 1 a 4, padrão de logging sanitizado e runbooks de contingência.

### 2. Cibersegurança & Pentest (SEC)
- 📕 **[Relatório Técnico de Vulnerabilidades e Pentest (PDF)](docs/relatorio-vulnerabilidades-pentest.pdf)** - Relatório completo de segurança cobrindo as 7 seções, testes automatizados e exploração de duas vulnerabilidades confirmadas.
- [Relatório de Remediação, Correção e Reteste (SEC-06)](docs/seguranca/correcoes-reteste.md) - Matriz comparativa Antes vs. Depois, testes de regressão e gestão de risco residual.
- [Relatório de Avaliação Automatizada Autenticada (SEC-04)](docs/seguranca/evidencias/dast-autenticado.md) - Varredura DAST/SAST autenticada com OWASP ZAP, catalogação de achados com validação de falsos positivos.
- [Modelagem de Ameaças STRIDE e Matriz DREAD (SEC-02)](docs/seguranca/modelagem-ameacas.md) - Fronteiras de confiança, análise STRIDE por componente (Web, Mobile, Broker MQTT, API) e plano de mitigação/hardening.

### 3. Gestão de Projetos (GP)
- [Declaração de Escopo e EAP / WBS (GP-02)](docs/gestao/escopo-eap.md) - Decomposição analítica em 8 macro-pacotes, catálogo de entregas, critérios de aceite e exclusões de escopo.
- [Organização do Backlog e Diretrizes Kanban (GP-04)](docs/gestao/backlog-kanban.md) - Fluxo de trabalho, políticas explícitas, limites de WIP e taxonomia de rastreabilidade multi-repositório.
- [Normas, Acordos de Equipe e Obrigações (GP-06)](docs/gestao/acordos-equipe.md) - Working agreements, ritos ágeis, convenções Git e critérios de avaliação do UniSENAI.
- [Relatório de Encerramento e Lições Aprendidas (GP-08)](docs/gestao/encerramento.md) - Comparativo linha de base vs. realizado, débitos técnicos gerenciados e modelo de autoavaliação.

### 4. Entrega Integrada e Demonstração da Banca (REL)
- [Manifesto de Entrega Integrada e Matriz de Versões (REL-02)](docs/manifesto-entrega.md) - Matriz de commits, tags de release v4.0.0 e guia de reprodução em clone limpo via Docker Compose.
- [Roteiro de Apresentação e Demonstração da Banca (REL-02)](docs/apresentacao.md) - Roteiro de 20 minutos com passo a passo prático para a banca avaliadora.

### 5. Empreendedorismo, Inovação e Negócios (NEG)
- [Validação com Usuários e Indicadores de Negócio (NEG-02)](docs/negocio/validacao.md) - Testes de usabilidade com operadores industriais, minimização de dados LGPD e métricas de impacto de negócio (MTTA, redução de tempo).

---

## 👥 Equipe do Projeto Integrador IV

| Integrante | GitHub | Frentes de Atuação Principal |
| :--- | :--- | :--- |
| **Giovani Miamoto** | [@giovanimiamotob](https://github.com/giovanimiamotob) | Governança de TI, Gestão de Projetos (EAP/Kanban) e Cibersegurança (STRIDE/DAST/Pentest) |
| **Victor Geroto** | [@victorgeroto](https://github.com/victorgeroto) | Planejamento, Riscos de Governança, Pentest Prático e Homologação |
| **Carlos Eduardo Oliveira** | [@ceduardooliveira](https://github.com/ceduardooliveira) | Backend & APIs: Migração para Java 21 / Spring Boot 3 e JPA |
| **André Fernandes** | [@AndreFernandes9010](https://github.com/AndreFernandes9010) | Frontend Web: Dashboard Industrial, Planta Baixa e Acessibilidade |
| **Gustavo Silveira** | [@GustavoSilveira1012](https://github.com/GustavoSilveira1012) | Mobile Offline-First (SQLite/Expo) e Infraestrutura IoT (MQTT/Mosquitto) |

---

## 🔗 Repositórios do Ecossistema LabControl 4.0

- [labcontrol-docs](https://github.com/labControl4-0/labcontrol-docs) - Repositório central de documentação e governança.
- [labcontrol-api](https://github.com/labControl4-0/labcontrol-api) - Backend central (transição .NET Core -> Spring Boot).
- [labcontrol-web](https://github.com/labControl4-0/labcontrol-web) - Frontend Web Industrial (React 18 + Tailwind).
- [labcontrol-mobile](https://github.com/labControl4-0/labcontrol-mobile) - Aplicação móvel de chão de fábrica (React Native + Expo + SQLite).
- [labcontrol-iot](https://github.com/labControl4-0/labcontrol-iot) - Broker MQTT Mosquitto, Node-RED e simulador de telemetria.
