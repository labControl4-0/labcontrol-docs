# LabControl 4.0 - Manifesto de Entrega Integrada e Matriz de Versões (Release v4.0.0)

**Identificador da Entrega:** `[S4][REL-02]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/manifesto-entrega.md`  
**Disciplina / Área:** Entrega Integrada do Projeto Integrador IV  
**Responsável:** Giovani Miamoto (@giovanimiamotob)  
**Issue de Referência:** [#29](https://github.com/labControl4-0/labcontrol-docs/issues/29)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  

---

## 1. Visão Geral da Release Final Integrada (PI-IV)

O **LabControl 4.0** consolida a sua entrega integrada do 4º Semestre no ecossistema do UniSENAI. Este manifesto fixa os commits, branches, tags, artefatos e instruções para reprodução em clone limpo de todos os 5 repositórios da organização [`labControl4-0`](https://github.com/labControl4-0).

---

## 2. Matriz de Versões e Commits por Repositório

| Repositório | Componente | Branch / Tag | Commit Hash Referência | Responsável Principal | Tecnologias Principais |
| :--- | :--- | :---: | :---: | :--- | :--- |
| **`labcontrol-docs`** | Governança, Gestão, Cibersegurança & PDFs | `main` / `v4.0.0` | Commit mais recente | Giovani Miamoto | Markdown, HTML, Headless PDF, GitHub Actions |
| **`labcontrol-api`** | Backend Central, APIs REST e Persistência | `main` | `84da384` | Carlos Eduardo / Victor | Java 21 / Spring Boot 3, .NET 9, PostgreSQL 15 |
| **`labcontrol-web`** | Frontend Web Industrial e Planta Baixa | `main` | `6b2e6b6` | André Fernandes | React 18, Vite, Tailwind CSS, TanStack Query |
| **`labcontrol-mobile`**| App Mobile de Chão de Fábrica | `develop` / `main` | `ff07943` | Gustavo Silveira | React Native, Expo 54, SQLite Offline, Push |
| **`labcontrol-iot`**   | Broker MQTT Mosquitto e Node-RED | `main` | `56c166e` | Gustavo Silveira | Mosquitto 2.0, Node-RED, Docker Compose |

---

## 3. Guia de Reprodução em Clone Limpo (Deploy Local)

Para inicializar todo o ecossistema integrado em uma máquina de avaliação limpa com Docker e Docker Compose:

### Passo 1: Inicialização da Infraestrutura IoT e Mensageria
```bash
git clone https://github.com/labControl4-0/labcontrol-iot.git
cd labcontrol-iot
docker compose up -d
# Verifica se o broker Mosquitto (porta 1883) e Node-RED (porta 1880) estão ativos
```

### Passo 2: Inicialização do Banco de Dados e Backend
```bash
git clone https://github.com/labControl4-0/labcontrol-api.git
cd labcontrol-api
docker compose up -d
# API REST disponível em http://localhost:8080/swagger ou http://localhost:8080/health
```

### Passo 3: Inicialização do Frontend Web Industrial
```bash
git clone https://github.com/labControl4-0/labcontrol-web.git
cd labcontrol-web
npm install
npm run dev
# Portal Web acessível em http://localhost:5173
```

### Passo 4: Execução do Mobile em Modo de Desenvolvimento
```bash
git clone https://github.com/labControl4-0/labcontrol-mobile.git
cd labcontrol-mobile/labcontrol-app
npm install
npx expo start
```

---

## 4. Índice Oficial de Documentos e Evidências Acadêmicas

Todos os documentos regulatórios exigidos pelas disciplinas do 4º semestre estão versionados com fontes editáveis e PDFs consolidados para download direto:

1. 📕 **[Plano Consolidado de Governança de TI (PDF)](plano-governanca-ti.pdf)**  
   - Fonte Editável: [`docs/plano-governanca-ti.html`](plano-governanca-ti.html)  
   - Matriz de Controle: [`docs/governanca/matriz-controle-evidencia.md`](governanca/matriz-controle-evidencia.md)
2. 📕 **[Relatório Técnico de Vulnerabilidades e Pentest (PDF)](relatorio-vulnerabilidades-pentest.pdf)**  
   - Fonte Editável: [`docs/relatorio-vulnerabilidades-pentest.html`](relatorio-vulnerabilidades-pentest.html)  
   - Relatório Markdown: [`docs/relatorio-vulnerabilidades-pentest.md`](relatorio-vulnerabilidades-pentest.md)  
   - Relatório de Remediação e Reteste: [`docs/seguranca/correcoes-reteste.md`](seguranca/correcoes-reteste.md)  
   - Evidência DAST OWASP ZAP: [`docs/seguranca/evidencias/dast-autenticado.md`](seguranca/evidencias/dast-autenticado.md)
3. 📋 **Gestão de Projetos e Escopo:**  
   - EAP e Escopo: [`docs/gestao/escopo-eap.md`](gestao/escopo-eap.md)  
   - Backlog e Kanban: [`docs/gestao/backlog-kanban.md`](gestao/backlog-kanban.md)  
   - Acordos de Equipe: [`docs/gestao/acordos-equipe.md`](gestao/acordos-equipe.md)
4. 📈 **Validação com Usuários:**  
   - Resultados de Negócio e Usabilidade: [`docs/negocio/validacao.md`](negocio/validacao.md)
