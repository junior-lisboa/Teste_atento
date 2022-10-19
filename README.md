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
### Os arquivos utilizados foram previamente armazenados no Drive

data2009=pd.read_json('/content/drive/MyDrive/Colab Notebooks/data-sample_data-nyctaxi-trips-2009-json_corrigido.json',  lines=True)
data2010=pd.read_json('/content/drive/MyDrive/Colab Notebooks/data-sample_data-nyctaxi-trips-2010-json_corrigido.json',  lines=True)
data2011=pd.read_json('/content/drive/MyDrive/Colab Notebooks/data-sample_data-nyctaxi-trips-2011-json_corrigido.json',  lines=True)
data2012=pd.read_json('/content/drive/MyDrive/Colab Notebooks/data-sample_data-nyctaxi-trips-2012-json_corrigido.json',  lines=True)

