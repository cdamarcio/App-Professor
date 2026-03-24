# Especificação Visual do Protótipo (UI/UX)

Este documento traduz a identidade visual e os componentes de interface apresentados nas maquetes digitais do aplicativo SEMEC.

## 1. Identidade Visual e Cores
O aplicativo utiliza uma paleta sóbria e institucional, focada na legibilidade e no contraste.

* **Header (Topo):** Azul Marinho (#1A3358) - Utilizado para cabeçalhos e barras de navegação superior.
* **Ações Primárias:** Verde Esmeralda (#2E7D32) - Utilizado para botões de "Entrar", "Salvar" e status de "Presença".
* **Ações de Destaque:** Azul Royal (#0D47A1) - Utilizado para o botão principal "Iniciar Chamada".
* **Status de Alerta:** Vermelho (#C62828) - Utilizado para o botão de "Falta".
* **Fundo:** Cinza Ultra-claro (#F5F5F5) - Para reduzir o cansaço visual em uso prolongado.

---

## 2. Detalhamento das Telas

### Tela 01: Autenticação (Login)
* **Logotipo:** Centralizado no topo com brasão oficial de Conceição do Araguaia.
* **Inputs:** Campos de texto com ícones laterais (Usuário/Cadeado) e rótulos flutuantes.
* **Botão de Ação:** "ENTRAR" em largura total (Full Width) para facilitar o toque.

### Tela 02: Dashboard (Home)
* **Perfil:** Foto e nome do professor no topo à esquerda.
* **Status de Sincronia:** Ícone de nuvem no canto superior direito indicando "Sincronizado".
* **Cards de Turma:** * Título da Escola e Turma em negrito.
    * Botões empilhados para "INICIAR CHAMADA" (Azul) e "CONTEÚDO" (Verde).
    * **Estado Finalizado:** Turmas já concluídas aparecem com botões em cinza para indicar bloqueio ou conclusão.

### Tela 03: Chamada Digital
* **Cabeçalho de Turma:** Identificação clara da turma (ex: 6º Ano A) e seletor de data.
* **Lista de Alunos:**
    * Avatar circular para foto do aluno.
    * Nome do aluno em destaque.
    * Subtexto com horário do último lançamento (Auditoria visual).
* **Controles de Frequência:**
    * **P (Verde):** Toggle/Switch para presença.
    * **F (Vermelho):** Toggle/Switch para falta.
    * **J (Cinza):** Toggle para justificativa.
* **Botão de Finalização:** Botão flutuante inferior "Salvar e Sincronizar" com ícone de check (confirmado).

---

## 3. Elementos de Navegação Inferior (Tab Bar)
O aplicativo utiliza uma barra de navegação fixa com três destinos principais:
1.  **Home:** Tela principal com as turmas do dia.
2.  **História (Histórico):** Consulta de lançamentos passados.
3.  **Perfil:** Configurações da conta e dados do docente.

---

## 4. Notas de Implementação Frontend
* **Elevação:** Cards de turmas devem ter um `elevation` (sombra) leve para dar profundidade.
* **Responsividade:** O layout deve se ajustar automaticamente entre telas de 5" e 6.7".
* **Toque:** Área mínima de toque para os botões de Presença/Falta deve ser de 44x44px para evitar erros de lançamento.
