
---
    title: Quick-guide-How-to-run-Apache-Airflow-with-docker
    date: 2021-01-01    
    draft: true
    tags: []
---
# Quick-guide-How-to-run-Apache-Airflow-with-dockerWe will create a docker-compose file with:
- airflow webserver
- airflow scheduler (with LocalExecutor)
- PostgreSQL DB (we will use it as DB for Airflow)
For **PostgreSQL**, we will use the official docker image: [https://hub.docker.com/_/postgres/](https://hub.docker.com/_/postgres/) version 9.6.14, for **Apache** **Airflow**: [https://hub.docker.com/r/puckel/docker-airflow/](https://hub.docker.com/r/puckel/docker-airflow/) version 1.10.6 (note: we will switch to use official docker image as soon as it will be released, now we can just check AIP and wait, or participate if you can and want in process of creation).
At the start, for quick development we will use one DAG folder that we will share between airflow scheduler and airflow webserver, so you will not need to rebuild and re-run server each time when you want to add dags.
1.3 Next, create a file with name **Dockerfile** (this is a default name for docker files to build images, let use it)
**In Dockerfile:**
```
FROM/RUN--ENVAIRFLOW_HOME///COPY/////
```
Short description: **FROM** — define a base image that we use to create our image, **ENV** — define environment variables in an image, **COPY** — copy file from the local path to an image, **RUN** — run command.
So, if you will put a file in main_folder/airflow/dags (**‘.’** — mean current work dir **where docker-compose.yaml is placed,** so this is **main_folder**) it will be shown in Airflow images in /usr/local/airflow/dags, so Airflow webserver and Airflow Scheduler will see it.
This will be enough for this tutorial, but…
If you don’t want to do it with way, you can spend a little time and create a .sh script to put in docker-compose airflow services wait till DB will not create, that is this you can see, for example, here: [https://github.com/vishnubob/wait-for-it](https://github.com/vishnubob/wait-for-it) but of course you need to modify sh to check is DB available to use or not.
**3.1 Let’s run:**
```
main_folderdocker-compose up postgres
```
3.1.1 after that in another terminal window run initdb (we need it only once if we clean up DB and start all from scratch)
```
docker-compose up initdb
```
3.2 After that run **in another terminal window:**
```
docker-compose up scheduler webserver
```
As you see postgres, schedule and webserver — names of our services, that we defined in docker-compose.yml
On next runs you can simply use (don’t forget to comment initdb service in docker-compose.yml):
```
docker-compose up
```
3.3 Now enter a UI to check at **[http://localhost:8080](http://localhost:8080/)**, that all run successfully.
4.1 Take it here (you need the whole file as a DAG):
And copy it in your dags folder, that was defined in the **volumes section of docker-compose file**
So, you got a structure of the main folder:
```
…/main_folder — airflow.cfg — Dockerfile - docker-compose.yml airflow_files/ dags/ - example_bash_operator.py
```
4.2 Wait for 10–15 sec and check the UI, refresh it and wait for more if it still empty.
