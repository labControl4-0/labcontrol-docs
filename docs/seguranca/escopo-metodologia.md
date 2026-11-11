# LabControl 4.0 - Escopo, Ambiente e Metodologia dos Testes de Segurança

**Identificador da Entrega:** `[S4][SEC-03]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/seguranca/escopo-metodologia.md`  
**Disciplina / Área:** Cibersegurança  
**Responsável:** Victor Geroto (@victorgeroto)  
**Issue de Referência:** [#20](https://github.com/labControl4-0/labcontrol-docs/issues/20)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  
**Status:** Rascunho v0.1 (2026-11-11) — **a autorização do grupo (seção 2) ainda não foi assinada; nenhum teste pode começar antes disso**

---

## 1. Finalidade

Definir **o que pode ser testado, onde, por quem, com quais limites** antes de qualquer varredura ou exploração (SEC-04, SEC-05, SEC-06). Este documento impede testes em terceiros ou em produção e deve ser citado como "Escopo e Metodologia" no relatório final (SEC-07).

Referências metodológicas: OWASP Web Security Testing Guide e NIST SP 800-115, como já adotado em [`../relatorio-vulnerabilidades-pentest.md`](../relatorio-vulnerabilidades-pentest.md).

---

## 2. Autorização e Regras de Engajamento

### 2.1 Declaração de autorização do grupo

> Os integrantes abaixo, **titulares dos repositórios e do ambiente de teste descritos neste documento**, autorizam a execução de testes de segurança **somente** sobre o escopo da seção 4, **no ambiente da seção 3**, para fins acadêmicos. Nenhum teste será dirigido a sistemas de terceiros.

| Integrante | Autoriza | Data |
| :--- | :---: | :--- |
| Giovani Miamoto | ☐ | __/__/____ |
| Victor Geroto | ☐ | __/__/____ |
| Carlos Eduardo Oliveira | ☐ | __/__/____ |
| André Fernandes | ☐ | __/__/____ |
| Gustavo Silveira | ☐ | __/__/____ |

Ciência do docente da disciplina: ☐ __/__/____ *(registrar como o docente confirmou)*.

### 2.2 Regras de engajamento

| Item | Regra |
| :--- | :--- |
| **Responsável pela execução** | Victor Geroto (pentest prático); apoio técnico de Giovani Miamoto (varredura automatizada) |
| **Janela de testes** | *a definir e comunicar à equipe antes de cada execução* (horário e duração) |
| **Comunicação** | Aviso no canal da equipe antes e depois de cada execução; achados reportados por issue |
| **Critérios de interrupção** | Parar imediatamente se: o alvo não estiver na lista da seção 4; houver tráfego para fora do ambiente local; dados reais de qualquer pessoa forem acessados; o ambiente ficar instável |
| **Intensidade** | Sem testes de negação de serviço volumétrica; taxa de requisições limitada ao necessário para a validação do achado |
| **Escalonamento** | Dúvida de escopo → parar e consultar a equipe; dúvida regulatória → docente |

---

## 3. Ambiente de Teste

| Item | Definição |
| :--- | :--- |
| **Tipo** | Ambiente **próprio, local e isolado**, subido por Docker Compose na máquina do executor |
| **URLs / portas locais** | API `http://localhost:8080` (Swagger em `/swagger`); web `http://localhost:3000`; MQTT `localhost:1883` (WebSocket `9001`); Node-RED `http://localhost:1880`; PostgreSQL `localhost:5432` |
| **Isolamento** | Rede Docker `labcontrol-network`; nenhum serviço apontado para hosts externos, exceto o provedor de IA (ver seção 4.2) |
| **Dados** | **Somente sintéticos**; banco criado do zero ou restaurado de backup sintético |
| **Contas de teste** | Ao menos **dois usuários sintéticos** (ex.: `usuario-a@example.test`, `usuario-b@example.test`) para testar isolamento entre usuários; credenciais em `.env` local, **nunca** no repositório |
| **Backup antes do teste** | Executar o backup de `docs/rollback.md` (GOV-07) e registrar o hash |
| **Restauração depois do teste** | Restaurar o banco ao estado anterior; remover contas e dados criados ("limpeza") |

### 3.1 Versão identificada do alvo

Commits da `main` de cada repositório em 2026-11-11. **Registrar novamente (SHA e data) no início de cada execução**; se houver mudança de versão, os resultados anteriores não valem para a nova.

| Componente | Repositório | Commit (`main`) |
| :--- | :--- | :--- |
| API (.NET 9) | `labcontrol-api` | `84da384` |
| Web | `labcontrol-web` | `6b2e6b6` |
| Mobile | `labcontrol-mobile` | `ff07943` |
| IoT | `labcontrol-iot` | `56c166e` |
| Documentação | `labcontrol-docs` | `1a2a30e` |

> O backend em Spring Boot (BE-02) **ainda não existe**. Ao ser criado, e novamente após o corte de API (BE-10), este escopo e a tabela acima devem ser revisados.

---

## 4. Escopo

### 4.1 Dentro do escopo

| Superfície | Detalhe | Tipo de análise |
| :--- | :--- | :--- |
| **API REST (versão da `main`)** | Famílias de rotas: `/api/Auth`, `/api/users`, `/api/plants`, `/api/sectors`, `/api/machines`, `/api/machine-metrics`, `/api/machine-events`, `/api/chat`, `/api/iot/metrics`; identificadores do tipo GUID | Automatizada autenticada e manual |
| **Aplicação web** | SPA servida pelo nginx; armazenamento do token no navegador; chamadas à API | Automatizada e manual |
| **Aplicativo mobile** | Build local; armazenamento de sessão; chamadas à API | Análise estática e manual |
| **Broker MQTT** | Mosquitto local: autenticação, controle de tópicos, mensagens malformadas | Manual |
| **Orquestração Docker** | Portas expostas, rede, variáveis de ambiente | Revisão de configuração |
| **Código e configuração versionados** | Busca de segredos e dependências vulneráveis | Análise estática (SEC-01) |

### 4.2 Fora do escopo (exclusões)

| Exclusão | Motivo |
| :--- | :--- |
| **Qualquer host de nuvem ou "produção"** | Só entra se houver **titularidade do grupo confirmada e autorização documentada**. Isso inclui o endereço de nuvem referenciado no código do aplicativo mobile, **que deve ser tratado como fora do escopo até essa confirmação** |
| **Serviços de terceiros** | Provedor de IA (Gemini), GitHub, Expo/EAS, Docker Hub, provedores de nuvem — apenas o tráfego do próprio ambiente até eles, **sem testá-los** |
| **Redes e sistemas da instituição** | Sem autorização específica |
| **Negação de serviço volumétrica / DDoS** | Risco à infraestrutura compartilhada; já excluída no relatório existente |
| **Engenharia social, phishing, acesso físico** | Fora do escopo acadêmico |
| **Hardware físico de sensores** | Excluído do projeto (EAP §4) |
| **Contas ou dados reais de qualquer pessoa** | Apenas contas e dados sintéticos |

---

## 5. Metodologia e Ferramentas

| Fase | Atividade | Ferramentas (registrar **versão exata** no relatório) | Saída |
| :--- | :--- | :--- | :--- |
| 1. Preparação | Subir o ambiente, registrar versões, backup, contas de teste | Docker Compose, `git` | Ambiente identificado |
| 2. Varredura automatizada autenticada | DAST e SAST no escopo da seção 4.1 | OWASP ZAP (o relatório SEC-04 cita a versão 2.15.0), `npm audit` (web e mobile), varredura de segredos | Lista de achados |
| 3. Triagem | Eliminar falsos positivos; classificar risco | Revisão manual | Achados confirmados |
| 4. Exploração controlada (SEC-05) | Provas limitadas a **achados confirmados**, sem ampliar além do necessário para demonstrar o impacto | `curl`, cliente HTTP, cliente MQTT | Evidências sanitizadas |
| 5. Remediação e reteste (SEC-06) | Corrigir e repetir o teste do achado | Mesmas ferramentas | Comparativo antes × depois |
| 6. Relatório (SEC-07) | Consolidar, com limitações e referências | Markdown/PDF | Relatório |

**Regra para exploração:** só entram na fase 4 vulnerabilidades **realmente confirmadas** na fase 3, na versão identificada. Se não houver duas, **registra-se a limitação e alinha-se a alternativa com o docente**; resultados não são inventados nem o ambiente é enfraquecido para cumprir a rubrica.

---

## 6. Evidências e Tratamento dos Resultados

- Guardar em `docs/evidencias/seguranca/`: comandos, entradas, saídas esperadas × observadas, versão, impacto e limpeza.
- **Sanitizar** antes de versionar: tokens, senhas, cabeçalhos de autorização, IPs reais e qualquer dado pessoal são mascarados ou substituídos por valores sintéticos.
- Capturas de tela sem informação sensível; arquivos brutos de ferramentas (que podem conter tokens) **não** são versionados.
- O CI de documentação bloqueia padrões de segredos em `docs/`; mesmo assim, a revisão manual do PR é obrigatória.

---

## 7. Reconciliação com os Relatórios Existentes (a resolver antes de SEC-05)

O relatório de vulnerabilidades já na `main` ([`relatorio-vulnerabilidades-pentest.md`](../relatorio-vulnerabilidades-pentest.md)) e a avaliação autenticada (SEC-04) descrevem rotas com prefixo `/api/v1/` (por exemplo `machines/{id}`, `telemetry/recent`, `alerts`, `sync`) e identificadores numéricos. Na **versão identificada da `main`** (seção 3.1) a API expõe as famílias de rotas da seção 4.1, com identificadores GUID, e **não** há rotas `telemetry`, `alerts` ou `sync`.

**Ação necessária:** antes de escolher as duas vulnerabilidades para SEC-05, registrar **contra qual versão e ambiente cada achado foi obtido** (SHA e data) e **reconfirmar cada achado** na versão do escopo. Achados que não puderem ser reproduzidos na versão testada **não** entram em SEC-05 e devem constar como limitação.

---

## 8. Limitações (a constar no relatório)

1. Ambiente local e dados sintéticos não reproduzem carga nem topologia de produção.
2. Resultados valem para a versão identificada; a migração para Spring Boot invalida resultados anteriores.
3. Ferramentas automatizadas geram falsos positivos e negativos.
4. Testes de negação de serviço volumétrica, engenharia social e acesso físico não foram realizados.
5. Hardware de sensores não faz parte do ambiente.

---

## 9. Critérios de Aceite (issue #20)

| Critério | Situação |
| :--- | :--- |
| Plano impede varredura em terceiros/produção | Atendido nas seções 2.2, 4.2 e critérios de interrupção; **depende da autorização assinada (2.1)** |
| Ambiente tem versão identificada e dados isolados | Atendido (seção 3 e 3.1); **registrar SHA novamente a cada execução** |
| Limitações estão no relatório | Atendido (seção 8); incluir no SEC-07 |
| Partes analisadas e fora do escopo, ambiente próprio/autorizado, contas sintéticas, ferramentas e versões | Atendido; **versões das ferramentas a registrar na execução** |

**Dependências:** GOV-03 (registro de riscos, #11) e BE-02 (#68, aplicação Spring — aberta).

---

## 10. Histórico de Alterações

| Versão | Data | Autor | Alteração |
| :--- | :--- | :--- | :--- |
| 0.1 | 2026-11-11 | @victorgeroto | Escopo, ambiente, regras de engajamento, metodologia e reconciliação com os relatórios existentes |
