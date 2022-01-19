## Projeto Full Data Scientist

A empresa HR Analytics obteve um número considerável de colaboradores
que saíram da empresa e precisa de uma análise profunda para saber o
real motivo, com isso foram apresentadas as perguntas abaixo definidas
pela área de negócio para a equipe de dados:

- Quais fatores influênciam para um colaborador deixar a empresa?

- Como reter pessoas?

- Podemos nos antecipar e saber se um determinado colaborador vai
sair da empresa?

- Como diminuir o turnover?



# Ferramentas e tecnologias utilizadas:

- Powershell para criação do diretório local para armazenamento dos arquivos 
e controle no Docker via prompt de comando;

- Containers Docker para Banco de Dados MySQL, Minio para Data Lake e 
Airflow para orquestração dos dados;

- VSCode e Jupyter Notebook para Análises exploratórias e Machine Learning;

- Streamlit para app final de visualização do projeto.



### Passo a passo do projeto realizado:

## Docker
- Criação do Banco de Dados MySQL habilitando as portas "3306:3307", em seguida
instalação da extensão Database Client no VSCode para conexão com o Banco;
- Criação do Data Lake nas portas "9000:9001" com user e password;
- Criação do Airflow com download via prompt de comando nas portas 8080:8080.


## Apache Airflow
- Criação das variáveis de acesso para as conexões abaixo:
- IP, login e senha do Minio;
- IP, login e senha do BD MySQL.
- Endereço do Dump do BD com os registros dos dados para empresa;
- Habilitação das Dags para o processo ETL.


## Minio Data Lake
- Criação dos Buckets landing, processing e curate;
- No bucket landing, criamos a pasta performance-evaluation e inserimos o 
arquivo employee_performance_evaluation.json e a pasta working-hours para os
arquivos .xlsx.


## VSCode
- Utilizamos a extensão Database Client para conexão com o container MySQL e
importação do arquivo dump para acesso aos arquivos.


## Diretório local
- Criação da pasta airflow e dags para inseração dos arquivos .py para efetuar
a orquestração dos dados.


### Modelagem dos dados utilizando Jupyter
- import das bibliotecas pandas, datetime, glob e math para modelagem;
- import da biblioteca pymysql para conexão com o Banco de Dados;
- conexão com o Data Lake para o arquivo .JSON e conversão para .CSV;
- criação de uma query sql para trazer o total de projetos que cada colaborador participava;
- criação de dataframe com registro de horas trabalhadas, tempo de empresa, salários e número de acidentes de trabalho existentes;
- cálculo do valor médio de horas trabalhadas dos últimos 3 meses.


### Análise Exploratória utilizando Jupyter
- instalação do minio para conexão com o Data Lake "!pip install minio"; e uso do arquivo .PARQUET para análise;
- import das bibliotecas pandas, datetime, glob, seaborn, matplotlib, pyarrow e fastparquet;
- exclusão dos arquivos nulos e duplicados
- alteração de nomes na linha head para uma melhor definição sobre os dados;
- cálculo da tx de turnover;
- nível de satisfação, performace, horas trabalhadas e salários.


### Machine Learning utilziando Jupyter
- import das bibliotecas pandas, datetime, glob, numpy e matplotlib;
- utilização do arquivo .PARQUET;
- conversão de atributos categóricos em valores numéricos;
- separação dos conjuntos de dados para treinamento dos algoritmos e testes;
- os algoritmos foram treinados em árvore de decisão, regressão logística e floresta aleatória;
- instalação e visualização das bibliotecas Pycaret e Scikit-learn;
- definição do setup após os modelos e verificação dos resultados via web no Streamlit;
- transferência dos arquivos .CSV para o bucket "Curate" do Data Lake.


### Conclusão

 Com base nos dados acima verificamos que:

- O Banco de Dados tinha 14.998 registros de empregados com uma rotatividade de 24% de Turnover
e satisfação média dos empregados atuais é de 61% e dos que deixaram a empresa era de 49%;

- Os departamentos com maiores índices de Turnover era Suporte, Técnica e Vendas, onde os salarios
variavam entre baixo e médio;

- Os colaboradores que estavam envolvidos entre 2, 6 e 7 projetos deixavam a empresa;
