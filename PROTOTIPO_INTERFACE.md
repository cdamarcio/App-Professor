# Protótipo de Interface e Fluxo de Navegação (UX/UI)

Este documento define a hierarquia visual e os elementos de interface para o aplicativo da SEMEC, priorizando a usabilidade em dispositivos de entrada e ambientes de alta luminosidade.

---

## 1. Guia de Estilo (Style Guide)
Baseado na identidade visual de **Conceição do Araguaia**:
* **Cores Primárias:** Azul Marinho (Confiança/Institucional) e Verde (Educação).
* **Cores de Status:** * Presença: Verde (#28A745)
    * Falta: Vermelho (#DC3545)
    * Pendente de Sincronia: Laranja (#FD7E14)
* **Tipografia:** Sans-serif (Roboto ou Open Sans) para máxima legibilidade.
* **Componentes:** Botões com altura mínima de 48dp (padrão Google Material Design).

---

## 2. Mapa de Telas (Sitemap)

1.  **Splash Screen:** Logo da Prefeitura + Verificação de Versão.
2.  **Login:** Campos CPF e Senha + Botão "Entrar".
3.  **Dashboard (Home):** * Resumo do dia (Turmas do turno).
    * Indicador de Sincronização (Nuvem).
4.  **Lista de Alunos (Chamada):** * Filtro por Data/Disciplina.
    * Lista vertical com Toggle (P/F).
5.  **Lançamento de Conteúdo:** * Campo de texto rico + Botão de Anexo (Câmera).
6.  **Histórico/Relatórios:**
    * Visualização de frequências passadas (Leitura).

---

## 3. Descrição Detalhada das Telas

### Tela A: Dashboard do Professor
* **Topo:** Nome do Professor e Botão de Sincronização Manual.
* **Corpo:** Cards das turmas. 
    * *Exemplo:* "6º Ano A - Escola Maria das Dores - [Botão Iniciar Chamada]"
* **Rodapé:** Ícones: Home, Histórico, Perfil.

### Tela B: Chamada Digital (A mais crítica)
* **Cabeçalho:** Nome da Turma + Data (Calendário).
* **Lista:** Foto do aluno (se disponível) + Nome.
* **Ação:** Lado direito com três estados:
    * [P] - Círculo Verde (Ativo se presencial).
    * [F] - Círculo Vermelho (Ativo se falta).
    * [J] - Ícone de Clip (Se houver justificativa).
* **Botão Flutuante (FAB):** "Salvar e Sincronizar".

### Tela C: Lançamento de Conteúdo
* **Input 1:** Título da Aula (Texto curto).
* **Input 2:** Desenvolvimento/Resumo (Texto longo).
* **Área de Mídia:** Grade de miniaturas de fotos tiradas do quadro.
* **Trava:** Mensagem "Editável até [Data/Hora]" para reforçar a regra das 48h.

---

## 4. Protótipo de Baixa Fidelidade (Wireframe Textual)

```text
+---------------------------------------+
|  [=]  SEMEC - Conceição do Araguaia   |
+---------------------------------------+
| Olá, Prof. Márcio!                    |
| Status: [ CLOUD_DONE ] Sincronizado   |
+---------------------------------------+
| SUAS TURMAS HOJE:                     |
|                                       |
| > 9º Ano B (Matutino)                 |
|   [ REALIZAR CHAMADA ] [ CONTEÚDO ]   |
|                                       |
| > 8º Ano C (Matutino)                 |
|   [ FINALIZADA (EDITAR) ]             |
+---------------------------------------+
|  [Início]    [Histórico]    [Ajustes] |
+---------------------------------------+
