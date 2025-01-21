# Projeto de Python com IA

## Conceito:
Esse projeto se baseia em uma situação-problema apresentada por um banco que consiste em apontar o score de crédito dos seus clientes de forma automática. Para resolver essa questão, foi criada uma IA que será capaz de prever a nota de crédito dos clientes como Boa, Ok ou Ruim, solucionando, dessa forma, o problema do banco fictício com mais de 80% de precisão, baseada nas características dos clientes. Essa IA será treinada utilizando uma base de dados que conta com 100.000 clientes que já possuem o score de crédito.

## Funcionalidades
- Classificar os clientes;

## Tecnologias Utilizadas

- [Python 3.12.7](https://www.python.org)

## Bibliotecas Utilizadas

- [Pandas 2.2.3](https://pandas.pydata.org)
- [Scikit-learn 1.6.1](https://scikit-learn.org/stable/index.html)

## Explicando detalhadamente o código:

### Passo 1:
Foi realizada a importação da base de dados através da biblioteca pandas.
Essa base de dados foi atribuída a uma variável.

### Passo 2:
Com o comando `display()`, foram visualizados os dados presentes na tabela de clientes. Além disso, foi feita a análise das possíveis colunas que poderiam ser retiradas, visando otimizar o treinamento da IA.

Após a análise, foram retiradas as colunas "id_cliente" e "mes", tendo em vista que esses dados não implicam no score de crédito.

Em seguida, foram visualizadas as informações da tabela, buscando valores ausentes e observando o tipo dos dados que foram passados:
- No caso, não há valores ausentes.

As colunas que apresentam dados do tipo "object" devem ser substituídas por "int", uma vez que os modelos de classificação não conseguem trabalhar com textos. O nome desse processo de substituição do tipo de informação é **LabelEncoder**. Dessa forma, através da biblioteca scikit-learn (sklearn), podemos realizar essa troca do tipo de dados de forma automática.
- Para realizar esse processo de **LabelEncoder**, você deve criar um codificador para cada coluna que será alterada. Posteriormente, deve aplicar esse codificador à coluna, e com isso ela será codificada. Vale ressaltar que, no caso atual, a coluna "score_credito" deve permanecer com o tipo "object", pois é a coluna que vamos prever.

### Passo 3:
Divisão dos dados entre X (dados que serão usados para prever o resultado) e Y (dado a ser previsto). Essa divisão é feita manualmente, e o programador deve apontar as colunas.

- Y -> a coluna "score_credito".
- X -> todas as outras colunas, exceto a coluna de Y.

Depois de separar X e Y, devemos, de forma automática e aleatória, dividir a base de dados entre treino e teste, para posteriormente utilizar com a IA. Isso é feito através de uma função presente na biblioteca sklearn - train_test_split. Para essa função, são passadas em sequência as 4 variáveis que vão receber os valores de treino e teste:

- x_treino, x_teste, y_treino, y_teste -> exatamente nessa ordem.
- Nessa função, também pode ser passado o parâmetro test_size, que determina a porcentagem de dados para teste e treino.

### Passo 4:
A criação de uma IA se divide em 3 etapas:

1. Importar a IA.
2. Criar a IA.
3. Treinar a IA.

É recomendado criar pelo menos 2 IAs para avaliar qual é a melhor diante do problema apresentado.

No caso, foram importadas as IAs RandomForest (Árvore de Decisão) e NearestNeighbors (Vizinhos Próximos), ambas presentes na biblioteca scikit-learn. Para criar, basta atribuir uma variável à função.

Após a criação, é necessário treinar e testar as IAs. Para isso, basta passar os modelos criados com o método `.fit()` juntamente com os X e Y de treino como parâmetros.

Esse processo pode demorar um pouco mais, pois depende do tamanho do treinamento que está sendo realizado com as IAs.

### Passo 5:
Nesta etapa, para escolher qual é a melhor IA para a resolução do problema, devemos observar a previsão de cada IA e, posteriormente, medir sua acurácia.

A previsão é atribuída a uma nova variável e, em seguida, a IA é utilizada com o método `.predict()` juntamente com o x_teste como parâmetro. A partir disso, a IA devolve os valores de Y, que são posteriormente comparados com o y_teste para avaliar se a IA está acertando ou não em suas previsões.

Obtendo as previsões, calcula-se a acurácia de cada IA. Para isso, importa-se o accuracy_score (que recebe como parâmetro o y_teste e as previsões da IA), responsável por comparar as previsões realizadas pela IA com o gabarito real. Isso retorna a porcentagem de acerto.

Visualizando a acurácia, identifica-se qual IA melhor se adaptou ao problema, definindo, assim, qual será utilizada.

### Passo 6:
Com a IA definida, agora vamos resolver o problema aplicando-a na nova base de dados com os novos clientes que não possuem o **score_credito** definido.

Antes disso, devemos realizar novamente o tratamento da nova tabela para que ela seja o mais similar possível à tabela em que a IA foi treinada. Para isso, realiza-se o processo de LabelEncoder novamente, substituindo os dados textuais por números. Caso haja alguma coluna a mais, ela deve ser excluída.

Nesse reuso do LabelEncoder, basta copiar o mesmo código usado anteriormente. Não é necessário criar um codificador novo, basta apenas trocar a tabela mencionada e substituir o método fit_transform por transform, uma vez que:
- `fit_transform()` -> Aprende o mapeamento das categorias únicas para os valores numéricos e converte os valores categóricos com base no mapeamento aprendido.
- `transform()` -> Após o codificador já ter sido treinado com `fit_transform()`, aplica o mapeamento aprendido a um novo conjunto de dados.

## Resultado:

Com isso, o objetivo de classificar o score do cliente foi alcançado com uma acurácia de 83%. Dessa forma, a empresa já consegue prever com boa acurácia o score dos clientes, o que permite tomar decisões de forma mais eficiente.

Além disso, foi possível definir quais pontos mais impactam na classificação do score do cliente. Com isso, o banco pode planejar medidas que visem minimizar o número de clientes com o score "Poor".

## Licença:

Este projeto está licenciado sob a licença MIT. Você é livre para usá-lo, modificá-lo e distribuí-lo, desde que inclua a licença original em todos os arquivos redistribuídos.