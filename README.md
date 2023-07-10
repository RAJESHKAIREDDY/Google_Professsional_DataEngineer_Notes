# Google_Professsional_DataEngineer_Notes

[a relative link](BigData_Processing.md)

## Normalization

Normalization is a process in database design that aims to improve data integrity and reduce data redundancy. It involves organizing data into well-structured tables, adhering to specific rules known as normal forms.

The first form of normalization, known as 1NF (First Normal Form), requires each column in a table to hold atomic values, eliminate any repeating groups, and have a primary key that uniquely identifies each row.

The second form of normalization, known as 2NF (Second Normal Form), builds upon the first form by introducing separate tables for values that apply to multiple rows. These related tables are linked using foreign keys, enabling better organization and data management.

The third form of normalization, known as 3NF (Third Normal Form), includes the requirements of 2NF and further eliminates any columns in a table that do not directly depend on the primary key. This helps to minimize data duplication and improve database efficiency.

By following the principles of normalization, database designers can create well-structured and efficient database schemas that ensure data integrity and facilitate effective data manipulation.

## Cloud SQL

Cloud SQL is a comprehensive managed service for relational databases, offering support for MySQL, PostgreSQL, and SQL Server. It is an ideal solution for regional applications that require efficient data storage and management, with a maximum data capacity of up to 30 TB per instance.

## Read Replicas

Read replicas are a valuable feature that enhances the performance of databases with high read workloads. By creating a copy of the primary instance's data in the same region, read replicas facilitate faster read operations. It is essential to enable binary logging to ensure the proper functioning of read replicas. However, note that performing backups on a read replica is not supported. Additionally, read replicas must be located within the same region as the primary instance.

## Cloud Spanner

Cloud Spanner is a globally distributed, horizontally scalable relational database provided by Google. It offers automatic replication for enhanced reliability. To optimize performance, Google recommends maintaining CPU utilization below 65 percent for regional instances and below 45 percent for multi-regional instances. Each node within Cloud Spanner can store up to 2 TB of data.

Cloud Spanner employs a voting mechanism to determine write operations. In regional instances, only read-only replicas participate, while multi-regional instances involve all three replica types:

- Read-write replicas: These replicas maintain full copies of data and serve read operations. They also actively participate in write operations by voting.
- Read-only replicas: These replicas store complete data copies and serve read operations but do not participate in write votes.
- Witness replicas: Witness replicas do not store full data copies but contribute to write votes. They play a crucial role in achieving a majority during voting.

To prevent hotspots, it is advisable to avoid using consecutive values for primary keys, as this can lead to uneven data distribution.

By leveraging the power of Cloud SQL and Cloud Spanner, developers can benefit from highly reliable, scalable, and performant database solutions for their applications.

## Cloud Bigtable

Cloud Bigtable is a highly scalable and fully managed NoSQL wide-column database designed to cater to real-time access and analytics workloads. It is particularly well-suited for applications that demand low millisecond (ms) latency, such as IoT, time-series, and finance applications. While Bigtable is a managed service, it is important to note that it does require some operational involvement, similar to Cloud SQL and Cloud Spanner.

Data in Bigtable is stored in a lexicographical order based on the row-key, which serves as the indexed column in a Bigtable table. When designing the row-key, the goal is to leverage Bigtable's sorted data storage approach for optimal performance.

Key characteristics of a well-designed row-key include:

1. Utilizing a prefix for multitenancy: This ensures data isolation for different customers, enhancing the efficiency of scans and reads. By organizing data blocks to contain information from a single customer, customers can query only their own data, improving overall performance.
2. Choosing non-frequently updated columns: Columns like user IDs or timestamps are ideal candidates for the row-key, as they offer stability and minimize unnecessary data movement.
3. Avoiding sequential values in the initial part of the row-key: This helps mitigate hotspots, as nonsequential values distribute data more evenly across the system.

It's important to note that Bigtable does not support secondary indexes, which are indexes created on columns other than the primary key. However, failover mechanisms are available in cloud computing to automatically transfer workloads from a primary resource to a secondary resource, minimizing downtime and ensuring uninterrupted service.

Hotspots can occur due to various factors, such as heavily used tables or inefficient queries that repeatedly access the same data. Database architecture can also contribute to hotspots if data is stored in a way that concentrates read or write operations in specific areas.

In summary, Cloud Bigtable offers a powerful solution for building high-volume, low-latency NoSQL databases. By leveraging its unique capabilities and following best practices for row-key design, developers can optimize performance and efficiency for their applications.

## Cloud Firestore

Cloud Firestore, a managed document database, is the successor to Google Cloud Datastore. It is specifically designed for automatic scaling, high performance, and seamless application development, integrating seamlessly with App Engine. Document databases are particularly useful when dealing with data that exhibits varying structures across different records.

Cloud Firestore operates in two modes:

1. Native Mode: In this mode, developers can leverage the new data model, real-time updates, and the rich features provided by mobile and web client libraries. These advanced capabilities are exclusively available in Native Mode.

2. Cloud Datastore Mode: In Datastore mode, Cloud Firestore offers strong consistency and removes the limitations associated with Cloud Datastore, such as the constraint of 25 entity groups and one write per second to an entity group.

When querying data in Cloud Firestore, indexes play a crucial role and must exist for any property referenced in filters. There are two types of indexes in Cloud Firestore:

1. Built-in Indexes: These indexes are automatically created for each property in an entity. They enable efficient querying of data based on specific properties.

2. Composite Indexes: Composite indexes come into play when multiple filter conditions are involved in a query. They are defined in a configuration file called index.yaml, allowing for more complex and optimized queries.

Cloud Firestore in Datastore Mode serves as a managed document database ideal for applications that require semi-structured data. It is a compelling choice when low-latency writes (less than 10 ms) are not essential. In scenarios where low-latency writes are a priority, Cloud Bigtable offers a more suitable option.

Overall, Cloud Firestore offers developers a powerful and scalable solution for working with document-based data, enabling effortless scaling, robust performance, and streamlined application development.


## BigQuery

BigQuery is a fully managed, petabyte-scale, and cost-effective analytics data warehouse. It supports Standard SQL, which includes advanced SQL features such as correlated subqueries, ARRAY and STRUCT data types, and complex join expressions.

When working with BigQuery, it is important to ensure that data is encoded in UTF-8. In the case of CSV files, BigQuery attempts to convert them to UTF-8, but the conversion may not always be accurate. To guarantee proper loading, it is recommended to specify the correct encoding. Similarly, when loading JSON files, they should be in UTF-8 encoding.

AVRO format is highly recommended for data loading in BigQuery due to its parallel data block reading capabilities, even with compression. Unlike CSV files, AVRO format avoids encoding issues, making it a preferred choice for efficient and reliable data loading. Another data storage format, PARQUET, utilizes a columnar model. Loading uncompressed CSV and JSON files can be faster than compressed files since they can be loaded in parallel. However, it is important to consider the potential higher storage costs when using Cloud Storage for uncompressed files.

BigQuery provides streaming inserts with best-effort de-duplication. By including an insertID that uniquely identifies a record, duplicates can be detected and prevented from being inserted. However, without an insertID, BigQuery does not attempt to de-duplicate the data.

To track performance metrics in BigQuery, Stackdriver Monitoring is utilized, which includes information such as query counts and query execution time. On the other hand, Stackdriver Logging is employed to monitor events like job executions or table creations in BigQuery. Logs help understand actions performed in BigQuery, while monitoring provides insights into query and job performance.

BigQuery supports nested and repeated structures in rows, representing nested data with the STRUCT type in SQL and repeated types with ARRAY types in SQL.

### Notes:

1. Sharding involves dividing a database into multiple smaller databases, while partitioning involves dividing a large table into smaller, manageable pieces.
2. SLA stands for Service Level Agreement, which is a commitment or guarantee made by a service provider regarding the level of service availability or performance.

Please note that wildcards cannot be used with views or external tables.

Caching is the process of storing frequently accessed data in temporary storage to enable quick retrieval without going back to the original source.

## Cloud Memorystore (Redis)

Cloud Memorystore is a managed Redis service commonly used for caching purposes.

In Redis, if the memory usage exceeds 80 percent of the system memory, the instance is considered to be under memory pressure. To alleviate this, several actions can be taken, including scaling up the instance, lowering the maximum memory limit, modifying the eviction policy, setting time-to-live (TTL) parameters, or manually deleting data. By default, Redis evicts the least recently used keys with TTLs set.

## Cloud Storage

Cloud Storage is a specialized storage system designed for unstructured data, such as files, images, videos, backups, and more. Data in Cloud Storage is organized and stored as individual objects, which are independent and self-contained units, enabling efficient storage and retrieval of unstructured data. It is not suitable for handling real-time streaming data.

A bucket in Cloud Storage is a group of objects that share access controls at the bucket level. Cloud Storage does not utilize a traditional file system.

Cloud Storage can be used both as a staging area for immediate data ingestion and as a long-term store for transformed data.

### Bucket Naming:

To ensure optimal performance when uploading files in parallel, it is advised not to use sequential names or timestamps. Files with sequentially close names may be assigned to the same server, resulting in a potential hotspot when writing files to Cloud Storage. By avoiding sequential naming, the distribution of files across servers can be more balanced, enhancing overall performance.

### Storage Classes:

Cloud Storage provides four types of storage classes, each designed to address specific use cases:

1. **Regional Storage:** This class stores multiple copies of an object in multiple zones within a single region. It offers high availability and is suitable for applications with regional requirements.

2. **Multi-regional Storage:** To mitigate the risk of a regional outage, multi-regional storage stores replicas of objects in multiple regions. It provides greater resilience and is recommended for globally distributed applications.

3. **Nearline Storage:** If data is accessed less than once in 30 days, Nearline storage is a suitable option. It offers cost-effective storage with slightly higher latency compared to regional storage. It is well-suited for backup and archival data.

4. **Coldline Storage:** Data accessed less than once a year is a good fit for Coldline storage. It provides the most cost-effective archival storage option, although with slightly higher access latency. Coldline storage is ideal for long-term retention of infrequently accessed data.

### Considerations:

All storage classes have the same latency in returning the first byte of data. However, it's important to note that the costs associated with accessing data and per-operation costs are higher for storage classes other than regional storage.

When selecting a storage class, consider the access patterns and frequency of data usage. Coldline storage is best suited for archival storage, while multi-regional storage may be the preferred choice for uploading user data, especially when users are geographically dispersed.

By following these best practices and selecting the appropriate storage class, you can optimize the performance, cost, and availability of your data in Cloud Storage.


## Change Data Capture Approach

In certain scenarios, it is crucial to capture and record every change that occurs in a source system. This approach enables the tracking of all changes over time, rather than just extracting the state of the database at a specific point in time. This can be particularly valuable when monitoring inventory levels of products or other similar use cases.

By implementing a change data capture approach, each modification in the source system is captured and stored in a dedicated data store. This provides a comprehensive historical record of all changes, allowing for in-depth analysis and understanding of the data's evolution.

It is important to note that highly correlated features can lead to overfitting and unnecessary complexity in models. Therefore, careful consideration should be given to feature selection and handling correlated features appropriately to avoid these pitfalls.

Data Warehouses and Dimensional Data Models:

Data warehouses serve as databases specifically designed to store data from multiple sources. They typically adopt a dimensional data model, which organizes data in a denormalized structure. This dimensional approach simplifies data analysis and enables efficient querying and reporting.

Windowing Techniques:

1. Sliding Windows: Sliding windows advance by a specified number of data points, less than the width of the window. They are utilized to visualize the evolution of aggregates, such as the average of the last three values, over time. Sliding windows provide a dynamic representation of how the aggregate changes with each incoming data point.

2. Tumbling Windows: Tumbling windows advance by the length of the window. They are employed when aggregating data over a fixed period, such as the last one minute. Tumbling windows allow for consistent and predictable time-based analysis.

Handling Late Arriving Data:

Late arriving data refers to data points that arrive after their expected or desired timestamp. Dealing with late arriving data involves determining an appropriate waiting period and deciding whether to process it immediately or treat it as missing data. Watermarks, on the other hand, are timestamps used to track the progress of event time and assess the completeness of data within a given time window. Data with timestamps earlier than the watermark is considered on-time, while data with timestamps later than the watermark is regarded as late.

By incorporating these concepts and techniques into your data processing pipelines, you can effectively capture and analyze changes over time, ensuring a comprehensive understanding of your data and facilitating informed decision-making.


## Cloud Pub/Sub

Cloud Pub/Sub is a fully managed messaging service designed for real-time communication. It provides support for both push and pull subscription models, offering flexibility in how messages are delivered and consumed. With Cloud Pub/Sub, there is no need for manual server or cluster provisioning, as automatic scaling and load partitioning are handled seamlessly.

Key features of Cloud Pub/Sub include:

- **Real-time Messaging**: Cloud Pub/Sub enables the exchange of messages in real-time, allowing applications to communicate and share data instantly.

- **Managed Service**: As a managed service, Cloud Pub/Sub eliminates the need for infrastructure management, ensuring ease of use and reduced operational overhead.

- **Message Persistence**: Messages published to a topic in Cloud Pub/Sub can be retained for up to seven days, providing durability and allowing subscribers to consume messages at their own pace.

- **Exactly Once Processing**: For guaranteed exactly once processing of messages, Cloud Dataflow PubsubIO can be leveraged. This integration with Cloud Dataflow ensures that messages are deduplicated based on their unique message ID, minimizing duplicate processing and maintaining data integrity.

- **Ordering of Messages**: Cloud Dataflow, when used with Cloud Pub/Sub, can enforce message processing in the order they were received. This ensures that messages are handled sequentially, maintaining the desired sequence of operations.

By utilizing Cloud Pub/Sub, applications can leverage the power of real-time messaging without the hassle of managing infrastructure. The automatic scaling and load partitioning capabilities of Cloud Pub/Sub enable seamless handling of high volumes of messages. Furthermore, when combined with Cloud Dataflow, advanced features such as deduplication and ordered processing can be achieved, providing additional reliability and control over message delivery.

## Cloud Dataflow

Cloud Dataflow is a fully managed service for both stream and batch processing of data. It provides a powerful platform for building data pipelines using the Apache Beam API. With Cloud Dataflow, developers can focus on writing the data processing logic without the need to configure instances or clusters, as it is a fully managed and serverless service. It seamlessly integrates with various Google Cloud services, including Cloud Pub/Sub, BigQuery, Cloud ML Engine, Bigtable, and Apache Kafka, enabling seamless data integration across the ecosystem.

Key Concepts of Cloud Dataflow include:

- **Pipelines**: A Dataflow pipeline is a directed acyclic graph (DAG) that represents the data processing tasks and their dependencies. Pipelines are composed of a series of transformations applied to input data to generate the desired output. They can be executed repeatedly to process data efficiently.

- **PCollection**: PCollection, short for "Processing Collection," represents a distributed and immutable dataset within a Dataflow pipeline. It can be thought of as a collection of elements flowing through the pipeline during processing. PCollections can be created from data sources or as outputs of transformations. They can be bounded (batch processing) or unbounded (streaming data).

- **Transforms**: Transformations are operations applied to data within a Dataflow pipeline. They operate on one or more PCollections as input and produce one or more output PCollections. Transformations include filtering, aggregating, joining, mapping, and more. They enable data processing and computation within the pipeline.

- **ParDo**: ParDo is a parallel processing operation that applies a user-specified function to each element in a PCollection. ParDo operates on data in parallel and can receive additional inputs from other PCollections through side inputs. It produces a main output PCollection and can also generate additional output collections using side outputs. Side outputs are useful for handling data that doesn't meet certain criteria or creating additional processing paths.

- **Pipeline I/O**: Pipeline I/O transforms are used for reading data into a pipeline from a source and writing data to a sink. They facilitate seamless integration with various data sources and destinations.

- **Aggregation**: Aggregation refers to the process of computing a result from multiple input values. Dataflow supports aggregation operations that allow efficient computation on large datasets.

- **User-defined Functions**: User-defined functions (UDFs) are user-specified code for performing custom operations within a pipeline. They are typically used with ParDo transforms to define specific data processing logic.

- **Runner**: Runners are software components responsible for executing Dataflow pipelines as jobs. Dataflow supports multiple runners, including the Dataflow service in Google Cloud Platform (GCP), Apache Flink, and Apache Spark. The runner manages the execution of the pipeline, resource allocation, and fault tolerance.

- **Triggers**: Triggers determine when and how often computations are performed on data within windows. They enable fine-grained control over processing behavior based on event time progress or data arrival, allowing the production of intermediate or final results.

With its serverless nature and seamless integration with other Google Cloud services, Cloud Dataflow offers a highly flexible and efficient solution for stream and batch processing needs.

## ParDo

ParDo is a powerful data processing operation that plays a crucial role in various data transformation tasks within a pipeline. It offers a range of capabilities that facilitate efficient data manipulation, including:

1. **Filtering**: ParDo allows you to examine each element in a collection (PCollection) and selectively retain or discard it based on specific criteria. This capability is invaluable for eliminating irrelevant or unwanted data from your pipeline.

2. **Formatting or Type Conversion**: With ParDo, you can effortlessly transform the format or type of individual elements in a PCollection. This flexibility enables you to convert data into a desired format or ensure compatibility with downstream processing steps.

3. **Extraction**: ParDo excels at extracting specific fields or components from each element in a PCollection. It empowers you to retrieve individual fields from complex data structures, such as extracting specific attributes from BigQuery table rows.

4. **Computation**: ParDo provides a powerful mechanism for performing computations on each element or a subset of elements in a PCollection. Whether it's simple arithmetic operations or complex calculations, ParDo empowers you to apply custom computations tailored to your data processing needs.

ParDo's versatility and customizability make it an indispensable tool for manipulating and transforming data within a pipeline. It enables efficient data filtering, format conversion, field extraction, and computation, ensuring your data is processed according to your specific requirements.

## Cloud Dataproc

Cloud Dataproc is a fully managed service that simplifies the deployment, management, and scaling of Apache Hadoop and Apache Spark clusters on Google Cloud Platform (GCP). It offers a cost-effective solution for running big data processing workloads. 

Cloud Dataproc clusters consist of two types of nodes: master nodes and worker nodes. The master node is responsible for managing workload distribution, cluster resources, task scheduling, and job execution. On the other hand, worker nodes handle the actual data processing tasks, including data ingestion, storage, processing, and analysis. They parallelize and distribute the workload across the cluster, ensuring high performance and scalability.

Cloud Dataproc provides the flexibility to create "ephemeral" clusters, which can be created for executing specific tasks and then terminated to optimize cost efficiency. It offers efficient resource allocation and manages the cluster infrastructure, allowing you to focus on your data processing tasks.

Please note that while the number of worker nodes can be adjusted based on workload demands, the number of master nodes remains fixed in a Cloud Dataproc cluster.

## Cloud Composer

Cloud Composer is a managed service that implements Apache Airflow, a popular workflow management platform. It automates the scheduling, monitoring, and orchestration of complex workflows. With Cloud Composer, you can define and manage workflows as code, enabling efficient and reliable execution of tasks.

By leveraging Apache Airflow's capabilities, Cloud Composer provides a rich set of features for workflow management, including task scheduling, dependency management, parallel execution, and task monitoring. It enables you to define complex data processing pipelines with ease and ensures the reliable execution of tasks according to specified dependencies and schedules.

