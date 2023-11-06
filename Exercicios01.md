#Visualização de dados Checkpoint para 30/10/23


#Realizar uma análise gráfica dos dados para verificar:
#Qual o ano de maior e menor número na contratação de funcionários? (Qual o ano com a maior e menor quantidade na contratação dos funcionários?)
#Como é o comportamento da distribuição na formação dos funcionários? (Pode-se usar o gráfico de colunas ou de pizza)
#Como é a distribuição da localidade dos funcionários? (Pode-se usar o gráfico de colunas ou de pizza)
#A idade dos funcionários, tem um comportamento próximo a uma distribuição normal? (Pode-se usar o histograma para verificação)
#Qual o gênero predominante? (Pode-se usar o gráfico de colunas ou de pizza)
#A quantidade de funcionários afastados dos projetos é relevante? (Pode-se usar o gráfico de colunas ou de pizza)
#Há uma diminuição no número de funcionários à medida que os anos de experiência aumentam? (técnica de groupby)
#Em relação a saída por um possível desgaste, como é o desejo dos funcionários? (vários gráficos podem ser inseridos para a conclusão da análise)
#Como é a distribuição dos funcionários em relação ao nível salarial? (vários gráficos podem ser inseridos para a conclusão da análise)
#A distribuição de idades entre os gêneros é uniforme e balanceada? (técnica de groupby)
#Como é a relação entre o nível salarial e o tempo de experiência? (dispersão)
#Como é a distribuição dos gêneros em relação as localidades? (mapa de calor)
#Verificar o nível de correlação das variáveis. (só para as variáveis numéricas)
#Faça uma análise comparando e relacionando os níveis salariais, as idades, gênero e tempo de experiência e elabore uma conclusão a respeito.

PARTE 1 

#Análise Exploratória dos Dados - Análise Univariada
##Separando os grupos LeaveOrNot

#NÃO SAÍRAM DA EMPRESA
df_0 = df.loc[df.LeaveOrNot == 0]

#SAÍRAM DA EMPRESA
df_1 = df.loc[df.LeaveOrNot == 1]

# CRIANDO FUNÇÃO PROBABILIDADE DE OCORRER UM EVENTO
def probab (A, E):
  resultado = (A / E)*100
  print('{:.2f}'.format(resultado))

# CRIANDO FUNÇÃO PROBABILIDADE DE NÃO OCORRER UM EVENTO
def probab_not (A, E):
  resultado = (1- (A / E))*100
  print('{:.2f}'.format(resultado))


# PROBABILIDADE DO FUNCIONÁRIO SAIR DA EMPRESA
p_sair = probab (len(df_1), len(df))

# PROBABILIDADE DO FUNCIONÁRIO NÃO SAIR DA EMPRESA
probab_not (len(df_1), len(df))


#Variável Education

#CONTAR QUANTOS VALORES ESTÃO DISPONÍVEIS NA COLUNA EDUCATION
df["Education"].value_counts()

#SEPARAR EM GRUPOS DE FORMAÇÃO
bachelors = df.loc[df.Education == 'Bachelors']
masters = df.loc[df.Education == 'Masters']
PHD = df.loc[df.Education == 'PHD']


#PROBABILIDADE FUNCIONARIO SER BACHAREL
p_bachelors = probab (len(bachelors), len(df))

#PROBABILIDADE FUNCIONARIO SER MESTRE
p_masters = probab (len(masters), len(df))

#PROBABILIDADE FUNCIONARIO SER PHD
p_PHD = probab (len(PHD), len(df))

#SEPARAR EM GRUPOS DE FORMAÇÃO QUE SAÍRAM DA EMPRESA
bachelors_1 = df_1.loc[df.Education == 'Bachelors']
masters_1 = df_1.loc[df.Education == 'Masters']
PHD_1 = df_1.loc[df.Education == 'PHD']


#CRIANDO UMA FUNÇÃO PARA PROBABILIDADE CONDICIONAL
def probab_cond (AB, B):
  resultado = (AB / B)*100
  print('{:.2f}'.format(resultado))


bachelors_1["Education"].value_counts()
#PROBABILIDADE FUNCIONARIO SER BACHAREL E SAIR DA EMPRESA
probab_cond(len(bachelors_1),len(df_1))

masters_1["Education"].value_counts()
#PROBABILIDADE FUNCIONARIO SER MESTRE E SAIR DA EMPRESA
probab_cond(len(masters_1),len(df_1))

#primeira conclusão: a probabilidade de saída de bacharéis (67.92) supera a saída de mestres e PHDs (28.40 + 3.68)