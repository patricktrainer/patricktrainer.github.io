---
 	layout: post
 	title: We-re-All-Using-Airflow-Wrong-and-How-to-Fix-It
 	date: 2021-01-01
 	draft: false
 	tags: []
---

# We-re-All-Using-Airflow-Wrong-and-How-to-Fix-ItWhen a DAG is executed, the Worker will execute the work of each Operator, whether it is an HTTPOperator, a BigQueryOperator, or any other Operator, on the Airflow worker itself.
The DAG for this workflow would look something like this:
First, because each step of this DAG is a different functional task, each step is created using a different Airflow Operator.
Developer after developer moved a previously-working workflow over to Airflow only to have it brought down by an issue with an Airflow Operator itself.
This will happen for every Operator that it executes:
This means that all Python package dependencies from each workflow will need to be installed on each Airflow Worker for Operators to be executed successfully.
*
When we took the time to enumerate our problems with Airflow, it was evident that the Airflow Operators, the things that were supposed to make Airflow powerful and flexible, were providing the wrong abstraction to the Airflow developer.
*
Here’s how the new Kubernetes Operator works:
The Airflow Worker, instead of executing any work itself, spins up Kubernetes resources to execute the Operator’s work at each step.
Instead of executing work on the Airflow Worker itself, the Kubernetes Operator will spin up a Kubernetes resource to execute the work (shown above).
