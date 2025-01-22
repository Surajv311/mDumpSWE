
# Databricks-Snowflake-Pinot

- Databricks is a unified, open analytics platform for building, deploying, sharing, and maintaining enterprise-grade data, analytics, and AI solutions at scale. The Databricks Lakehouse Platform integrates with cloud storage and security in your cloud account, and manages and deploys cloud infrastructure on your behalf. Databricks has two different types of clusters: 
    - Interactive clusters are used to analyse data with notebooks, thus give you much more visibility and control. This should be used in the development phase of a project. 
      - Job clusters are used to run automated workloads using the UI or API. Jobs can be used to schedule Notebooks, they are recommended to be used in Production for most projects and that a new cluster is created for each run of each job. Cluster nodes have a single driver node and multiple worker nodes.
  - The driver and worker nodes can have different instance types, but by default they are the same. A driver node runs the main function and executes various parallel operations on the worker nodes. 
  - The worker nodes read and write from and to the data sources. The driver node maintains state information of all notebooks attached to the cluster. The driver node also maintains the SparkContext, interprets all the commands you run from a notebook or a library on the cluster, and runs the Apache Spark master that coordinates with the Spark executors.
  - A cluster consists of one driver node and zero or more worker nodes. You can pick separate cloud provider instance types for the driver and worker nodes, although by default the driver node uses the same instance type as the worker node. Different families of instance types fit different use cases, such as memory-intensive or compute-intensive workloads. Databricks worker nodes run the Spark executors and other services required for proper functioning clusters. When you distribute your workload with Spark, all the distributed processing happens on worker nodes.
  - Databricks runs one executor per worker node. Therefore, the terms executor and worker are used interchangeably in the context of the Databricks architecture.
  - **Query Federation in Databricks**: Query federation allows Databricks to execute queries against data served by other Databricks metastores as well as many third-party database management systems (DBMS) such as PostgreSQL, mySQL, AWS Redshift and Snowflake. To query data from another system you must: Create a foreign connection., etc. Simply put, from databricks UI itself you can run queries over external/third-party db post necessary connections are set up. 
  - Databricks Utilities (dbutils), a module for basic data file handling and data manipulation within Databricks Notebooks/ ecosystem.
  - A Delta Table is an advanced table format used in Databricks that enhances the capabilities of traditional data tables. It is essentially a collection of Parquet files stored in a data lake, accompanied by a transaction log that tracks all changes made to the data. This setup allows for several powerful features:
    - ACID Transactions: Ensures that all operations on the table are atomic, consistent, isolated, and durable, which prevents issues like partial updates.
    - Data Versioning: Users can perform "time travel," allowing them to query historical versions of the data.
    - Schema Enforcement: Ensures that only data conforming to the defined schema can be written to the table, maintaining data integrity.
    - Performance Optimizations: Techniques such as data skipping, caching, and compaction enhance query performance and reduce storage costs
  - Delta Lake manages its data like this:
    - Base Data: This is the initial dataset stored in Delta Tables.
    - Layering Changes: As new updates or changes occur (like inserts, updates, or deletes), these are recorded in the transaction log without modifying the original base data directly. Instead, they create new versions of the dataset.
    - Compression Over Time: Over time, these changes can be compacted into fewer files using operations like OPTIMIZE, which enhances performance by reducing small file overhead and improving query execution times
  - Delta Lake is the optimized storage layer that provides the foundation for tables in a lakehouse on Databricks. Delta Lake is open source software that extends Parquet data files with a file-based transaction log for ACID transactions and scalable metadata handling. Delta Lake runs on top of your existing data lake and is fully compatible with Apache Spark APIs.
    - Vacuum table snapshots is a command that removes old snapshots and other files from a table to free up storage space and improve system performance. We can also vacuum a delta table. 

- Snowflake is a cloud data warehouse that can store and analyze all your data records in one place. It can automatically scale up/down its compute resources to load, integrate, and analyze data. Snowflake supports both transformation during (ETL) or after loading (ELT). Snowflake uses OLAP (Online Analytical Processing) as a foundational part of its database schema and acts as a single, governed, and immediately queryable source for your data.
  - **Star vs Snowflake vs OBT Schema**:
    - In **star schema**, The fact tables and the dimension tables are contained. It's design is simple but may have high data redundancy.
    - In **snowflake schema**, The fact tables, dimension tables as well as sub dimension tables are contained. It's design is complex & has more foreign keys but less data redundancy. To simply put, Snowflake schema is a more detailed & branched out version of star schema. 
    - **One big table** is a concept in which data is stored in a single table rather than being partitioned across multiple tables. This approach can offer several advantages, including simpler data management, faster query performance, and easier scalability. [Star vs Snowflake schema _vl](https://www.youtube.com/watch?v=hQvCOBv_-LE&ab_channel=codebasics) 

- Pinot is a column-oriented, open-source, distributed data store written in Java. Pinot is designed to execute OLAP (online analytical processing) queries with low latency.


----------------------------------------------------------------------





















