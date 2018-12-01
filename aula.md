> Link do curso: http://bit.ly/pybrpandas


```
Colinha: 

bit.ly/pybrpandas

Análise de Dados Públicos com Pandas (curso básico para divulgação)

Bloco de notas colaborativo, neste workshop favor somente copiar (CTRL + C) 

Se quiserem entrar com contato comigo:
https://about.me/fmasanori

Material para aprendizagem 0800 (gratuito):
https://www.pycursos.com/python-para-zumbis/
https://github.com/fmasanori/PPZ
https://github.com/fmasanori/treinamento

Instalação, checagem:
Depois de instalar o Python 3.6 ou Python 3.7

Procurar > CMD > enter (terminal no Linux)

para checar se o python está acessível

python -V

na tela preta digitar os comandos abaixo

python -m pip install --upgrade pip

No Ubuntu 16:
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt-get update
sudo apt-get install python3.6

No MacOS 
https://wsvincent.com/install-python3-mac/

pip install requests beautifulsoup4 spotipy pdfminer3k selenium twitter wbdata pandas matplotlib lxml tweepy uber-rides xlrd PyPDF2 pytrends seaborn numpy ipython jupyter

Mínimo:
pip install requests beautifulsoup4 wbdata pandas matplotlib lxml pytrends seaborn numpy ipython jupyter

https://github.com/fmasanori/treinamento
Bruxarias com Pandas.zip baixar e descompactar

Link direto, se preferir: https://github.com/fmasanori/treinamento/blob/master/Bruxaria%20com%20Pandas.zip

Baixar e descompactar arquivo SUS de Santa Catarina, renomear tirando o acento

https://drive.google.com/open?id=10YGsNwr8dQWXZhr9i6z-Ttp10GYHTg3N

procurar cmd enter 

jupyter notebook

print ("Alô Mundo")

Print ("Alô Mundo")

print (Alô Mundo)

print "Alô Mundo"

nome = "Epaminondas"
print (nome)

resposta = 42
print (resposta)

print (nome + " gosta de " + resposta)

print (f'{nome} gosta de {resposta}')

dir (nome)

help (nome.upper)

print (nome.upper())

import random
dir (random)

help (random.choice)

random.choice(['Aline', 'Virgínia', 'Joana', 'Tayssa'])

random.choice('Aline Virgínia Joana Tayssa'.split())

import requests
p = requests.get('http://beans.itcarlow.ie/prices.html')
print (p.text)

from bs4 import BeautifulSoup as bs
s = bs(p.text, 'html.parser')
print (s.strong)
print (s.h2.string)

p = requests.get('http://beans.itcarlow.ie/prices-loyalty.html')
s = bs(p.text, 'html.parser')
print (s.strong.string)

for nome in 'Aline Virgínia Joana Tayssa'.split():
    print (f'Oi {nome}!')

nomes = 'Aline Virgínia Joana Tayssa'.split()
print (nomes[1:3])

print (nomes[1:-1])

No navegador: https://sismpconsultapublica.mpsp.mp.br/

import requests
from bs4 import BeautifulSoup as bs
url = 'https://sismpconsultapublica.mpsp.mp.br/ConsultarDistribuicao/ObterProcedimentosPorMembro'
p = requests.get(url)
s = bs(p.text, 'html.parser')
lista = s.findAll('option')
nomes = lista[1:-5] 
for name in nomes:
    print (name.string, name['value'])
  
print (len(nomes))

Google filiados partidos TSE
import requests
from bs4 import BeautifulSoup as bs

u = 'http://filiaweb.tse.jus.br/filiaweb/portal/relacoesFiliados.xhtml'
p = requests.get(u)
s = bs(p.text, 'html.parser')
itens = s.findAll('option')
for p in itens:
    print (p['value'])

partidos = itens[:-27] #correto
partidos = itens[14:16] #para não demorar...
ufs = itens[-27:] #correto
ufs = itens[-27:-25] #para não demorar
url = 'http://agencia.tse.jus.br/estatistica/sead/eleitorado/filiados/uf/filiados_'
from urllib.request import urlretrieve
for p in partidos:
    for uf in ufs:
        u = f'{url}{p["value"]}_{uf["value"]}.zip'
        file = f'{p["value"]}_{uf["value"]}.zip'
        print (file)
        urlretrieve (u, file)

Atenção: neste momento todos nós estaremos acessando ao mesmo tempo o TSE, pode ocorrer do servidor bloquear momentaneamente nosso acesso, pois saberá que é um robô fazendo download, também podemos ter uma limitação da internet local

from zipfile import ZipFile
import os

files = os.listdir(".")
for f in files:
  if f.endswith('.zip'):
    try:
      print (f)
      z = ZipFile(f, 'r')
      z.extractall('Filiados')
      z.close()
    except:
      print (f'{f} está com erro')

Caso tenhamos optado por interromper o processamento algum arquivo  irá dar erro na descompactação

https://www.nabuscadocandidato.com.br/

google pytrends example

from pytrends.request import TrendReq
pytrend = TrendReq(hl='BR')
candidatos = 'Bolsonaro Haddad'.split()
pytrend.build_payload(kw_list=candidatos)
trends = pytrend.related_queries()
for p in trends:
  print (f'Rising {p}')
  print (trends[p]['rising'])
  print (f'Top {p}')
  print (trends[p]['top'])
  print ()

#Creditos Larissa Lautert
import pandas as pd
import seaborn as sb
low_memory=False
%matplotlib inline
pd.options.display.max_columns = 80
pd.options.display.max_rows = 90

filename = 'fila-publica-2017-11-30.csv'
df = pd.read_csv(filename)

df.shape

df.describe()

df.info()

df.rename(columns={'MUNICÍPIO DE RESIDÊNCIA': 'MUNICÍPIODERESIDÊNCIA',
                   'CENTRAL DE REGULAÇÃO/RESPONSÁVEL': 'CENTRALDEREGULAÇÃO/RESPONSÁVEL',
                   'TEMPO MÉDIO DE ESPERA(DIAS)': 'TEMPOMÉDIODEESPERA(DIAS)',
                   'DATA DA SOLICITAÇÃO': 'DATADASOLICITAÇÃO',
                   'DESCRIÇÃO DO PROCEDIMENTO': 'DESCRIÇÃODOPROCEDIMENTO',
                   'CNES DA CENTRAL EXECUTANTE': 'CNESDACENTRALEXECUTANTE',
                   'CNES DA UNIDADE SOLICITANTE': 'CNESDAUNIDADESOLICITANTE'
                  }, inplace=True)

df.sample(10)

df.groupby('SERVIÇO').size().sort_values().plot(kind='barh')

df.groupby('MUNICÍPIODERESIDÊNCIA').size().sort_values().tail(20).plot(kind='barh', figsize=(10,10))

df.query('SERVIÇO == "Exame"')['MUNICÍPIODERESIDÊNCIA'].value_counts().head().plot(kind='barh')

df.query('SERVIÇO == "Exame"')['MUNICÍPIODERESIDÊNCIA'].value_counts().head()

df.query('SERVIÇO == "Exame" and MUNICÍPIODERESIDÊNCIA == "PALHOCA"').DOCUMENTO.value_counts().describe()

df.query('SERVIÇO == "Exame" and MUNICÍPIODERESIDÊNCIA == "PALHOCA"').DOCUMENTO.value_counts().head()

df.query('DOCUMENTO == 704207709501384')[['DESCRIÇÃODOPROCEDIMENTO','DATADASOLICITAÇÃO', 'CENTRALDEREGULAÇÃO/RESPONSÁVEL', 'POSIÇÃO', 'CNESDACENTRALEXECUTANTE', 'CNESDAUNIDADESOLICITANTE']].sort_values(by='DESCRIÇÃODOPROCEDIMENTO').head(10)

df.query('DOCUMENTO == 700603418445267')[['DESCRIÇÃODOPROCEDIMENTO','DATADASOLICITAÇÃO', 'CENTRALDEREGULAÇÃO/RESPONSÁVEL', 'POSIÇÃO', 'CNESDACENTRALEXECUTANTE', 'CNESDAUNIDADESOLICITANTE']].sort_values(by='DESCRIÇÃODOPROCEDIMENTO').head(10)

def deduplicate_stats(query=None):
    if query:
        df_tmp = df.query(query)
    else:
        df_tmp = df
    total_rows = len(df_tmp)
    unique_rows = len(df_tmp.groupby(['DOCUMENTO', 'DESCRIÇÃODOPROCEDIMENTO']))
    unique_rows_same_date = len(df_tmp.groupby(['DOCUMENTO', 'DESCRIÇÃODOPROCEDIMENTO', 'DATADASOLICITAÇÃO']))
    reducao_fila = (total_rows - unique_rows) / total_rows
    print('           registros na fila:', total_rows)
    print('    registros únicos na fila:', unique_rows)
    print('          duplicados (total):', total_rows - unique_rows)
    print('duplicados (mesmo timestamp):', total_rows - unique_rows_same_date)
    print('    redução com deduplicação:', int(100*reducao_fila), '%')

deduplicate_stats('MUNICÍPIODERESIDÊNCIA == "PALHOCA"')

deduplicate_stats()

deduplicate_stats('MUNICÍPIODERESIDÊNCIA == "FLORIANOPOLIS"')

deduplicate_stats('MUNICÍPIODERESIDÊNCIA == "JOINVILLE"')

df['DESCRIÇÃODOPROCEDIMENTO'].value_counts().to_frame().head(10)

df.query('DESCRIÇÃODOPROCEDIMENTO == "CONSULTA EM OFTALMOLOGIA - GERAL"')['MUNICÍPIODERESIDÊNCIA'].value_counts().to_frame().head(10)

Pacientes de Canelinha, ao solicitar uma consulta em oftalmologia, são direcionadas a 4 centrais executantes diferentes, que possuem tempo de espera entre 34 e 417 dias. Sugestão: rotear as pessoas para centrais com menos pacientes.

df.query('DESCRIÇÃODOPROCEDIMENTO == "CONSULTA EM OFTALMOLOGIA - GERAL"').groupby(['CÓDIGO SIGTAP DO PROCEDIMENTO', 'MUNICÍPIODERESIDÊNCIA', 'CNESDACENTRALEXECUTANTE', 'TEMPOMÉDIODEESPERA(DIAS)', 'CLASSIFICAÇÃO']).count()[['POSIÇÃO']].query('MUNICÍPIODERESIDÊNCIA == "CANELINHA"')

import re
p = re.compile(r'\d+')
d, m, a = p.findall('09-03-2018')
print (d, m, a)
d, m, a = p.findall('09/03/2018')
print (d, m, a)

a, m, d = p.findall('6(anos) 2(meses) 10(dias)')
print(a, m, d)
a, m, d = p.findall('6a2m10d')
print(a, m, d)

Save esse Jupyter Notebook com algum nome 

Baixar e descompactar Bruxarias com Pandas

Abrir o Jupyter Notebook Bruxaria com Pandas

Exemplo concreto de uma ex-aluna jornalista da Folha de Análise das Pesquisas Eleitorais (Natália Portinari)
https://gist.github.com/nportinari/bc42c14524990178e67a815eff4da1b8#file-pesquisas-eleitorais-ipynb
```
