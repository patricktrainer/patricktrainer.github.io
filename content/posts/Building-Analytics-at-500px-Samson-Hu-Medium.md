---
date: '2021-01-01'
draft: false
tags: '[]'
title: Building-Analytics-at-500px-Samson-Hu-Medium
---

# Building-Analytics-at-500px-Samson-Hu-Medium

A place where:
- Everyone understands company metrics and knows how their work fits into the measurement framework
- We measure the impact of decisions and acknowledge their success or failure
- Teams use self service tools to answer their own questions with data
- We can predict the future by digging into the data and finding leading indicators
I knew that it wouldn’t be easy.
## The Dimensional Data Warehouse Schema
The schemas of data warehouses have two types of tables:
- *Fact tables* record measurements in time of a process.
## ETL
In order to populate our data warehouse with data from our production databases and logs, we apply a process called ETL.
An ETL script that has to turn messy production data into clean data warehouse data will naturally be extremely messy.
## The Finished Data Warehouse
So that’s our data model — stored on Amazon Redshift, and fed new data every night by ETL pipelines run on Luigi.
You can think of three funnels at 500px:
- visitor -> signup -> daily active -> daily engaged -> paid subscriber
- visitor -> signup -> photo upload -> photo submit to marketplace -> photo sold on marketplace
- visitor -> signup -> purchase photo from marketplace
Each team owns different parts of this funnel for different products:
- The marketing teams own (page views) and the top and bottom (revenue) of this funnel
- The product teams has less of an emphasis on top of funnel metrics
- The development teams (web and mobile), want to see the entire funnel with respect to their own products.
There’s so much room for failure in this system:
- Logs could get parsed wrong, and you undercount or over-count an event
- The log sender on an API server could fail and you don’t notice and you miss a fraction of your events
- There might be network issues one day, and 10% of your log entries might fail to send to S3
- Some metrics that are important might be hard to query in the database and you might pull the wrong number
- etc
This doesn’t include hard fail events like your ETL’s failing and the metrics not being refreshed.
