# :money_with_wings: Pesquisa sobre reembolsos feitos a senadores

[Link do Google Colab](https://colab.research.google.com/drive/1VaGdKiQtwS5ZBPTfhi-zrGxxD1CnLSf6?usp=sharing)

Fonte dos dados: [CEAPS](https://www12.senado.leg.br/transparencia/dados-abertos-transparencia/dados-abertos-ceaps) (Cota para Exercício da Atividade Parlamentar dos Senadores)

Pesquisa feita como parte das atividades do #7DaysOfCode

Este Readme é apenas um resumo com apresentação de alguns gráficos. As visualizações completas e detalhes das conclusões devem ser consultadas no .ipynb.

# Limpeza e preparação dos dados

Os dados do CEAPS são separados por ano. O período escolhido abrange os anos de 2011 a 2022 (até 11/08).

Os arquivos possuem uma primeira linha que informa data e hora da última atualização feita, isso faz com que o Pandas use multiindex, o que atrapalha os primeiros tratamentos. Essas datas foram armazenadas em variáveis. A leitura do dataset em si pode ser feita da segunda linha em diante, juntamente com outros parêmetros vistos em código.

Como haviam muitas datas inconsistentes (anos de 200 a 5201) optei com levar em consideração a data em que as requisições de reembolso foram feitas ao invés da data do gasto. 

Os campos nulos eram relacionados à justificativa dos gastos, foram preenchidos com "Não informado".

Os reembolsos com valores negativos foram tratados com módulo.

Após esses tratamentos, os tipos das colunas puderam ser convertidos facilmente.

### Problemas encontrados

* Há diversas entradas em que os valores de reembolso são muito baixos (abaixo de R$ 1,00) e totalmente inconsistentes com o tipo de despesa e detalhamento (por exemplo: uma passagem aérea com valor de R$ 0,01).

Valores assim distorcem as médias dos gastos e podem mascarar possíveis valores exorbitantes que podem ser encontrados.

# Análises sobre os tipos de despesa que totalizaram valores mais altos e os senadores envolvidos (2019 a 11/08/2022)

* As análises foram feitas sobre os três tipos de despesa com maiores gastos.
* Os nomes foram abreviados no gráfico abaixo para melhor visualização.

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-reembolsos-CEAPS/blob/main/img/gastos_por_tipo_de_despesa_destaque.png?raw=true"/>
</div>

* Todas as análises foram feitas seguindo o seguinte modelo:

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-reembolsos-CEAPS/blob/main/img/hist_box_contratacao.png?raw=true"/>
</div>

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-reembolsos-CEAPS/blob/main/img/top10_senadores_sum_contratacao.png?raw=true"/>
</div>

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-reembolsos-CEAPS/blob/main/img/top10_senadores_count_contratacao.png?raw=true"/>
</div>

* Os três tipos de despesas com maiores gastos possuem um comportamernto semelhante: muitos reembolsos de valores baixos e poucos reembolsos de valores muito altos em relação à média.

* Boa parte deste comportamente pode ser explicado pela abrangência de serviços de determinado tipo. Por exemplo: os reembolsos do tipo 'Locomoção, hospedagem, alimentação, combustíveis e lubrificantes' abrange desde garrafas d'água até locação de aeronaves particulares.

* Despesas com valores subnotificados podem não ser reais e, somadas, causarem tanto prejuízo quanto uma quantidade menor de entradas superfaturadas, além de atrapalhar a detecção das mesmas de forma automática.

# Análises por senador

* Senadores que mais gastaram.

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-reembolsos-CEAPS/blob/main/img/top15_senadores_sum_2019-2022.png?raw=true"/>
</div>

# Gastos ao longo do tempo

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-reembolsos-CEAPS/blob/main/img/temporal_gastos_2019_07-2022.png?raw=true"/>
</div>

* O mês atual ainda não está com os valores completos, o que faria com que a linha mais escura tivesse uma queda brusca. Por isso, optei por desconsiderá-lo.

* Em 2022, os gastos dos senadores foram mais altos até maio, depois tiveram uma queda brusca. Isso pode estar relacionado tanto à inflação quanto à proximidade das eleições, que ocorrerão em outubro.

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-reembolsos-CEAPS/blob/main/img/temporal_gastos_2011_07-2022.png?raw=true"/>
</div>

* Observa-se um pico de mais de 6 milhões de reais em agosto de 2015.

### Investigação do pico de gastos

* Foi feita uma comparação entre o valor do pico e os outros 4 gastos mais altos do período. 

* Com exceção dos dois maiores gastos, o valor reembolsado em 08/2015 seria de R$ 2.127.935,96, um somatório menor do que os meses com maiores gastos de 2011 a 2022.

* Analisando-se outros campos da entradas, é possível que o valor exorbitante tenha sido causado por equívoco no preenchimento nos dados.

# Gastos em anos de eleições

* Considerei os anos 2014, 2018 e 2022.

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-reembolsos-CEAPS/blob/main/img/temporal_gastos_anos_eleitorais.png?raw=true"/>
</div>

* Visualmente, dois dos anos eleitorais do dataset (incluindo o atual, 2022) tiveram gastos maiores até o mês de maio, e gastos mais baixos em setembro.

* Para uma afirmação mais concreta sobre as médias de gastos, são necessários testes estatísticos que considerem as taxas de inflação a cada mês e ano.

🌱
