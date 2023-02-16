---
                title: Bringing-Data-Sources-Together-with-PipelineWise
                date: 2021-01-01    
                draft: true
                tags: []
               ---


            # Bringing-Data-Sources-Together-with-PipelineWise

# Bringing Data Sources Together with PipelineWise
Created: December 5, 2019 2:04 PM
Tags: Data
URL: [https://tech.transferwise.com/bringing-data-sources-together-with-pipelinewise/?utm_campaign=Up%20%26%20Running%20Weekly&utm_medium=email&utm_source=Revue%20newsletter](https://tech.transferwise.com/bringing-data-sources-together-with-pipelinewise/?utm_campaign=Up%20%26%20Running%20Weekly&utm_medium=email&utm_source=Revue%20newsletter)
TransferWise is open sourcing it’s data replication framework.[PipelineWise](https://transferwise.github.io/pipelinewise/) is a Data Pipeline Framework using the [Singer.io](https://www.singer.io/) specification to replicate data from various sources to various destinations.# Defining the Requirements
The tool had to be able to replicate hundreds of data sources into a centralised analytics data store where data analysts can do further transformations and can get real insights from data.The following minimal conditions had to be met:
- **Compatibility** with various data sources and analytics data stores as target
- **Change Data Capture** ([CDC](https://en.wikipedia.org/wiki/Change_data_capture)) mechanism wherever it’s possible to keep the lag as low as possible
- Maximum **security** and self hosted solution with the capability to obfuscate and mask PII and sensitive data at load time
- Apply **schema changes** automatically
- **Scalability**
- Avoiding vendor lock-in; accessing the source code to develop new features and fix issues quickly
- Keeping configuration as **code**
Our first approach was to look for a data transportation product that could satisfy our known use cases and also pass the rigorous requirements defined by our security team.# Team Effort and Running on Production
[PipelineWise](https://transferwise.github.io/pipelinewise/) was created by our Analytics Platform team in close cooperation with our Data Analysts, and some of the product teams as the main consumers of the data.PipelineWise now meets all the above initial requirements and is used to replicate **hundreds of GB** of data every day from **120 microservices**, **1500+ tables** and a bunch of external tools into our *Snowflake* data warehouse, with only **minutes of lag**.[Bringing%20Data%20Sources%20Together%20with%20PipelineWise%20aeefac37300e452e8ceb4cea5e01d2d9/pipelinewise-monitoring-grafana.png](Bringing%20Data%20Sources%20Together%20with%20PipelineWise%20aeefac37300e452e8ceb4cea5e01d2d9/pipelinewise-monitoring-grafana.png)
*Monitoring with [Grafana](https://grafana.com/): Replicating 120 data sources, 1500+ tables into Snowflake with PipelineWise on 3 nodes of c5.2xlarge EC2 instances*
# Limitations
Like any other tools PipelineWise also has limitations:
- **Not Real-Time**: The currently supported target connectors are micro-batch oriented.