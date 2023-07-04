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

- **Streaming inserts** in BigQuery provide best effort de-duplication. By including an insertID that uniquely identifies a record, BigQuery can detect duplicates and prevent them from being inserted. However, if no insertID is provided, BigQuery does not attempt to de-duplicate the data.
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
- **Stackdriver Trace** is a distributed tracing system designed to collect data on how long it takes to process requests to services. It is available in Compute Engine, Kubernetes Engine. It useful when you’re using microservices architectures.

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
**AVRO**:-It is the recommended format for data loading in BigQuery due to its ability to read data blocks in parallel, even when the file is compressed. Unlike CSV files, Avro does not have encoding issues, making it a preferred choice for efficient and reliable data loading.
**PARQUET**:-It is another data storage format that utilizes a columnar model. Uncompressed CSV and JSON files can be loaded faster compared to compressed files because they can be loaded in parallel. However, loading uncompressed files in parallel can result in higher storage costs when using Cloud Storage.





