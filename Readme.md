# :money_with_wings: Pesquisa sobre reembolsos feitos a senadores

[Link do Google Colab](https://colab.research.google.com/drive/1HhqgbnKFFbxwqcpNT19zcPQ7hWn-o-S7?usp=sharing)

Fonte dos dados: [CEAPS](https://www12.senado.leg.br/transparencia/dados-abertos-transparencia/dados-abertos-ceaps) (Cota para Exercício da Atividade Parlamentar dos Senadores)

Pesquisa feita como parte das atividades do #7DaysOfCode

# Limpeza e preparação dos dados

Os dados do CEAPS são separados por ano. O período escolhido abrange os anos de 2018 a 2022(até 31/05).

Algumas datas estavam com problemas que considerei erros de digitação. 

Seguindo o padrão de dois primeiros dígitos do ano trocados, fiz as seguintes substituições:
- 0202 = 2002
- 0219 = 2019

Após esse tratamento, os tipos das colunas puderam ser convertidos facilmente.
