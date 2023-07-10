# Databases
![Alt text](image.png)

## Cloud SQL
 - Cloud SQL is a **fully managed relational database** service that supports **MySQL, PostgreSQL, and SQL Server** databases.
 - Cloud SQL is well suited for **regional applications** that do not need to store more than **30 TB** of data in a single instance
 - Automatic replication,Managed backups
 - It facilitates **Vertical** & **Horizontal** Scaling.
 - Cloud SQL is similar to **Amazon RDS**.

 ### Read Replicas:- 
 - A replica database that enables parallel read operations, improving read performance and scalability by offloading read traffic from the primary database. Read replicas must be in the same region as the primary instance
 - It is a copy of the primary instance’s data that is maintained in the same region as the primary instance. Binary logging must be enabled to support read replicas. we  cannot perform backups on a read replica.
- It's important to note that read replicas are not intended for high availability or disaster recovery purposes. They are primarily used for scaling read workloads and improving performance.

**Failover replica**: A secondary replica database that automatically takes over as the primary in the event of a failure, ensuring high availability and minimal downtime.

## Cloud Spanner
- Cloud Spanner is Google’s relational, horizontally scalable, global database. It also manages automatic replication.Cloud Spanner is suitable for read/write operations.
- Google recommends keeping CPU utilization below 65 percent in regional instances and below 45 percent in multi-regional instances. Also, each node can store up to 2 TB of data.
- Spanner can compromise (A)Availability from CAP theorem 
- Cloud Spanner uses a voting mechanism to determine writes.Regional instances use only read-only replicas; multi-regional instances use all three 
types
**Read-write replicas**:- maintain full copies of data and serve read operations, and they can vote on write operations
**Read-only replicas**:-  maintain full copies of data and serve read operations, but they do not vote on write operation
**Witness replicas**:- Witness replicas do not keep full copies of data but do participate in write votes. Witness replicas are helpful in achieving a 
majority when voting.
- Avoid hotspots by not using consecutive values for primary keys.  

## BigQuery
- BigQuery is fully managed, petabyte-scale, low-cost analytics data warehouse databases.Standard SQL supports advanced SQL features, such as correlated subqueries, ARRAY and STRUCT data types, as well as complex join expressions.
- BigQuery supports nested and repeated structures in rows. Nested data is represented in STRUCT type in SQL, and repeated types are represented in ARRAY types in SQL


**BigQuery Data Transfer Service**:- It is a fully managed service that automates the transfer of data from SaaS applications like Google Analytics, into BigQuery. This service simplifies the process of importing data from Google Analytics and provides features like scheduling, monitoring, and error handling.It automate the data movement from data sources such as Google Ads and Google AD Manager.

- Cloud Scheduler is a fully managed enterprise-grade cron job scheduler. It is not an multi-cloud orchestration tool.
- Federated storage is used to query data stored in Cloud Storage, Bigtable, or Google Drive
- An external data source (also known as a **federated data source**) is a data source that allows you to query directly even though the data is not stored in BigQuery.using external tables in BigQuery is useful for such cases:
  - Perform ETL operations on data.
  - Frequently changed data.
  - Data is being ingested periodically.
- BigQuery maintains a seven-day history of changes so that you can query a point-intime snapshot of data

 **Streaming inserts** in BigQuery provide best effort de-duplication. By including an insertID that uniquely identifies a record, BigQuery can detect duplicates and prevent them from being inserted. However, if no insertID is provided, BigQuery does not attempt to de-duplicate the data.
- BigQuery supports both batch and streaming data processing.Batching data to BigQuery is free, while streaming data is charged based on size.
Federated queries on protobuf message fields from Bigtable cannot be performed using BigQuery.
- Wildcard tables support built-in BigQuery storage only. You cannot use wildcards when querying an external table or a view.

### Caching
- predictive (pre-fetch) cache is only active for data sources that use the owner’s credentials to access the underlying data.
- Data Studio caching maximum period is 12 hours.
- BigQuery writes query results to a table, either a destination table specified by the user or a temporary, cached results table.Temporary, cached results tables incur no storage costs and are maintained per-user, per-project; whereas storing query results in a permanent table will result in storage charges.
- Temporary, cached results tables are created in an "anonymous dataset" with restricted access.Access to anonymous datasets is limited to the dataset owner.
- Anonymous datasets are hidden and their names start with an underscore, not appearing in the datasets list in the GCP Console or the classic BigQuery web UI.Listing anonymous datasets and auditing access controls can be done using the CLI or the API.

### StackDriver
- Stackdriver Monitoring is utilized for tracking performance metrics in BigQuery, including query counts and query execution time.
- The data collected by Stackdriver Monitoring can be viewed on Stackdriver Monitoring dashboards and used for alerting.
- Stackdriver Logging is employed to monitor events such as job executions or table creations in BigQuery.
- Logs are useful for understanding who is performing actions in BigQuery, whereas monitoring is useful for understanding how your queries and jobs are performing.
- Logs are maintained in Stackdriver for a specific period of time known as the retention period.If you want to keep them longer, you will need to export the logs before the end of the retention period.
- Admin activity audit logs, system event audit logs, and access transparency logs are kept for 400 days. Data access audit logs and other logs not related to auditing are kept 30 days.
 **Stackdriver Trace** is a distributed tracing system designed to collect data on how long it takes to process requests to services. It is available in Compute Engine, Kubernetes Engine. It useful when you’re using microservices architectures.

**Partitioning**:-
Partitioning and clustering can be effective strategies to improve query performance in BigQuery. Partitioning involves dividing a large table into smaller and more manageable pieces based on a specified column, such as date or region. This allows queries to only scan the relevant partitions, rather than scanning the entire table, which can significantly reduce query time and cost.

**Clustering**:-
Clustering, on the other hand, involves grouping related rows in a table together based on one or more columns, such as product or category. This can improve query performance by reducing the amount of data that needs to be scanned within a partition, since the related data will be physically located closer together.

**Points to Remember**:-
- sharding is a method of dividing a database into multiple, smaller databases, while partitioning is a method of dividing a single, large table into smaller, more manageable pieces.
- splitting data by date or timestamp, you can use partitions, and to split data into multiple tables by other attributes, you can try sharding
- **SLA** stands for **Service Level Agreement**. It is a commitment or guarantee made by a service provider to its users or customers regarding the level of service availability or performance they can expect
- Wildcards cannot be used with views or external tables.
- Caching is the process of storing frequently accessed data in a temporary storage area so that it can be quickly retrieved at a later time without having to go back to the original source.
- cluster nodes can download the dependencies from Cloud Storage from internal IPs.
- Dataproc has a BigQuery connector library which allows it directly interface with BigQuery.BigQuery connector is a Java library that enables Hadoop to process data from BigQuery using abstracted versions of the Apache Hadoop InputFormat and OutputFormat classes.
- **_PARTITIONTIME and _PARTITIONDATE** are available only in ingestion-time partitioned tables. Partitioned tables do not have pseudo columns.
BigQuery requires data to be encoded in UTF-8. If a CSV file is not in UTF-8, BigQuery attempts to convert it, but the conversion may not always be accurate, leading to differences in some bytes. To ensure proper loading, specify the correct encoding. Similarly, JSON files need to be in UTF-8 encoding when loading into BigQuery.
- **AVRO**:-It is the recommended format for data loading in BigQuery due to its ability to read data blocks in parallel, even when the file is compressed. Unlike CSV files, Avro does not have encoding issues, making it a preferred choice for efficient and reliable data loading.
- **PARQUET**:-It is another data storage format that utilizes a columnar model. Uncompressed CSV and JSON files can be loaded faster compared to compressed files because they can be loaded in parallel. However, loading uncompressed files in parallel can result in higher storage costs when using Cloud Storage.

## Cloud Firestore

- Google Cloud Datastore is a NoSQL document database built for automatic scaling, high performance, and ease of application development and integrating well with App Engine.
- Cloud Firestore is the managed document database that is replacing Cloud Datastore.Document databases are used when the structure of data can vary from one record to another.
- It store highly structured objects in a document database, with support for ACID transactions and SQL-like queries. Cloud Firestore operates in one of two modes: 
	
**Native Mode**:- the new data model, realtime updates, and mobile and web client library features are available only in Native Mode
**Cloud Datastore Mode**:- In Datastore mode, Firestore offers strong consistency and removes the limitations of 25 entity groups and one write per second to an entity group that were present in Datastore.

- Indexes are used when querying and must exist for any property referenced in filters
- Cloud Firestore uses two kinds of indexes:

**built-in indexes**:- Built-in indexes are created by default for each property in an eyntity. 
**composite indexes**:- They are used when there are multiple filter conditions in a query. They are defined in a configuration file called index.yaml

- Cloud Firestore in Datastore Mode is a managed document database that is well suited for applications that require semi-structured data but that do not require low-latency writes (< 10 ms).
- When low-latency writes are needed, Bigtable is a better option Firestore is a suitable choice if you need to store well-organized data in a document database, ensuring transactional integrity and the ability to perform SQL-like queries.
- Datastore is designed for web applications of a small scale.

## Cloud Big Table:-
- Bigtable provides a scalable, fully-managed NoSQL wide-column database that is suitable for both real-time access and analytics workloads.
- Cloud Bigtable is a wide-column NoSQL database used for high-volume databases that require low millisecond (ms) latency.
- Cloud Bigtable is used for IoT, time-series, finance, and similar applications.Bigtable is a managed service, but it is not a NoOps service: like Cloud SQL and Cloud Spanner.
- Bigtable also excels as a storage engine for batch MapReduce operations, stream processing/analytics, and machine-learning applications.
- Data is stored in Bigtable lexicographically by row-key, which is the one indexed column in a Bigtable table.
- goal when designing a row-key is to take advantage of the fact that Bigtable stores data in a sorted order.

- Bigtable provides eventual consistency, which means that the data in clusters may not be the same sometimes, but they eventually will have the same data
- When creating a Cloud Bigtable instance and cluster, the choice between SSD or HDD storage for the cluster is permanent and cannot be changed using the Google Cloud Platform Console.
- If you need to convert an existing HDD cluster to SSD, or vice-versa, you can export the data from the existing instance and import it into a new instance.
- Alternatively, you can use a Cloud Dataflow or Hadoop MapReduce job to copy the data from one instance to another.
- It's important to note that migrating an entire instance takes time, and you may need to add nodes to your Cloud Bigtable clusters before initiating the migration.
- The dataset location cannot be changed once created. The dataset needs to be copied using Cloud Storage.
- preemptible nodes can have persistent disks. Dataproc handles the addition and removal of preemptible nodes.preemptible workers cannot store the data. 	
- Production instances have clusters with a minimum of three nodes; development instances have a single node and do not provide for high availability.

## Characteristics of a good row-key:-
- Using a prefix for multitenancy isolates data from different customers, making scans and reads more efficient by ensuring that data blocks contain data from one customer only, allowing customers to query only their own data.
- Columns that are not frequently updated, such as a user ID or a timestamp
- Nonsequential value in the first part of the row-key, which helps avoid hotspots
- To avoid hotspots, never use a timestamp value as a row key prefix.
- Field promotion is a recommended practice as it helps prevent hotspotting and simplifies the design of a row key for efficient querying.

- Key Visualizer is a tool that helps you analyze your Bigtable usage patterns. It generates visual reports for your tables that break down your usage based on the row keys that you access.
- Bigtable does not have secondary indexes

**Best Practices**:-
- Bigtable has a limit of 1,000 tables per instance.
- Limit table to around 100 column families to avoid performance issues.
- Limit row size to 100 MB or less to maintain optimal read performance.
- Keep cell size below 10 MB and use shorter row keys(4 KB or less) to optimize memory, storage, and response times in Cloud Bigtable.
-  Minimum 1TB is required to store the data in bigtable

**Note**:-
- Failover in cloud computing is the process of automatically transferring workloads from a failed or failing primary resource to a secondary resource in order to minimize downtime and ensure continuity of service.
- Hotspots can be caused by a number of factors, such as a heavily used table or an inefficient query that repeatedly touches the same data.
- They can also result from the database architecture itself, such as data being stored in a manner that causes read or write operations to be heavily concentrated in certain areas.
- Primary index is always based on the primary key of a table, which is a unique identifier for each row. 
- Secondary indexes, on the other hand, can be created on any column or set of columns in the table.





