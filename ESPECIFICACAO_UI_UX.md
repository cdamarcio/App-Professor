# Especificação de Interface e Experiência do Usuário (UI/UX)

Este documento consolida a arquitetura de navegação, o guia de estilo e o detalhamento visual do aplicativo SEMEC, garantindo uma experiência fluida e institucional para os professores.

---

## 1. Identidade Visual (Style Guide)

O design foi concebido para ser funcional em ambientes escolares (alta luminosidade) e dispositivos de diversos desempenhos.

### Paleta de Cores
| Elemento | Hexadecimal | Aplicação |
| :--- | :--- | :--- |
| **Primária** | `#1A3358` | Headers, Barras de Navegação e Títulos. |
| **Destaque** | `#0D47A1` | Botão "Iniciar Chamada" (Ação Principal). |
| **Sucesso** | `#2E7D32` | Botão "Entrar", "Salvar" e Status "Presença". |
| **Alerta** | `#C62828` | Botão "Falta" e erros críticos. |
| **Fundo** | `#F5F5F5` | Background das telas para reduzir fadiga visual. |

### Tipografia e Componentes
* **Fonte:** Sans-serif (Roboto ou Open Sans).
* **Botões:** Altura mínima de 48dp com cantos levemente arredondados (8px).
* **Elevação:** Sombra suave (Level 1) em cards de turmas para profundidade.

---

## 2. Mapa de Navegação (Sitemap)

1.  **Splash Screen:** Logo da Prefeitura + Verificação de Versão.
2.  **Login:** Autenticação via CPF/Senha integrada ao E-SEMEC.
3.  **Dashboard (Home):** Listagem das turmas do turno e status de sincronia.
4.  **Chamada Digital:** Tela de marcação de Presença/Falta (P/F/J).
5.  **Lançamento de Conteúdo:** Registro de tema, tópicos e anexos de imagem.
6.  **Perfil/Histórico:** Consulta de dados do docente e registros passados.

---

## 3. Detalhamento das Telas Principais

### 3.1. Tela de Login
* **Visual:** Logotipo da Prefeitura centralizado.
* **UX:** Inputs com ícones laterais e botão "ENTRAR" em largura total (Full Width).
* **Feedback:** Mensagens de erro claras para "CPF Inválido" ou "Senha Incorreta".

### 3.2. Dashboard (Home)
* **Status de Sincronia:** Ícone de nuvem no topo direito.
    * *Nuvem com Check:* Sincronizado.
    * *Nuvem com Seta:* Sincronizando...
    * *Nuvem com X:* Erro ou Offline.
* **Cards de Turma:** Exibem Nome da Escola, Turma e Turno.
    * Botões ativos: Iniciar Chamada (Azul) e Conteúdo (Verde).
    * Botões inativos: "Finalizada" em cinza após o envio.

### 3.3. Chamada Digital (Frequência)
* **Interface:** Lista vertical com avatar do aluno e nome em destaque.
* **Controles de Frequência:**
    * **P (Verde):** Switch para Presença.
    * **F (Vermelho):** Switch para Falta.
    * **J (Cinza):** Ícone para anexar justificativa.
* **UX:** Botão flutuante (FAB) "Salvar e Sincronizar" que aparece somente após a marcação de todos os alunos.

### 3.4. Lançamento de Conteúdo
* **Campos:** Título da aula e campo de texto longo para desenvolvimento.
* **Mídia:** Área para anexar fotos do quadro ou atividades.
* **Trava Temporal:** Exibição da contagem regressiva para a regra das 48h.

---

## 4. Comportamentos e Micro-interações (UX)

* **Offline-First:** O app deve permitir todas as ações sem internet, mudando apenas o status da "nuvem" para laranja (Pendente).
* **Feedback Tátil (Haptic):** Pequena vibração ao marcar uma falta para evitar erros acidentais.
* **Acessibilidade:** Suporte a leitores de tela (TalkBack/VoiceOver) e contraste AA (WCAG 2.1).
* **Bloqueio de Edição:** Após 48h, os campos tornam-se "Read-Only" e o botão de salvar é ocultado.

---

## 5. Referência Visual (Mockups)
> *Nota: Para visualizar as telas, consulte os arquivos de imagem anexados ao repositório ou o protótipo no Figma.*

```text
[ LOGIN ] ----> [ DASHBOARD ] ----> [ CHAMADA ]
   |               |                   |
 (Auth)       (Lista Turmas)      (Lista Alunos)