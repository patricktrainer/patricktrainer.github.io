---
                title: How-to-start-automating-your-data-pipelines-with-A
                date: 2021-01-01    
                draft: true
                tags: []
               ---


            # How-to-start-automating-your-data-pipelines-with-A

[How%20to%20start%20automating%20your%20data%20pipelines%20with%20A%203357f45d3f42478594e6578a8c435e54/1xbaTpPkyt_Q5czvXTzZ0wQ.png](How%20to%20start%20automating%20your%20data%20pipelines%20with%20A%203357f45d3f42478594e6578a8c435e54/1xbaTpPkyt_Q5czvXTzZ0wQ.png)
The DAG that we are building using Airflow
In Airflow, Directed Acyclic Graphs (DAGs) are used to create the workflows.Defining a DAG enables the scheduler to know which tasks can be run immediately, and which have to wait for other tasks to complete.To ensure that Airflow knows all the DAGs and tasks that need to be run, there can only be one scheduler.Tasks are defined as “what to run?” and operators are “how to run”.## Importing various packages
```
# airflow relatedfrom airflow import DAGfrom airflow.operators.python_operator import PythonOperatorfrom airflow.operators.bash_operator import BashOperator# other packagesfrom datetime import datetimefrom datetime import timedelta
```
We import three classes, `DAG`, `BashOperator` and `PythonOperator` that will define our basic setup.## Defining our DAG, Tasks, and Operators
Let’s define all the tasks for our existing workflow.```
def source1_to_s3(): # code that writes our data from source 1 to s3def source2_to_hdfs(config, ds, **kwargs): # code that writes our data from source 2 to hdfs # ds: the date of run of the given task.