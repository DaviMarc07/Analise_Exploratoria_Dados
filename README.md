# Análise Exploratória de Dados (EDA) de Churn

1. Visão Geral do Projeto
Este projeto consiste na fase de Análise Exploratória de Dados (EDA), seguindo a etapa de limpeza e pré-processamento realizada no módulo anterior (base churn_telecon_limpo.csv).

O objetivo principal é entender as características e os comportamentos dos clientes que estão propensos ao Churn (Churn: yes) versus aqueles que permanecem (Churn: no), utilizando visualizações e estatísticas descritivas para extrair insights de negócio valiosos para a empresa de telecomunicações.

2. Leitura de Dados e Estatísticas Descritivas
Esta seção inicia o processo carregando a base de dados limpa e obtendo uma visão numérica inicial.

Importação de Bibliotecas: Foram importadas as bibliotecas pandas, numpy, seaborn, matplotlib.pyplot e plotly.express.

Justificativa: O plotly.express é incluído para criar gráficos interativos e dinâmicos, que são mais avançados e podem ser explorados pelo usuário (ex: gráficos de dispersão).

Leitura do CSV: A base churn_telecon_limpo.csv é carregada. É importante notar que o delimitador (delimiter=',') foi especificado corretamente, pois bases limpas salvas pelo Pandas usam a vírgula como padrão.

Estatísticas Descritivas (df.describe().T): O método .describe().T gera métricas como média, desvio padrão, mínimo, máximo e quartis para as variáveis quantitativas (tempo_como_cliente, pagamento_mensal, etc.). Isso oferece uma base para entender a tendência central e a dispersão dessas features antes da visualização.

3. Análise Univariada (Distribuição de Variáveis Individuais)
A análise univariada foca em entender a distribuição de cada variável isoladamente.

Plot 1: Distribuição do tempo_como_cliente (Quantitativa):

Gráfico: Histograma com estimativa de densidade de Kernel (sns.histplot(..., kde=True)).

Justificativa: O histograma é a ferramenta ideal para visualizar a forma da distribuição. Ele ajuda a identificar se a maioria dos clientes é nova (distribuição concentrada em valores baixos) ou antiga.

Plot 2: Frequência de servico_internet (Categórica):

Gráfico: Gráfico de Contagem (sns.countplot).

Justificativa: Usado para medir a frequência de cada categoria (ex: DSL, Fibra Ótica, Nenhum) e entender qual serviço é o mais predominante na base.

Plot 3: Frequência de servico_telefone (Categórica):

Gráfico: Gráfico de Contagem (sns.countplot).

Justificativa: Similar ao anterior, identifica a penetração do serviço de telefone entre os clientes.

Plot 4: Distribuição do pagamento_mensal (Quantitativa):

Gráfico: Histograma com KDE.

Justificativa: Revela se os pagamentos estão concentrados em faixas de preço baixas, médias ou altas.

4. Análise Bivariada (Relação com o Churn)
Esta é a seção mais crítica da EDA, pois cruza as variáveis com o alvo (churn) para extrair os drivers de saída de clientes.

Plot 5: tempo_como_cliente por churn (Boxplot):

Gráfico: Boxplot (sns.boxplot(x='churn', y='tempo_como_cliente', ...)).

Justificativa: O Boxplot é a melhor ferramenta para comparar a distribuição de uma variável quantitativa em relação a uma categórica. O resultado visual demonstra que a mediana de tempo como cliente para quem sai (yes) é significativamente menor do que para quem fica (no), confirmando que o risco de Churn é maior no início do contrato (clientes novos).

Plot 6: tipo_contrato por churn (Contagem Segmentada):

Gráfico: Gráfico de Contagem com segmentação (sns.countplot(x='tipo_contrato', hue='churn', ...)).

Justificativa: Permite visualizar a Taxa de Churn por tipo de contrato. Clientes com contratos de 2 anos (maior fidelidade) devem ter a menor taxa de Churn, enquanto contratos mensais devem ter a maior.

Plot 7: servico_internet por churn (Contagem Segmentada):

Gráfico: Gráfico de Contagem segmentada.

Justificativa: Ajuda a identificar se a qualidade ou o tipo de serviço de internet (ex: Fibra Ótica) está causando insatisfação e Churn.

Plot 8: pagamento_mensal por churn (Boxplot):

Gráfico: Boxplot.

Justificativa: Revela se o Churn está sendo impulsionado pelos clientes que pagam mais ou menos. O insight de que a mediana de pagamento mensal para clientes que saem é mais alta é crucial, indicando que a empresa está perdendo clientes de alto valor.

5. Geração de Insights de Negócio
O código finaliza o notebook compilando as observações estatísticas e visuais em conclusões de negócio.

Tempo de Cliente: A maior taxa de Churn ocorre no primeiro ano de contrato (mediana de aproximadamente 10 meses para clientes que saem).

Tipo de Contrato: Contratos mensais apresentam um risco de Churn drasticamente mais alto do que contratos de 1 ou 2 anos, confirmando a importância da fidelização.

Pagamento Mensal: Clientes de alto valor (maior pagamento_mensal) são mais propensos a sair, um insight de alto risco para o negócio.

Fatores Preditivos: O código identifica e lista as variáveis que mais se correlacionam com o Churn (ex: tipo_contrato, tempo_como_cliente, servico_internet), definindo o foco para a etapa de modelagem preditiva.
