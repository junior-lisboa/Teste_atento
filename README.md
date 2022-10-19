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

#### Nesse desafio foram filtrados dos dados referentes aos 4 anos, as colunas de ID dos Vendors e a coluna faturamento total:
dfvendors=dfgeral[['vendor_id','total_amount']]
#### Para efetuar a soma dos valores de acordo com cada vendor cadastrado foi necessario usar uma função de groupby tendo os parametros da coluna vendor para agrupar, e posteriormente utilizouse a função de soma para somar os valores arrecadados:
dfvendors2=dfvendors.groupby('vendor_id', as_index=False)['total_amount'].sum()
#### Para apresentar os dados na forma decrescente para sabermos os 3 maiores vendors, foi utilizado a função sort_values indicando a coluna de faturamento total como parametro e indicando "Falso" a demonstração ascendente dos dados:
dfvendors2.sort_values('total_amount', ascending=False)

## Terceiro desafio
### Faça um histograma da distribuição mensal, nos 4 anos, de corridas pagas em dinheiro

####  Nesse desafio foram filtrados dos dados referentes aos 4 anos, as colunas da data de ida(pickup_datetime) e a coluna tipo de pagamento(payment_type):
dfgrafico=dfgeral[['pickup_datetime','payment_type']]
#### Neste ponto foi feita uma conversão dos dados da coluna de data de ida que estava como objeto e foi convertida para datetime, assim sendo possivel trabalhar com as datas:
dfgrafico['pickup_datetime']=pd.to_datetime(dfgrafico.pickup_datetime)
#### Neste ponto foi feita uma padronização da coluna de metodo de pagamento para deixar todos os dados em caixa alta:
dfgrafico['payment_type']=dfgrafico['payment_type'].str.upper()
#### Neste trecho filtramos todos os dados que são referentes ao pagamento em dinheiro
dfFiltrado=dfgrafico[dfgrafico['payment_type']=='CASH']
#### Neste trecho foi montado o grafico de histograma que apresenta neste caso os 4 anos, mostrando uma barra para cada mês dos anos(48 barras):
plt.hist(dfFiltrado['pickup_datetime'],48,rwidth=0.9)
plt.title('Pagamento em dinheiro', fontsize=18)
plt.xlabel('Meses por anos(por semestre)')
plt.ylabel('Pagamento em dinheiro')
plt.figure(figsize=(1,1))
plt.show()

## Quarto desafio
### Faça um gráfico de série temporal contando a quantidade de gorjetas de cada dia, nos últimos 3 meses de 2012

#### Neste desafio foram pegos as colunas de data de ida(Pickup_datetime) e a coluna de gorjeta(tip_amount) referentes ao ano de 2012:
dfgorjetas=data2012[['pickup_datetime','tip_amount']]
#### Neste ponto foi feita uma conversão dos dados da coluna de data de ida que estava como objeto e foi convertida para datetime, assim sendo possivel trabalhar com as datas:
dfgorjetas['pickup_datetime']=pd.to_datetime(dfgorjetas.pickup_datetime)
#### Neste ponto são filtrados os dados para serem pegos apenas os ultmos meses do ano que são apartir de outubro(10) no caso do codigo abaixo, e esses dados são salvos em uma nova variavel:
selecao = dfgorjetas[dfgorjetas['pickup_datetime'].dt.month >= 10]
df20123 = selecao
#### Neste momento é retirado os dados de "hora" da coluna de data:
df20123['pickup_datetime']= df20123['pickup_datetime'].dt.date
#### Neste momento são agrupados os dados do mesmo dia e somados os valores de gorjeta, assim facilitando a criação do grafico de serie temporal:
dfFinal=df20123.groupby('pickup_datetime', as_index=False)['tip_amount'].sum()
#### Finalmente é apresentado o grafico de serie temporal utilizando a biblioteca seaborn apartir do codigo abaixo
plt.figure( figsize = ( 12, 5)) 
sns.lineplot( x = 'pickup_datetime', 
             y = 'tip_amount', 
             data = dfFinal, 
             label = 'Gorjetas por dia')
