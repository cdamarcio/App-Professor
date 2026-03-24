# Lógica de Negócio e Estados do Sistema

Este documento descreve as regras de transição de dados e a validação temporal para o lançamento de frequência e conteúdo.

## 1. Diagrama de Estados da Frequência (UML State Machine)
Define como um registro de aula se comporta desde a criação no celular do professor até o arquivamento no E-SEMEC.

```mermaid
stateDiagram-v2
    [*] --> Criado: Professor inicia chamada
    Criado --> GravadoLocal: Salvar (Offline/Online)
    
    state GravadoLocal {
        [*] --> PendenteSync: Aguardando Conexão
        PendenteSync --> Sincronizando: Request Enviado
        Sincronizando --> PendenteSync: Falha (Timeout/500)
    }

    GravadoLocal --> Sincronizado: Sucesso API (200/201)
    
    state Sincronizado {
        [*] --> AbertoEdicao: < 48h do lançamento
        AbertoEdicao --> Alterado: Professor edita registro
        Alterado --> AbertoEdicao: Re-sincronizado
        AbertoEdicao --> Bloqueado: > 48h do lançamento
    }

    Bloqueado --> [*]: Registro Consolidado
