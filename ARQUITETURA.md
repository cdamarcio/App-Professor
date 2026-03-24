# Arquitetura do Sistema

## Fluxo de Sincronização
O aplicativo utiliza uma estratégia de **Queue-First**. Toda ação do professor é salva localmente (SQLite/WatermelonDB) e enviada para uma fila de sincronização.

1. **Local Save:** Dados gravados no dispositivo.
2. **Sync Manager:** Tenta disparar para a API.
3. **Conflict Resolution:** Em caso de erro 409 (conflito), o servidor prioriza o registro mais recente.

## Integração E-SEMEC
Os endpoints principais seguem o padrão REST:
- `POST /auth/login`
- `GET /students?class_id={id}`
- `POST /attendance/push`

## Diagrama de Dados (Simplificado)
- **Professor:** (ID, Nome, CPF, Token)
- **Turma:** (ID, Nome, Serie, Turno)
- **Registro:** (ID, Aluno_ID, Data, Status, Sincronizado: Boolean)
