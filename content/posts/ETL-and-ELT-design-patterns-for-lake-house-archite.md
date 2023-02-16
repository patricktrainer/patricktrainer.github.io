
---
    title: ETL-and-ELT-design-patterns-for-lake-house-archite
    date: 2021-01-01    
    draft: true
    tags: []
---
# ETL-and-ELT-design-patterns-for-lake-house-archite# ETL and ELT design patterns for lake house architecture using Amazon Redshift: Part 2 | AWS Big Data Blog
Created: January 28, 2020 8:42 PM
Tags: Data
URL: https://aws.amazon.com/blogs/big-data/etl-and-elt-design-patterns-for-lake-house-architecture-using-amazon-redshift-part-2/?nc1=b_rp
Part 1 of this multi-post series, [ETL and ELT design patterns for lake house architecture using Amazon Redshift: Part 1](https://aws.amazon.com/blogs/big-data/etl-and-elt-design-patterns-for-lake-house-architecture-using-amazon-redshift-part-1/), discussed common customer use cases and design best practices for building ELT and ETL data processing pipelines for data lake architecture using [Amazon Redshift Spectrum](https://docs.aws.amazon.com/redshift/latest/dg/c-getting-started-using-spectrum.html), [Concurrency Scaling](https://docs.aws.amazon.com/redshift/latest/dg/concurrency-scaling.html), and recent support for data lake export.
You also want to share the data with other AWS services such as Athena with its pay-per-use and serverless ad hoc and on-demand query model, AWS Glue and [Amazon EMR](http://aws.amazon.com/emr) for performing ETL operations on the unloaded data and data integration with your other datasets (such as ERP, finance, or third-party data) stored in your data lake, and [Amazon SageMaker](https://aws.amazon.com/documentation/sagemaker/) for machine learning.
Now that you have an external data catalog in AWS Glue named `etlblogpost`, create an external schema in the persistent cluster named `eltblogpost` using the following SQL from your SQL Workbench/J (replace **):
```
create external schema spectrum_eltblogpost from data catalog database 'eltblogpost' iam_role 'arn:aws:iam:::role/redshift-elt-test-role' create external database if not exists;
```
Using Spectrum, you can now query the three AWS Glue catalog tables you set up earlier.
"monthly_revenue_by_region_manufacturer_category_brand" where year = '1992' and month = 'March' and supplier_region = 'AFRICA' order by revenue desc limit 10; brand | category | manufacturer | revenue ----------+----------+--------------+----------- MFGR#1313 | MFGR#13 | MFGR#1 | 5170356068 MFGR#5325 | MFGR#53 | MFGR#5 | 5106463527 MFGR#3428 | MFGR#34 | MFGR#3 | 5055551376 MFGR#2425 | MFGR#24 | MFGR#2 | 5046250790 MFGR#4126 | MFGR#41 | MFGR#4 | 5037843130 MFGR#219 | MFGR#21 | MFGR#2 | 5018018040 MFGR#159 | MFGR#15 | MFGR#1 | 5009626205 MFGR#5112 | MFGR#51 | MFGR#5 | 4994133558 MFGR#5534 | MFGR#55 | MFGR#5 | 4984369900 MFGR#5332 | MFGR#53 | MFGR#5 | 4980619214
```
- Monthly revenue for the region `AMERICA` for the year 1995 across all brands:
```
SELECT month, sum(revenue) revenue FROM "spectrum_eltblogpost".
"yearly_revenue_by_city" where supplier_city in ('ETHIOPIA 4') and year between '1992' and '1995' and month = 'December' group by year, supplier_city order by year, supplier_city; year | supplier_city | revenue -----+---------------+------------ 1992 | ETHIOPIA 4 | 91006583025 1993 | ETHIOPIA 4 | 90617597590 1994 | ETHIOPIA 4 | 92015649529 1995 | ETHIOPIA 4 | 89732644163
```
When the data is in S3 and cataloged in the AWS Glue catalog, you can query the same catalog tables using Athena, AWS Glue, Amazon EMR, Amazon SageMaker, [Amazon QuickSight](https://aws.amazon.com/quicksight/), and many more AWS services that have seamless integration with S3.
You want to query the unloaded data from your data lake using Redshift Spectrum if you have an existing cluster, Athena with its pay-per-use and serverless ad hoc and on-demand query model, AWS Glue and Amazon EMR for performing ETL operations on the unloaded data and data integration with your other datasets in your data lake, and Amazon SageMaker for machine learning.
Connect to the cluster from the SQL Workbench/J.To use Redshift Spectrum for querying data from data lake (S3), you need to have the following:
- An Amazon Redshift cluster and a SQL client (SQL Workbench/J or another tool of your choice) that can connect to your cluster and execute SQL commands.
