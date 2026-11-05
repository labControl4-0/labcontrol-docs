# LabControl 4.0 - Matriz de Controle e Evidências de Governança de TI

**Identificador da Entrega:** `[S4][GOV-08]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/governanca/matriz-controle-evidencia.md`  
**Disciplina / Área:** Governança de TI  
**Responsável:** Giovani Miamoto (@giovanimiamotob)  
**Issue de Referência:** [#16](https://github.com/labControl4-0/labcontrol-docs/issues/16)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  

---

## 1. Finalidade da Matriz Controle-Evidência

Em conformidade com a rubrica acadêmica do UniSENAI (Alinhamento Estratégico 20%, Responsabilidades/RACI 15%, Riscos e Conformidade 20%, Controles no Repositório 25%, Indicadores e Nível de Serviço 10%, Plano Consolidado 10%), esta matriz estabelece a **rastreabilidade bidirecional** entre cada diretriz de governança, o controle implementado e a evidência concreta e verificável no código-fonte ou documentação.

---

## 2. Matriz Rastreável de Controles e Evidências

| ID Controle | Domínio / Diretriz de Governança | Descrição do Controle Implementado | Repositório | Arquivo / Artefato de Evidência | Status da Evidência |
| :---: | :--- | :--- | :--- | :--- | :---: |
| **CTL-01** | **Alinhamento e Escopo** | Decomposição analítica do sistema em 8 macro-pacotes rastreáveis com backlog oficial. | `labcontrol-docs` | [`docs/gestao/escopo-eap.md`](../gestao/escopo-eap.md) | **Implementado** |
| **CTL-02** | **Governança de Pessoas & RACI** | Atribuição formal de responsabilidades para os 5 membros em todas as disciplinas e decisão de alçadas. | `labcontrol-docs` | [`docs/governanca/partes-interessadas-raci.md`](partes-interessadas-raci.md) | **Implementado** |
| **CTL-03** | **Gestão de Mudanças & PRs** | Regra de branch protection na branch `main`, aprovação por pares e checklist obrigatório. | `labcontrol-docs` | [`docs/governanca/mudancas-ci.md`](mudancas-ci.md) + [PR #30](https://github.com/labControl4-0/labcontrol-docs/pull/30) | **Implementado** |
| **CTL-04** | **Automação de CI / Build** | Pipeline automatizado que valida integridade, links e ausência de segredos a cada commit/PR. | `labcontrol-docs` | [`.github/workflows/ci.yml`](../../.github/workflows/ci.yml) (Run #1 verde) | **Implementado** |
| **CTL-05** | **Prevenção de Vazamento de Segredos** | Step automatizado de scan anti-leak no CI e proibição estrita de credenciais em código versionado. | `labcontrol-docs` | [`.github/workflows/ci.yml`](../../.github/workflows/ci.yml) (Step `Secret Leak Scan`) | **Implementado** |
| **CTL-06** | **Gestão de Serviços e SLAs** | Catálogo dos 4 serviços de TI, categorização de incidentes (SEV 1 a 4) e runbooks de resolução rápida. | `labcontrol-docs` | [`docs/operacao/servico.md`](../operacao/servico.md) | **Implementado** |
| **CTL-07** | **Higienização e Auditoria de Logs** | Esquema JSON padronizado com mascaramento obrigatório de tokens, senhas e dados sensíveis. | `labcontrol-docs` | [`docs/operacao/servico.md`](../operacao/servico.md#3-padrão-de-logging-sanitizado-e-observabilidade) | **Implementado** |
| **CTL-08** | **Modelagem de Riscos & Ameaças** | Análise STRIDE cobrindo Web, Mobile, Broker e API, priorizada com cálculo de impacto DREAD. | `labcontrol-docs` | [`docs/seguranca/modelagem-ameacas.md`](../seguranca/modelagem-ameacas.md) | **Implementado** |
| **CTL-09** | **Armazenamento Seguro Mobile** | Migração do armazenamento de credenciais de AsyncStorage simples para Expo SecureStore. | `labcontrol-mobile` | [PR #12](https://github.com/labControl4-0/labcontrol-mobile/pull/12) (`feature/MOB-02-armazenamento-seguro`) | **Implementado** |
| **CTL-10** | **Resiliência e Operação Offline** | Fila local de transações com SQLite para garantir contingência sem rede no chão de fábrica. | `labcontrol-mobile` | [PR #13](https://github.com/labControl4-0/labcontrol-mobile/pull/13) (`feature/MOB-03-sqlite-fila-offline`) | **Implementado** |
| **CTL-11** | **Isolamento de Rede IoT** | Orquestração Docker com rede interna dedicada (`labcontrol-network`) conectando Node-RED e Mosquitto. | `labcontrol-iot` | [`docker-compose.yml`](https://github.com/labControl4-0/labcontrol-iot/blob/main/docker-compose.yml) | **Implementado** |
| **CTL-12** | **Publicação Consolidada do Plano** | Versão PDF completa e legível do Plano de Governança de TI disponível para download no repositório. | `labcontrol-docs` | [`docs/plano-governanca-ti.pdf`](../plano-governanca-ti.pdf) | **Implementado** |

---

## 3. Instruções de Verificação e Auditoria Acadêmica

Qualquer avaliador docente pode auditar os controles desta matriz executando os seguintes passos no repositório:
1. **Clone Limpo:**
   ```bash
   git clone https://github.com/labControl4-0/labcontrol-docs.git
   cd labcontrol-docs
   ```
2. **Conferência do PDF:** Abrir o arquivo `docs/plano-governanca-ti.pdf` em qualquer leitor de PDF padrão (Acrobat Reader, Chrome, Edge) e verificar correspondência com as fontes markdown em `docs/governanca/`.
3. **Auditoria de CI no GitHub:** Acessar a aba [Actions](https://github.com/labControl4-0/labcontrol-docs/actions) e constatar que o workflow `CI - Docs Quality & Compliance` executou e passou com sucesso.
