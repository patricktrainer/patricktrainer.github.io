---
                title: AirflowETL
                date: 2021-01-01    
                draft: true
                tags: []
               ---


            # AirflowETL

Airflow is a platform to schedule and monitor workflows and in this post I will show you how to use it to extract the daily weather in New York from the [OpenWeatherMap](https://openweathermap.org/api) API, convert the temperature to Celsius and load the data in a simple [PostgreSQL](https://www.postgresql.org/) database.Specifically I transform and load the following into the database,
- the city name
- the country name
- the latitude and longitude of the city
- the date the API call was made
- the humidity
- the pressure
- the minimum temperature of the day
- the maximum temperature of the day
- the current temperature
- a description of the weather
This script is stored in a file name `makeTable.py` and can be run using the command,
```
python makeTable.py
```
From the appropriate directory and ***before we set up our Airflow job*** .We can now install airflow with PostgreSQL using pip:
```
pip install airflow[postgres]
```
We then initialize the metadata database by typing,
```
airflow initdb
```
Out of the box, Airflow uses a [SQLite](https://www.sqlite.org/) database, which you should outgrow fairly quickly since no parallelization is possible using this database backend.## An Example ETL Pipeline With Airflow
Let's go over an example of an Airflow DAG to that calls the OpenWeatherMap API daily to get weather in Brooklyn, NY and stores the data in the Postgres database that we created.First you can see if there is Python syntax error by "compiling it,"
```
python dag_def_.py
```
You can then test an individual task within a dag by using the command,
```
airflow test
```
You can also test the whole dag by doing a backfill,
```
Airflow backfill -s -e
```
Sometimes, in order to notify Airflow of an update you may need to delete the *.pyc* files or even the DAGs themselves.If you need to delete a dag, first delete the DAG data from the metadata_db database:
```
Use the UI -> Browse -> Dag Runs -> Then delete them all.```
Then you can delete DAGs by clearing the task instance states:
```
airflow clear
```
Airflow is an extremely useful tool for building data pipelines and scheduling jobs in Python.