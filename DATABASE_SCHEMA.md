# Esquema do Banco de Dados (Database Schema)

Este documento define a estrutura de dados para o sistema de Frequência e Conteúdo. O projeto utiliza uma arquitetura híbrida: **PostgreSQL** no servidor central (E-SEMEC) e **SQLite** no dispositivo móvel (App).

---

## 1. Dicionário de Dados (Entidades Principais)

### Tabela: `schools` (Escolas)
| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `id` | UUID (PK) | Identificador único da escola. |
| `inep_code` | VARCHAR(8) | Código INEP oficial. |
| `name` | VARCHAR(255) | Nome da instituição. |

### Tabela: `teachers` (Professores)
| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `id` | UUID (PK) | Identificador único. |
| `cpf` | VARCHAR(11) | CPF (Login/Identificação). |
| `password_hash`| TEXT | Senha criptografada (Argon2/Bcrypt). |
| `full_name` | VARCHAR(255) | Nome completo do docente. |

### Tabela: `classes` (Turmas)
| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `id` | UUID (PK) | Identificador único da turma. |
| `school_id` | UUID (FK) | Relacionamento com a escola. |
| `grade` | VARCHAR(50) | Ano/Série (ex: 5º Ano A). |
| `shift` | ENUM | Turno: 'Matutino', 'Vespertino', 'Noturno'. |

### Tabela: `attendance` (Frequência)
| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `id` | UUID (PK) | Identificador único do registro. |
| `student_id` | UUID (FK) | ID do aluno no E-SEMEC. |
| `class_id` | UUID (FK) | ID da turma. |
| `status` | CHAR(1) | 'P' (Presença), 'F' (Falta), 'J' (Justificada). |
| `date` | DATE | Data da aula. |
| `created_at` | TIMESTAMPTZ | Data/Hora real da criação (para regra 48h). |
| `updated_at` | TIMESTAMPTZ | Data da última alteração. |
| `synced` | BOOLEAN | Flag de controle para o App Mobile (Default: false). |

---

## 2. Implementação SQL (PostgreSQL - Servidor)

```sql
-- Extensão para geração de UUID
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";

-- Tabela de Frequência com Regra de Auditoria
CREATE TABLE attendance (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    teacher_id UUID REFERENCES teachers(id),
    student_id UUID NOT NULL,
    class_id UUID REFERENCES classes(id),
    attendance_status CHAR(1) CHECK (attendance_status IN ('P', 'F', 'J')),
    lesson_date DATE NOT NULL,
    observation TEXT,
    created_at TIMESTAMPTZ DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMPTZ DEFAULT CURRENT_TIMESTAMP,
    sync_id UUID UNIQUE -- ID gerado pelo App para evitar duplicidade (Idempotência)
);

-- Indexação para performance de relatórios (RNF-014)
CREATE INDEX idx_attendance_date ON attendance(lesson_date);
CREATE INDEX idx_attendance_class ON attendance(class_id);
