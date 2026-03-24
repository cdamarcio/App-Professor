# Fluxos de Processos e Sequência (UML)

Este documento detalha o comportamento do sistema para as operações críticas de lançamento de frequência e sincronização.

## 1. Diagrama de Atividades: Registro de Frequência (Modo Offline/Online)
Este fluxo descreve a lógica desde a abertura da turma até a persistência dos dados.

```mermaid
graph TD
    A[Início: Professor abre Turma] --> B{Possui Conexão?}
    B -- Sim --> C[Busca Lista Atualizada no E-SEMEC]
    B -- Não --> D[Carrega Lista do Cache Local]
    C --> E[Exibe Lista de Alunos]
    D --> E[Exibe Lista de Alunos]
    E --> F[Professor Marca Presença/Falta]
    F --> G[Salva no Banco Local - SQLite]
    G --> H{Conexão Disponível?}
    H -- Sim --> I[Dispara Sincronização Automática]
    H -- Não --> J[Mantém na Fila de Sincronização]
    I --> K[Confirmação de Sucesso no E-SEMEC]
    K --> L[Atualiza Status: Sincronizado]
    L --> M[Fim]
    J --> M
