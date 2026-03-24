# Checklist de Testes e Aceitação (QA/UAT)

Este documento serve como guia para a validação final das funcionalidades antes da homologação pela Secretaria de Educação.

---

## 1. Testes de Autenticação e Segurança
- [ ] **TC-01:** Login com CPF/Senha válidos do E-SEMEC (Sucesso).
- [ ] **TC-02:** Tentativa de login com senha incorreta 5x (Bloqueio Temporário).
- [ ] **TC-03:** Acesso ao app após 30 min de inatividade (Exigência de Re-autenticação).
- [ ] **TC-04:** Logout manual (Limpeza de tokens de sessão no dispositivo).

## 2. Testes de Frequência (Funcional)
- [ ] **TC-05:** Lançamento de presença para toda a turma (Caminho Feliz).
- [ ] **TC-06:** Lançamento de falta com justificativa/observação (Texto livre).
- [ ] **TC-07:** Edição de frequência dentro do prazo de 24h/48h.
- [ ] **TC-08:** Tentativa de edição de frequência após 48h (Deve estar bloqueado).
- [ ] **TC-09:** Visualização de alerta visual para alunos com >25% de faltas.

## 3. Testes de Conteúdo Pedagógico
- [ ] **TC-10:** Registro de tema e tópicos da aula.
- [ ] **TC-11:** Seleção de conteúdo baseado na Matriz Curricular pré-carregada.
- [ ] **TC-12:** Anexo de foto/imagem do quadro ou atividade (Upload com sucesso).
- [ ] **TC-13:** Consulta ao histórico de conteúdos de meses anteriores.

## 4. Testes de Resiliência (Offline/Sincronia)
- [ ] **TC-14:** Lançamento de chamada com o celular em "Modo Avião" (Persistência local).
- [ ] **TC-15:** Sincronização automática ao reativar Wi-Fi/4G.
- [ ] **TC-16:** Fechamento forçado do app durante a sincronização (Integridade do banco SQLite).
- [ ] **TC-17:** Verificação de consumo de dados (O app não deve exceder 5MB por sincronia de texto).

## 5. Testes de Usabilidade e Interface (UX)
- [ ] **TC-18:** Leitura da tela sob luz solar direta (Contraste e Legibilidade).
- [ ] **TC-19:** Tempo de carregamento da lista de alunos (Deve ser < 2 segundos).
- [ ] **TC-20:** Facilidade de clique nos botões de rádio (Presença/Falta) com uma mão.
- [ ] **TC-21:** Responsividade em telas pequenas (Ex: Smartphones de entrada).

## 6. Conformidade LGPD
- [ ] **TC-22:** Verificação se nomes de alunos não ficam expostos em notificações push.
- [ ] **TC-23:** Confirmação de que dados sensíveis são apagados se o app for desinstalado.

---

## Relatório de Erros (Bug Report)

Caso algum item acima falhe, favor registrar no padrão abaixo:

| ID Caso | Descrição do Erro | Severidade | Comportamento Esperado |
| :--- | :--- | :--- | :--- |
| Ex: TC-08 | Botão de editar continua ativo após 72h | Crítica | Botão deve ficar cinza/desabilitado |
| Ex: TC-12 | App trava ao anexar foto > 5MB | Média | Exibir aviso: "Arquivo muito grande" |

---

### Critério de Aprovação Final
O projeto será considerado **HOMOLOGADO** apenas se:
1. Todos os itens de Severidade **Crítica** estiverem corrigidos.
2. 100% dos testes de Sincronia (Offline) passarem sem perda de dados.
3. A Secretaria de Educação assinar o termo de recebimento técnico.
