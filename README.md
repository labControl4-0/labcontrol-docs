# LabControl 4.0 - Documentação Oficial do Projeto (PI-IV)

[![CI - Docs Quality & Compliance](https://github.com/labControl4-0/labcontrol-docs/actions/workflows/ci.yml/badge.svg)](https://github.com/labControl4-0/labcontrol-docs/actions/workflows/ci.yml)
[![Organization](https://img.shields.io/badge/Organization-labControl4--0-blue)](https://github.com/labControl4-0)
[![Project](https://img.shields.io/badge/GitHub_Project-Project_3-green)](https://github.com/orgs/labControl4-0/projects/3)

Repositório central de documentação acadêmica, técnica, de governança de TI, cibersegurança e gestão de projetos do **LabControl 4.0**, desenvolvido no âmbito do **Projeto Integrador IV (PI-IV)** da Faculdade de Tecnologia SENAI (UniSENAI).

---

## 📑 Índice Geral de Evidências e Documentação

### 1. Gestão de Projetos (GP)
- [Declaração de Escopo e EAP / WBS (GP-02)](docs/gestao/escopo-eap.md) - Decomposição analítica em 8 macro-pacotes, catálogo de entregas, critérios de aceite e exclusões de escopo.
- [Organização do Backlog e Diretrizes Kanban (GP-04)](docs/gestao/backlog-kanban.md) - Fluxo de trabalho, políticas explícitas, limites de WIP e taxonomia de rastreabilidade multi-repositório.
- [Normas, Acordos de Equipe e Obrigações (GP-06)](docs/gestao/acordos-equipe.md) - Working agreements, ritos ágeis, convenções de código, DoR, DoD e critérios de avaliação do UniSENAI.

### 2. Governança de TI (GOV)
- [Mapeamento de Stakeholders e Matriz RACI (GOV-02)](docs/governanca/partes-interessadas-raci.md) - Mapeamento de partes interessadas, matriz RACI integral de papéis e fóruns de tomada de decisão.
- [Política de Gestão de Mudanças e CI (GOV-04)](docs/governanca/mudancas-ci.md) - Classificação de mudanças, proteção de branch `main`, checklist padrão de PR e automações de integração contínua.
- [Catálogo de Serviços, Observabilidade e Incidentes (GOV-06)](docs/operacao/servico.md) - Catálogo dos 4 serviços de TI, matriz de resposta a incidentes SEV 1 a 4, padrão de logging sanitizado e runbooks de contingência.

### 3. Cibersegurança & Pentest (SEC)
- [Modelagem de Ameaças STRIDE e Matriz DREAD (SEC-02)](docs/seguranca/modelagem-ameacas.md) - Fronteiras de confiança, análise STRIDE por componente (Web, Mobile, Broker MQTT, API) e plano de mitigação/hardening.

---

## 👥 Equipe do Projeto Integrador IV

| Integrante | GitHub | Frentes de Atuação Principal |
| :--- | :--- | :--- |
| **Giovani Miamoto** | [@giovanimiamotob](https://github.com/giovanimiamotob) | Governança de TI, Gestão de Projetos (EAP/Kanban) e Cibersegurança (STRIDE/DAST) |
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
