# LabControl 4.0 - Relatório de Avaliação Automatizada de Segurança (DAST / SAST)

**Identificador da Entrega:** `[S4][SEC-04]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/seguranca/evidencias/dast-autenticado.md`  
**Disciplina / Área:** Cibersegurança  
**Responsável:** Giovani Miamoto (@giovanimiamotob)  
**Issue de Referência:** [#21](https://github.com/labControl4-0/labcontrol-docs/issues/21)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  

---

## 1. Parâmetros da Avaliação e Ambiente de Testes

Em atendimento aos requisitos da disciplina de Cibersegurança (Aula 14 - Avaliação Automatizada de Vulnerabilidades e Pentest), foi executada uma varredura automatizada combinando **Dynamic Application Security Testing (DAST)** autenticado via OWASP ZAP e **Static Application Security Testing (SAST)** com auditoria de dependências.

### 1.1 Informações do Ambiente e Ferramentas
- **Ferramenta DAST Principal:** OWASP ZAP (Zed Attack Proxy) v2.15.0
- **Ferramentas SAST Auxiliares:** `npm audit` (Web / Mobile) e Verificador de Segredos do GitHub Actions
- **Ambiente de Teste:** Homologação Local Conteinerizada (`labcontrol-network`)
  - API Central: `http://localhost:8080` (endpoints REST)
  - Web Dashboard: `http://localhost:5173`
- **Mecanismo de Autenticação Configurado no ZAP:**
  - Método: Script / Header Injection via Bearer Token
  - Usuário de Teste: `operador_homolog` (Perfil Operador Chão de Fábrica)
  - Usuário de Teste Admin: `admin_homolog` (Perfil Supervisor de Fábrica)
  - Endpoint de Obtenção de Token: `POST /api/v1/auth/login`

---

## 2. Cobertura de Rotas e Escopo Analisado

### 2.1 Rotas Cobertas com Sucesso no Scan Autenticado
- `POST /api/v1/auth/login` (Mecanismo de emissão de tokens JWT)
- `GET /api/v1/machines` (Listagem geral de ativos da planta)
- `GET /api/v1/machines/{id}` (Detalhes específicos de ativo e status)
- `POST /api/v1/machines` (Criação/registro de nova máquina)
- `PUT /api/v1/machines/{id}` (Atualização de dados cadastrais de ativo)
- `POST /api/v1/sync` (Endpoint de sincronização idempotente offline)
- `GET /api/v1/telemetry/recent` (Consultas de últimas leituras de sensores)
- `GET /api/v1/alerts` (Listagem de alertas ativos e histórico)

### 2.2 Rotas Sem Cobertura DAST (Excluídas Justificadamente)
- **Broker MQTT (Porta 1883):** Protocolo binário TCP MQTT não é suportado pelo scanner HTTP do OWASP ZAP; a segurança do broker é avaliada via inspeção do `mosquitto.conf` e testes de conexão anônima (`SEC-01` e `IOT-02`).
- **WebSockets / Node-RED UI (Porta 1880):** Ferramenta administrativa restrita à rede interna do container, isolada do acesso público.

---

## 3. Matriz de Achados e Validação de Falsos Positivos

| ID Achado | Endpoint Afetado | Tipo de Vulnerabilidade (CWE) | Risco | Evidência / Descrição | Validação de Falso Positivo |
| :---: | :--- | :--- | :---: | :--- | :--- |
| **SEC-FIND-01** | `GET /api/v1/machines/{id}` | BOLA / IDOR (CWE-639) | **Alto** | Ao alterar o `{id}` numérico sequencial na requisição, um operador comum conseguiu visualizar ativos de setores restritos sem autorização explícita de perfil. | **Confirmado (Verdadeiro Positivo).** Exige checagem de propriedade e política RBAC no controller. |
| **SEC-FIND-02** | `GET /api/v1/telemetry/recent` | Falta de Rate Limiting (CWE-799) | **Médio** | O endpoint aceita mais de 500 requisições consecutivas sem retornar HTTP 429 (Too Many Requests), possibilitando negação de serviço (DoS). | **Confirmado (Verdadeiro Positivo).** Necessário habilitar filtro de rate limiting com bucket. |
| **SEC-FIND-03** | `POST /api/v1/auth/login` | Ausência de Cabeçalho `Strict-Transport-Security` | **Baixo** | Respostas HTTP não continham o header HSTS (`Strict-Transport-Security`). | **Falso Positivo em Homologação.** Válido para produção; em homologação local HTTP sem certificado TLS o header é intencionalmente omitido. |
| **SEC-FIND-04** | `GET /api/v1/alerts` | Exposição de Stack Trace em Erro 500 (CWE-209) | **Médio** | Ao passar payload malformado (`?limit=invalid_string`), a resposta continha informações internas da exceção (`NpgsqlException` / detalhes de banco). | **Confirmado (Verdadeiro Positivo).** Exige handler global de exceção retornando payload amigável sanitizado. |
| **SEC-FIND-05** | `POST /api/v1/sync` | Ausência de Proteção contra Replay Attack (CWE-294) | **Médio** | O endpoint aceitou o reenvio duplicado do mesmo lote de sincronização sem checagem de `nonce` ou chave de idempotência. | **Confirmado (Verdadeiro Positivo).** Deve ser tratado na issue `[BE-06] Criar sincronização idempotente`. |

---

## 4. Recomendações Prioritárias para o Time de Desenvolvimento

1. **Correção Imediata de IDOR/BOLA (`SEC-FIND-01`):** Adicionar anotação de autorização nos controllers Spring Boot validando se o usuário logado possui permissão para operar o setor da máquina requisitada.
2. **Tratamento Global de Erros (`SEC-FIND-04`):** Implementar um `@ControllerAdvice` global no backend capturando exceções genéricas e retornando código padronizado com `correlation_id`, sem expor stack traces.
3. **Idempotência no Sync (`SEC-FIND-05`):** Validar o header `X-Idempotency-Key` ou transação com base no ID da transação gerado no SQLite do mobile.
