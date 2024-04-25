
# Hadoop

Hadoop architecture comprises four key components: 

- **HDFS** (Hadoop Distributed File System for distributed storage):
The **NameNode** serves as the master in a Hadoop cluster, overseeing the **DataNodes** (slaves). Its primary role is to manage metadata, such as transaction logs tracking user activity. The NameNode instructs DataNodes on operations like creation, deletion, and replication. DataNodes, acting as slaves, are responsible for storing data in the Hadoop cluster. It’s recommended to have DataNodes with high storage capacity to accommodate a large number of file blocks. In Hadoop, data is stored in blocks, each typically set to a default size of 128 MB or 256 MB. This block size ensures efficient storage and processing of large datasets. Replication in HDFS ensures data availability and fault tolerance. By default, Hadoop sets a replication factor of 3, creating copies of each file block for backup purposes. Rack Awareness in Hadoop involves the physical grouping of nodes in the cluster. This information is used by the NameNode to select the closest DataNode, reducing network traffic and optimizing read/write operations.
- **MapReduce** (for distributed processing): MapReduce process involves a client that submits a job to the Hadoop MapReduce Manager. The job is then divided into job parts (smaller tasks) by the Hadoop MapReduce Master. Input data is processed through Map() and Reduce() functions, resulting in output data. The Map function breaks down data into key-value pairs, which are then further processed by the Reduce function. Multiple clients can continuously submit jobs for processing. The map reduce functions are idempotent, i.e: output remains constant irrespective of multiple runs. [Map Reduce function _vl](https://www.youtube.com/watch?v=cHGaQz0E7AU)
- **YARN** (Yet Another Resource Negotiator): YARN, or Yet Another Resource Negotiator, is a vital component in the Hadoop framework, overseeing resource management and job scheduling. It separates these functions, employing a global Resource Manager and ApplicationMasters for individual applications. The NodeManager monitors container resource usage, providing data for efficient allocation of CPU, memory, disk, and connectivity by the ResourceManager. Features: multi-tenancy, scalability, cluster-utilization, etc. [Hadoop architecture _al](https://www.interviewbit.com/blog/hadoop-architecture/)

----------------------------------------------------------------------





















