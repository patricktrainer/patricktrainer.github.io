
---
    title: Syncing-Redshift-PostgreSQL-in-real-time-with-Ka
    date: 2021-01-01    
    draft: true
    tags: []
---
# Syncing-Redshift-PostgreSQL-in-real-time-with-KaBefore showing Kafka Connect, we’ll walk through some setup
- Setting up a distributed Kafka cluster
- Setting up a PostgreSQL database on AWS RDS
- Setting up an AWS Redshift instance
- Setting up Confluent’s open source platform
If you’re curious about how Kafka Connect works, I highly recommend reading the [concepts](http://docs.confluent.io/3.1.2/connect/concepts.html) and [architecture and internals](http://docs.confluent.io/3.1.2/connect/design.html) of Kafka Connect on Confluent’s platform documentation.
We can see the data in the table as below:
Now that we have some data in our PostgreSQL table, we can use Kafka Connect to get these rows as messages in a Kafka topic and have a process listening for any inserts/updates on this table.
- `timestamp.column.name`: the column name which has the timestamps
- `incrementing.column.name`: the column which has incremental IDs
- `topic.prefix`: to identify the Kafka topics ingested from PostgreSQL we can specify a prefix value which will be appended to all the table names and the topic name will be prefix+table name
The `source-postgres.properties` should look like this:
## Schema Registry
The JDBC connector from Confluent uses [Schema Registry](http://docs.confluent.io/3.1.2/schema-registry/docs/index.html) to store schema for the messages.
We can start schema registry as follows:
```
~$ /usr/local/confluent/bin/schema-registry-start /usr/local/confluent/etc/schema-registry/schema-registry.properties &
```
## Ingest data from PostgreSQL tables to Kafka topics
Let’s create a topic in which we want to consume the updates from PostgreSQL.
```
~$ /usr/local/kafka/bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 3 --partitions 1 --topic postgres_users
```
You can check that the topic exists using the following command:
```
~$ /usr/local/kafka/bin/kafka-topics.sh --describe --zookeeper localhost:2181 --topic postgres_users
```
We will be using Kafka Connect in stand-alone mode and we can start the stand-alone job to start consuming data from PostgreSQL table as follows:
```
~$ /usr/local/confluent/bin/connect-standalone /usr/local/confluent/etc/schema-registry/connect-avro-standalone.properties /usr/local/confluent/etc/kafka-connect-jdbc/source-postgres.properties
```
The `jdbc` connector serializes the data using Avro and we can use the Avro console consumer provided by Confluent to consume these messages from Kafka topic.
Change the following properties:
- `name`: name for the connector
- `topics`: Kafka topic to write data from
- `connection.url`: JDBC endpoint for Redshift
- `auto.create`: it is `true` by default and we will change it to `false` as we’ve already created the table in Redshift that this data should be written to.
The `sink-redshift.properties` should look as follows:
## Send messages from the Kafka topic to Redshift
We are all set to have messages from the Kafka topic write to the Redshift table.
