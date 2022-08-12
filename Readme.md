# :money_with_wings: Pesquisa sobre reembolsos feitos a senadores

[Link do Google Colab](https://colab.research.google.com/drive/1VaGdKiQtwS5ZBPTfhi-zrGxxD1CnLSf6?usp=sharing)

Fonte dos dados: [CEAPS](https://www12.senado.leg.br/transparencia/dados-abertos-transparencia/dados-abertos-ceaps) (Cota para Exercício da Atividade Parlamentar dos Senadores)

Pesquisa feita como parte das atividades do #7DaysOfCode

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

# Análises sobre estatísticas de cada tipo de despesa e os senadores envolvidos

Até o momento, as análises estão sendo feitas separadas por tipo de despesa, totalizando sete:

- Locomoção, hospedagem, alimentação, combustíveis e lubrificantes
- Passagens aéreas, aquáticas e terrestres nacionais
- Aluguel de imóveis para escritório político, compreendendo despesas concernentes a eles
- Aquisição de material de consumo para uso no escritório político, inclusive aquisição ou locação de software, despesas postais, aquisição de publicações, locação de móveis e de equipamentos
- Divulgação da atividade parlamentar
- Contratação de consultorias, assessorias, pesquisas, trabalhos técnicos e outros serviços de apoio ao exercício do mandato parlamentar
- Serviços de Segurança Privada

Cada tipo está sendo analisado da seguinte forma:
- Reembolsos com valores altos (quartis 95% e 99%)
- Reembolsos com valores baixos (quartis 5% e 1%)
- Senadores com maiores somatórios em requisições de reembolsos com valores baixos e os fornecedores que mais receberam
- Senadores com maiores somatórios em requisições de reembolsos com valores altos e os fornecedores que mais receberam

### Problemas encontrados

* Haviam passagens aéreas que supostamente foram mais baratas que passagens não aéreas. Como eram poucas (22), optei por remover estas entradas do dataset. Entretanto, considerando que o valor reembolsado aos senadores seja exatamente o que consta no CEAPS, o ideal seria identificar os valores reais destas passagens e descobrir a causa do equívoco.

* Despesas com valores subnotificados podem não ser reais e, somadas, causarem tanto prejuízo quanto uma quantidade menor de entradas superfaturadas, além de atrapalhar a detecção das mesmas de forma automática.
