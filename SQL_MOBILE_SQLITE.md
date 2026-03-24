# Estrutura do Banco de Dados Local (SQLite)

Este documento define a tabela principal de persistência no dispositivo móvel. Esta estrutura foi projetada para garantir a integridade dos dados antes da sincronização com o servidor central E-SEMEC.

## 1. Definição da Tabela: `local_attendance`

Esta tabela armazena temporariamente os registros de frequência e status de sincronização.

```sql
-- Tabela para armazenamento offline de frequência
CREATE TABLE local_attendance (
    id TEXT PRIMARY KEY,           -- UUID v4 gerado no App para evitar colisões
    student_id TEXT NOT NULL,      -- ID único do aluno (origem: E-SEMEC)
    class_id TEXT NOT NULL,        -- ID da turma (origem: E-SEMEC)
    status TEXT NOT NULL,          -- 'P' (Presença), 'F' (Falta), 'J' (Justificada)
    date TEXT NOT NULL,            -- Data da aula (Formato ISO8601: YYYY-MM-DD)
    created_at TEXT NOT NULL,      -- Timestamp de criação (Formato: YYYY-MM-DD HH:MM:SS)
    synced INTEGER DEFAULT 0,      -- Flag de Sincronia: 0 = Pendente, 1 = Sincronizado
    error_log TEXT,                -- Armazena a última mensagem de erro retornada pela API
    updated_at TEXT                -- Timestamp da última alteração local
);
