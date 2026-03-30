# Mapa de Integração Vertical e Horizontal — LabControll 4.0

*Disciplina:* Integração Vertical e Horizontal  
*Projeto:* LabControll 4.0  
*Curso:* Análise e Desenvolvimento de Sistemas  

---

## 1. Objetivo

Este documento apresenta o *mapa de integração vertical e horizontal* do sistema *LabControll 4.0*, demonstrando como sensores IoT, backend, banco de dados e aplicações se comunicam dentro da arquitetura do sistema.

---

## 2. Integração Vertical

A integração vertical representa o fluxo de dados entre os diferentes níveis do sistema.

Fluxo:
    
    Sensores IoT / Controladores → Backend (API REST) → Banco de Dados → Aplicações (Web e Mobile)

Nesse fluxo, os dados coletados dos ambientes (máquinas, consumo energético, temperatura e ocupação) são enviados ao backend, processados e disponibilizados para visualização e tomada de decisão.

---

## 3. Integração Horizontal

A integração horizontal representa a comunicação entre sistemas no mesmo nível da arquitetura.

Exemplos:

- Backend ↔️ Banco de Dados  
- Backend ↔️ Cloud / Serviços externos  
- Backend ↔️ Aplicação Web  
- Backend ↔️ Aplicativo Mobile  
- Web ↔️ Mobile (consumo da mesma API)

---

## 4. Diagrama de Integração

```mermaid
flowchart TB

subgraph Operacional
IOT[Sensores IoT / Controladores]
end

subgraph Tatico
BACK[Backend / API REST]
DB[Banco de Dados]
end

subgraph Estrategico
WEB[Dashboard Web]
APP[Aplicativo Mobile]
end

IOT --> BACK
BACK --> DB
BACK --> WEB
BACK --> APP

BACK <--> DB
BACK <--> WEB
BACK <--> APP