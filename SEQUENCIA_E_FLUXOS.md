# Diagramas de Sequência e Lógica de Sistema (UML)

Este documento detalha as interações temporais entre os componentes do sistema e a lógica de transição de estados para garantir a integridade dos dados escolares.

## 1. Diagrama de Sequência: Autenticação e Sincronização
Este fluxo detalha a troca de mensagens desde o aperto do botão de login até a confirmação de sincronização dos dados de frequência.

```mermaid
sequenceDiagram
    autonumber
    participant P as Professor (App Mobile)
    participant L as Local DB (SQLite)
    participant A as API Integração (Backend)
    participant S as Base E-SEMEC (PostgreSQL)

    Note over P, S: Etapa 1: Autenticação e Carga Inicial
    P->>A: POST /auth/login (CPF + Senha)
    A->>S: SELECT user FROM teachers WHERE...
    S-->>A: Dados do Professor (OK)
    A-->>P: HTTP 200 (JWT Token + Perfil + Turmas)
    P->>L: INSERT INTO local_classes/students (...)
    Note right of P: App pronto para uso Offline

    Note over P, S: Etapa 2: Registro e Sincronização de Frequência
    P->>L: UPDATE attendance SET status='P', synced=false
    
    rect rgb(240, 240, 240)
    Note right of P: Loop de Sincronização (Background)
    P->>A: POST /attendance/push (JSON + Bearer Token)
    alt Sucesso (Online)
        A->>S: UPSERT INTO frequency (...)
        S-->>A: 201 Created
        A-->>P: HTTP 200 (Success)
        P->>L: UPDATE attendance SET synced=true
    else Falha de Conexão ou Servidor
        A-->>P: HTTP 503 / Timeout
        P->>L: Manter synced=false (Retry em 5 min)
    end
    end
