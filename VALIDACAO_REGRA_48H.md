# Lógica de Validação de Edição (Regra das 48 Horas)

Este documento detalha o algoritmo de trava temporal necessário para cumprir a regra de negócio da SEMEC: registros de frequência e conteúdo só podem ser alterados em até 48 horas após sua criação.

## 1. Algoritmo de Validação (Pseudocódigo)

A lógica abaixo deve ser aplicada como um **Middleware** no Backend e como um **Interceptador de UI** no Frontend Mobile.

```python
# Módulo de Validação Temporal
# Entrada: timestamp_criacao (Data que o registro foi gerado no servidor)
# Entrada: timestamp_atual (Horário oficial do servidor - UTC-3)

FUNÇÃO validar_janela_edicao(timestamp_criacao, timestamp_atual):
    
    # 1. Calcular a diferença absoluta em milissegundos ou segundos
    diferenca_ms = timestamp_atual - timestamp_criacao
    
    # 2. Converter para horas (3.600.000 ms = 1 hora)
    horas_decorridas = diferenca_ms / 3600000
    
    # 3. Verificação da Regra de Negócio
    SE horas_decorridas < 0:
        RETORNAR {
            status: "ERRO",
            permissao: FALSO,
            mensagem: "Erro de integridade: Data de registro no futuro."
        }
        
    SE horas_decorridas <= 48:
        RETORNAR {
            status: "SUCESSO",
            permissao: VERDADEIRO,
            mensagem: "Edição autorizada: Registro dentro do prazo de 48h."
        }
    SENÃO:
        RETORNAR {
            status: "BLOQUEADO",
            permissao: FALSO,
            mensagem: "Prazo de 48h expirado. Alteração não permitida."
        }
FIM_FUNÇÃO
