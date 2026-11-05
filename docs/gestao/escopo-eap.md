# LabControl 4.0 - Declaração de Escopo e Estrutura Analítica do Projeto (EAP / WBS)

**Identificador da Entrega:** `[S4][GP-02]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/gestao/escopo-eap.md`  
**Disciplina / Área:** Gestão de Projetos  
**Responsável:** Giovani Miamoto (@giovanimiamotob)  
**Issue de Referência:** [#2](https://github.com/labControl4-0/labcontrol-docs/issues/2)  
**Projeto:** [GitHub Project 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  

---

## 1. Visão Geral e Justificativa do Projeto

O **LabControl 4.0** é uma plataforma integrada voltada para o monitoramento, telemetria em tempo real e controle de ativos operacionais em plantas industriais e laboratoriais. 

No âmbito do **Projeto Integrador IV (PI-IV)** do UniSENAI, o projeto entra em sua fase de continuidade e consolidação arquitetural, endereçando a modernização tecnológica, resiliência operacional, conformidade regulatória, governança de serviços e endurecimento de cibersegurança (hardening e pentest).

### 1.1 Objetivos Estratégicos do 4º Semestre
1. **Modernização do Backend:** Transição planejada da API legada (.NET 9) para uma arquitetura robusta baseada em **Java 21 / Spring Boot 3**, com JPA/Hibernate, validação declarativa e persistência relacional (PostgreSQL).
2. **Resiliência Mobile Offline-First:** Implementação de armazenamento seguro com SQLite local, fila de sincronização assíncrona bidirecional com tratamento de conflitos e suporte a notificações push via Expo.
3. **Planta Industrial Web Interativa:** Aprimoramento da visualização e editor de planta baixa em tempo real com React 18, Tailwind CSS e consumo unificado da API.
4. **Governança de TI Operacional:** Formalização de papéis (RACI), processos de gestão de mudanças (CI/CD com branch protection e pull requests), runbooks de incidentes e matriz controle-evidência.
5. **Cibersegurança e Conformidade:** Modelagem formal de ameaças (STRIDE), avaliação automatizada e autenticada de vulnerabilidades (DAST/SAST) e testes de intrusão com plano de remediação.

---

## 2. Estrutura Analítica do Projeto (EAP / WBS)

A EAP decompõe todo o ecossistema do LabControl 4.0 em 8 macro-pacotes de trabalho (Nível 1), subdivididos em pacotes executáveis (Nível 2), 100% rastreáveis com as issues ativas do backlog do Projeto Integrador IV:

```
1. LabControl 4.0 (PI-IV)
├── 1.1 Gestão de Projetos (GP)
│   ├── 1.1.1 Termo de Abertura e Continuidade [GP-01]
│   ├── 1.1.2 Escopo, EAP e Catálogo de Entregas [GP-02]
│   ├── 1.1.3 Cronograma, Custos e Recursos [GP-03]
│   ├── 1.1.4 Backlog e Quadro Kanban [GP-04]
│   ├── 1.1.5 Metodologia e Ferramentas Ágeis [GP-05]
│   ├── 1.1.6 Normas, Acordos e Obrigações [GP-06]
│   ├── 1.1.7 Monitoramento e Controle de Sprints [GP-07]
│   └── 1.1.8 Encerramento e Lições Aprendidas [GP-08]
├── 1.2 Governança de TI (GOV)
│   ├── 1.2.1 Plano de Governança de TI (Fonte Base) [GOV-01]
│   ├── 1.2.2 Partes Interessadas, Matriz RACI e Decisões [GOV-02]
│   ├── 1.2.3 Registro de Riscos e Planos de Resposta [GOV-03]
│   ├── 1.2.4 Revisão de Mudanças, PRs e CI [GOV-04]
│   ├── 1.2.5 Políticas de Dados, Acesso e Licenciamento [GOV-05]
│   ├── 1.2.6 Observabilidade, Runbooks e Gestão do Serviço [GOV-06]
│   ├── 1.2.7 Backup, Recuperação de Desastres e Rollback [GOV-07]
│   ├── 1.2.8 Matriz Controle-Evidência e Compilação do Plano [GOV-08]
│   └── 1.2.9 Avaliação e Defesa Individual [GOV-09]
├── 1.3 Cibersegurança e Pentest (SEC)
│   ├── 1.3.1 Avaliação de Segredos e Dados Versionados [SEC-01]
│   ├── 1.3.2 Modelagem de Ameaças STRIDE e Revisão de Acesso [SEC-02]
│   ├── 1.3.3 Escopo e Ambiente de Testes de Segurança [SEC-03]
│   ├── 1.3.4 Avaliação Automatizada Autenticada (DAST/SAST) [SEC-04]
│   ├── 1.3.5 Exploração Controlada de Vulnerabilidades [SEC-05]
│   ├── 1.3.6 Correção e Reteste de Achados [SEC-06]
│   └── 1.3.7 Relatório Final de Vulnerabilidades e Pentest [SEC-07]
├── 1.4 Backend & APIs (BE)
│   ├── 1.4.1 Estratégia de Migração .NET -> Spring Boot [BE-01]
│   ├── 1.4.2 Setup e Build Reproduzível Spring Boot [BE-02]
│   ├── 1.4.3 Modelagem de Entidades e Relacionamentos JPA [BE-03]
│   ├── 1.4.4 Autenticação e Autorização (Spring Security + JWT) [BE-04]
│   ├── 1.4.5 CRUD de Ativos, DTOs e Validações [BE-05]
│   ├── 1.4.6 Endpoint de Sincronização Idempotente [BE-06]
│   ├── 1.4.7 Registro de Dispositivos e Push Notification [BE-07]
│   ├── 1.4.8 Ingestão MQTT e Motor de Regras de Alertas [BE-08]
│   ├── 1.4.9 Consultas de Telemetria e Dashboard [BE-09]
│   └── 1.4.10 Homologação e Virada de Chave (Corte de API) [BE-10]
├── 1.5 Frontend Web (WEB)
│   ├── 1.5.1 Unificação do Cliente HTTP, Sessão e Rotas [WEB-01]
│   ├── 1.5.2 Dashboard Industrial em Tempo Real [WEB-02]
│   ├── 1.5.3 Editor e Renderizador de Planta Baixa [WEB-03]
│   ├── 1.5.4 Histórico de Versões da Planta Industrial [WEB-04]
│   ├── 1.5.5 Central de Alertas e Detalhamento de Ativos [WEB-05]
│   ├── 1.5.6 Internacionalização, Acessibilidade e Padrão PT-BR [WEB-06]
│   ├── 1.5.7 Otimização de Performance e Redução de Overhead [WEB-07]
│   └── 1.5.8 Suíte de Testes Automatizados (Vitest/Playwright) [WEB-08]
├── 1.6 Mobile Industrial (MOB)
│   ├── 1.6.1 Cliente HTTP e Gestão Assíncrona de Sessão [MOB-01]
│   ├── 1.6.2 Armazenamento Seguro de Credenciais e Tokens [MOB-02]
│   ├── 1.6.3 Banco Local SQLite e Fila de Operações Offline [MOB-03]
│   ├── 1.6.4 Mecanismo de Sincronização e Resolução de Conflitos [MOB-04]
│   ├── 1.6.5 Configuração do Expo Notifications e Development Build [MOB-05]
│   ├── 1.6.6 Recepção de Push e Navegação Deep-Link por Payload [MOB-06]
│   ├── 1.6.7 Documentação e Exercícios Práticos [MOB-07]
│   ├── 1.6.8 Revisão de Estados e UI/UX Ergonomia Industrial [MOB-08]
│   └── 1.6.9 Testes de Ponta a Ponta do Fluxo Mobile [MOB-09]
├── 1.7 Internet das Coisas & Broker MQTT (IOT)
│   ├── 1.7.1 Padronização de Tópicos e Payloads JSON [IOT-01]
│   ├── 1.7.2 Hardening do Broker Mosquitto e Ferramentas [IOT-02]
│   ├── 1.7.3 Simulador Reproduzível de Falhas e Telemetria [IOT-03]
│   └── 1.7.4 Orquestração Docker Compose Unificada e Docs IoT [IOT-04]
└── 1.8 Negócios, Validação e Entrega Integrada (NEG / REL)
    ├── 1.8.1 Proposta de Valor e Modelagem de Negócio [NEG-01]
    ├── 1.8.2 Validação com Operadores e Indicadores de Valor [NEG-02]
    ├── 1.8.3 Pitch Executivo e Critérios de Aceite [NEG-03]
    ├── 1.8.4 Homologação Integrada Ponta a Ponta [REL-01]
    └── 1.8.5 Manifesto de Release e Apresentação Acadêmica [REL-02]
```

---

## 3. Catálogo de Entregas e Matriz de Rastreabilidade

| Código EAP | Pacote / Atividade | Repositório | Responsável | Issue GitHub | Entregável Principal |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **GP-01** | Termo de Abertura do Projeto | `labcontrol-docs` | @victorgeroto | [#1](https://github.com/labControl4-0/labcontrol-docs/issues/1) | `docs/gestao/termo-abertura.md` |
| **GP-02** | Declaração de Escopo e EAP | `labcontrol-docs` | @giovanimiamotob | [#2](https://github.com/labControl4-0/labcontrol-docs/issues/2) | `docs/gestao/escopo-eap.md` |
| **GP-03** | Estimativas, Cronograma e Custos | `labcontrol-docs` | @victorgeroto | [#3](https://github.com/labControl4-0/labcontrol-docs/issues/3) | `docs/gestao/cronograma-custos.md` |
| **GP-04** | Organização do Backlog e Kanban | `labcontrol-docs` | @giovanimiamotob | [#4](https://github.com/labControl4-0/labcontrol-docs/issues/4) | `docs/gestao/backlog-kanban.md` + GitHub Project 3 |
| **GP-05** | Metodologia e Ferramentas Ágeis | `labcontrol-docs` | @victorgeroto | [#5](https://github.com/labControl4-0/labcontrol-docs/issues/5) | `docs/gestao/metodologia-agil.md` |
| **GP-06** | Normas, Acordos e Obrigações | `labcontrol-docs` | @giovanimiamotob | [#6](https://github.com/labControl4-0/labcontrol-docs/issues/6) | `docs/gestao/acordos-equipe.md` |
| **GP-07** | Monitoramento e Controle de Sprints| `labcontrol-docs` | @victorgeroto | [#7](https://github.com/labControl4-0/labcontrol-docs/issues/7) | `docs/gestao/controle-sprints.md` |
| **GP-08** | Encerramento e Lições Aprendidas | `labcontrol-docs` | @giovanimiamotob | [#8](https://github.com/labControl4-0/labcontrol-docs/issues/8) | `docs/gestao/encerramento.md` |
| **GOV-01** | Fonte do Plano de Governança | `labcontrol-docs` | @victorgeroto | [#9](https://github.com/labControl4-0/labcontrol-docs/issues/9) | `docs/governanca/plano-base.md` |
| **GOV-02** | Stakeholders, RACI e Decisões | `labcontrol-docs` | @giovanimiamotob | [#10](https://github.com/labControl4-0/labcontrol-docs/issues/10) | `docs/governanca/partes-interessadas-raci.md` |
| **GOV-03** | Registro de Riscos e Respostas | `labcontrol-docs` | @victorgeroto | [#11](https://github.com/labControl4-0/labcontrol-docs/issues/11) | `docs/governanca/riscos-respostas.md` |
| **GOV-04** | Revisão de Mudanças e CI | `labcontrol-docs` | @giovanimiamotob | [#12](https://github.com/labControl4-0/labcontrol-docs/issues/12) | `docs/governanca/mudancas-ci.md` + `.github/workflows/` |
| **GOV-05** | Políticas de Dados e Acesso | `labcontrol-docs` | @victorgeroto | [#13](https://github.com/labControl4-0/labcontrol-docs/issues/13) | `docs/governanca/politicas-acesso-dados.md` |
| **GOV-06** | Observabilidade e Gestão de Serviço | `labcontrol-docs` | @giovanimiamotob | [#14](https://github.com/labControl4-0/labcontrol-docs/issues/14) | `docs/operacao/servico.md` + Runbook |
| **GOV-07** | Backup, Recuperação e Rollback | `labcontrol-docs` | @victorgeroto | [#15](https://github.com/labControl4-0/labcontrol-docs/issues/15) | `docs/governanca/backup-rollback.md` |
| **GOV-08** | Matriz Controle-Evidência e PDF | `labcontrol-docs` | @giovanimiamotob | [#16](https://github.com/labControl4-0/labcontrol-docs/issues/16) | `docs/plano-governanca-ti.pdf` |
| **GOV-09** | Avaliação e Defesa Individual | `labcontrol-docs` | @victorgeroto | [#17](https://github.com/labControl4-0/labcontrol-docs/issues/17) | `docs/governanca/defesa-individual.md` |
| **SEC-01** | Auditoria de Segredos Versionados | `labcontrol-docs` | @victorgeroto | [#18](https://github.com/labControl4-0/labcontrol-docs/issues/18) | `docs/seguranca/auditoria-segredos.md` |
| **SEC-02** | Modelagem de Ameaças STRIDE | `labcontrol-docs` | @giovanimiamotob | [#19](https://github.com/labControl4-0/labcontrol-docs/issues/19) | `docs/seguranca/modelagem-ameacas.md` |
| **SEC-03** | Escopo e Ambiente de Pentest | `labcontrol-docs` | @victorgeroto | [#20](https://github.com/labControl4-0/labcontrol-docs/issues/20) | `docs/seguranca/escopo-pentest.md` |
| **SEC-04** | Avaliação Automatizada (DAST/SAST)| `labcontrol-docs` | @giovanimiamotob | [#21](https://github.com/labControl4-0/labcontrol-docs/issues/21) | `docs/seguranca/evidencias/dast-autenticado.md` |
| **SEC-05** | Exploração de Vulnerabilidades | `labcontrol-docs` | @victorgeroto | [#22](https://github.com/labControl4-0/labcontrol-docs/issues/22) | `docs/seguranca/evidencias/poc-vulnerabilidades.md` |
| **SEC-06** | Correção e Reteste de Achados | `labcontrol-docs` | @giovanimiamotob | [#23](https://github.com/labControl4-0/labcontrol-docs/issues/23) | `docs/seguranca/correcoes-reteste.md` |
| **SEC-07** | Relatório de Pentest e Cibersegurança | `labcontrol-docs` | @giovanimiamotob | [#24](https://github.com/labControl4-0/labcontrol-docs/issues/24) | `docs/relatorio-vulnerabilidades-pentest.pdf` |
| **BE-01 a 10** | Migração e Implementação Spring Boot | `labcontrol-api` | @ceduardooliveira | [#67 a #76](https://github.com/labControl4-0/labcontrol-api/issues) | Código Java/Spring + DTOs + Testes |
| **WEB-01 a 08** | Evolução da Interface Web Industrial | `labcontrol-web` | @AndreFernandes9010 | [#1 a #8](https://github.com/labControl4-0/labcontrol-web/issues) | Aplicação React + Tailwind + Vitest |
| **MOB-01 a 09** | App Mobile Offline-First e Push | `labcontrol-mobile` | @GustavoSilveira1012| [#2 a #10](https://github.com/labControl4-0/labcontrol-mobile/issues) | App Expo + SQLite + Push Receiver |
| **IOT-01 a 04** | Orquestração IoT e Tópicos MQTT | `labcontrol-iot` | @GustavoSilveira1012| [#1 a #4](https://github.com/labControl4-0/labcontrol-iot/issues) | Docker Compose + Mosquitto + Node-RED |
| **NEG-01 a 03** | Modelagem de Negócio e Validação | `labcontrol-docs` | @victorgeroto / @giovanimiamotob | [#25 a #27](https://github.com/labControl4-0/labcontrol-docs/issues) | `docs/negocio/` + Pitch |
| **REL-01 a 02** | Homologação Integrada e Release | `labcontrol-docs` | @victorgeroto / @giovanimiamotob | [#28 e #29](https://github.com/labControl4-0/labcontrol-docs/issues) | `docs/manifesto-entrega.md` + Release |

---

## 4. Limites e Exclusões do Escopo (O que NÃO está no escopo)

Para resguardar a viabilidade das entregas acadêmicas dentro do prazo sem incorrer em sobrecarga ou indefinições técnicas, ficam formalmente excluídos:
1. **Hardware Físico de Sensores em Produção Real:** Toda a telemetria industrial de chão de fábrica é modelada via simuladores reproduzíveis (Node-RED e publicadores Python em container Docker), não dependendo de aquisição física de microcontroladores ESP32 em bancada de fábrica.
2. **Alta Disponibilidade Geodistribuída (Multi-Região Cloud):** O foco arquitetural do 4º semestre é a reprodutibilidade local e em homologação conteinerizada (Docker Compose) e deploy cloud único, sem replicação ativa-ativa entre regiões.
3. **Migração de Histórico de Produção Não-Sintético:** Não haverá migração de dados reais de clientes legados; a base de dados de homologação utilizará geradores de dados e cenários sintéticos (`dump.sql`).
4. **Publicação em Lojas Oficiais (Apple App Store / Google Play Store):** O aplicativo mobile será distribuído via build de desenvolvimento Expo (`apk` standalone / development build local), sem submissão a lojas comerciais.

---

## 5. Pendências e Itens Sujeitos à Confirmação

- **Unidade Curricular Eletiva:** A confirmação do tema específico e rubrica da eletiva do 4º semestre pelo colegiado do UniSENAI. Assim que for publicada pelo docente, a atividade será vinculada em issue complementar sem impacto no caminho crítico atual.
- **Data Final da Banca de Defesa:** O cronograma macro está balizado no calendário letivo oficial, com previsão de homologação integrada 2 semanas antes do encerramento.
