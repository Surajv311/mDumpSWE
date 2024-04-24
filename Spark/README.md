
# Spark

Apache Spark is a data processing framework that can quickly perform processing tasks on very large data sets, and can also distribute data processing tasks across multiple computers, either on its own or in tandem with other distributed computing tools. 

- At the heart of Apache Spark is the concept of the **Resilient Distributed Dataset (RDD)**, a programming abstraction that represents an immutable collection of objects that can be split across a computing cluster. Operations on the RDDs can also be split across the cluster and executed in a parallel batch process, leading to fast and scalable parallel processing. 
- Apache Spark turns the user’s data processing commands into a **Directed Acyclic Graph, or DAG**. The DAG is Apache Spark’s scheduling layer; it determines what tasks are executed on what nodes and in what sequence. 
- Spark runs in a distributed fashion by combining a **Driver** core process that splits a Spark application into tasks and distributes them among many **Executor** processes that do the work. These executors can be scaled up and down as required for the application’s needs. 

Concept of application, job, stage and task in Spark:
- **Application** - A user program built on Spark using its APIs. It consists of a driver program and executors on the cluster.
- **Job** - A parallel computation consisting of multiple tasks that gets spawned in response to a Spark action (e.g., save(), collect()). During interactive sessions with Spark shells, the driver converts your Spark application into one or more Spark jobs. It then transforms each job into a DAG. This, in essence, is Spark’s execution plan, where each node within a DAG could be a single or multiple Spark stages.
- **Stage** - Each job gets divided into smaller sets of tasks called stages that depend on each other. As part of the DAG nodes, stages are created based on what operations can be performed serially or in parallel. Not all Spark operations can happen in a single stage, so they may be divided into multiple stages. Often stages are delineated on the operator’s computation boundaries, where they dictate data transfer among Spark executors.
- **Task** - A single unit of work or execution that will be sent to a Spark executor. Each stage is comprised of Spark tasks (a unit of execution), which are then federated across each Spark executor; each task maps to a single core and works on a single partition of data. As such, an executor with 16 cores can have 16 or more tasks working on 16 or more partitions in parallel, making the execution of Spark’s tasks exceedingly parallel. 
Spark processes queries by distributing data over multiple nodes and calculating the values separately on every node. However, occasionally, the nodes need to exchange the data. After all, that’s the purpose of Spark - processing data that doesn’t fit on a single machine. [Application, Job, Stage in Spark _al](https://stackoverflow.com/questions/42263270/what-is-the-concept-of-application-job-stage-and-task-in-spark)

By default, Spark/Pyspark creates **partitions** that are equal to the number of CPU cores in the machine. Data of each partition resides in a single machine. Spark/Pyspark creates a task for each partition. Spark shuffle operations move the data from one partition to other partitions. Partitioning is an expensive operation as it creates a data shuffle (Data could move between the nodes). Partition is a logical division of the data , this idea is derived from Map Reduce (split). Logical data is specifically derived to process the data. Small chunks of data also it can support scalability and speed up the process. Input data, intermediate data, and output data everything is partitioned RDD. Spark uses the map-reduce API to do the partition the data. Do not partition by columns having high cardinality. For example, don’t use your partition key such as roll no, employee id etc , Instead your state code, country code etc. Partition data by specific columns that will be mostly used during filter and group by operations. [Spark Partition _al](https://statusneo.com/everything-you-need-to-understand-data-partitioning-in-spark/)

**Shuffling** is the process of exchanging data between partitions as seen earlier. As a result, data rows can move between worker nodes when their source partition and the target partition reside on a different machine. Spark doesn’t move data between nodes randomly. Shuffling is a time-consuming operation, so it happens only when there is no other option. Spark nodes read chunks of the data (data partitions), but they don’t send the data between each other unless they need to. When do they do it? When you explicitly request data repartitioning (using the repartition functions), when you join DataFrames or group data by a column value. When we join the data in Spark, it needs to put the data in both DataFrames in buckets. Those buckets are calculated by hashing the partitioning key (the column(s) we use for joining) and splitting the data into a predefined number of buckets. We can control the number of buckets using the spark.sql.shuffle.partitions parameter. The same hashing and partitioning happen in both datasets we join. The corresponding partitions from both datasets are transferred to the same worker node. The goal is to have the data locally on the same worker before we start joining the values. Spark partitions the data also when we run a grouping operation and calculate an aggregate. This time we have only one dataset, but we still need the data that belongs to a single group on a single worker node. Otherwise, we couldn’t calculate the aggregations. Of course, some aggregations, like calculating the number of elements in a group or a sum of the parts, don’t require moving data to a single node. If we calculate the sum on every node separately and then move the results to a single node, we can calculate the final sum. 

Problem with Shuffling: What if one worker node receives more data than any other worker? You will have to wait for that worker to finish processing while others do nothing. What’s even worse, the worker may fail, and the cluster will need to repeat a part of the computation. You can avoid such problems by enabling **speculative execution** - use the spark.speculation parameter. With this feature enabled, the idle workers calculate a copy of long-running tasks, and the cluster uses the results produced by the worker who finished sooner. When does one worker receive more data than others?: It happens when one value dominates the partitioning key (for example, the null). All rows with the same partitioning key value must be processed by the same worker node (in the case of partitioning). So if we have 70% of null values in the partitioning key, one node will get at least 70% of the rows. When this happens, we have two options: First, we can isolate the dominating value by filtering it out from the DataFrame. After filtering, we can calculate the aggregate using the remaining rows. After that, we can calculate the aggregate of the filtered out value separately. The second solution is to create a **surrogate partitioning key** by combining multiple columns or generating an artificial partitioning value. Such a key should help us uniformly distribute the work across all worker nodes. [Spark Shuffling _al](https://mikulskibartosz.name/shuffling-in-apache-spark)

In Spark partitions: 
If partition count: 
- Too few partitions You will not utilize all of the cores available in the cluster.
- Too many partitions There will be excessive overhead in managing many small tasks (remember Driver -> Job -> Stage -> Task). 

(Or)

If partition size:
- Too small - slow read time downstream, large task creation overhead, driver OOM 
- Too large - long computation time, slow write times, executor/worker OOM [Spark basics partitions _vl](https://www.youtube.com/watch?v=hvF7tY2-L3U)

Between the two the first one is far more impactful on performance. Scheduling too many small tasks has a relatively small impact at this point for partition counts below 1000. If you have on the order of tens of thousands of partitions then spark gets very slow. Once the user has submitted his job into the cluster, each partition is sent to a specific executor for further processing. Only one partition is processed by one executor at a time, so the size and number of partitions transferred to the executor are directly proportional to the time it takes to complete them. Thus the more partitions the more work is distributed to executors, with a smaller number of partitions the work will be done in larger pieces (and often faster).

As a note: Apache Spark supports two types of partitioning “hash partitioning” and “range partitioning”. [Partition types _vl](https://www.youtube.com/watch?v=BvyOJuik8FA&ab_channel=DataSavvy). The Apache Spark documentation recommends using 2-3 tasks per CPU core in the cluster. Therefore, if you have eight worker nodes and each node has four CPU cores, you can configure the number of partitions to a value between 64 and 96. By default, Spark creates one partition for each block of the file (blocks being 128MB by default in HDFS), but you can also ask for a higher number of partitions by passing a larger value.
RDD's as we know are collection of various data items that are so huge in size, that they cannot fit into a single node and have to be partitioned across various nodes. 

Spark automatically partitions RDDs and distributes the partitions across different nodes. A partition in spark is an atomic chunk of data (logical division of data) stored on a node in the cluster. Partitions are basic units of parallelism in Apache Spark.

Ways to manage partitions:
- **Repartition** operation: Under repartitioning meant the operation to reduce or increase the number of partitions in which the data in the cluster will be split. This process involves a full shuffle. Consequently, it is clear that repartitioning is an expensive process. In a typical scenario, most of the data should be serialized, moved, and deserialized.
- **Coalesce** operation: This operation reduces the number of partitions. It avoids full shuffle, instead of creating new partitions, it shuffles the data using default Hash Partitioner, and adjusts into existing partitions, this means it can only decrease the number of partitions. The executor can safely leave data on a minimum number of partitions, moving data only from redundant nodes. Therefore, it is better to use coalesce than repartition if you need to reduce the number of partitions. 
However, you should understand that you can drastically reduce the parallelism of your data processing — coalesce is often pushed up further in the chain of transformation and can lead to fewer nodes for your processing than you would like. 
(As a note: To avoid this, you can pass shuffle = true. There are three stages at the physical level where the number of partitions is important. They are input, shuffle, and output. [Spark partition tuning _al](https://luminousmen.com/post/spark-tips-partition-tuning))
So, it would go something like this:

```
Node 1 = 1,2,3
Node 2 = 4,5,6
Node 3 = 7,8,9
Node 4 = 10,11,12
Then coalesce down to 2 partitions:
Node 1 = 1,2,3 + (10,11,12)
Node 3 = 7,8,9 + (4,5,6)
Notice that Node 1 and Node 3 did not require its original data to move.
```

Note that coalesce results in partitions with different amounts of data (sometimes partitions that have much different sizes) and repartition results in roughly equal sized partitions. Coalesce may run faster than repartition, but unequal sized partitions are generally slower to work with than equal sized partitions. You'll usually need to repartition datasets after filtering a large data set.
    - `outputData.coalesce(1).write.parquet(outputPath)` will write with 1 worker. So, even though you give 10 CPU core, it will write with 1 worker (single partition). Problem will be if your file very big (10 gb or more). But can be used if you have small file (100 mb)
- **partitionBy operation**: So instead of coalesce and repartition functions, it will change the folder structure of the underlying data. Example, in a CSV data say we can partition the data by ‘country’ column, as it has low cardinality and more likely to be used as a filter condition. However, partitionBy has no control on how many part files will be created under each folder. In some use-case, you may want to create a single file per partitioned folders, for that you need to use repartition along with partitionBy as following:

```
scala>  DF.repartition($”country”).write.mode(“overwrite”).partitionBy(“country”).option(“header”,true).csv(“/Users/d0d02t4/Desktop/data/partition_by_test.csv”)
```

Useful links:
[Data partitioning spark _al](https://medium.com/@dipayandev/everything-you-need-to-understand-data-partitioning-in-spark-487d4be63b9c), [Spark repartition vs coalesce _al](https://stackoverflow.com/questions/31610971/spark-repartition-vs-coalesce)


Now, when you have a small dataset, then to run spark jobs for testing on them, in short you could use: [Spark Jobs on Small Test Datasets _al](https://luminousmen.com/post/how-to-speed-up-spark-jobs-on-small-test-datasets)

```
.master("local[1]")
.config("spark.sql.shuffle.partitions", 1)
.config("spark.default.parallelism", <number_of_cores>)
.config("spark.rdd.compress", "false")
.config("spark.shuffle.compress", "false")
.config("spark.dynamicAllocation.enabled", "false")
.config("spark.executor.cores", 1)
.config("spark.executor.instances", 1)
.config("spark.ui.enabled", "false")
.config("spark.ui.showConsoleProgress", "false")
``` 

- **Broadcast Join** is an optimization technique in the PySpark SQL engine that is used to join two DataFrames. This technique is ideal for joining a large DataFrame with a smaller one. With broadcast join, PySpark broadcast the smaller DataFrame to all executors and the executor keeps this DataFrame in memory and the larger DataFrame is split and distributed across all executors so that PySpark can perform a join without shuffling any data from the larger DataFrame as the data required for join colocated on every executor. [Normal vs Broadcast join _al](https://www.linkedin.com/pulse/apache-spark-101-shuffle-join-vs-broadcast-joins-shanoj-kumar-v-g779c/)

- **Salting** is a technique used in Apache Spark to evenly distribute data across partitions. It involves adding a random or unique identifier (called a "salt") to each record before performing operations like grouping or joining. This helps avoid data skew and improves parallelism in data processing.

- Spark uses two engines to optimize and run the queries - Catalyst and Tungsten, in that order. Catalyst basically generates an optimized physical query plan from the logical query plan by applying a series of transformations like predicate pushdown, column pruning, and constant folding on the logical plan. This optimized query plan is then used by Tungsten to generate optimized code, that resembles hand written code, by making use of Whole-stage Codegen functionality introduced in Spark 2.0. This functionality has improved Spark's efficiency by a huge margin from Spark 1.6, which used the traditional Volcano Iterator Model. [Spark engine _al](https://www.linkedin.com/pulse/catalyst-tungsten-apache-sparks-speeding-engine-deepak-rajak/)

- In **PySpark** (PySpark is the Python API for Apache Spark. It enables you to perform real-time, large-scale data processing in a distributed environment using Python), Python and JVM codes live in separate OS processes. 
  - PySpark uses Py4J, which is a framework that facilitates interoperation between the two languages, to exchange data between the Python and the JVM processes. When you launch a PySpark job, it starts as a Python process, which then spawns a JVM instance and runs some PySpark specific code in it. It then instantiates a Spark session in that JVM, which becomes the driver program that Spark sees. That driver program connects to the Spark master or spawns an in-proc one, depending on how the session is configured.
  - When you create RDDs or Dataframes, those are stored in the memory of the Spark cluster just as RDDs and Dataframes created by Scala or Java applications. Transformations and actions on them work just as they do in JVM, with one notable difference: anything, which involves passing the data through Python code, runs outside the JVM. So, if you create a Dataframe, and do something like: `df.select("foo", "bar").where(df["foo"] > 100).count()`, this runs entirely in the JVM as there is no Python code that the data must pass through. 
  - On the other side, if you do: `a = t.reduce(add)`, since the add operator is a Python one, the RDD gets serialised, then sent to one or more Python processes where the reduction is performed, then the result is serialised again and returned to the JVM, and finally transferred over to the Python driver process for the final reduction.

[Pyspark code run in jvm or python subprocess _al](https://stackoverflow.com/questions/61816236/does-pyspark-code-run-in-jvm-or-python-subprocess), 
[Pyspark internals _al](https://cwiki.apache.org/confluence/display/SPARK/PySpark+Internals)

- The `createOrReplaceTempView()` is used to create a temporary view/table from the Spark DataFrame or Dataset objects. It is part of Spark 2.0. In Spark 1.0 `registerTempTable()` was used. 
- Why spark faster than hadoop?: 
  - Spark is faster than Hadoop MapReduce due to in-memory data processing, reducing the need for disk I/O and improving performance for iterative algorithms.
  - Spark efficiently manages memory and can spill data to disk if the memory is not sufficient, allowing it to handle larger datasets than Hadoop MapReduce.
  - Spark uses its Catalyst Query Planner, which optimizes query execution plans, leading to better performance and more efficient resource utilization.
- Spark does lazy evaluation. 
  - For transformations, Spark adds them to a DAG of computation and only when driver requests some data, does this DAG actually gets executed. One advantage of this is that Spark can make many optimization decisions after it had a chance to look at the DAG in entirety. This would not be possible if it executed everything as soon as it got it. For example -- if you executed every transformation eagerly, what does that mean? Well, it means you will have to materialize that many intermediate datasets in memory. This is evidently not efficient -- for one, it will increase your GC costs. (Because you're really not interested in those intermediate results as such. Those are just convenient abstractions for you while writing the program.) So, what you do instead is -- you tell Spark what is the eventual answer you're interested and it figures out best way to get there. [spark lazy evaluation _al](https://stackoverflow.com/questions/38027877/spark-transformation-why-is-it-lazy-and-what-is-the-advantage)
  - Lazy Evaluation: It is an evaluation strategy which holds the evaluation of an expression until its value is needed. It avoids repeated evaluation. 
- [Spark RDD vs Dataframe vs Dataset _al](https://sparkbyexamples.com/spark/spark-rdd-vs-dataframe-vs-dataset/):

| Context             | RDDs                                                                                                                  | Dataframes                                                                                                                                   | Dataset                                                                                                                        |
|---------------------|-----------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| Interoperability    | Can be easily converted to DataFrames and vice versa using the `toDF()` and `rdd()` methods.                        | Can be easily converted to RDDs and Datasets using the `rdd()` and `as[]` methods respectively.                                             | Can be easily converted to DataFrames using the `toDF()` method, and to RDDs using the `rdd()` method.                         |
| Type safety         | Not type-safe                                                                                                        | DataFrames are not type-safe. When trying to access a column that doesn't exist, Dataframe APIs do not support compile-time error detection. | Datasets are type-safe. Datasets provide compile-time type checking, helping to catch errors early in the development process. |
| Performance         | Low-level API with more control over the data, but lower-level optimizations compared to DataFrames and Datasets.    | Optimized for performance, with high-level API, Catalyst optimizer, and code generation.                                                     | Datasets are faster than DataFrames because they use JVM bytecode generation, leveraging the JVM’s optimization capabilities.   |
| Memory Management  | Provide full control over memory management, as they can be cached in memory or disk as per the user’s choice.       | Have more optimized memory management, with a Spark SQL optimizer that helps to reduce memory usage.                                           | Support most available data types.                                                                                           |
| Serialization      | Uses Java serialization when distributing data within the cluster or writing data to disk.                          | DataFrames use a generic encoder that can handle any object type.                                                                           | Datasets are serialized using specialized encoders optimized for performance.                                                  |
| APIs                | Provide a low-level API requiring more code to perform transformations and actions on data.                        | Provide a high-level API making it easier to perform transformations and actions on data.                                                   | Datasets provide a richer set of APIs, supporting both functional and object-oriented programming paradigms.                 |
| Schema enforcement | Do not have an explicit schema, and are often used for unstructured data.                                             | DataFrames enforce schema at runtime. Have an explicit schema describing the data and its types.                                           | Datasets enforce schema at compile time, catching errors in data types or structures earlier in the development cycle.       |
| Programming Language Support | RDD APIs are available in Java, Scala, Python, and R languages.                                                  | Available in Java, Python, Scala, and R languages.                                                                                            | Only available in Scala and Java.                                                                                            |
| Optimization       | No inbuilt optimization engine is available in RDD.                                                                  | It uses a Catalyst optimizer for optimization.                                                                                              | It includes the concept of a Dataframe Catalyst optimizer for optimizing query plans.                                            |
| Data types         | Suitable for structured and semi-structured data processing with a higher level of abstraction.                     | DataFrames support most available data types.                                                                                               | Datasets support all data types supported by DataFrames and also support user-defined types.                                  |
| Use Cases          | Suitable for low-level data processing and batch jobs that require fine-grained control over data.                   | Suitable for structured and semi-structured data processing with a higher level of abstraction.                                               | Suitable for high-performance batch and stream processing with strong typing and functional programming.                      |

- Can we write files with specific name in Pyspark than the usual way it writes with names like: `part-000...parquet`?
  - Because you are using spark, your data is spread across multiple nodes, computing in parallel and sent in part to your directory. One of the reasons to use spark is that the data cannot be stored locally. So this is how the data is output. The larger your file the larger more "part" files should come through.
  - Pyspark stores the files in smaller chunks and processes across worker nodes. You can compute data in chunks and can write it as a single file using coalesce() but do not have the luxury to write with specific name, as with coalesce, it sits on 1 worker and writes. You can use dbutils, or other ways to rename file. 
  - A way which I (Suraj) figured out to do it in S3 reading online articles: 

```
Pseudocode: 

After writing a single file with coalesce() function pyspark with name part-000.json. I will rename it as 0.json. 

def get_dbutils(spark):
    try:
        from pyspark.dbutils import DBUtils
        dbutils = DBUtils(spark)
    except ImportError:
        import IPython
        dbutils = IPython.get_ipython().user_ns["dbutils"]
    return dbutils

def some_fun_process():
## some process - to generate a single part-000 file with coalesce() spark ##
## now renaming it 

    dbutils = get_dbutils(spark)
        try:
            files = dbutils.fs.ls(target_path)
        except Exception as err:
            _log.info(f'Error when listing files in S3 using dbutils: {err}')
            raise Exception('Files cannot be listed. Ensure there are files written in dir to rename them accordingly')
        _log.info(f'Copying file in same location with updated name') 
        for file in files:
            if file.name.endswith('json'):
                file_name = file.name
        dbutils.fs.cp(target_path + f'/{file_name}', target_path + '/0.json')
        _log.info(f'Deleting redundant files') 
        files_to_remove = [file.path for file in files if file.name.endswith(".json") and file.name != "0.json"] # deleting all files ending with .json name except 0.json file which is renamed/updated file
        for file_path in files_to_remove: # Remove all json files except '0.json'
            dbutils.fs.rm(file_path)
```

- Spark session: 
  - You should always close your SparkSession when you are done with its use (even if the final outcome were just to follow a good practice of giving back what you've been given). Closing a SparkSession may trigger freeing cluster resources that could be given to some other application. SparkSession is a session and as such maintains some resources that consume JVM memory. You can have as many SparkSessions as you want (see SparkSession.newSession to create a session afresh) but you don't want them to use memory they should not if you don't use one and hence close the one you no longer need.
  - You can have as many SparkSessions as needed. You can have one and only one SparkContext on a single JVM, but the number of SparkSessions is pretty much unbounded.
  - [Spark session close _al](https://stackoverflow.com/questions/44058122/what-happens-if-sparksession-is-not-closed), [Total spark sessions _al](https://stackoverflow.com/questions/47723761/how-many-sparksessions-can-a-single-application-have)

```
To check if there is an active spark session: 
spark = SparkSession.builder.appName("ProcessEvent").getOrCreate()
spark.stop()
if (spark.getActiveSession()):
    print('yes')
else:
    print('no')
```

- Spark UDFs are executed at workers, so the print statements inside them won't show up in the output (which is from the driver). The best way to handle issues with UDFs is to change the return type of the UDF to a struct or a list and pass the error information along with the returned output. Eg, sample code: [UDF print code eg _al](https://stackoverflow.com/questions/54252682/pyspark-udf-print-row-being-analyzed)

```
import pyspark.sql.functions as F
def myF(input):
  myF.lineNumber += 1
  if (somethingBad):
    res += 'Error in line {}'.format(myF.lineNumber)
  return res
myF.lineNumber = 0
myF_udf =  F.udf(myF, StringType())
```

- 

----------------------------------------------------------------------





















