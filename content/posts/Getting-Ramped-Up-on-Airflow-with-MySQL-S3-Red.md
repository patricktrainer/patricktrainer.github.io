
---
    title: Getting-Ramped-Up-on-Airflow-with-MySQL-S3-Red
    date: 2021-01-01    
    draft: true
    tags: []
---
# Getting-Ramped-Up-on-Airflow-with-MySQL-S3-Red# Getting Ramped-Up on Airflow with MySQL → S3 → Redshift - By Austin Gibbons
Created: January 28, 2020 8:06 PM
Tags: Data
URL: https://hackernoon.com/getting-ramped-up-on-airflow-with-mysql-s3-redshift-defcc4522c8c
I recently joined [Plaid](https://www.plaid.com/) as a data engineer and was getting ramped up on [Airflow](https://medium.com/airbnb-engineering/airflow-a-workflow-management-platform-46318b977fd8), a workflow tool that we used to manage ETL pipelines internally.
Around the time that I was joining, Plaid was migrating onto [Periscope Data](https://www.periscopedata.com/) for visualizing SQL queries, and my immediate mission became to get more of the data people relied on for analytics insights into our nascent [Redshift](https://hackernoon.com/tagged/redshift) cluster, the data warehouse we query from Periscope.
[Getting%20Ramped-Up%20on%20Airflow%20with%20MySQL%20%E2%86%92%20S3%20%E2%86%92%20Red%20f60cc11edad34b0a89feae207ee0d59a/0Dt4pTxhZXWN8CtwF](Getting%20Ramped-Up%20on%20Airflow%20with%20MySQL%20%E2%86%92%20S3%20%E2%86%92%20Red%20f60cc11edad34b0a89feae207ee0d59a/0Dt4pTxhZXWN8CtwF)
Plaid ETL pipeline circa early 2018
### Motivation
Kindly, my coworker left a more straightforward task to me to help me get ramped up with Airflow — moving data regularly from MySQL to Redshift.
](https://docs.aws.amazon.com/datapipeline/latest/DeveloperGuide/dp-template-redshift.html) We can pull the schema out of MySQL using a straightforward query:
```
selectfromwhere
```
We handled a few types manually, for example instead of moving binary data over we would detect a binary type and instead return a boolean as for whether the column was null or non-null, to avoid having to copy a large amount of binary data over the wire that would be unusable for analytics.
Storing the state in the data warehouse manager instead lets us more easily modify the system— automatically adding and removing tables and columns as they get added or dropped from the upstream database and adding custom functionality like setting Redshift sort and distribution keys, and deploying better methodology for our database ingestion.
If you’re looking for a cloud provider, we’ve had success using [Stitch Data](https://www.stitchdata.com/) for data processing pipelines, [this post from Amazon](https://aws.amazon.com/blogs/aws/fast-easy-free-sync-rds-to-redshift/) recommends additional vendors, and [Panoply](https://blog.panoply.io/how-to-move-your-mysql-to-amazon-redshift) recommends a similar method using mysqldump.
Plaid works with many different data sources, and for non-sensitive datasets + 3rd-party data [Stitch](https://www.stitchdata.com/) and [Segment](https://segment.com/) have been instrumental in building up data workflows.
