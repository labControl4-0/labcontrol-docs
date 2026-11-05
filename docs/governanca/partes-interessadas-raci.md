# LabControl 4.0 - Mapeamento de Partes Interessadas, Matriz RACI e Governança de Decisões

**Identificador da Entrega:** `[S4][GOV-02]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/governanca/partes-interessadas-raci.md`  
**Disciplina / Área:** Governança de TI  
**Responsável:** Giovani Miamoto (@giovanimiamotob)  
**Issue de Referência:** [#10](https://github.com/labControl4-0/labcontrol-docs/issues/10)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  

---

## 1. Mapeamento de Partes Interessadas (Stakeholders)

O sucesso da governança do LabControl 4.0 depende da clara identificação dos grupos de interesse, de suas expectativas e de seu nível de influência no ciclo de vida da solução.

| Stakeholder / Papel | Representantes | Interesses e Expectativas Principais | Grau de Influência | Grau de Interesse |
| :--- | :--- | :--- | :--- | :--- |
| **Banca Docente Avaliadora** | Professores das disciplinas de Governança, Segurança, GP, Mobile, Backend e PI | Conformidade metodológica, aderência às rubricas acadêmicas, evidências no repositório e comprovação da entrega integrada. | Alto | Alto |
| **Operador Industrial (Chão de Fábrica)** | Usuário final do Web e Mobile | Interface intuitiva, legibilidade em ambientes de pouca/alta luz, alertas em tempo real e capacidade de operar offline. | Médio | Alto |
| **Supervisor / Gestor de Manutenção** | Gestor da planta fabril | Visão consolidada de indicadores (status das máquinas, tempo de resposta a falhas, histórico de telemetria). | Alto | Alto |
| **Equipe de Desenvolvimento & Arquitetura** | Giovani Miamoto, Victor Geroto, Carlos Eduardo, André Fernandes, Gustavo Silveira | Código limpo, desacoplamento arquitetural, estabilidade de APIs, processos claros e cumprimento de prazos. | Alto | Alto |
| **Auditoria e Cibersegurança** | Time interno de segurança / Docente de Segurança | Rastreabilidade de acessos, ausência de credenciais em código, mitigação de riscos e proteção contra ataques comuns. | Alto | Médio |

---

## 2. Matriz RACI do LabControl 4.0

A matriz RACI estabelece a atribuição clara de papéis e responsabilidades operacionais para cada frente do projeto:
- **R - Responsible (Responsável pela Execução):** Quem desenvolve a tarefa.
- **A - Accountable (Dono da Entrega / Aprovador):** Quem responde pelo resultado final (apenas 1 por linha).
- **C - Consulted (Consultado):** Quem apoia com insumos técnicos ou validação.
- **I - Informed (Informado):** Quem é mantido informado sobre o andamento e conclusão.

### Tabela da Matriz RACI por Frente de Trabalho

| Frente de Trabalho / Pacote EAP | Giovani Miamoto | Victor Geroto | Carlos Eduardo | André Fernandes | Gustavo Silveira | Docentes |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Gestão de Projetos: EAP, Backlog e Acordos (GP-02, 04, 06)** | **A / R** | C | I | I | I | I |
| **Gestão de Projetos: Termo, Custos e Sprints (GP-01, 03, 05, 07)** | C | **A / R** | I | I | I | I |
| **Governança: Stakeholders, RACI, CI e Observabilidade (GOV-02, 04, 06, 08)** | **A / R** | C | C | C | C | I |
| **Governança: Plano Base, Riscos, Backup e Políticas (GOV-01, 03, 05, 07, 09)** | C | **A / R** | I | I | I | I |
| **Cibersegurança: Modelagem STRIDE, DAST e Relatório (SEC-02, 04, 06, 07)** | **A / R** | C | C | C | C | I |
| **Cibersegurança: Segredos, Escopo e Pentest (SEC-01, 03, 05)** | C | **A / R** | I | I | I | I |
| **Backend: Migração Spring Boot, JPA, Auth e APIs (BE-01 a 10)** | I | C | **A / R** | C | C | I |
| **Frontend Web: Dashboard, Planta Baixa e A11y (WEB-01 a 08)** | C | I | C | **A / R** | I | I |
| **Mobile: SQLite Offline, Push e Sincronização (MOB-01 a 09)** | C | I | C | I | **A / R** | I |
| **IoT: Broker MQTT, Node-RED e Simulação (IOT-01 a 04)** | I | I | C | I | **A / R** | I |
| **Negócios & Validação de Usuário (NEG-01 a 03)** | **R** | **A / R** | I | C | C | I |
| **Homologação Integrada e Release Final (REL-01, 02)** | **A / R** | **A / R** | C | C | C | **I / Aprovador** |

---

## 3. Modelo de Tomada de Decisão e Governança

Para manter a integridade arquitetural sem burocracia excessiva, adotam-se três fóruns de decisão:

```
[ Decisão Operacional ] -------------> [ Decisão de Arquitetura (ADR) ] -------------> [ Decisão de Escopo / Crítica ]
   (Desenvolvedor)                        (Consenso da Equipe no PR)                     (Reunião Geral + Docente)
```

1. **Decisões Operacionais (Nível 1):** Escolha de bibliotecas utilitárias menores, refatoração interna de componentes ou ajustes de layout. Decididas pelo desenvolvedor responsável com validação no Code Review do PR.
2. **Decisões de Arquitetura de Software (Nível 2):** Contratos de API (Swagger/OpenAPI), modelos de dados JPA, protocolos de rede (MQTT payload) e estratégia de sincronização offline. Devem ser documentadas no PR com aprovação mínima de 2 membros envolvidos (ex: Backend + Mobile/Web).
3. **Decisões Estratégicas e de Escopo (Nível 3):** Alterações nas datas de entrega, exclusão ou inclusão de pacotes da EAP e mudanças estruturais de infraestrutura. Exigem consenso do time e alinhamento com a orientação docente.

---

## 4. Matriz de Escalonamento de Problemas e Conflitos

Em caso de divergências técnicas ou bloqueios prolongados:
- **Nível 1 (Autonomia da Dupla):** Conversa técnica direta entre as partes envolvidas para alinhamento em até 12 horas.
- **Nível 2 (Colegiado da Equipe):** Se o bloqueio persistir, o tema é levado para votação na Weekly Sync ou sessão extraordinária; o responsável pelo pacote (`Accountable` na matriz RACI) detém o voto de desempate técnico.
- **Nível 3 (Mediação Docente):** Dúvidas regulatórias, de escopo do semestre ou rubricas de avaliação são formalmente submetidas aos professores orientadores.
