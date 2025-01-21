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
Foi realizada a importação da base de dados atraves da biblioteca pandas.
Essa base de dados foi atribuida a uma variável.

### Passo 2:
Com o comando display foi visualizado os dados presente na tabela de clientes, bem como, foi feita a análise das possíveis colunas que poderiam ser retiradas visando otimizar o treinamento da IA.

Após analise foi retirado as colunas "id_cliente" e "mes", tendo em vista que esses dados não implicam no score de crédito.

Em seguida foi visualizado as informações da tabela, buscando valores ausentes e observando o tipo dos dados que foram passados.
- No caso, não possui valores ausentes;

As colunas que apresentam dados do tipo "object" devem ser substituidas por int, uma vez que, os modelos de classificação não conseguem trabalhar com textos, o nome desse processo de substituição do tipo de informação é LabelEnconder. Dessa forma, através da biblioteca scikit_learn (sklearn) podemos realizar essa troca do tipo de dados de forma automática.
- Para realizar esse processo de LabelEnconder você deve criar um codificador para cada coluna que será alterada, posterior a esse processo você deve aplicar esse codificador na coluna e com isso a coluna será codificada. Vale ressaltar que no caso atual a coluna "score_credito" deve permanecer com o tipo "object", pois é a coluna que vamos prever. 

### Passo 3:
Divisão dos dados entre X: aqueles dados que serão usados para prevê o resultado e Y: que é o dado a ser previsto. Essa divisão é feita manualmente, o programador deve apontar as colunas. 
- Y -> a coluna "score_credito"
- X -> todas as outras colunas, tirando a coluna do Y 

Depois de separa o X e Y devemos agora de forma automática e aleatória dividir a base de dados entre treino e teste para posteriormente utilizar com a IA. Isso é feito através de uma função presente na biblioteca do sklearn - train_test_split. Para essa função é passada em sequência as 4 variáveis que vão receber os valores de treino e teste
- x_treino, x_test, y_treino, y_test -> exatamente nessa ordem
- Nessa função pode ser passado também como parâmetro o test_size que vai determinar a porcentagem de teste e treino.

### Passo 4:
A criação de uma IA se divide em 3 etapas:
- Importar a IA;
- Criar a IA;
- Treinar a IA.

É recomendado a criação de pelo menos 2 IA para que se saiba qual a melhor diante do problema apresentado

No caso foi importando a IA RandomForest (Árvore de decisão) e a IA NearestNeighbors (Vizinhos proxímos) ambas presentes na biblioteca scikit-learn. Para criar basta atribuir uma variável a função. 

Após criado é necessário treinar e testar as IA. Para isso bastar passar os modelos criados com o método .fit() juntamente com os X e Y de treino como parâmetro.

Esse processo demora um pouco mais pois depende do tamanho do treinamento que está acontecendo com as IAs.

### Passo 5:
Nessa etapa de escolher qual a melhor IA para resolução do problema devemos observar a previsão de cada IA e posteriomente medir a sua acurácia. A previsão é atribuida a uma nova variável e é passada a IA com o método .predict() juntamente com o x_teste como parâmetro, a partir disso a IA deve devolver o valor de Y que posteriormente será comparado com o y_teste para saber se a IA está acertando ou não em suas previsões. 

Obtendo as previsões vamos calcular a acurácia de cada IA, para isso devemos importar o accuracy_score(recebe como parâmetro o y_teste e as previsões da IA) que vai ser responsável por comparar as previsões realizadas pela IA com o real gabarito. Isso vai retornar a porcentagem de acerto. 

Visualizando a acurácia sabe-se qual a IA que melhor se adaptou ao problema definido assim qual será utilizada.

### Passo 6:
Com a IA definida agora vamos resolver o problema aplicando-a na nova base de dados com os novos clientes que não possuem o score_credito definido.

Antes disso, devemos realizar novamente o tratamento da tabela nova para que ela seja o mais igual a tabela em que a IA foi treinada para isso foi realizado o processo de LabelEnconder para substituir novamente os dados escrito por números e caso tivesse alguma coluna a mais deveria ser excluida. 
- Nesse reuso do LabelEnconder basta copiar o mesmo código que foi usado anteriormente, não precisa criar um códificador novo basta apenas trocar a tabela mencionada e o método fit_transform por transform, uma vez que, o método fit_transform -> Aprende o mapeamento das categorias únicas para os valores numéricos e converte os valores categóricos com base no mapeamento aprendido. Já o transform -> é usado após o codificador já ter sido treinado com fit_transform ele aplica o mapeamento aprendido a um novo conjunto de dados.

## Resultado
Com isso, o objetivo de classificar o score do cliente foi alcançado com uma acurácia de 83%. Então a empresa já conseguiria prever com uma boa acurácia o score dos clientes e com isso pode fazer suas decisões de forma mais eficiente. 

Além disso, foi possível definir quais os pontos que mais impactam na classificação do score do cliente e a partir disso é possivel que o banco planeje medidas que objetivam minimizar os clientes com um score "Poor". 

## Licença

Este projeto está licenciado sob a licença MIT. Você é livre para usá-lo, modificá-lo e distribuí-lo, desde que inclua a licença original em todos os arquivos redistribuídos.
