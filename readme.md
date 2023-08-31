# Debezium, Kafka and Postgres

## The goal of this project is stream changes from your database to Kafka topic.

### Running this sample
To start tools
```shell
docker-compose up -d
```

Configuring stream for table shipments
```shell
curl -H 'Content-Type: application/json' localhost:8083/connectors --data '
{
  "name": "shipments-connector",  
  "config": {
    "connector.class": "io.debezium.connector.postgresql.PostgresConnector", 
    "plugin.name": "pgoutput",
    "database.hostname": "postgres", 
    "database.port": "5432", 
    "database.user": "postgresuser", 
    "database.password": "postgrespw", 
    "database.dbname" : "shipment_db", 
    "database.server.name": "postgres", 
    "table.include.list": "public.shipments" 
  }
}'
```

### Tools used:
- [Debezium](https://debezium.io/) - Debezium is an open source distributed platform for change data capture. Start it up, point it at your databases, and your apps can start responding to all of the inserts, updates, and deletes that other apps commit to your databases. Debezium is durable and fast, so your apps can respond quickly and never miss an event, even when things go wrong.
- [Postgres](https://www.postgresql.org/) - PostgreSQL is a powerful, open source object-relational database system with over 35 years of active development that has earned it a strong reputation for reliability, feature robustness, and performance.
- [akhq](https://akhq.io/) - Manage & view data inside your Apache Kafka ® cluster
- [ZooKeeper](https://zookeeper.apache.org/) - Apache ZooKeeper is an effort to develop and maintain an open-source server which enables highly reliable distributed coordination.
- [Kafka](https://kafka.apache.org/) - Apache Kafka is an open-source distributed event streaming platform used by thousands of companies for high-performance data pipelines, streaming analytics, data integration, and mission-critical applications.
- [Schema-Registry](https://docs.confluent.io/platform/current/schema-registry/index.html) - Schema Registry provides a centralized repository for managing and validating schemas for topic message data, and for serialization and deserialization of the data over the network. Producers and consumers to Kafka topics can use schemas to ensure data consistency and compatibility as schemas evolve. Schema Registry is a key component for data governance, helping to ensure data quality, adherence to standards, visibility into data lineage, audit capabilities, collaboration across teams, efficient application development protocols, and system performance.
- [Kafka Connect](https://docs.confluent.io/platform/current/connect/index.html) - Kafka Connect is a tool for scalably and reliably streaming data between Apache Kafka® and other data systems. It makes it simple to quickly define connectors that move large data sets in and out of Kafka. Kafka Connect can ingest entire databases or collect metrics from all your application servers into Kafka topics, making the data available for stream processing with low latency. An export connector can deliver data from Kafka topics into secondary indexes like Elasticsearch, or into batch systems–such as Hadoop for offline analysis.