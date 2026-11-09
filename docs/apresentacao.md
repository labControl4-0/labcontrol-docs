# LabControl 4.0 - Roteiro de Apresentação e Demonstração Integrada (Banca PI-IV)

**Identificador da Entrega:** `[S4][REL-02]`  
**Repositório:** `labControl4-0/labcontrol-docs`  
**Caminho do Artefato:** `docs/apresentacao.md`  
**Disciplina / Área:** Entrega Integrada do Projeto Integrador IV  
**Responsável:** Giovani Miamoto (@giovanimiamotob)  
**Issue de Referência:** [#29](https://github.com/labControl4-0/labcontrol-docs/issues/29)  
**Projeto:** [GitHub Projects 3 - LabControl 4.0](https://github.com/orgs/labControl4-0/projects/3)  

---

## 1. Estrutura e Tempo da Apresentação da Banca (20 Minutos)

```
[ 00:00 - 03:00 ] Visão Geral, Alinhamento de Negócio e EAP (Giovani / Victor)
[ 03:00 - 08:00 ] Demonstração Prática Ponta a Ponta: Telemetria IoT e Planta Web (André / Gustavo)
[ 08:00 - 13:00 ] Demonstração Mobile Offline-First com SQLite e Push (Gustavo / Carlos)
[ 13:00 - 17:00 ] Evidências de Governança de TI, Pentest e Cibersegurança (Giovani / Victor)
[ 17:00 - 20:00 ] Conclusão, Resultados de Negócio e Perguntas da Banca (Todos)
```

---

## 2. Roteiro Passo a Passo de Demonstração Técnica

### Bloco A: Abertura e Alinhamento Estratégico (3 min)
- **Apresentador:** Giovani Miamoto / Victor Geroto.
- **Telas:** Apresentação de slides / [EAP em `docs/gestao/escopo-eap.md`](gestao/escopo-eap.md).
- **Pontos-chave:**
  - Problema real de chão de fábrica: paradas de máquinas por atraso no reconhecimento de falhas e falta de conectividade em galpões industriais.
  - Como os 8 macro-pacotes da EAP organizaram o trabalho dos 5 integrantes sem atritos de responsabilidade (RACI).

### Bloco B: Demonstração de Telemetria e Planta Baixa Web (5 min)
- **Apresentador:** André Fernandes / Gustavo Silveira.
- **Ação Prática:**
  1. Abrir o Web Dashboard em `http://localhost:5173`.
  2. Acionar injeção de evento no simulador Node-RED (elevando temperatura da Máquina CNC-01 para 85°C).
  3. Visualizar o alerta em tempo real no mapa interativo da planta baixa (mudança de cor para vermelho e disparo de aviso visual).

### Bloco C: Demonstração Mobile Offline-First e Sincronização (5 min)
- **Apresentador:** Gustavo Silveira / Carlos Eduardo.
- **Ação Prática:**
  1. Abrir o app no smartphone do operador.
  2. Colocar o dispositivo em **Modo Avião** (desconectado).
  3. Registrar apontamento de manutenção corretiva (troca de correia dentada) salvo localmente no **SQLite**.
  4. Desativar o Modo Avião.
  5. Demonstrar o worker de sincronização integrando os dados com a API central com idempotência comprovada (`X-Idempotency-Key`).

### Bloco D: Cibersegurança Ofensiva/Defensiva e Governança de TI (4 min)
- **Apresentador:** Giovani Miamoto.
- **Telas:** PDFs versionados no GitHub ([`plano-governanca-ti.pdf`](plano-governanca-ti.pdf) e [`relatorio-vulnerabilidades-pentest.pdf`](relatorio-vulnerabilidades-pentest.pdf)).
- **Pontos-chave:**
  - Demonstração dos resultados do scan automatizado OWASP ZAP (5 achados).
  - PoC da vulnerabilidade de BOLA/IDOR e como o reteste com `@PreAuthorize` retornou HTTP 403 Forbidden.
  - Pipeline de CI do GitHub Actions em execução verde, comprovando validação automatizada de mudanças e scan anti-vazamento de segredos.

### Bloco E: Encerramento e Métricas de Negócio (3 min)
- **Apresentador:** Todos.
- **Pontos-chave:**
  - Resultados práticos medidos: redução do MTTA de 22 minutos para 1m12s (94% de ganho).
  - Economia de 35 minutos diários de preenchimento manual por operador.
