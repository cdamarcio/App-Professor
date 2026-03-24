# Mapeamento de Casos de Borda (Edge Cases)

Este documento identifica cenários de exceção e comportamentos esperados para garantir a resiliência do aplicativo de frequência da SEMEC, especialmente em condições de baixa conectividade ou tentativas de manipulação de dados.

## 1. Conflitos de Temporalidade (Regra das 48h)

| Cenário | Descrição | Comportamento Esperado (Requisito) |
| :--- | :--- | :--- |
| **Relógio do Celular Adulterado** | O professor altera a data do smartphone para tentar editar um registro antigo. | **Bloqueio:** O sistema deve ignorar o `timestamp` do dispositivo e utilizar exclusivamente o `timestamp` do servidor (NTP) para validar a janela de 48h. |
| **Sincronização Tardira** | O registro foi feito offline dentro das 48h, mas a internet só retornou após 50h. | **Permissão:** O sistema deve aceitar o pacote se o `timestamp_criacao_local` for válido, porém deve marcar o registro com uma *flag* de "Sincronização Extemporânea" para auditoria. |
| **Mudança de Fuso Horário** | Professor viaja para outra região (ex: Palmas ou Brasília) com fuso diferente. | **Padronização:** Todo o sistema deve operar em `UTC-3` (Horário de Brasília), independente da configuração local do aparelho. |

## 2. Conectividade e Sincronização

| Cenário | Descrição | Comportamento Esperado (Requisito) |
| :--- | :--- | :--- |
| **Queda de Sinal Durante Upload** | A conexão cai exatamente enquanto o JSON de frequência está sendo enviado. | **Idempotência:** O App deve retransmitir o dado. A API deve usar um `UUID` de transação para não duplicar a falta/presença no banco de dados. |
| **Cache Local Cheio** | O dispositivo do professor está sem espaço para armazenar novas fotos/anexos de conteúdo. | **Priorização:** O sistema deve alertar o usuário e impedir novos anexos, mas **nunca** impedir o lançamento de texto (frequência), que ocupa poucos bytes. |
| **Login Expirado Offline** | O Token JWT expira enquanto o professor está em uma zona rural sem sinal. | **Grace Period:** O App deve permitir o uso em "Modo de Emergência" por até 12h adicionais, sincronizando obrigatoriamente assim que detectar rede. |

## 3. Integridade de Dados Escolares

| Cenário | Descrição | Comportamento Esperado (Requisito) |
| :--- | :--- | :--- |
| **Aluno Transferido** | Um aluno é removido da turma no E-SEMEC enquanto o professor faz a chamada offline. | **Conciliação:** Na sincronização, a API deve rejeitar o registro desse aluno específico e notificar o professor: "Aluno [Nome] não pertence mais a esta turma". |
| **Edição Concorrente** | O Professor edita no App e o Coordenador edita no Web simultaneamente. | **Last Write Wins:** O registro com o `updated_at` mais recente prevalece, mas uma entrada no log de auditoria deve preservar o histórico de ambos. |
| **Duplicidade de Turma** | O professor possui duas turmas idênticas em horários subsequentes. | **Validação:** O sistema deve exigir a confirmação da disciplina/horário para evitar que a frequência da "Turma A" seja lançada erroneamente na "Turma B". |

## 4. Segurança e Acesso

| Cenário | Descrição | Comportamento Esperado (Requisito) |
| :--- | :--- | :--- |
| **Múltiplas Falhas de Login** | Tentativas sucessivas de acesso com CPF/Senha errados. | **Rate Limiting:** Bloqueio temporário do IP/Dispositivo por 15 minutos após 5 tentativas (conforme RF-005). |
| **Perda do Dispositivo** | O celular do professor é furtado ou perdido. | **Remote Wipe:** Caso o professor reporte, a próxima vez que o App conectar (mesmo sem login), deve disparar um comando para apagar o cache local de dados sensíveis dos alunos. |

---

### Diretriz para o Time de QA (Testes)
Todos os casos acima devem constar no **Plano de Testes de Estresse**. 
Especial atenção deve ser dada ao teste de **"Sincronização com Bateria Fraca"**, garantindo que o banco de dados local (`SQLite`) não seja corrompido caso o celular desligue durante um `COMMIT`.
