# Trabalho-Final-de-APC


# Grupo G - Coronavírus (COVID-19) in Brazil

### Membros
|Matrícula|Nome Completo|
|:---|:---|
|200061143|Calebe Cardoso de Aragão|
|222008468|Danilo Sarmento Barros|
|222029243|Victor Hugo dos Santos Bernardes |
|222006178|Thales Henrique Euflauzino dos Santos |
|222008922|Júlio César da Costa Santos |
|222023590|João Victor Fonseca Reis |
## Avaliação


### Geral


### Gráficos

Os critérios da avaliação são divididos em:
* Objetivo(O) [0-10]: avalia se o objetivo do gráfico está claro.
* LayoutxObjetivo(LO) [0-10]: avalia se o layout do gráfico está coerente com o objetivo.
* Código de Preparação do Dado (CD) [0:10]: avalia se o código usado para gerar/processar o dado usado pelo gráfico faz uso de estruturas de decisão e repetição e **NÃO FEZ USO DOS RECURSOS DO PANDAS DATAFRAME**.
* Código de Geração/Configuração do Gráfico(CG) [0-10]: avalia o código usado do Plotly está correto. 
* Compreensão do Código(CC) [0-10]:	avalia o conhecimento do aluno sobre o código do gráfico apresentado.
* Nota(N) [0-100]: nota resultante de cada gráfico. $N=\frac{O+2*LO+4*CD+3*DG}{10}*CC$
* Avaliação do Grupo pelo Professor [0-100]: nota final do grupo para a avaliação. $AGP=\frac{\sum_{i=1}^n N_i}{i}$
import pandas as pd
from numpy.lib.function_base import average
import io
_str = '''|Grafico|O|LO|CD|CG|CC|
|Gráfico de porcentagem de casos acumulados de COVID-19 no Brasil| 10|10|10|10|10|
|Grafico de porcentagem de óbitos acumulados de COVID-19 no Brasil| 10|10|10|10|10|
|Gráfico dos Casos Novos de COVID-19 no Brasil por estado em relação a região Sudeste| 10|10|10|10|10|
|Gráfico dos Casos Acumulados de COVID-19 no Brasil por estado em relação a região Sudeste| 10|10|10|10|10|
|Gráfico dos Óbitos Novos de COVID-19 no Brasil por estado em relação a região Sudeste| 10|10|10|10|10|
|Gráfico dos Óbitos Acumulados de COVID-19 no Brasil por estado em relação a região Sudeste| 10|10|10|10|10|
'''
strIO = io.StringIO(_str)
df = pd.read_csv(strIO, sep='|', ).iloc[:, 1:-1]
df['N'] = df['CC']*(df['O']+ 2*df['LO']+4*df['CD']+3*df['CG'])/10
display(df)
print(f'AGP = {df[["N"]].mean()[0]}')
## Objetivo
O intuito desse projeto é analisar os dados refentes ao inicio do contágio do vírus SARS-CoV-2, o coronavírus (COVID-19) no Brasil no período entre o início de 2020 até o dia 14 de abril do mesmo ano, tendo em vista como foi dado contágio por meio dos casos além de analisar os óbitos que pesaram o país.
## Bases de Dados

|Nome|Descrição|Colunas| Amostras|
|:---|:---|--:|--:|
|[Base 1](https://drive.google.com/file/d/1WJKA-2bSywKdDnU6Bv547qXIYwgm_urs/view?usp=share_link)|Dados sobre a pandemia de Covid19 no Brasil|7|2052|

### Base 1
pip install pandas
pip install pandas plotly.express
import pandas as pd
import plotly.express as px
from google.colab import drive
drive.mount('/content/drive')
dataset = pd.read_csv('/content/drive/MyDrive/COVID19ee.csv', sep = ",")
tabela = dataset.values.tolist()

dataset.head(5)
## Gráficos
1. Gráfico de porcentagem de casos acumulados de COVID-19 no Brasil.
2. Grafico de porcentagem de óbitos acumulados de COVID-19 no Brasil.
3. Gráfico dos Casos Novos de COVID-19 no Brasil por estado em relação a região Sudeste.
4.  Gráfico dos Casos Acumulados de COVID-19 no Brasil por estado em relação a região Sudeste.
5. Gráfico dos Óbitos Novos de COVID-19 no Brasil por estado em relação a região Sudeste.
6. Gráfico dos Óbitos Acumulados de COVID-19 no Brasil por estado em relação a região Sudeste.
### Gráfico de porcentagem de Casos Acumulados de COVID-19 no Brasil.

O intuito deste gráfico é apresentar a porcentagem do Casos Acumulados de Covid19 no Brasil por região.


casosnovos = []
region = []
newdeaths = []
tablepie = []
piedataset = []

for row in tabela:
  if not row[2] == '':
    casosnovos = row[3]
    region = row[0]
    tablepie.append([region, casosnovos])   

for row in tablepie:
  piedataset.append({"Region": row[0], "Casos Novos": row[1]})


fig = px.pie(piedataset, values="Casos Novos", names="Region", color="Region", title='Porcentagem de Casos Acumulados de Covid19 por Região em relação ao Brasil',
             color_discrete_map={'Nordeste':'red',
                                 'Norte':'darkorange',
                                 'Centro-Oeste':'deeppink',
                                 'Sul':'yellow',
                                 'Sudeste':'darkred'})
fig.update_traces(textposition = 'inside', textinfo = 'percent+label')
fig.show()
### Gráfico de porcentagem de Óbitos Acumulados de COVID-19 no Brasil.

O intuito deste gráfico é apresentar a porcentagem de óbitos acumulados de Covid19 no Brasil por região.

tablepie1 = []
MortesNovas = []
regiao = []
piedataset1 = []

i = 0
num_elements_list = len(tabela)
while i < num_elements_list:
  row = tabela[i]
  regiao = row[0]
  MortesNovas = row[5]
  if not row[2] == '': 
    tablepie1.append([regiao, MortesNovas])
  i += 1

i = 0
tamanho = len(tablepie1)

while i < tamanho:
    piedataset1.append({"Regiao": tablepie1[i][0], "Obitos Novos": tablepie1[i][1]})
    i += 1
fig = px.pie(piedataset1, values = 'Obitos Novos', names = 'Regiao', color = 'Regiao', title = 'Porcentagem de Óbitos Acumulados de Covid19 por Região em relação ao Brasil',       
             color_discrete_map={'Nordeste':'red',
                                 'Norte':'darkorange',
                                 'Centro-Oeste':'deeppink',
                                 'Sul':'yellow',
                                 'Sudeste':'darkred'})
fig.update_traces(textposition='inside', textinfo='percent+label')
fig.show()
### Estrutura de códigos para os gráficos de linha.

Essa estrutura tem o objetivo de gerar os dados dos gráficos de linhas filtrando pelos estados da região Sudeste.

Código usado para Casos/Óbitos novos com FOR.
Estado = []
Data = [] 
CasosNovos = []
ObitosNovos = []
TabelaNova = []
dfdataset = []

for row in tabela:
  Estado = row[1]
  Data = row[2]
  CasosNovos = row[3]
  ObitosNovos = row[5]
  if not row[2] == '':
    # if Estado == 'São Paulo' or Estado == 'Rio de Janeiro' or Estado == 'Espírito Santo' or Estado == 'Minas Gerais':
       TabelaNova.append([Data, Estado, CasosNovos, ObitosNovos])

for i in TabelaNova:
  dfdataset.append({"Data": i[0], "Estado": i[1], "Casos Novos": i[2], "Obitos Novos": i[3]})
Código usado para Casos/Óbitos acumulados com WHILE.
Estado = []
Data1 = [] 
CasosAcumulados = []
ObitosAcumulados = []
tablewhile = []
whiledataset = []
print(tabela)

i = 0
tamanholista = len(tabela)
while i < tamanholista:
  row = tabela[i]
  Estado = row[1]
  Data1 = row[2]
  CasosAcumulados = row[4]
  ObitosAcumulados = row[6]

  if not row[2] == '':
    if Estado == 'São Paulo' or Estado == 'Rio de Janeiro' or Estado == 'Espírito Santo' or Estado == 'Minas Gerais':
      if row[4] >= 1:
        tablewhile.append([Data1, Estado, CasosAcumulados, ObitosAcumulados])
  i += 1

i = 0
tamanho = len(tablewhile)
while i < tamanho:
    whiledataset.append({"Data1": tablewhile[i][0], "Estado": tablewhile[i][1], "Casos Acumulados": tablewhile[i][2], "Obitos Acumulados": tablewhile[i][3]})
    i += 1
### Gráfico dos Casos Novos de COVID-19 no Brasil por estado em relação a região Sudeste.

Esse gráfico tem como função demonstrar exponencialmente o crescimento de Casos Novos de Covid19 no Brasil por estado, desde o início do ano de 2020.


x = px.line(dfdataset, x = 'Data', y = 'Casos Novos',title= 'Casos Novos de Covid19 no Brasil por Estado em Relação a Região Sudeste', color= 'Estado', markers=True)
x.update_yaxes(title= 'Quantidade de Casos Novos',title_font_color = 'red', ticks = 'outside', tickfont_color='green')
x.update_xaxes(title_text='Dias do ano', title_font_color='red', ticks='outside',tickfont_color='green')
x.show()
### Gráfico dos Casos Acumulados de COVID-19 no Brasil por estado em relação a região Sudeste.

Esse gráfico tem como função demonstrar exponencialmente o crescimento de Casos Acumulados de Covid19 no Brasil por estado, desde o início do ano de 2020.


fig = px.line(whiledataset, x = 'Data1', y = 'Casos Acumulados',title= 'Casos Acumulados de Covid19 no Brasil por Estado em Relação a Região Sudeste', color= 'Estado', markers=True)
fig.update_yaxes(title= 'Quantidade de Casos Acumulados',title_font_color = 'red', ticks = 'outside', tickfont_color='green')
fig.update_xaxes(title_text='Dias do ano', title_font_color='red',ticks='outside',tickfont_color='green')
fig.show()
###Gráfico dos Óbitos Novos de COVID-19 no Brasil por estado em relação a região Sudeste.

Esse gráfico tem como função demonstrar exponencialmente o crescimento de óbitos novos de Covid19 no Brasil por estado, desde o início do ano de 2020.


fig = px.line(dfdataset, x = 'Data', y = 'Obitos Novos',title= 'Obitos Novos de Covid19 no Brasil por Estado em Relação a Região Sudeste', color= 'Estado', markers=True)
fig.update_yaxes(title= 'Quantidade de Obitos Novos',title_font_color = 'red', ticks = 'outside', tickfont_color='green')
fig.update_xaxes(title_text='Dias do ano', title_font_color='red',ticks='outside',tickfont_color='green')
fig.show()
###Gráfico dos Óbitos Acumulados de COVID-19 no Brasil por estado em relação a região Sudeste.

Esse gráfico tem como função demonstrar exponencialmente o crescimento de óbitos acumulados de Covid19 no Brasil por estado, desde o início do ano de 2020.

fig = px.line(whiledataset, x = 'Data1', y = 'Obitos Acumulados',title= 'Obitos Acumulados de Covid19 no Brasil por Estado em Relação a Região Sudeste', color= 'Estado', markers=True)
fig.update_yaxes(title= 'Quantidade de Obitos Acumulados',title_font_color = 'red', ticks = 'outside', tickfont_color='green')
fig.update_xaxes(title_text='Dias do ano', title_font_color='red',ticks='outside',tickfont_color='green')
fig.show()
#Dashboard
pip install dash
import pandas as pd
import plotly.express as px
from dash import Dash, html, dcc, Input, Output

from google.colab import drive
drive.mount("/content/drive", force_remount=True)

app = Dash(__name__)
dataset = pd.read_csv('/content/drive/MyDrive/COVID19ee.csv', sep = ",")
tabela = dataset.values.tolist()

casosnovos = []
region = []
newdeaths = []
tablepie = []
piedataset = []

for row in tabela:
    if not row[2] == '':
        casosnovos = row[3]
        region = row[0]
        tablepie.append([region, casosnovos])

for row in tablepie:
    piedataset.append({"Region": row[0], "Casos Novos": row[1]})

tablepie1 = []
MortesNovas = []
regiao = []
piedataset1 = []

i = 0
num_elements_list = len(tabela)
while i < num_elements_list:
    row = tabela[i]
    regiao = row[0]
    MortesNovas = row[5]
    if not row[2] == '':
        tablepie1.append([regiao, MortesNovas])
    i += 1

i = 0
tamanho = len(tablepie1)

while i < tamanho:
    piedataset1.append(
        {"Regiao": tablepie1[i][0], "Obitos Novos": tablepie1[i][1]})
    i += 1

regiao = []
Estado = []
Data = []
CasosNovos = []
ObitosNovos = []
TabelaNova = []
dfdataset = []

for row in tabela:
    regiao = row[0]
    Estado = row[1]
    Data = row[2]
    CasosNovos = row[3]
    ObitosNovos = row[5]
    if not row[2] == '':
        # if Estado == 'São Paulo' or Estado == 'Rio de Janeiro' or Estado == 'Espírito Santo' or Estado == 'Minas Gerais':
        TabelaNova.append([regiao, Data, Estado, CasosNovos, ObitosNovos])

for i in TabelaNova:
    dfdataset.append({"regiao": i[0], "Data": i[1], "Estado": i[2],
                     "Casos Novos": i[3], "Obitos Novos": i[4]})

Estado = []
Data1 = []
CasosAcumulados = []
ObitosAcumulados = []
tablewhile = []
whiledataset = []

i = 0
tamanholista = len(tabela)
while i < tamanholista:
    row = tabela[i]
    Estado = row[1]
    Data1 = row[2]
    CasosAcumulados = row[4]
    ObitosAcumulados = row[6]

    if not row[2] == '':
        # if Estado == 'São Paulo' or Estado == 'Rio de Janeiro' or Estado == 'Espírito Santo' or Estado == 'Minas Gerais':
        if row[4] >= 1:
            tablewhile.append(
                [Data1, Estado, CasosAcumulados, ObitosAcumulados])
    i += 1

i = 0
tamanho = len(tablewhile)
while i < tamanho:
    whiledataset.append({"Data1": tablewhile[i][0], "Estado": tablewhile[i][1],
                        "Casos Acumulados": tablewhile[i][2], "Obitos Acumulados": tablewhile[i][3]})
    i += 1

opcoes = ('Obitos Acumulados por Região', 'Casos Acumulados por Região', 'Casos Novos por Estado',
          'Casos Acumulados por Estado', 'Obitos Novos por Estado', 'Obitos Acumulados por Estado')

opcoes1 = ('Sudeste', 'Sul', 'Centro-Oeste', 'Norte', 'Nordeste')

app.layout = html.Div(children=[
    html.H1(children='Coronavírus (COVID-19) no Brasil.'),
    html.H2(children='''
        Gráficos sobre COVID-19 no Brasil entre Janeiro e Abril.
    '''),
    html.H3(children='''
        Escolha o Gráfico referente ao dado desejado.
    '''),
    html.Div([
        dcc.Dropdown(opcoes, value='NYC', id='Grafico-1', style={
                     'width': '50%', 'display': 'inline-block'}),
        dcc.Graph(
            id='graph1'
        ),
        html.Div([
            html.H2(children='Casos Acumulados de COVID19 no Brasil por Região'),
            html.H3(children='Escolha qual região deseja ver os dados'),
            dcc.Dropdown(opcoes1, value='NYC', id='Grafico-2', style={
                'width': '50%', 'display': 'inline-block'}),
            dcc.Graph(
                id='graph2'
            ),
            html.Div([
                html.H2(
                    children='Óbitos Acumulados de COVID19 no Brasil por Região'),
                html.H3(children='Escolha qual região deseja ver os dados'),
                dcc.Dropdown(opcoes1, value='NYC', id='Grafico-3', style={
                    'width': '50%', 'display': 'inline-block'}),
                dcc.Graph(
                    id='graph3'
                ),
            ])
        ])
    ]),
])

# CALLBACKS FIRST DROPDOWN

@ app.callback(
    Output('graph1', 'figure'),
    Input('Grafico-1', 'value'),
)
def update_output(value):
    if value == 'Obitos Acumulados por Região':
        fig = px.pie(piedataset1, names='Regiao', values='Obitos Novos', title="GRAFICO ESCOLHIDO",
                     color_discrete_sequence=px.colors.sequential.RdBu)
        fig.update_traces(textposition='inside', textinfo='percent+label')

    if value == 'Casos Acumulados por Região':
        fig = px.pie(piedataset, names='Region', values='Casos Novos', title="GRAFICO ESCOLHIDO",
                     color_discrete_sequence=px.colors.sequential.RdBu)
        fig.update_traces(textposition='inside', textinfo='percent+label')

    if value == 'Casos Novos por Estado':
        fig = px.line(dfdataset, x='Data', y='Casos Novos', color='Estado',
                      markers=True, title="GRAFICO ESCOLHIDO")
        fig.update_yaxes(title='Quantidade de Casos Novos',
                         title_font_color='red', ticks='outside', tickfont_color='green')
        fig.update_xaxes(title_text='Dias do ano', title_font_color='red',
                         ticks='outside', tickfont_color='green')

    if value == 'Casos Acumulados por Estado':
        fig = px.line(whiledataset, x='Data1', y='Casos Acumulados', color='Estado',
                      markers=True, title="GRAFICO ESCOLHIDO")
        fig.update_yaxes(title='Quantidade de Casos Acumulados',
                         title_font_color='red', ticks='outside', tickfont_color='green')
        fig.update_xaxes(title_text='Dias do ano', title_font_color='red',
                         ticks='outside', tickfont_color='green')

    if value == 'Obitos Novos por Estado':
        fig = px.line(dfdataset, x='Data', y='Obitos Novos', color='Estado',
                      markers=True, title="GRAFICO ESCOLHIDO")
        fig.update_yaxes(title='Quantidade de Obitos Novos',
                         title_font_color='red', ticks='outside', tickfont_color='green')
        fig.update_xaxes(title_text='Dias do ano', title_font_color='red',
                         ticks='outside', tickfont_color='green')

    if value == 'Obitos Acumulados por Estado':
        fig = px.line(whiledataset, x='Data1', y='Obitos Acumulados', color='Estado',
                      markers=True, title='Grafico Escolhido')
        fig.update_yaxes(title='Quantidade de Obitos Acumulados',
                         title_font_color='red', ticks='outside', tickfont_color='green')
        fig.update_xaxes(title_text='Dias do ano', title_font_color='red',
                         ticks='outside', tickfont_color='green')

    return fig

Estado = []
Data1 = []
CasosAcumulados = []
ObitosAcumulados = []
tableSudeste = []
tableSul = []
tableNorte = []
tableNordeste = []
tableCentrooeste = []

# i = 0
# tamanholista = len(tabela)
# while i < tamanholista:
# row = tabela[i]

for row in tabela:
    Estado = row[1]
    Data1 = row[2]
    CasosAcumulados = row[4]
    ObitosAcumulados = row[6]
    if not row[2] == '':
        if Estado == 'São Paulo' or Estado == 'Rio de Janeiro' or Estado == 'Espírito Santo' or Estado == 'Minas Gerais':
            if row[4] >= 1:
                tableSudeste.append(
                    [Data1, Estado, CasosAcumulados, ObitosAcumulados])
            whiledatasetSudeste = []
            for i in tableSudeste:
                whiledatasetSudeste.append({"Data Sudeste": i[0], "Estados Sudeste": i[1],
                                            "Casos Acumulados Sudeste": i[2], "Obitos Acumulados Sudeste": i[3]})

        elif Estado == 'Distrito Federal' or Estado == 'Mato Grosso do Norte' or Estado == 'Mato Grosso do Sul' or Estado == 'Goiás':
            if row[4] >= 1:
                tableCentrooeste.append(
                    [Data1, Estado, CasosAcumulados, ObitosAcumulados])
            whiledatasetCentrooeste = []
            for i in tableCentrooeste:
                whiledatasetCentrooeste.append({"Data Centro Oeste": i[0], "Estados Centro Oeste": i[1],
                                                "Casos Acumulados Centro Oeste": i[2], "Obitos Acumulados Centro Oeste": i[3]})
        elif Estado == 'Amazonas' or Estado == 'Acre' or Estado == 'Roraima' or Estado == 'Pará' or Estado == 'Rondônia' or Estado == 'Amapá' or Estado == 'Tocantins':
            if row[4] >= 1:
                tableNorte.append(
                    [Data1, Estado, CasosAcumulados, ObitosAcumulados])
            whiledatasetNorte = []
            for i in tableNorte:
                whiledatasetNorte.append({"Data Norte": i[0], "Estados Norte": i[1],
                                          "Casos Acumulados Norte": i[2], "Obitos Acumulados Norte": i[3]})
        elif Estado == 'Bahia' or Estado == 'Ceará' or Estado == 'Maranhão' or Estado == 'Paraíba' or Estado == 'Pernambuco' or Estado == 'Piauí' or Estado == 'Sergipe' or Estado == 'Rio Grande do Norte':
            if row[4] >= 1:
                tableNordeste.append(
                    [Data1, Estado, CasosAcumulados, ObitosAcumulados])
            whiledatasetNordeste = []
            for i in tableNordeste:
                whiledatasetNordeste.append({"Data Nordeste": i[0], "Estados Nordeste": i[1],
                                             "Casos Acumulados Nordeste": i[2], "Obitos Acumulados Nordeste": i[3]})
        elif Estado == 'Rio Grande do Sul' or Estado == 'Paraná' or Estado == 'Santa Catarina':
            if row[4] >= 1:
                tableSul.append(
                    [Data1, Estado, CasosAcumulados, ObitosAcumulados])
            whiledatasetSul = []
            for i in tableSul:
                whiledatasetSul.append({"Data Sul": i[0], "Estados Sul": i[1],
                                        "Casos Acumulados Sul": i[2], "Obitos Acumulados Sul": i[3]})

# CALLBACKS SECOND DROPDOWN

@app.callback(
    Output('graph2', 'figure'),
    Input('Grafico-2', 'value'),
)
def update_output(value):
    if value == 'Sudeste':
        fig = px.line(whiledatasetSudeste, x='Data Sudeste', y='Casos Acumulados Sudeste', color='Estados Sudeste',
                      markers=True, title="Casos Acumulados de Covid19 no Brasil por Região Desejada")
        fig.update_yaxes(title='Quantidade de Casos Acumulados',
                         title_font_color='red', ticks='outside', tickfont_color='green')
        fig.update_xaxes(title_text='Dias do ano', title_font_color='red',
                         ticks='outside', tickfont_color='green')

    elif value == 'Sul':
        fig = px.line(whiledatasetSul, x='Data Sul', y='Casos Acumulados Sul', color='Estados Sul',
                      markers=True, title="Casos Acumulados de Covid19 Brasil por Região Desejada")
        fig.update_yaxes(title='Quantidade de Casos Acumulados',
                         title_font_color='red', ticks='outside', tickfont_color='green')
        fig.update_xaxes(title_text='Dias do ano', title_font_color='red',
                         ticks='outside', tickfont_color='green')

    elif value == 'Norte':
        fig = px.line(whiledatasetNorte, x='Data Norte', y='Casos Acumulados Norte', color='Estados Norte',
                      markers=True, title="Casos Acumulados de Covid19 no Brasil por Região Desejada")
        fig.update_yaxes(title='Quantidade de Casos Acumulados',
                         title_font_color='red', ticks='outside', tickfont_color='green')
        fig.update_xaxes(title_text='Dias do ano', title_font_color='red',
                         ticks='outside', tickfont_color='green')

    elif value == 'Nordeste':
        fig = px.line(whiledatasetNordeste, x='Data Nordeste', y='Casos Acumulados Nordeste', color='Estados Nordeste',
                      markers=True, title="Casos Acumulados de Covid19 no Brasil por Região Desejada")
        fig.update_yaxes(title='Quantidade de Casos Acumulados',
                         title_font_color='red', ticks='outside', tickfont_color='green')
        fig.update_xaxes(title_text='Dias do ano', title_font_color='red',
                         ticks='outside', tickfont_color='green')

    elif value == 'Centro-Oeste':
        fig = px.line(whiledatasetCentrooeste, x='Data Centro Oeste', y='Casos Acumulados Centro Oeste', color='Estados Centro Oeste',
                      markers=True, title="Casos Acumulados de Covid19 no Brasil por Região Desejada")
        fig.update_yaxes(title='Quantidade de Casos Acumulados',
                         title_font_color='red', ticks='outside', tickfont_color='green')
        fig.update_xaxes(title_text='Dias do ano', title_font_color='red',
                         ticks='outside', tickfont_color='green')

    return fig

# CALLBACKS THIRD DROPDOWN

@app.callback(
    Output('graph3', 'figure'),
    Input('Grafico-3', 'value'),
)
def update_output(value):
    if value == 'Sudeste':
        fig = px.line(whiledatasetSudeste, x='Data Sudeste', y='Obitos Acumulados Sudeste', color='Estados Sudeste',
                      markers=True, title="Óbitos Acumulados de Covid19 no Brasil por Região Desejada")
        fig.update_yaxes(title='Quantidade de Óbitos Acumulados',
                         title_font_color='red', ticks='outside', tickfont_color='green')
        fig.update_xaxes(title_text='Dias do ano', title_font_color='red',
                         ticks='outside', tickfont_color='green')

    elif value == 'Sul':
        fig = px.line(whiledatasetSul, x='Data Sul', y='Obitos Acumulados Sul', color='Estados Sul',
                      markers=True, title="Óbitos Acumulados de Covid19 no Brasil por Região Desejada")
        fig.update_yaxes(title='Quantidade de Óbitos Acumulados',
                         title_font_color='red', ticks='outside', tickfont_color='green')
        fig.update_xaxes(title_text='Dias do ano', title_font_color='red',
                         ticks='outside', tickfont_color='green')

    elif value == 'Norte':
        fig = px.line(whiledatasetNorte, x='Data Norte', y='Obitos Acumulados Norte', color='Estados Norte',
                      markers=True, title="Óbitos Acumulados de Covid19 no Brasil por Região Desejada")
        fig.update_yaxes(title='Quantidade de Óbitos Acumulados',
                         title_font_color='red', ticks='outside', tickfont_color='green')
        fig.update_xaxes(title_text='Dias do ano', title_font_color='red',
                         ticks='outside', tickfont_color='green')

    elif value == 'Nordeste':
        fig = px.line(whiledatasetNordeste, x='Data Nordeste', y='Obitos Acumulados Nordeste', color='Estados Nordeste',
                      markers=True, title="Óbitos Acumulados de Covid19 no Brasil por Região Desejada")
        fig.update_yaxes(title='Quantidade de Óbitos Acumulados',
                         title_font_color='red', ticks='outside', tickfont_color='green')
        fig.update_xaxes(title_text='Dias do ano', title_font_color='red',
                         ticks='outside', tickfont_color='green')

    elif value == 'Centro-Oeste':
        fig = px.line(whiledatasetCentrooeste, x='Data Centro Oeste', y='Obitos Acumulados Centro Oeste', color='Estados Centro Oeste',
                      markers=True, title="Óbitos Acumulados de Covid19 no Brasil por Região Desejada")
        fig.update_yaxes(title='Quantidade de Óbitos Acumulados',
                         title_font_color='red', ticks='outside', tickfont_color='green')
        fig.update_xaxes(title_text='Dias do ano', title_font_color='red',
                         ticks='outside', tickfont_color='green')

    return fig

if __name__ == '__main__':
    app.run_server(debug=True)
