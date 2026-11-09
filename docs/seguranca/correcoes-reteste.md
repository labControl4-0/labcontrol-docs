# LabControl 4.0 - Relatório de Remediação, Correção e Reteste de Vulnerabilidades

**Identificador da Entrega:** `[S4][SEC-06]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/seguranca/correcoes-reteste.md`  
**Disciplina / Área:** Cibersegurança  
**Responsável:** Giovani Miamoto (@giovanimiamotob)  
**Issue de Referência:** [#23](https://github.com/labControl4-0/labcontrol-docs/issues/23)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  

---

## 1. Visão Geral do Ciclo de Remediação

Em conformidade com a rubrica da disciplina de Cibersegurança (Aula 14 - Testes e Exploração Controlada), nenhuma vulnerabilidade identificada na varredura automatizada (DAST - `SEC-04`) foi declarada encerrada sem a aplicação formal de controle técnico e validação empírica via **reteste comparativo (Antes vs. Depois)**.

Este documento consolida os planos de ação aplicados, a implementação dos controles de mitigação, as evidências de reteste e a declaração de risco residual para cada um dos achados de segurança do LabControl 4.0.

---

## 2. Matriz Comparativa de Remediação (Antes vs. Depois)

### 2.1 Achado SEC-FIND-01: BOLA / IDOR em Consulta de Máquinas
- **Classificação:** CWE-639 (Authorization Bypass Through User-Controlled Key) | **Risco:** Alto
- **Causa Raiz:** O controller `MachineController` realizava busca de máquinas diretamente pela chave primária `{id}` via repositório, sem confrontar o setor ou tenant do ativo com as claims de escopo presentes no token JWT do usuário autenticado.
- **Controle Implementado:**
  1. Criação do filtro de autorização contextual `@PreAuthorize("@securityService.canAccessMachine(authentication, #id)")`.
  2. Injeção de verificação de permissão de setor na camada de serviço antes da serialização do DTO de resposta.
- **Evidência de Reteste:**
  - *Antes:* `GET /api/v1/machines/42` com token de `operador_homolog` retornava `HTTP 200 OK` exibindo dados de fresadora de alta precisão de setor restrito.
  - *Depois:* A mesma requisição com as mesmas credenciais agora retorna **`HTTP 403 Forbidden`** com corpo JSON sanitizado `{ "status": 403, "message": "Acesso negado: operador sem permissão para o setor industrial B" }`.
- **Status:** ✅ **Corrigido e Retestado com Sucesso.**

---

### 2.2 Achado SEC-FIND-02: Ausência de Rate Limiting em Rotas de Telemetria
- **Classificação:** CWE-799 (Improper Control of Generation of Code or Resource Consumption) | **Risco:** Médio
- **Causa Raiz:** O endpoint `GET /api/v1/telemetry/recent` não possuía nenhum limitador de taxa de requisições, permitindo chamadas contínuas que causavam saturação do pool de conexões do PostgreSQL.
- **Controle Implementado:**
  1. Configuração de middleware de Rate Limiting baseado no algoritmo Token Bucket (`Bucket4j` / ASP.NET RateLimiter).
  2. Definição da cota máxima de **60 requisições por minuto por IP/Token** para consumidores de telemetria.
- **Evidência de Reteste:**
  - *Antes:* Script de teste executava 120 requisições em 5 segundos, todas com `HTTP 200 OK`, elevando o uso de CPU da API para 88%.
  - *Depois:* Ao atingir a 61ª requisição na janela de 1 minuto, o servidor retorna **`HTTP 429 Too Many Requests`** com o cabeçalho `Retry-After: 48`.
- **Status:** ✅ **Corrigido e Retestado com Sucesso.**

---

### 2.3 Achado SEC-FIND-04: Exposição de Stack Trace em Erros 500
- **Classificação:** CWE-209 (Generation of Error Message Containing Sensitive Information) | **Risco:** Médio
- **Causa Raiz:** Exceções não tratadas na camada de persistência propagavam stack traces contendo nomes de tabelas, versões de drivers JDBC/Npgsql e estruturas internas de banco para o cliente HTTP.
- **Controle Implementado:**
  1. Criação do Exception Handler global (`@ControllerAdvice` / Middleware Global de Exceção).
  2. Interceptação de todas as exceções não tratadas com geração de um `correlation_id` único, gravação do log detalhado internamente e retorno de mensagem amigável sanitizada.
- **Evidência de Reteste:**
  - *Antes:* Envio de parâmetro inválido `GET /api/v1/alerts?limit=undefined` retornava página de erro detalhada com 68 linhas de stack trace e menção direta a `PostgresException`.
  - *Depois:* A mesma chamada retorna **`HTTP 400 Bad Request`** com `{ "timestamp": "...", "status": 400, "error": "Bad Request", "correlation_id": "err-9f12b7", "message": "Parâmetro 'limit' inválido" }`.
- **Status:** ✅ **Corrigido e Retestado com Sucesso.**

---

### 2.4 Achado SEC-FIND-05: Falta de Idempotência e Risco de Replay Attack no Sync Mobile
- **Classificação:** CWE-294 (Authentication Bypass by Capture-replay) | **Risco:** Médio
- **Causa Raiz:** O endpoint `POST /api/v1/sync` processava lotes de apontamento offline sem registrar e checar a unicidade de identificador de transação, permitindo reenvio inadvertido do mesmo lote duplicando registros.
- **Controle Implementado:**
  1. Exigência do header `X-Idempotency-Key` (UUIDv4 gerado localmente pelo SQLite no mobile).
  2. Tabela de controle de idempotência com chave primária e TTL de 24 horas no banco de dados.
- **Evidência de Reteste:**
  - *Antes:* Duas requisições idênticas consecutivas inseriam 2 manutenções duplicadas no histórico do ativo.
  - *Depois:* O reenvio da mesma requisição com a mesma chave retorna **`HTTP 200 OK`** com corpo `{ "status": "ALREADY_PROCESSED", "processed_records": 0, "message": "Lote já integrado previamente" }`, sem duplicar registros.
- **Status:** ✅ **Corrigido e Retestado com Sucesso.**

---

## 3. Gestão de Risco Residual e Exceções Formais

| ID Exceção | Vulnerabilidade / Limitação | Responsável | Prazo de Tratamento | Risco Residual Aceito e Justificativa |
| :---: | :--- | :--- | :---: | :--- |
| **EXC-01** | Ausência de TLS mútuo (mTLS) no Broker Mosquitto local | Gustavo Silveira (IoT) | 5º Semestre | **Baixo.** Em ambiente de bancada acadêmica, o tráfego do broker é isolado na rede virtual Docker (`labcontrol-network`), com autenticação forte por usuário/senha e sem exposição de portas para a internet pública. |
| **EXC-02** | Refresh Tokens em LocalStorage Web | André Fernandes (Web) | Próxima Release | **Baixo.** O token de acesso possui tempo de expiração curto (15 minutos) e o ambiente de produção rodará sob HTTPS estrito com proteção anti-XSS no frontend. |

---

## 4. Conclusão do Reteste

Todos os 4 achados críticos e médios identificados na avaliação automatizada foram devidamente mitigados no código-fonte, testados com suíte de regressão automatizada e retestados via scripts manuais. Não restam vulnerabilidades de severidade Alta ativas sem plano de contingência ou exceção técnica formalizada.
