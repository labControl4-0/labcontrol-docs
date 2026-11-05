# LabControl 4.0 - Catálogo de Serviços, Observabilidade e Gestão de Incidentes

**Identificador da Entrega:** `[S4][GOV-06]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/operacao/servico.md`  
**Disciplina / Área:** Governança de TI  
**Responsável:** Giovani Miamoto (@giovanimiamotob)  
**Issue de Referência:** [#14](https://github.com/labControl4-0/labcontrol-docs/issues/14)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  

---

## 1. Catálogo de Serviços de TI do LabControl 4.0

O LabControl 4.0 oferece quatro serviços tecnológicos interconectados para a operação industrial:

```
+---------------------------------------------------------------------------------------------------+
|                                 Catálogo de Serviços LabControl 4.0                              |
+---------------------------------------------------------------------------------------------------+
| 1. Serviço de Telemetria e Mensageria IoT (Mosquitto MQTT + Node-RED)                             |
|    - Função: Ingestão de dados de sensores industriais (temperatura, vibração, RPM, status).    |
|    - Portas/Protocolos: 1883 (TCP MQTT), 9001 (WebSockets), 1880 (Node-RED UI).                  |
|    - SLA Alvo: 99.0% de uptime | Latência: < 500ms fim a fim.                                    |
+---------------------------------------------------------------------------------------------------+
| 2. Serviço de API Central, Autenticação e Sincronização (.NET Core / Spring Boot + PostgreSQL)    |
|    - Função: Gestão de ativos, controle de acesso RBAC, armazenamento relacional e sync offline. |
|    - Portas/Protocolos: 8080 (HTTP/REST), 5432 (PostgreSQL).                                      |
|    - SLA Alvo: 99.5% de uptime | Tempo Médio de Resposta: < 300ms.                               |
+---------------------------------------------------------------------------------------------------+
| 3. Serviço de Dashboard e Supervisão Web (React 18 + Tailwind + Nginx)                            |
|    - Função: Visualização de telemetria em tempo real, editor de planta baixa e alertas.          |
|    - Portas/Protocolos: 80 / 443 (HTTP/HTTPS via Nginx).                                          |
|    - SLA Alvo: 99.0% de uptime.                                                                  |
+---------------------------------------------------------------------------------------------------+
| 4. Serviço de Aplicação Mobile de Chão de Fábrica (React Native / Expo)                           |
|    - Função: Operação assistida para operadores, coleta offline em SQLite e push de emergência.  |
|    - SLA Alvo: Operação autônoma sem rede (modo offline) de até 8 horas ininterruptas.            |
+---------------------------------------------------------------------------------------------------+
```

---

## 2. Níveis de Severidade de Incidentes e Matriz de Resposta

| Nível de Severidade | Impacto Operacional | Exemplos Práticos | SLA de Resposta | Responsável Técnico |
| :--- | :--- | :--- | :--- | :--- |
| **SEV 1 - Crítico** | Parada total da coleta de telemetria ou queda da API; risco de perda de visibilidade da fábrica. | Mosquitto inacessível; falha crítica de conexão com o banco PostgreSQL. | **Até 30 minutos** | Carlos Eduardo (Backend) / Gustavo Silveira (IoT) |
| **SEV 2 - Alto** | Degradação severa; funcionalidade essencial inacessível, mas com plano de contingência. | Falha no endpoint de sincronização mobile; alertas de máquina não disparados. | **Até 2 horas** | Gustavo Silveira (Mobile) / André Fernandes (Web) |
| **SEV 3 - Médio** | Funcionalidade parcial afetada; operadores conseguem trabalhar com desvio contornável. | Lentidão no carregamento do mapa da planta baixa; inconsistência visual de cor de ativo. | **Até 8 horas** | André Fernandes (Web) |
| **SEV 4 - Baixo** | Dúvida de uso, solicitação de relatório cosmético ou sugestão de melhoria. | Dúvida sobre exportação de CSV ou ajuste tipográfico em formulário. | **Até 24 horas** | Giovani Miamoto / Victor Geroto |

---

## 3. Padrão de Logging Sanitizado e Observabilidade

Para assegurar a auditabilidade em conformidade com as diretrizes de governança e a LGPD, os logs de todos os componentes devem seguir a estrutura JSON padronizada:

### 3.1 Esquema de Log Estruturado
```json
{
  "timestamp": "2026-11-04T21:00:00.000Z",
  "level": "INFO",
  "service": "labcontrol-api",
  "correlation_id": "a9f8b2c4-7d1e-4a6f-98e3-0b1a2c3d4e5f",
  "endpoint": "POST /api/v1/sync",
  "status_code": 200,
  "duration_ms": 42,
  "client_id": "mob-terminal-04",
  "message": "Operacao de sincronizacao concluida com sucesso. 3 registros integrados."
}
```

### 3.2 Regra Estrita de Sanitização (Data Masking)
É proibido gravar nos logs:
- Senhas em texto claro (campos `password`, `senha`).
- Tokens JWT completos (gravar apenas os últimos 6 caracteres: `Bearer ...a7x9f`).
- Dados bancários, CPFs de operadores ou dados biométricos.
- Em caso de exceção (Stack Trace), mascarar parâmetros de query strings contendo tokens.

---

## 4. Runbook Operacional de Resolução de Incidentes

### Procedimento A: Broker Mosquitto Parado ou Sem Conexão
1. **Sintoma:** Dashboard Web e Mobile exibem status "Desconectado do Broker" ou gráficos estáticos.
2. **Diagnóstico:**
   ```bash
   docker ps | grep mosquitto
   docker logs --tail 50 labcontrol-iot-mosquitto-1
   ```
3. **Ação de Recuperação:**
   - Reiniciar o serviço do broker:
     ```bash
     docker compose -f labcontrol-iot/docker-compose.yml restart mosquitto
     ```
   - Verificar permissões do arquivo `mosquitto.conf`.

### Procedimento B: API Não Responde às Chamadas REST
1. **Sintoma:** Frontend Web retorna HTTP 502 Bad Gateway ou `Network Error`.
2. **Diagnóstico:**
   - Testar o healthcheck local:
     ```bash
     curl -i http://localhost:8080/health
     ```
   - Verificar logs de conexão com PostgreSQL:
     ```bash
     docker logs --tail 50 labcontrol-api
     ```
3. **Ação de Recuperação:**
   - Caso o banco esteja com limite de conexões excedido, reiniciar o pool de conexões da API ou reiniciar o container da API.

### Procedimento C: Conflito de Sincronização Mobile Offline
1. **Sintoma:** O aplicativo mobile reporta "Conflito de versão na máquina XYZ".
2. **Diagnóstico:** Dois operadores editaram o mesmo ativo enquanto um deles estava desconectado.
3. **Regra de Desempate (Last-Write-Wins Auditado):** O servidor acata a alteração com o timestamp UTC mais recente e armazena a versão anterior na tabela de histórico `audit_logs` para conferência posterior do supervisor.
