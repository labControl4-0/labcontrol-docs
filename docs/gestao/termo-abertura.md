# LabControl 4.0 - Termo de Abertura e Continuidade do Projeto

**Identificador da Entrega:** `[S4][GP-01]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/gestao/termo-abertura.md`  
**Disciplina / Área:** Gestão de Projetos  
**Responsável:** Victor Geroto (@victorgeroto)  
**Issue de Referência:** [#1](https://github.com/labControl4-0/labcontrol-docs/issues/1)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  
**Status:** Rascunho v0.1 (2026-11-11) — pendente de validação da equipe (ver seção 9)

---

## 1. Identificação do Projeto

| Item | Descrição |
| :--- | :--- |
| **Projeto** | LabControl 4.0 — continuidade no Projeto Integrador IV (PI-IV) |
| **Instituição / Curso** | Faculdade de Tecnologia SENAI (UniSENAI - Sorocaba) — CST em Análise e Desenvolvimento de Sistemas, 4º semestre |
| **Organização GitHub** | [labControl4-0](https://github.com/labControl4-0) |
| **Repositórios** | `labcontrol-docs`, `labcontrol-api`, `labcontrol-web`, `labcontrol-mobile`, `labcontrol-iot` |
| **Quadro de trabalho** | [GitHub Project 3](https://github.com/orgs/labControl4-0/projects/3) |
| **Base de continuidade** | Entregas dos semestres anteriores (Sprint 1 e 2 em [`Sprints/`](../../Sprints/entrega01/entregaSprint01.md)) e o documento de demanda [SAGA](../../Sprints/entrega01/documentoSAGA.md) |
| **Estado verificado em** | 2026-11-11 — `main` de cada repositório (docs `1a2a30e`, api `84da384`, web `6b2e6b6`, mobile `ff07943`, iot `56c166e`) |

---

## 2. Problema Industrial e Oportunidade

Em laboratórios e plantas industriais, o acompanhamento de máquinas costuma depender de inspeção presencial e de registros manuais. Isso atrasa a percepção de falhas (superaquecimento, vibração anormal), dificulta localizar o equipamento afetado e deixa o consumo energético sem visibilidade. O **LabControl 4.0** propõe reunir, em uma única plataforma, a **planta baixa interativa**, o **monitoramento de máquinas por telemetria** (MQTT) e os **alertas/eventos**, acessíveis por web e mobile.

> A magnitude do problema (tempo de reação, desperdício) é **hipótese de negócio** neste termo. Medições dessa natureza só serão tratadas como resultado quando houver evidência anexada (ver NEG-01, NEG-02 e REL-01).

---

## 3. Patrocinador Acadêmico, Usuários e Aprovadores

| Papel | Quem | Interesse |
| :--- | :--- | :--- |
| **Patrocinador acadêmico / aprovador** | Docentes do PI-IV e das disciplinas vinculadas (Governança de TI, Cibersegurança, Gestão de Projetos, Backend, Mobile) — *nomes a preencher pela equipe* | Aderência às rubricas, evidências no repositório, entrega integrada |
| **Usuário-alvo: operador industrial** | Operador / técnico de manutenção | Alertas claros, localizar a máquina, operar mesmo sem rede |
| **Usuário-alvo: supervisor / gestor** | Supervisor de manutenção, gestor da planta | Visão consolidada do estado das máquinas e histórico de eventos |
| **Equipe de desenvolvimento** | 5 integrantes (seção 6) | Prazos viáveis, processos claros |

O mapeamento completo de stakeholders e a matriz RACI estão em [`partes-interessadas-raci.md`](../governanca/partes-interessadas-raci.md).

---

## 4. Valor Esperado

- **Para o usuário:** menos tempo para perceber e localizar uma falha; registro de ocorrências mesmo sem rede (mobile offline).
- **Para a gestão:** visão única de plantas, setores e máquinas e histórico de eventos.
- **Para o semestre (acadêmico):** demonstrar engenharia integrada — backend, web, mobile e IoT — com governança, segurança e evidências rastreáveis.

---

## 5. Objetivos Mensuráveis e Vínculo com o Quadro

Estado do quadro em 2026-11-11: **60 issues da Sprint 4, 14 concluídas (23%)**; 425 h estimadas, das quais 89 h concluídas (21%) — detalhes em `docs/gestao/cronograma-custos.md` (GP-03).

| # | Objetivo | Indicador / meta (verificável) | Entregas no quadro | Situação em 2026-11-11 |
| :---: | :--- | :--- | :--- | :--- |
| O1 | Migrar o backend de .NET 9 para Java 21 / Spring Boot 3 | Rotas hoje usadas por web e mobile com paridade documentada; corte de API realizado e validado | BE-01 a BE-10 (`labcontrol-api` #67–#76) | 0 de 10 concluídas; nenhuma branch de Spring no repositório |
| O2 | Mobile offline-first com sincronização | Registro offline sincronizado sem duplicidade; push abrindo a ocorrência correta | MOB-01 a MOB-09 (`labcontrol-mobile` #2–#10) | 0 de 9 concluídas; PRs #11–#16 abertos (MOB-01 a MOB-06) |
| O3 | Web com dashboard e central de alertas | Dashboard consumindo a API real; testes automatizados úteis | WEB-01 a WEB-08 (`labcontrol-web` #1–#8) | 0 de 8 concluídas; sem PRs |
| O4 | Telemetria padronizada e broker protegido | Tópico/payload únicos; broker recusa conexão anônima (teste reproduzível) | IOT-01 a IOT-04 (`labcontrol-iot` #1–#4) | 0 de 4 concluídas; `allow_anonymous true` na `main` |
| O5 | Governança rastreável | 100% das issues P0 com evidência vinculada; revisão por par e proteção de branch ativas | GP, GOV (`labcontrol-docs`) | 14 de 29 issues de docs concluídas; proteção de branch desativada nos 5 repositórios |
| O6 | Segurança verificável | Nenhuma credencial real versionada; achados confirmados corrigidos e retestados | SEC-01 a SEC-07 | SEC-02, 04, 06 e 07 concluídas; SEC-01, 03 e 05 abertas |
| O7 | Entrega integrada homologada | Fluxo ponta a ponta executado na mesma versão dos 4 componentes, falhas registradas em issues | REL-01, REL-02 | REL-02 concluída; REL-01 aberta (depende de BE-10, MOB-09, WEB-08, IOT-04) |

---

## 6. Equipe e Papéis

| Integrante | GitHub | Frentes principais |
| :--- | :--- | :--- |
| Giovani Miamoto | @giovanimiamotob | Governança, gestão (EAP/Kanban), segurança (STRIDE/DAST) |
| Victor Geroto | @victorgeroto | Planejamento, riscos, políticas, pentest prático e homologação |
| Carlos Eduardo Oliveira | @ceduardooliveira | Backend: migração para Spring Boot |
| André Fernandes | @AndreFernandes9010 | Frontend web |
| Gustavo Silveira | @GustavoSilveira1012 | Mobile e IoT |

Responsabilidades detalhadas (Responsible/Accountable/Consulted/Informed) em [`partes-interessadas-raci.md`](../governanca/partes-interessadas-raci.md).

---

## 7. Escopo do Semestre: o que existe, o que está em andamento e o que é só proposta

Para evitar que algo apenas descrito seja lido como implementado, o escopo é separado em quatro grupos. A classificação vem da leitura da `main` de cada repositório e dos PRs/issues abertos em 2026-11-11; **"existe na main" não significa homologado** — o fluxo ponta a ponta só é comprovado em REL-01.

### 7.1 Existe na `main` (implementado, não homologado)

| Componente | Capacidades |
| :--- | :--- |
| `labcontrol-api` (.NET 9) | Cadastro/login com JWT; CRUD de plantas, setores e máquinas; métricas e eventos de máquinas; ingestão de telemetria por MQTT e HTTP; chat com IA (Gemini) |
| `labcontrol-web` (React/Vite) | Login e cadastro; gestão de plantas; editor de planta baixa (setores e máquinas) |
| `labcontrol-mobile` (Expo) | Login e cadastro; lista de plantas e máquinas; visualização da planta baixa; chat; perfil; dashboard com **dados simulados** |
| `labcontrol-iot` | Mosquitto e Node-RED em Docker Compose (simulação; sem hardening) |
| `labcontrol-docs` | Documentos de gestão, governança e segurança; workflow de CI de documentação |

### 7.2 Em desenvolvimento (PR aberto, não mesclado)

`labcontrol-mobile`: MOB-01 (#11), MOB-02 (#12), MOB-03 (#13), MOB-04 (#14), MOB-05 (#15) e MOB-06 (#16). MOB-08 tem branch, sem PR.

### 7.3 Previsto (issue aberta, sem código na `main`)

BE-01 a BE-10 (migração Spring Boot); WEB-01 a WEB-08; IOT-01 a IOT-04; MOB-07 e MOB-09; GOV-01, 03, 05, 07, 09; SEC-01, 03, 05; GP-01, 03, 05, 07; NEG-01, 03; REL-01.

### 7.4 Descrito no SAGA e **não implementado**

Perfis de acesso com permissões aplicadas (a coluna de perfil existe, sem regras); recuperação de senha (existe só a tela no mobile); CPF e cargo no cadastro (a API não coleta — ver GOV-05); integrações com RH, segurança do trabalho e centro de operações; trilhas de auditoria e geração automática de relatórios; controle remoto de iluminação e equipamentos; monitoramento de temperatura/umidade/ocupação por sala; painel de consumo energético no web (`Dashboard.tsx` está vazio).

### 7.5 Fora do semestre (exclusões formais)

Conforme [`escopo-eap.md`](escopo-eap.md) §4: hardware físico de sensores; alta disponibilidade multirregião; migração de dados reais de produção; publicação em lojas de aplicativos.

---

## 8. Premissas, Restrições e Riscos Iniciais

**Restrição tripla** (detalhada em GP-03):

| Dimensão | Estado |
| :--- | :--- |
| **Escopo** | 60 issues / 425 h; 255 h abertas em issues P0 |
| **Prazo** | Data final da banca ainda **não confirmada** pelo docente (ver [`escopo-eap.md`](escopo-eap.md) §5); datas só serão fixadas depois |
| **Custo** | Sem orçamento financeiro; custos de infraestrutura e dispositivo Android a levantar |

**Premissas:** dados de homologação sintéticos; ambiente reproduzível por Docker Compose; Android físico disponível para o *development build* (MOB-05).

**Riscos iniciais (resumo; registro completo em GOV-03):** atraso da migração Spring (caminho crítico); credenciais versionadas em repositório público; ausência de CI e de proteção de branch nos repositórios de código; broker sem autenticação; dependência de uma única pessoa por frente.

---

## 9. Critérios de Aceite e Validação

| Critério (issue #1) | Situação |
| :--- | :--- |
| Equipe valida objetivo e escopo | **Pendente** — registrar abaixo |
| Nenhum recurso apenas descrito no SAGA é apresentado como implementado | Atendido neste rascunho (seção 7); revisar a cada marco |

**Registro de validação** *(preencher após a reunião de alinhamento)*:

| Integrante | Validou objetivos e escopo (data) |
| :--- | :--- |
| Giovani Miamoto | ☐ __/__/____ |
| Victor Geroto | ☐ __/__/____ |
| Carlos Eduardo Oliveira | ☐ __/__/____ |
| André Fernandes | ☐ __/__/____ |
| Gustavo Silveira | ☐ __/__/____ |

---

## 10. Histórico de Alterações

| Versão | Data | Autor | Alteração |
| :--- | :--- | :--- | :--- |
| 0.1 | 2026-11-11 | @victorgeroto | Rascunho inicial a partir do estado verificado dos repositórios |
