# Apache Airflow with Python

![image](https://user-images.githubusercontent.com/69597971/200195293-edfac1eb-5099-4fdd-99e7-2337d07ce31f.png)

# O que é Airflow?

O `Apache Airflow` é uma plataforma de código aberto para desenvolvimento (criar), agendamento e monitoramento de fluxos de trabalho de forma programática.

Quando os fluxos de trabalho são definidos como código, eles se tornam mais fáceis de manter, versáteis, testáveis e colaborativos.

A estrutura `Python` extensível do Airflow permite que você crie fluxos de trabalho conectando-se a praticamente qualquer tecnologia. Uma interface da Web ajuda a gerenciar o estado de seus fluxos de trabalho. O `Airflow` pode ser implantado de várias maneiras, variando de um único processo em seu laptop a uma configuração distribuída para oferecer suporte até mesmo aos maiores fluxos de trabalho.

O Airflow é usado para criar fluxos de trabalho como `Gráficos Acíclicos Direcionados` (`DAGs`) de tarefas. O scheduler (agendador) do Airflow executa suas tarefas em uma matriz de trabalhadores (workers) enquanto segue as dependências especificadas. A rica interface do usuário facilita a visualização de pipelines em execução na produção, o monitoramento do progresso e a solução de problemas quando necessário.


# Fluxos de trabalho (Workflows) como código

A principal característica dos fluxos de trabalho do Airflow é que todos os fluxos de trabalho são definidos em código `Python`. “Fluxos de trabalho como código” serve a vários propósitos:

* `Dinâmico`: os pipelines de Airflow são configurados como código Python, permitindo a geração dinâmica de pipeline.

* `Extensível`: o framework do Airflow contém operadores para conectar-se a várias tecnologias. Todos os componentes do Airflow são extensíveis para se ajustarem facilmente ao seu ambiente.

* `Flexível`: a parametrização do **fluxo de trabalho** é incorporada, aproveitando o mecanismo de modelagem [Jinja](https://jinja.palletsprojects.com/en/3.1.x/).


A seguir mostramos um exemplo de um trecho de código:

![image](https://user-images.githubusercontent.com/69597971/200350653-75962f6f-806c-4033-9733-379d72797107.png)


Nesse trecho de código (acima) observamos o seguinte:

* O `DAG` chamado "demo", começando em 1º de janeiro de 2022 e sendo executado uma vez por dia. Um `DAG` é a representação do Airflow de um fluxo de trabalho

* Duas tarefas, um `BashOperator` executando um script Bash e uma função Python definida usando o decorador `@task`

* `>>` entre as tarefas define uma dependência e controla em qual ordem as tarefas serão executadas

O Airflow avalia esse script e executa as tarefas no intervalo definido e na ordem definida. A seguir vamos a entender mais um pouco sobre DAGs: 


# O que é um DAG?

`DAG` é uma abreviação para `Directed Acyclic Graphs` - Grafos Acíclicos Dirigidos em tradução livre. A seguir vamos entender o que significa cada um desses termos:

* Grafo é uma ferramenta matemática com nós e arestas responsáveis por conectar esses nós.

* Dirigidos quer nos dizer que o fluxo de trabalho se dá apenas em uma direção.

* Acíclico significa que a execução não entrará em um laço de repetição, então eventualmente acabaremos em um nó final que não estará conectado com o nó inicial.


Lembra que ma task é a unidade mais básica de um DAG a qual é responsável por implementar determinada lógica no pipeline.


# Principais conceitos no Airflow

## Webserver

É o responsável por oferecer a interface de usuário do Airflow que torna possível visualizar de forma geral o estado dos DAGs, códigos que estão presentes nesses DAGs, estados de execução, logs de erro, entre outras funcionalidades. Também permite gerenciar usuários, funções e diversas configurações do Airflow.














Links de estudo:

* [Apache Airflow](https://airflow.apache.org/docs/apache-airflow/stable/index.html)

* [Airflow - Entendendo os DAGs](https://www.alura.com.br/artigos/airflow-entendendo-dags#:~:text=A%20principal%20ideia%20do%20Airflow,tasks%20juntas%20formam%20um%20DAG.)

* [https://github.com/apache/airflow](https://github.com/apache/airflow)



Thanks God!
