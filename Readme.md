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

As análises foram feitas sobre os três tipos de despesa com maiores gastos

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-reembolsos-CEAPS/blob/main/img/grafico_gastos_por_tipo_de_despesa_destaque.png?raw=true"/>
</div>

## Contratação de consultorias, assessorias, pesquisas, trabalhos técnicos e outros serviços de apoio ao exercício do mandato parlamentar

Houveram muitos gastos de valores "baixos", e alguns gastos com valores muito acima da média.

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-reembolsos-CEAPS/blob/main/img/graficos_contratacao.png?raw=true"/>
</div>

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-reembolsos-CEAPS/blob/main/img/top10_senadores_contratacao.png?raw=true"/>
</div>

### Problemas encontrados

* As requisições de reembolso com valores baixos (até R$ 58,88, quartil 5%) não apresentaram somas muito exorbitantes. Entretanto, dentre os fornecedores especificados nestas requisições haviam duas companhias aéreas. Em uma delas o detalhamento era relacionado a despesa com frete de documentos, mas na outra não havia nenhuma especificação.

## Passagens aéreas, aquáticas e terrestres nacionais (2019 - 11/08/2022)

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-reembolsos-CEAPS/blob/main/img/graficos_passagens.png?raw=true"/>
</div>

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-reembolsos-CEAPS/blob/main/img/top10_senadores_passagens.png?raw=true"/>
</div>

### Problemas encontrados

* Haviam passagens aéreas que supostamente foram mais baratas que passagens não aéreas. Como eram poucas (22), optei por remover estas entradas do dataset. Entretanto, considerando que o valor reembolsado aos senadores seja exatamente o que consta no CEAPS, o ideal seria identificar os valores reais destas passagens e descobrir a causa do equívoco.

## Locomoção, hospedagem, alimentação, combustíveis e lubrificantes

Este tipo de despesa é o que sofreu maior variação entre valores mais altos e mais baixos.

Os gastos mais baixos foram feitos por senadores que adquiriram itens baratos de consumo, como água e alimentação. Os três gastos mais altos, de R$ 39.000,00 a R$ 66.730,00, vieram da contratação de táxi aéreo (voos particulares).

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-reembolsos-CEAPS/blob/main/img/graficos_locomocao.png?raw=true"/>
</div>

<div align="center">
  <img src="https://github.com/Tathy/Pesquisa-reembolsos-CEAPS/blob/main/img/top10_senadores_locomocao.png?raw=true"/>
</div>

### Problemas encontrados

* Despesas com valores subnotificados podem não ser reais e, somadas, causarem tanto prejuízo quanto uma quantidade menor de entradas superfaturadas, além de atrapalhar a detecção das mesmas de forma automática.

🌱
