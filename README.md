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

É o responsável por oferecer a `interface de usuário do Airflow` que torna possível visualizar de forma geral o estado dos DAGs, códigos que estão presentes nesses DAGs, estados de execução, logs de erro, entre outras funcionalidades. Também permite gerenciar usuários, funções e diversas configurações do Airflow.


## Metadata Database

O `Airflow` possui suporte para uma grande variedade de bancos de dados. É nesses bancos de dados que estão todas as informações a respeito dos DAGs, suas configurações, além de todas as configurações internas do Airflow, como os usuários e seus níveis de acesso. Ao realizarmos qualquer modificação no `Webserver` essas modificações são atualizadas no banco de dados de metadados (`Metadata Database`) pelo Scheduler (Agendador).


## Scheduler

O `Scheduler` (agendador) é responsável por assegurar que as `tasks` dentro de um `DAG` sejam executadas no momento adequado. Em outras palavras, o scheduler é um processo que cuida do agendamento dos fluxos de trabalho e faz o envio das tasks para o executor, seguindo as etapas:

* Faz a leitura dos arquivos DAG criado pelo usuário, extrai as informações e as coloca no banco de dados;

* Determina quais tarefas serão executadas e as coloca no estado enfileirado para executar na ordem correta; e

* Busca e executa as tarefas que estão no estado enfileirado.


## Executor

Executor é o mecanismo que trata do modo de execução das tasks. O Airflow permite apenas um executor configurado por vez e inicialmente ele é definido no momento da instalação. Existem dois tipos de executores, os que executam as tarefas localmente e os que fazem isso de forma remota. Abaixo estão alguns executores locais e remotos:

* Executores locais:

    * [Sequential Executor](https://airflow.apache.org/docs/apache-airflow/stable/executor/sequential.html)

    * [Local Executor](https://airflow.apache.org/docs/apache-airflow/stable/executor/local.html)

* Executores remotos:

    * [Celery Executor](https://airflow.apache.org/docs/apache-airflow/stable/executor/celery.html)

    * [Kubernetes Executor](https://airflow.apache.org/docs/apache-airflow/stable/executor/kubernetes.html)

    * [CeleryKubernetes Executor](https://airflow.apache.org/docs/apache-airflow/stable/executor/celery_kubernetes.html)


## Operator

`Operator` é o componente que determina qual ferramenta será utilizada para executar as tasks. As tasks podem utilizar diferentes tecnologias, `por exemplo`, poderíamos primeiro rodar um `script Bash` na primeira task, a segunda poderia ser um `script em Python`, . . . etc. O `Airflow` fornece uma grande variedade de operadores. Para trabalhar com tasks escritas em Python utilizamos o `PythonOperator`. Já para trabalhar com scripts Bash será utilizado o `BashOperator`. Em trabalhos mais complexos poderemos utilizar o `DockerOperator` que irá executar um comando dentro de um container Docker e você pode ainda criar seu próprio operador.

![image](https://user-images.githubusercontent.com/69597971/200391317-b356a138-46d0-41bf-bdbb-15eac573e8c1.png)

Podemos dizer então que a principal função de um DAG é realizar a orquestração dos operadores definidos, e isso inclui iniciar e parar os operadores, iniciar o operador consecutivo à medida que o anterior tiver finalizado.


## DAG run

É a execução de fato do DAG, e isso inclui os horários, tempo de execução de cada uma das tasks, entre outras informações relevantes do DAG. Quando um DAG é executado, um DAG Run é criado e todas as tasks desse DAG são executadas. Um detalhe é que cada `DAG run` é executado de forma separada dos demais, isso significa que você pode executar o mesmo DAG diversas vezes ao mesmo tempo ou executar vários DAGs diferentes ao mesmo tempo.

Colocando tudo que foi falado anteriormente em ordem, temos uma noção mais ampla da arquitetura do Airflow e de como ele funciona em volta do conceito de DAG.

![image](https://user-images.githubusercontent.com/69597971/200392121-f5075faa-9559-4c20-b267-bc005ad1183c.png)



Links de estudo:

* [Apache Airflow](https://airflow.apache.org/docs/apache-airflow/stable/index.html)

* [Airflow - Entendendo os DAGs](https://www.alura.com.br/artigos/airflow-entendendo-dags#:~:text=A%20principal%20ideia%20do%20Airflow,tasks%20juntas%20formam%20um%20DAG.)

* [https://github.com/apache/airflow](https://github.com/apache/airflow)



Thanks God!
