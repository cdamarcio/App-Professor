# Plano de Contingência e Recuperação de Desastres (DRP)

Este documento estabelece os procedimentos operacionais para a Secretaria Municipal de Educação de Conceição do Araguaia em caso de falha total ou parcial dos sistemas digitais.

## 1. Níveis de Incidente e Resposta

| Nível | Descrição | Ação Imediata |
| :--- | :--- | :--- |
| **Nível 1: Baixo** | Indisponibilidade da API < 4 horas. | **Operação em Modo Offline:** Professores continuam usando o app normalmente. A sincronização ocorrerá automaticamente após o restabelecimento. |
| **Nível 2: Médio** | Indisponibilidade > 12 horas ou Erro de Banco. | **Alerta da SEMEC:** A secretaria emite comunicado via WhatsApp/E-mail orientando a manutenção dos dados no App e proibindo a desinstalação do mesmo. |
| **Nível 3: Crítico** | Falha de Hardware no Servidor > 48 horas. | **Retorno ao Analógico:** Autorização temporária para registro em Diário de Classe físico (Papel) até a recuperação do ambiente. |

## 2. Protocolo de Recuperação de Dados (Data Recovery)

Caso ocorra uma perda de dados no servidor central (E-SEMEC), os dados armazenados nos smartphones dos professores (SQLite) servem como **Backup Distribuído**.

1.  **Identificação:** A TI da SEMEC identifica o último `backup_id` válido.
2.  **Solicitação de Re-sync:** O App recebe um comando "Force Sync" na próxima conexão.
3.  **Upload de Reconstrução:** O App reenvia todos os registros marcados como `synced=1` que ainda constam na base local, reconstruindo a linha do tempo do servidor.

## 3. Segurança e Integridade (Segurança do Trabalho/Dados)

* **Integridade do Dispositivo:** Em caso de erro de sincronização persistente que impeça o professor de trabalhar, o suporte técnico da SEMEC deve realizar o **Backup Manual** do arquivo `local_attendance.db` via cabo USB antes de qualquer formatação.
* **Ergonomia Cognitiva:** Se o sistema apresentar lentidão constante, os professores devem ser orientados a realizar a chamada apenas ao final do turno para evitar estresse e atraso nas atividades pedagógicas.

## 4. Comunicação de Crise

Em caso de Incidente Nível 3, o fluxo de comunicação segue a hierarquia:
1.  **TI SEMEC** detecta falha -> Notifica **Secretário de Educação**.
2.  **Secretaria** emite Nota Oficial para os **Diretores de Escola**.
3.  **Diretores** orientam os **Professores** sobre o uso do papel ou manutenção do app.

---

### Medidas de Prevenção (Mitigação)
- **Backup Diário:** O banco PostgreSQL deve ter backup automatizado às 00:00 e 12:00 (RNF-031).
- **Redundância:** Hospedagem em nuvem (AWS/Azure) com zonas de disponibilidade distintas.
- **Treinamento:** Professores devem ser treinados para identificar a "Nuvem com X" (ícone de erro de sync) e reportar ao suporte se persistir por mais de 24h.
