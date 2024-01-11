[![author](https://img.shields.io/badge/Author-Alex&nbsp;Teixeira-red.svg)](https://www.linkedin.com/in/alex-teixeira-soares-dos-santos-203137a8/)
[![](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://www.python.org/)


## Case iFood

Considere uma empresa bem estabelecida que atua no setor de varejo de alimentos. Atualmente, eles têm milhares de clientes registrados e atendem quase um milhão de consumidores por ano. Eles vendem produtos de 5 grandes categorias: vinhos, carnes, frutas exóticas, peixes especialmente preparados e produtos doces. Estes podem ser divididos ainda mais em produtos *gold* e regulares. Os clientes podem encomendar e adquirir produtos por meio de 3 canais de vendas: lojas físicas, catálogos e site da empresa. Globalmente, a empresa teve receitas sólidas e uma linha de fundo saudável nos últimos 3 anos, mas as perspectivas de crescimento dos lucros para os próximos 3 anos não são promissoras... Por esse motivo, várias iniciativas estratégicas estão sendo consideradas para inverter essa situação. Um deles é melhorar o desempenho das atividades de marketing, com foco especial em campanhas de marketing.

![pairplot](images/pairplot_clusters.png)

Projeto baseado em um processo setivo para Analista de dados do iFood disponível [neste repositório](https://github.com/ifood/ifood-data-business-analyst-test).


## Objetivo

Construir um modelo preditivo que apoiará iniciativas de marketing direto que produza maior lucro para a próxima campanha.

Objetivos detalhados:

- Realizar uma análise exploratória robusta.
- Segmentação de clientes através da base fornecida.
- Determinar o melhor número de clusters.
- Construir um modelo de classificação para prever se um cliente irá comprar o produto oferecido na campanha.
- Fornecer insights de negócio agregar valor a empresa partindo de dados.

## Estrutura do repositório

```
├── case
├── data
├── images
├── notebooks
├── reports
```

- Na pasta `case` temos o objetivo do projeto.
- Na pasta `data` estão os dados utilizados no projeto. O arquivo ml_project1_data.csv é o dataset utilizado originalmente. Os demais arquivos são os datasets gerados durante o projeto.
- Na pasta `images` estão as imagens utilizadas neste README.
- Na pasta `notebooks` estão os notebooks com o desenvolvimento do projeto.
- Na pasta `reports` estão os relatórios gerados durante o projeto utilizando a biblioteca ydata-profiling.

## Detalhes da análsise

Uma descrição detalhada do dataset utilizado está disponível [aqui](data/README.md).

### Etapa1: Análise exploratória

Com objetivo de resumir suas características para que possamos chegar a insights que irão nos orientar em anásises mais profundas. É de grande importância realizar esse procedimento pois através dele podemos formular hipóteses.

- Ao avaliar a base foi notado que temos a necessidade de criar algumas colunas como por exemplo: existe duas colunas uma com quantidade de crianças e outra com quantidade de adolescentes foi transformado para uma coluna HasChildren (tem filhos), outra coluna com intervalo de idades também foi criada entre outras.
- Identificamos outliers nas colunas Age, Income e MntTotal que aparentemente parece erro de digitação de usuário então dropamos essas linhas pois eram poucas.
- A escolha de colunas que adotamos como importantes para nossa análise é subjetivo sendo assim foi escolhido as colunas abaixo:
  - Income(Renda): Essa coluna escolhida pois legal ver o comportamento de quem tem uma renda maior ou menos;
  - Recency(Tempo para retorno): Para saber se o cliente tem compras recentes ou não;
  - DaysSinceEnrolled(Dias cadastrado): Avaliar o comportamento dos clientes mais recentes versus os mais antigos;
  - Age(idade): Assim como na coluna anterior ver o comportamento de consumo dos grupos de idade;
  - MntTotal(Valor gasto total em produtos): Essa coluna por exemplo acho interessante correlacionar ela com a Income;
  - HasChildren(tem filhos): E essa coluna foi escolhida para ser usada como um parametro hue no pairplot.
- Após análise dessas colunas utilizando boxplots foi percebido que poderiamos estar usando o Dummies e fazer uma correlação com nosso target.
- Foi gerado um no dataset "customers_new_features_and_drop"
- Segue abaixo visualização da nossa correlação:

![corr](images/output.png)

##
### Etapa2: Clusterização

Clustering é a categorização e agrupamento de dados de um conjunto. É feito através de características em comum entre dados.
O pré-processamento é fundamental na análise dos dados. pois ele envolve a limpeza de dados facilitando serem utilizados no aprendizado de máquinas.
Para essa etapa usaremos o arquivo gerado na última etapa(customers_new_features_and_drop).

- Após chamar o dataset gerado faremos um pré-processamento utilizando as funções: **OneHotEnconder** para converter as colunas categóricas em uma representação numérica, **StandardScaler** para padronizar as features removendo a média e escalonando para ter variância unitária, **MinMaxScaler** para realiza uma transformação linear em nossos dados, escalonando cada feature para um intervalo específico, geralmente [0, 1] e **PowerTransformer** está funcão irá aplicar transformações de potência para estabilizar a variância e tornar a distribuição dos dados mais próxima da normal.
- Com os resultados obtidos criamos um DataFrame, para aplicarmos dois métodos **Elbow Method** e uma técnica usada em análise de clusterização para que possamos determinar o número ideal de clusters a ser utilizado. E o **Silhouette Method** ulilizado para avaliar a validade dos clusters, ele mede quão semelhantes são os objetos no mesmo cluster e a diferença dos clusters vizinhos. 






