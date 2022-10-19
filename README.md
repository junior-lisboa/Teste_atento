# Teste_atento
Teste Realizado para avaliação tecnica Atento, todos os desafios que requeriram código foram realizados
no ambiente do Google Colab.

## Importação das bibliotecas do Python utilizadas

import pandas as pd  

import numpy as np

import matplotlib.pyplot as plt

import seaborn as sns

from matplotlib.pyplot import figure

## importação dos dados utilizados no teste
### Os arquivos utilizados foram previamente armazenados no Drive para assim ser possivel utilizalos no google colab

#### Nesse trecho os arquivos JSON são lidos do diretorio do drive para serem armazenados em variaveis do Python
data2009=pd.read_json('/content/drive/MyDrive/Colab Notebooks/data-sample_data-nyctaxi-trips-2009-json_corrigido.json',  lines=True)
data2010=pd.read_json('/content/drive/MyDrive/Colab Notebooks/data-sample_data-nyctaxi-trips-2010-json_corrigido.json',  lines=True)
data2011=pd.read_json('/content/drive/MyDrive/Colab Notebooks/data-sample_data-nyctaxi-trips-2011-json_corrigido.json',  lines=True)
data2012=pd.read_json('/content/drive/MyDrive/Colab Notebooks/data-sample_data-nyctaxi-trips-2012-json_corrigido.json',  lines=True)

#### Nesta variavel estão sendo concatenadas as variaveis anteriores em uma, para facilitar as analise que tem como relevancia os 4 anos
dfgeral=pd.concat([data2009,data2010,data2011,data2012])

## Primeiro desafio
### Qual a distância média percorrida por viagens com no máximo 2 passageiros

#### Nesse desafio foi necessario pegar os dados dos 4 anos juntos, e passar apenas as colunas referentes a quantidade de passageiros(passenger_count) e a distancia percorrida(trip_distance):
dfmediaviagem=dfgeral[['passenger_count','trip_distance']]
#### Após filtradas as colunas foi feita uma filtragem nos dados para serem pegas apenas as viagens com até 2 passageiros:
dfresultado1=dfmediaviagem[dfmediaviagem['passenger_count'] <= 2]
#### E finalmente após serem filtrados apénas os dados necessarios para a analise foi usado uma função da biblioteca pandas para adquirir a média de distancia:
dfresultado1.mean()

## Segundo desafio
### Quais os 3 maiores vendors em quantidade total de dinheiro arrecadado
