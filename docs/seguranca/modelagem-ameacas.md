# LabControl 4.0 - Modelagem de Ameaças STRIDE e Análise de Vetores de Ataque

**Identificador da Entrega:** `[S4][SEC-02]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/seguranca/modelagem-ameacas.md`  
**Disciplina / Área:** Cibersegurança  
**Responsável:** Giovani Miamoto (@giovanimiamotob)  
**Issue de Referência:** [#19](https://github.com/labControl4-0/labcontrol-docs/issues/19)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  

---

## 1. Escopo e Fronteiras de Confiança (Trust Boundaries)

O ecossistema do **LabControl 4.0** opera na convergência entre Tecnologia da Informação (TI) e Tecnologia da Operação (TO / Indústria 4.0). Esta integração amplia a superfície de ataque ao conectar a instrumentação de chão de fábrica (sensores e atuadores) com interfaces de usuário web e móveis.

```
+------------------------------------------------------------------------------------------------------------------------+
|                                              ARQUITETURA E FRONTEIRAS DE CONFIANÇA                                     |
+------------------------------------------------------------------------------------------------------------------------+

 [ Sensores Industriais / ]  -- (MQTT TCP:1883) --> [ Broker Mosquitto ] -- (Ingestão) --> [ API Central ] 
 [ Simulador Node-RED     ]                          [ (Trust Zone 1)   ]                   [ Spring / .NET ]
                                                                                               | (TCP 5432)
                                                                                               v
 [ App Mobile (Expo/React) ] -- (HTTPS REST:8080) -> [ API Central (Trust Zone 2) ] <---- [ PostgreSQL DB ]
 [ Web Dashboard (React)   ]                                                               [ (Trust Zone 3) ]
+------------------------------------------------------------------------------------------------------------------------+
```

### Zonas de Confiança (Trust Boundaries)
1. **TB-01 (Chão de Fábrica / IoT para Broker):** Tráfego MQTT proveniente de publicadores industriais. Risco de falsificação de sensores e injeção de telemetria maliciosa caso o broker não exija credenciais e TLS.
2. **TB-02 (Clientes Externos para API Central):** Comunicação HTTP/REST originada no Web Dashboard (navegadores) e App Mobile (smartphones de operadores). Risco de ataques na camada de aplicação (OWASP Top 10), força bruta e roubo de tokens.
3. **TB-03 (API Central para Banco de Dados):** Conexão JDBC/TCP entre o container da API e o container do PostgreSQL na rede interna do Docker (`labcontrol-network`).

---

## 2. Modelagem de Ameaças pelo Modelo STRIDE

| Categoria STRIDE | Descrição da Ameaça no LabControl 4.0 | Componente Afetado | Vetor de Ataque / Cenário | Gravidade |
| :--- | :--- | :--- | :--- | :---: |
| **S - Spoofing** *(Falsificação de Identidade)* | Um atacante na rede local forja a identidade de um sensor de temperatura e injeta telemetria falsa, ou forja credenciais de operador. | Broker Mosquitto / API Auth | Conexão anônima ao Mosquitto sem autenticação; captura de token JWT não expirado. | **Alta** |
| **T - Tampering** *(Adulteração de Dados)* | Alteração em trânsito dos valores de telemetria de uma máquina ou modificação direta do banco local SQLite no smartphone do operador. | Broker MQTT / SQLite Mobile | Sniffing de pacotes em rede aberta (sem TLS); adulteração de banco em dispositivo com root. | **Alta** |
| **R - Repudiation** *(Repúdio)* | Um operador altera o status de segurança de uma prensa industrial para "Liberada" e depois nega a autoria em caso de incidente de trabalho. | API / Auditoria | Ausência de trilhas de auditoria imutáveis com ID de usuário, IP e timestamp nas operações de escrita. | **Média** |
| **I - Information Disclosure** *(Vazamento de Informações)* | Exposição de segredos de conexão, chaves de API ou dados de processo industrial em logs, mensagens de erro detalhadas ou repositório. | API / Docker Compose / Web | Stack traces expostos com senhas de banco; commit acidental de arquivos `.env`; credenciais no GitHub. | **Crítica** |
| **D - Denial of Service** *(Negação de Serviço)* | Inundação de requisições de autenticação ou saturação do broker MQTT com mensagens gigantes em loop, derrubando o monitoramento. | Broker Mosquitto / API Gateway | Flooding de mensagens MQTT em tópicos wildcard (`#`); ausência de rate limiting nas rotas REST. | **Alta** |
| **E - Elevation of Privilege** *(Elevação de Privilégio)* | Um usuário autenticado com perfil de visualizador/operador manipula parâmetros de requisição para executar ações de administrador. | Spring Security / RBAC API | Falha na validação de papéis nos endpoints REST (BOLA - Broken Object Level Authorization). | **Crítica** |

---

## 3. Matriz de Priorização de Risco DREAD

Avaliando o impacto das ameaças pelo cálculo DREAD (Damage + Reproducibility + Exploitability + Affected Users + Discoverability / 5):

| Código | Ameaça Identificada | D (1-10) | R (1-10) | E (1-10) | A (1-10) | D (1-10) | Score DREAD | Risco |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **THR-01** | Elevação de privilégio por falha em anotações RBAC na API | 9 | 8 | 8 | 9 | 7 | **8.2** | **Crítico** |
| **THR-02** | Credenciais padrão ou anônimas no Broker Mosquitto MQTT | 8 | 9 | 9 | 8 | 7 | **8.2** | **Crítico** |
| **THR-03** | Segredos de infraestrutura ou chaves JWT expostas em código | 9 | 9 | 8 | 9 | 6 | **8.2** | **Crítico** |
| **THR-04** | Injeção de telemetria maliciosa via spoofing de tópico MQTT | 7 | 8 | 8 | 7 | 7 | **7.4** | **Alto** |
| **THR-05** | Armazenamento inseguro de tokens no mobile (fora do SecureStore) | 7 | 7 | 7 | 5 | 7 | **6.6** | **Médio** |
| **THR-06** | Negação de serviço na API por ausência de Rate Limiting | 6 | 7 | 8 | 8 | 4 | **6.6** | **Médio** |

---

## 4. Plano de Mitigação e Requisitos de Hardening

### 4.1 Hardening do Broker MQTT (`labcontrol-iot`)
- Desabilitar terminantemente a diretiva `allow_anonymous true` no arquivo `mosquitto.conf`.
- Configurar autenticação baseada em arquivo de usuários (`password_file /mosquitto/config/passwords`).
- Implementar lista de controle de acesso (ACL) delimitando quais tópicos cada publicador pode enviar.

### 4.2 Segurança da API Central (`labcontrol-api`)
- Garantir anotações estritas de controle de acesso (`@PreAuthorize("hasRole('ADMIN')")` no Spring Boot) em todas as rotas que alteram ativos ou configuram usuários.
- Validação estrita de claims e tempo de vida curto para tokens JWT (máximo 60 minutos), acompanhado de refresh token seguro.
- Ativação de CORS restrito permitindo apenas as origens autorizadas do Web Dashboard.
- Configuração de sanitização global de exceções para impedir vazamento de stack traces em respostas de erro (HTTP 500 padronizado).

### 4.3 Segurança do Aplicativo Mobile (`labcontrol-mobile`)
- Obrigatoriedade do uso do pacote `expo-secure-store` para guardar tokens JWT e credenciais de login, nunca utilizando `AsyncStorage` comum para dados sensíveis (conforme PR #12).
- Validação de integridade e timestamp nas mensagens da fila offline SQLite para evitar ataques de repetição (replay attack).

### 4.4 Segurança do Frontend Web (`labcontrol-web`)
- Configuração de cabeçalhos de segurança no Nginx (`X-Content-Type-Options: nosniff`, `X-Frame-Options: SAMEORIGIN`, `Content-Security-Policy`).
- Higienização de entradas de usuário com sanitização no editor de planta baixa contra injeção de scripts (XSS).
