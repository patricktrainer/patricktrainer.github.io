---
                title: Product-Overview-Materialize
                date: 2021-01-01    
                draft: true
                tags: []
               ---


            # Product-Overview-Materialize

All of the interactive queryable capabilities of a traditional SQL data warehouse, but connecting directly to your streaming data sources, and staying up-to-date within milliseconds.Materialize delivers SQL exploration for streaming events and real-time data.[Product%20Overview%20%E2%80%93%20Materialize%20cf57caaf7a794979bf60da5471332f90/rest-of-SQL-01-1250.png](Product%20Overview%20%E2%80%93%20Materialize%20cf57caaf7a794979bf60da5471332f90/rest-of-SQL-01-1250.png)
Many streaming solutions require the denormalization of data in order to maintain low latency - thereby prohibiting any kind of data enrichment like joins.[Product%20Overview%20%E2%80%93%20Materialize%20cf57caaf7a794979bf60da5471332f90/connect-to-kafka-01-1250.png](Product%20Overview%20%E2%80%93%20Materialize%20cf57caaf7a794979bf60da5471332f90/connect-to-kafka-01-1250.png)
### Connects directly to event stream processors
Materialize connects directly to your streaming infrastructure, ingesting streams of data from event stream processors like Kafka.[Product%20Overview%20%E2%80%93%20Materialize%20cf57caaf7a794979bf60da5471332f90/postgres-01-1250.png](Product%20Overview%20%E2%80%93%20Materialize%20cf57caaf7a794979bf60da5471332f90/postgres-01-1250.png)
### Presents as Postgres downstream
Materialize is wire compatible with PostgreSQL, presenting to downstream tools like any Postgres database, simplifying the development of custom applications and streamlining the process of connecting existing data analysis tools.### Build views on views on views - or export back to your event stream processor
Transformations on streaming data can be used to feed into other transformations of that data - say joining several sources, then further querying that information.[Product%20Overview%20%E2%80%93%20Materialize%20cf57caaf7a794979bf60da5471332f90/read-replica-01-1250.png](Product%20Overview%20%E2%80%93%20Materialize%20cf57caaf7a794979bf60da5471332f90/read-replica-01-1250.png)
## Use Materialize as an Optimized Read Replica Database
Traditional read replica databases are optimized for transactional loads – but are usually suboptimal for analytics or visualization.