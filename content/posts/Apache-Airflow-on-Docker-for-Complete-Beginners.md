
---
    title: Apache-Airflow-on-Docker-for-Complete-Beginners
    date: 2021-01-01    
    draft: true
    tags: []
---
# Apache-Airflow-on-Docker-for-Complete-BeginnersBut over time, OLAP usually starts to become too burdensome to run on your production tables:
- OLAP queries are more computationally expensive (aggregations, joins)
- OLAP often requires intermediate steps like data cleaning and featurization
- Analytics usually runs at regular time intervals, while OLTP is usually event based (e.g. a user does something, so we hit the database)
For these reasons and more, Bill Inmon, Barry Devlin, and Paul Murphy [developed the concept of a Data Warehouse in the 1980’s](https://en.m.wikipedia.org/wiki/Data_warehouse#History).
Some of the major issues that data teams face scheduling ETL jobs with Cron:
- ETL jobs fail *all the time* for *a million reasons*, and Cron makes it *very* difficult to debug for a number of reasons
- ETL tends to have a lot of dependencies (on past jobs, for example) and Cron isn’t built to account for that
- Data is getting larger, and modern distributed data stacks (HDFS, Hive, Presto) don’t always work well with Cron
Unsurprisingly, [data teams have been trying to find more sophisticated ways](https://medium.com/videoamp/what-we-learned-migrating-off-cron-to-airflow-b391841a0da4) to schedule and run ETL jobs.
Airflow lets you:
- Design complex, sophisticated ETL jobs with multiple layers of dependencies
- Schedule jobs to run at any time and wait for their dependencies to finish, with the option to run distributed workloads (using [Celery](http://www.celeryproject.org/))
- Monitor all of your jobs, know exactly where and when they failed, and get detailed logs on what the errors were
It’s important to note that **Airflow is not an ETL tool**, even though that happens to be what it’s used most for.
Some really clutch features that you might find yourself using:
- Seeing the structure of your DAG in a graph format
- Checking on all of your DAG runs and seeing when they failed
- Adding and editing Connections
- Looking at how long your tasks typically take in one of your DAGs
The Webserver definitely gives Cron a run for its money, and is probably the most compelling feature Airflow has to offer over Cron for beginners.
It also tells the container to immediately run `airflow initdb`, `airflow webserver`, and `airflow scheduler`, so you don’t have to run those manually.
***2) Decide on how you want to deploy and test***
The typical structure for building the Airflow Docker Image, which is also how this repo is designed, is two fold:
- A bunch of local files exist that are your “source of truth”
- When Docker Images are built, all of the local data and files are copied over to containers
What this *means* that you’d make edits to any local files like `script/entrypoint.sh` or `config/airflow.cfg`, and then build your image.
Here’s the way that `puckel/docker-airflow` does it:
- The Fernet Key is generated with a Python command and exported as an environment variable in `entrypoint.sh`
- In the `airflow.cfg` file, the `fernet_key` parameter is set to `$FERNET_KEY`, which is the name of the environment variable exported above
There’s an [open issue](https://github.com/puckel/docker-airflow/issues/290) (created by yours truly) with this process, though: if you build your Docker Image through plain old Docker Build and Docker Run commands, it doesn’t work.
