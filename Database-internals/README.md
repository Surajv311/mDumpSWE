
# Database_internals

- **Tables**:
  - Thay are simply a general-purpose data structure which can be used to represent relations. 

- **Database engine**:
  - It is software that handles the data structure and physical storage and management of data. Different storage engines have different features and performance characteristics, so a single DBMS could use multiple engines. Ideally, they should not affect the logical view of data presented to users of the DBMS. [Db engine _al](https://dba.stackexchange.com/questions/4603/what-exactly-is-a-database-engine), [RDBMS & DB Engine _al](https://stackoverflow.com/questions/42242931/what-is-rdbms-and-database-engine).

- **DB Schema vs Table Schema**:
  - Database Schema: It refers to the overall blueprint or logical structure of a database. It defines the structure of the entire database, including tables, views, relationships, constraints, indexes, and other database objects. The database schema provides a high-level view of how data is organized and the relationships between different components. In a database schema, you define the following:
    - Tables and their relationships
    - Views that represent subsets of data
    - Indexes to optimize data retrieval
    - Constraints to enforce data integrity rules (such as unique keys or foreign keys)
    - Stored procedures, triggers, and functions
    - Permissions and access controls
  - Table Schema: A table schema, on the other hand, specifically refers to the structure of an individual table within the database. It defines the columns (fields) that make up the table, their data types, constraints, and other attributes. The table schema outlines the specifics of how data is stored within that particular table. In a table schema, you define the following:
    - Columns and their data types (e.g., integer, string, date)
    - Constraints on columns (e.g., primary key, unique constraints)
    - Default values for columns
    - Relationships with other tables (via foreign keys)
    - Indexes on specific columns for performance optimization
  - In summary, the key difference is that the "database schema" encompasses the entire structure of the database, including multiple tables, views, and other database objects, while the "table schema" focuses specifically on the structure and attributes of an individual table within the database.

- OLAP & OLTP databases: 
  - Purpose of online analytical processing (OLAP) is to analyze aggregated data.
  - Purpose of online transaction processing (OLTP) is to process database transactions. 
  - You use OLAP systems to generate reports, perform complex data analysis, and identify trends or reporting. In contrast, you use OLTP systems to process orders, update inventory, transactional processing and real-time updates, and manage customer accounts. [Olap, Oltp _al](https://aws.amazon.com/compare/the-difference-between-olap-and-oltp/)

- Normalization: The main purpose of database normalization is to avoid complexities, eliminate duplicates, and organize data in a consistent way. In normalization, the data is divided into several tables linked together with relationships. 1NF, 2NF, and 3NF are the first three types of database normalization. They stand for first normal form, second NF, and third NF, respectively. There are also 4NF, 5NF, 6NF - not commonly used.
  - 1 NF:
    - a single cell must not hold more than one value (atomicity)
    - there must be a primary key for identification
    - no duplicated rows or columns
    - each column must have only one value for each row in the table
  - 2 NF: 
    - it’s already in 1NF 
    - has no partial dependency. That is, all non-key attributes are fully dependent on a primary key
  - 3NF: 
    - be in 2NF 
    - have no transitive partial dependency

[Normalization in tables 1,2,3 nf](https://www.freecodecamp.org/news/database-normalization-1nf-2nf-3nf-table-examples/)

- Cardinality: Simply put, it refers to uniqueness of data contained in a column. Say, a column has lot of duplicated data (eg: "true" or "false"), it has low cardinality. Similarly, say having "id" of employees, would mean having high cardinality in id column. Cardinality can have effect on query performance. 

- (From Opensource Github repos knowledge extraction section | system-design-primer): 
  - **ACID** is a set of properties of relational database transactions.
    - Atomicity - Each transaction is all or nothing
    - Consistency - Any transaction will bring the database from one valid state to another
    - Isolation - Executing transactions concurrently has the same results as if the transactions were executed serially
    - Durability - Once a transaction has been committed, it will remain so
  - There are many techniques to scale a relational database: **master-slave replication**, **master-master replication**, **federation**, **sharding**, **denormalization**, and **SQL tuning**.
  - Replication (we have covered it in last section specially the master-slave, master-master)
  - Federation: Federation (or functional partitioning) splits up databases by function. For example, instead of a single, monolithic database, you could have three databases: forums, users, and products, resulting in less read and write traffic to each database and therefore less replication lag. Smaller databases result in more data that can fit in memory, which in turn results in more cache hits due to improved cache locality. With no single central master serializing writes you can write in parallel, increasing throughput.
    - (Disadvantages): Federation is not effective if your schema requires huge functions or tables. You'll need to update your application logic to determine which database to read and write. Joining data from two databases is more complex with a server link. Federation adds more hardware and additional complexity.
  - Sharding: Sharding distributes data across different databases such that each database can only manage a subset of the data. Taking a users database as an example, as the number of users increases, more shards are added to the cluster. Similar to the advantages of federation, sharding results in less read and write traffic, less replication, and more cache hits. Index size is also reduced, which generally improves performance with faster queries. If one shard goes down, the other shards are still operational, although you'll want to add some form of replication to avoid data loss. Like federation, there is no single central master serializing writes, allowing you to write in parallel with increased throughput. Common ways to shard a table of users is either through the user's last name initial or the user's geographic location.
    - (Disadvantage): You'll need to update your application logic to work with shards, which could result in complex SQL queries. Data distribution can become lopsided in a shard.Joining data from multiple shards is more complex. Sharding adds more hardware and additional complexity.
  - Denormalization: Denormalization attempts to improve read performance at the expense of some write performance. Redundant copies of the data are written in multiple tables to avoid expensive joins. Some RDBMS such as PostgreSQL and Oracle support materialized views which handle the work of storing redundant information and keeping redundant copies consistent. In most systems, reads can heavily outnumber writes 100:1 or even 1000:1. A read resulting in a complex database join can be very expensive, spending a significant amount of time on disk operations.
    - (Disadvantage): Data is duplicated. Constraints can help redundant copies of information stay in sync, which increases complexity of the database design. A denormalized database under heavy write load might perform worse than its normalized counterpart.
  - SQL Tuning: [Refer the link](https://github.com/donnemartin/system-design-primer?tab=readme-ov-file#sql-tuning)
    - Tighten up the schema, Use good indices, Avoid expensive joins, Partition tables, Tune the query cache
  - NoSQL is a collection of data items represented in a key-value store, document store, wide column store, or a graph database. Data is denormalized, and joins are generally done in the application code. Most NoSQL stores lack true ACID transactions and favor eventual consistency.
    - BASE is often used to describe the properties of NoSQL databases. In comparison with the CAP Theorem, BASE chooses availability over consistency.
      - Basically available - the system guarantees availability.
      - Soft state - the state of the system may change over time, even without input.
      - Eventual consistency - the system will become consistent over a period of time, given that the system doesn't receive input during that period.
    - In addition to choosing between SQL or NoSQL, it is helpful to understand which type of NoSQL database best fits your use case(s). 
      - A key-value store generally allows for O(1) reads and writes and is often backed by memory or SSD. Data stores can maintain keys in lexicographic order, allowing efficient retrieval of key ranges. Key-value stores can allow for storing of metadata with a value. Key-value stores provide high performance and are often used for simple data models or for rapidly-changing data, such as an in-memory cache layer. Since they offer only a limited set of operations, complexity is shifted to the application layer if additional operations are needed. A key-value store is the basis for more complex systems such as a document store, and in some cases, a graph database.
      - A document store is centered around documents (XML, JSON, binary, etc), where a document stores all information for a given object. Document stores provide APIs or a query language to query based on the internal structure of the document itself. Note, many key-value stores include features for working with a value's metadata, blurring the lines between these two storage types. Based on the underlying implementation, documents are organized by collections, tags, metadata, or directories. Although documents can be organized or grouped together, documents may have fields that are completely different from each other. Some document stores like MongoDB and CouchDB also provide a SQL-like language to perform complex queries. DynamoDB supports both key-values and documents. Document stores provide high flexibility and are often used for working with occasionally changing data.
      - A wide column store's basic unit of data is a column (name/value pair). A column can be grouped in column families (analogous to a SQL table). Super column families further group column families. You can access each column independently with a row key, and columns with the same row key form a row. Each value contains a timestamp for versioning and for conflict resolution. Google introduced Bigtable as the first wide column store, which influenced the open-source HBase often-used in the Hadoop ecosystem, and Cassandra from Facebook. Stores such as BigTable, HBase, and Cassandra maintain keys in lexicographic order, allowing efficient retrieval of selective key ranges. Wide column stores offer high availability and high scalability. They are often used for very large data sets.
      - In a graph database, each node is a record and each arc is a relationship between two nodes. Graph databases are optimized to represent complex relationships with many foreign keys or many-to-many relationships. Graphs databases offer high performance for data models with complex relationships, such as a social network. They are relatively new and are not yet widely-used; it might be more difficult to find development tools and resources. Many graphs can only be accessed with REST APIs.
    - Reasons for choosing SQL db: Structured data; Strict schema; Relational data; Need for complex joins; Transactions; Clear patterns for scaling; More established: developers, community, code, tools, etc; Lookups by index are very fast
    - Reasons for NoSQL db: Semi-structured data; Dynamic or flexible schema; Non-relational data; No need for complex joins; Store many TB (or PB) of data; Very data intensive workload; Very high throughput for IOPS

- **Database Indexing**: 
  - An index is just a data structure that makes the searching faster for a specific column in a database. This structure is usually a b-tree or a hash table but it can be any other logic structure. Another definition: Indexing is a way of sorting a number of records on multiple fields. Creating an index on a field in a table creates another data structure which holds the field value, and a pointer to the record it relates to. This index structure is then sorted, allowing Binary Searches to be performed on it. The downside to indexing is that these indices require additional space on the disk since the indices are stored together in a table using the MyISAM engine, this file can quickly reach the size limits of the underlying file system if many fields within the same table are indexed.
  - B-tree is a special type of self-balancing search tree in which each node can contain more than one key and can have more than two children. It is a generalized form of the binary search tree. It is also known as a height-balanced m-way tree. Time complexity for insert, delete, update operations is O(n). 
  - Classic example "Index in Books" Consider a "Book" of 1000 pages, divided by 10 Chapters, each section with 100 pages. Now, imagine you want to find a particular Chapter that contains a word "Alchemist". Without an index page, you have no other option than scanning through the entire book/Chapters. i.e: 1000 pages. This analogy is known as "Full Table Scan" in database world. enter image description here But with an index page, you know where to go! And more, to lookup any particular Chapter that matters, you just need to look over the index page, again and again, every time. After finding the matching index you can efficiently jump to that chapter by skipping the rest. But then, in addition to actual 1000 pages, you will need another ~10 pages to show the indices, so totally 1010 pages. Thus, the index is a separate section that stores values of indexed column + pointer to the indexed row in a sorted order for efficient look-ups.
  - Why is it needed: 
    - When data is stored on disk-based storage devices, it is stored as blocks of data. These blocks are accessed in their entirety, making them the atomic disk access operation. Disk blocks are structured in much the same way as linked lists; both contain a section for data, a pointer to the location of the next node (or block), and both need not be stored contiguously. Due to the fact that a number of records can only be sorted on one field, we can state that searching on a field that isn’t sorted requires a Linear Search which requires (N+1)/2 block accesses (on average), where N is the number of blocks that the table spans. If that field is a non-key field (i.e. doesn’t contain unique entries) then the entire tablespace must be searched at N block accesses. Whereas with a sorted field, a Binary Search may be used, which has log2 N block accesses. Also since the data is sorted given a non-key field, the rest of the table doesn’t need to be searched for duplicate values, once a higher value is found. Thus the performance increase is substantial.
  - How does it work: Firstly, let’s outline a sample database table schema;

```

Field name       Data type      Size on disk
id (Primary key) Unsigned INT   4 bytes
firstName        Char(50)       50 bytes
lastName         Char(50)       50 bytes
emailAddress     Char(100)      100 bytes

Note: char was used in place of varchar to allow for an accurate size on disk value. This sample database contains five million rows and is unindexed. The performance of several queries will now be analyzed. These are a query using the id (a sorted key field) and one using the firstName (a non-key unsorted field).
```
    - Example 1 - sorted vs unsorted fields: Given our sample database of r = 5,000,000 records of a fixed size giving a record length of R = 204 bytes and they are stored in a table using the MyISAM engine which is using the default block size B = 1,024 bytes. The blocking factor of the table would be bfr = (B/R) = 1024/204 = 5 records per disk block. The total number of blocks required to hold the table is N = (r/bfr) = 5000000/5 = 1,000,000 blocks. A linear search on the id field would require an average of N/2 = 500,000 block accesses to find a value, given that the id field is a key field. But since the id field is also sorted, a binary search can be conducted requiring an average of log2 1000000 = 19.93 = 20 block accesses. Instantly we can see this is a drastic improvement. Now the firstName field is neither sorted nor a key field, so a binary search is impossible, nor are the values unique, and thus the table will require searching to the end for an exact N = 1,000,000 block accesses. It is this situation that indexing aims to correct. Given that an index record contains only the indexed field and a pointer to the original record, it stands to reason that it will be smaller than the multi-field record that it points to. So the index itself requires fewer disk blocks than the original table, which therefore requires fewer block accesses to iterate through. The schema for an index on the firstName field is outlined below;

```

Field name       Data type      Size on disk
firstName        Char(50)       50 bytes
(record pointer) Special        4 bytes

Note: Pointers in MySQL are 2, 3, 4 or 5 bytes in length depending on the size of the table.
```
    - Example 2 - indexing: Given our sample database of r = 5,000,000 records with an index record length of R = 54 bytes and using the default block size B = 1,024 bytes. The blocking factor of the index would be bfr = (B/R) = 1024/54 = 18 records per disk block. The total number of blocks required to hold the index is N = (r/bfr) = 5000000/18 = 277,778 blocks. Now a search using the firstName field can utilize the index to increase performance. This allows for a binary search of the index with an average of log2 277778 = 18.08 = 19 block accesses. To find the address of the actual record, which requires a further block access to read, bringing the total to 19 + 1 = 20 block accesses, a far cry from the 1,000,000 block accesses required to find a firstName match in the non-indexed table.
    - When should it be used?: Given that creating an index requires additional disk space (277,778 blocks extra from the above example, a ~28% increase), and that too many indices can cause issues arising from the file systems size limits, careful thought must be used to select the correct fields to index. Since indices are only used to speed up the searching for a matching field within the records, it stands to reason that indexing fields used only for output would be simply a waste of disk space and processing time when doing an insert or delete operation, and thus should be avoided. Also given the nature of a binary search, the cardinality or uniqueness of the data is important. Indexing on a field with a cardinality of 2 would split the data in half, whereas a cardinality of 1,000 would return approximately 1,000 records. With such a low cardinality the effectiveness is reduced to a linear sort, and the query optimizer will avoid using the index if the cardinality is less than 30% of the record number, effectively making the index a waste of space. [How indexing works _al](https://stackoverflow.com/questions/1108/how-does-database-indexing-work). As a note: **Secondary indexing** is a database management technique used to create additional indexes on data stored in a database. [Query time observation with and without index _vl](https://www.youtube.com/watch?v=-qNSXK7s7_w)

- **Clustered & Non clustered Index**: With a clustered index the rows are stored physically (physically as in the actual bits stored on the disk) on the disk in the same order as the index. Therefore, there can be only one clustered index. With a non clustered index there is a second list that has pointers to the physical rows. You can have many non clustered indices, although each new index will increase the time it takes to write new records. It is generally faster to read from a clustered index if you want to get back all the columns. You do not have to go first to the index and then to the table. Writing to a table with a clustered index can be slower, if there is a need to rearrange the data. [Clustered  & Non clustered indexing _al](https://stackoverflow.com/questions/1251636/what-do-clustered-and-non-clustered-index-actually-mean)

(Note: Details about SQL functions and constructs in another section)

- [VIEW Tables _al](https://stackoverflow.com/questions/6015175/difference-between-view-and-table-in-sql): A view is a virtual table whose contents are defined by a query. Unless indexed, a view does not exist as a stored set of data values in a database. Instead of sending the complex query to the database all the time, you can save the query as a view and then SELECT * FROM view. You can think of a view as a "saved select statement" that you can repeat. It's not really a table; even though some databases allow to create views that have a real table beneath, it's really just a SELECT statement which returns results.
  - You can think of a view as a virtual table that does not store any data, but only references the underlying tables or views. You can create a view using the CREATE VIEW statement, and then use it like a regular table in your queries.
  - Eg: `CREATE or REPLACE VIEW table_views.employee_info AS SELECT employees_table.name::varchar(100), employees_table.salary::varchar(100) FROM employee_schema.employees_table;`. It is recommended to typecast datatypes to columns when creating view to avoid any mismatch. 
  - Materialized VIEW: A materialized view in SQL is a special type of view that stores the result of a query in a physical table. Unlike a regular view, a materialized view does not update automatically when the underlying tables or views change. Instead, you have to refresh the materialized view manually or on a schedule using the REFRESH MATERIALIZED VIEW statement.
  - The main difference between views and materialized views is that views are dynamic and materialized views are static. This means that views always reflect the latest data from the underlying tables or views, while materialized views only show the data from the last refresh. Therefore, views are more suitable for queries that need real-time data, while materialized views are more suitable for queries that need precomputed data. Another difference is that views are more lightweight and flexible, while materialized views are more resource-intensive and rigid. This means that views do not take up any storage space or require any maintenance, while materialized views do. However, views also depend on the availability and performance of the underlying tables or views, while materialized views do not. Therefore, views are more convenient for creating temporary or ad hoc queries, while materialized views are more reliable for creating permanent or recurring queries.
  - Both views and materialized views can improve query performance by simplifying them and reducing the amount of data to process. For instance, you can filter out irrelevant or sensitive data, join multiple tables into one virtual table, aggregate or calculate data, or rename or reformat columns or values. By using views or materialized views, you can avoid repeating complex or lengthy queries every time you need the same data; instead, you can use a simple query on the view or materialized view. However, the performance benefits of views and materialized views depend on several factors such as the size and frequency of the underlying data, the complexity and frequency of queries, and the configuration and optimization of the database. [Materialized Views _al](https://www.linkedin.com/advice/3/what-materialized-view-how-does-differ-from-dpgbc)

#### Timeseries DB

- A time series database (TSDB) is a database optimized for time-stamped or time series data. Time series data is often a continuous flow of data like measurements from sensors and intraday stock prices. A time-series database lets you store large volumes of timestamped data in a format that allows fast insertion and fast retrieval to support complex analysis on that data.
- TSDBs work by capturing a set of fixed values along with a set of dynamic values. As a simple example, in an oil well where many metrics of the rig are captured, one set of data points might have the label “Oil Pressure Rig #1” and the associated dynamic values would be the pressure measurement along with the timestamp. This example time series data is useful for tracking trends in the oil pressure which, when analyzed along with other metrics, could lead to predictions on maintenance needs as well as decisions on the abandonment of the well. These records are written to a storage medium in a format that allows fast time-based reads and writes.
- The time series data is typically sent in batches or streams over a network protocol such as TCP or UDP. Upon receiving the data, the TSDB performs data validation, parsing, and tagging to ensure that the data is in the correct format and can be efficiently indexed and queried.
- The data model of a TSDB is typically columnar, meaning that each column represents a time series or a metric. Once the data is validated and parsed, the TSDB stores it in a compressed, columnar format optimized for storage and retrieval efficiency.
- The storage engine typically uses a combination of in-memory and disk-based storage to balance performance and storage efficiency. Some TSDBs also use compression techniques such as delta encoding or run-length encoding to further optimize storage.
- To enable efficient querying of large datasets, the TSDB uses indexing mechanisms to organize the data by timestamp and tags. 
- TSDBs are designed to store time-series data for long periods of time. To optimize storage, the TSDB supports data retention policies that allow you to configure how long data is stored before it is deleted or archived. Some TSDBs also support data compression and downsampling techniques to optimize storage for longer retention periods.

[TSDB internals _al](https://medium.com/@vinciabhinav7/whats-tsdb-part-2-concepts-and-example-ce12a4c8be9f)

----------------------------------------------------------------------





















