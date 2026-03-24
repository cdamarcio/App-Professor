# Justificativa Técnica de Contratação
**Projeto:** Aplicativo Móvel de Gestão Escolar (Frequência e Conteúdo)
**Interessado:** Secretaria Municipal de Educação (SEMEC) - Conceição do Araguaia/PA
**Data:** Março de 2026

## 1. Contextualização e Objeto
A presente justificativa visa fundamentar a necessidade de desenvolvimento de uma solução tecnológica móvel (aplicativo) integrada ao sistema central **E-SEMEC**. O objetivo é digitalizar o registro de frequência de alunos e o lançamento de conteúdos programáticos pelos professores da rede municipal de ensino.

## 2. Diagnóstico da Situação Atual
Atualmente, o registro de classe em diversas unidades escolares de Conceição do Araguaia ainda ocorre de forma analógica (papel) ou depende de acesso constante à internet em computadores fixos nas secretarias das escolas. Esta modalidade apresenta os seguintes gargalos:
* **Déficit de Temporalidade:** Os dados de infrequência escolar demoram dias ou semanas para chegar à Secretaria, impedindo ações rápidas contra a evasão escolar.
* **Inconsistência de Dados:** O preenchimento manual está sujeito a erros de grafia e perda física de documentos.
* **Baixa Eficiência Administrativa:** O retrabalho de digitar dados do papel para o sistema E-SEMEC consome horas produtivas de secretários e coordenadores.

## 3. Motivação e Benefícios Técnicos
A implementação do aplicativo proposto baseia-se nos pilares de **Inovação, Transparência e Economia**:

### 3.1. Sincronização Híbrida (Offline-First)
Dada a realidade geográfica do município, onde o sinal de internet pode ser instável em determinadas unidades escolares ou zonas rurais, a tecnologia **Offline-First** garantirá que o professor realize seu trabalho sem interrupções, sincronizando os dados automaticamente assim que houver conectividade.

### 3.2. Rastreabilidade e Auditoria
O sistema implementará uma **janela de edição de 48 horas**, garantindo a integridade dos registros e impedindo alterações retroativas injustificadas. Além disso, o uso de logs de auditoria permitirá identificar o autor e o horário exato de cada lançamento, atendendo às exigências dos órgãos de controle.

### 3.3. Conformidade com a LGPD
O desenvolvimento sob medida assegura que os dados sensíveis dos menores de idade (alunos) sejam tratados estritamente conforme a **Lei Geral de Proteção de Dados (Lei 13.709/2018)**, com criptografia em repouso e em trânsito.

## 4. Resultados Esperados
1. **Redução de Evasão:** Identificação imediata de alunos com baixa frequência para intervenção do Conselho Tutelar e SME.
2. **Eliminação de Papel:** Redução de custos com impressão e armazenamento físico de diários de classe.
3. **Gestão em Tempo Real:** Dashboard para a Secretaria com indicadores precisos do cumprimento da matriz curricular em toda a rede.

## 5. Parecer de Viabilidade
Considerando a maturidade do sistema E-SEMEC e a crescente digitalização dos serviços públicos, o desenvolvimento desta ferramenta é tecnicamente viável e essencial para a modernização da gestão pública em Conceição do Araguaia. A solução proposta adota padrões de arquitetura modernos (API REST, PostgreSQL, SQLite) que garantem escalabilidade para os próximos 5 anos.
