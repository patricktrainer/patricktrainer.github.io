---
 	layout: post
 	title: Export-MySQL-Data-to-Amazon-S3-Using-AWS-Data-Pipe
 	date: 2021-01-01
 	draft: false
 	tags: []
---

# Export-MySQL-Data-to-Amazon-S3-Using-AWS-Data-Pipe# Export MySQL Data to Amazon S3 Using AWS Data Pipeline - AWS Data Pipeline
Created: April 18, 2020 3:05 PM
URL: https://docs.aws.amazon.com/datapipeline/latest/DeveloperGuide/dp-copydata-mysql.html
This tutorial walks you through the process of creating a data pipeline to copy data (rows) from a table in MySQL database to a CSV (comma-separated values) file in an Amazon S3 bucket and then sending an Amazon SNS notification after the copy activity completes successfully.
You will use an EC2 instance provided by AWS Data Pipeline for this copy activity.
**Pipeline Objects**
The pipeline uses the following objects:
