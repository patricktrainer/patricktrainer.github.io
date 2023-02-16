---
date: '2021-01-01'
draft: false
tags: '[]'
title: Why-Robinhood-uses-Airflow-Robinhood-Engineering
---

# Why-Robinhood-uses-Airflow-Robinhood-Engineering

We started off with using cron to schedule these jobs but with their growing number and complexity, it became increasingly challenging for us to manage them using cron:
- **Managing dependencies** between jobs was difficult.
## Dependency Management
Airflow uses [Operators](https://airflow.incubator.apache.org/concepts.html#operators) as the fundamental unit of abstraction to define tasks, and uses a [DAG](https://airflow.incubator.apache.org/concepts.html#dags) (Directed Acyclic Graph) to define workflows using a set of operators.
It provides historical views of the jobs and tools to control the state of jobs — such as kill a running job or manually re-running a job.
We also use Airflow sensors to run jobs right after market close, while handling market half-days.
- The **Scheduler** works separately for scheduled jobs and backfill jobs.
- Airflow was built primarily for data batch processing due to which the Airflow designers made a decision to always **schedule jobs for the previous interval**.
Hence, a job scheduled to run daily at midnight will pass in the execution date “2016–12–31 00:00:00” to the job’s context when run on “2017–01–01 00:00:00”.
