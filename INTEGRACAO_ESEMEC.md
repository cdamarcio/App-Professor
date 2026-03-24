# Especificação de Integração API (E-SEMEC)

Este documento define os objetos JSON para a comunicação entre o Aplicativo Mobile e o Servidor Central.

## 1. Endpoint: Sincronização de Frequência
**POST** `/api/v1/attendance/sync`

### Payload de Envio (App -> Servidor)
```json
{
  "sync_batch_id": "uuid-do-lote",
  "teacher_id": "uuid-professor",
  "data": [
    {
      "id": "uuid-local-sqlite",
      "student_id": "uuid-aluno",
      "class_id": "uuid-turma",
      "status": "P",
      "date": "2026-03-24",
      "created_at": "2026-03-24T14:30:00Z"
    }
  ]
}
