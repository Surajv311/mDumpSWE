## Spark: The Definitive Guide: Big Data Processing Made Simple (Matei Zaharia)

#### Interesting points/notes:

- Note that in some places, I've googled/chatgpt'd few terms/reordered explanations and added here in the README for understanding. 

---------------------------------

- Chapter 1: What Is Apache Spark?
  - Apache Spark is a unified computing engine and a set of libraries for parallel data processing on computer clusters.
  - For example, if you load data using a SQL query and then evaluate a machine learning model over it using Spark’s ML library, the engine can combine these steps into one scan over the data. The combination of general APIs and high-performance execution, no matter how you combine them, makes Spark a powerful platform for interactive and production applications. At the same time that Spark strives for unification, it carefully limits its scope to a computing engine. By this, we mean that Spark handles loading data from storage systems and performing computation on it, not permanent storage as the end itself. However, Spark neither stores data long term itself, nor favors one over another. The key motivation here is that most data already resides in a mix of storage systems. Data is expensive to move so Spark focuses on performing computations over the data, no matter where it resides. Spark’s focus on computation makes it different from earlier big data software platforms such as Apache Hadoop. ***Hadoop included both a storage system (the Hadoop file system, designed for low-cost storage over clusters of commodity servers) and a computing system (MapReduce), which were closely integrated together***. However, this choice makes it difficult to run one of the systems without the other. For most of their history, computers became faster every year through processor speed increases: the new processors each year could run more instructions per second than the previous year’s. As a result, applications also automatically became faster every year, without any changes needed to their code. This trend led to a large and established ecosystem of applications building up over time, most of which were designed to run only on a single processor. These applications rode the trend of improved processor speeds to scale up to larger computations and larger volumes of data over time. ***Unfortunately, this trend in hardware stopped around 2005: due to hard limits in heat dissipation, hardware developers stopped making individual processors faster, and switched toward adding more parallel CPU cores all running at the same speed***. This change meant that suddenly applications needed to be modified to add parallelism in order to run faster, which set the stage for new programming models such as Apache Spark. 
  - On top of that, the technologies for storing and collecting data did not slow down appreciably in 2005, when processor speeds did. ***The cost to store 1 TB of data continues to drop by roughly two times every 14 months***, meaning that it is very inexpensive for organizations of all sizes to store large amounts of data. Moreover, many of the technologies for collecting data (sensors, cameras, public datasets, etc.) continue to drop in cost and improve in resolution. For example, camera technology continues to improve in resolution and drop in cost per pixel every year, to the point where a 12-megapixel webcam costs only $3 to $4; this has made it inexpensive to collect a wide range of visual data, whether from people filming video or automated sensors in an industrial setting. Moreover, cameras are themselves the key sensors in other data collection devices, such as telescopes and even gene-sequencing machines, driving the cost of these technologies down as well.
  - The end result is a world in which collecting data is extremely inexpensive—many organizations today even consider it negligent not to log data of possible relevance to the business—but processing it requires large, parallel computations, often on clusters of machines. Moreover, in this new world, the software developed in the past 50 years cannot automatically scale up, and neither can the traditional programming models for data processing applications, creating the need for new programming models. It is this world that Apache Spark was built for.
  - ***Apache Spark began at UC Berkeley in 2009*** as the Spark research project, which was first published the following year in a paper entitled “Spark: Cluster Computing with Working Sets” by ***Matei Zaharia***, Mosharaf Chowdhury, Michael Franklin, Scott Shenker, and Ion Stoica of the UC Berkeley AMPlab. 

---------------------------------

- Chapter 2: A Gentle Introduction to Spark
  - Typically, when you think of a “computer” you think about one machine sitting on your desk at home or at work. This machine works perfectly well for watching movies or working with spreadsheet software. However, as many users likely experience at some point, there are some things that your computer is not powerful enough to per‐ form. One particularly challenging area is data processing. Single machines do not have enough power and resources to perform computations on huge amounts of information (or the user probably does not have the time to wait for the computation to finish). A cluster, or group, of computers, pools the resources of many machines together, giving us the ability to use all the cumulative resources as if they were a sin‐ gle computer. Now, a group of machines alone is not powerful, you need a framework to coordinate work across them. ***Spark does just that, managing and coordinating the execution of tasks on data across a cluster of computers. The cluster of machines that Spark will use to execute tasks is managed by a cluster manager like Spark’s standalone cluster manager, YARN, or Mesos.*** 
  - ***We then submit Spark Applications to these cluster managers, which will grant resources to our application so that we can complete our work. Spark Applications consist of a driver process and a set of executor processes. The driver process runs your main() function, sits on a node in the cluster, and is responsible for three things:***
    - maintaining information about the Spark Application; 
    - responding to a user’s program or input; and 
    - analyzing, distributing, and scheduling work across the executors (discussed momentarily). 
  - ***The driver process is absolutely essential—it’s the heart of a Spark Application and maintains all relevant information during the lifetime of the application.***
  - ***The executors are responsible for actually carrying out the work that the driver assigns them. This means that each executor is responsible for only two things:***
    - executing code assigned to it by the driver, and 
    - reporting the state of the computation on that executor back to the driver node.
  - Spark, in addition to its ***cluster mode, also has a local mode***. The driver and executors are simply processes, which means that they can live on the same machine or different machines. ***In local mode, the driver and executurs run (as threads) on your individual computer instead of a cluster***. 
  - The executors, for the most part, will always be running Spark code. However, the driver can be “driven” from a number of different languages through Spark’s language APIs - Java, Scala, Python, R (Spark has two commonly used R libraries: one as a part of Spark core (SparkR) and another as an R community-driven package (sparklyr))
  - There is a SparkSession object available to the user, which is the entrance point to running Spark code. ***When using Spark from Python or R, you don’t write explicit JVM instructions; instead, you write Python and R code that Spark translates into code that it then can run on the executor JVMs.***
  - Spark has two fundamental sets of APIs: 
    - the low-level “unstructured” APIs, and 
    - the higher-level structured APIs. 
  - You control your Spark Application through a ***driver process called the SparkSession***. The SparkSession instance is the way Spark executes user-defined manipulations across the cluster. There is a ***one-to-one correspondence between a SparkSession and a Spark Application***. You may have seen: <pyspark.sql.session.SparkSession at 0x7efda4c1ccd0>. 
  - A DataFrame is the most common Structured API and simply represents a table of data with rows and columns.
  - The reason for putting the data on more than one computer should be intuitive: either the data is too large to fit on one machine or it would simply take too long to perform that computation on one machine.
  - To allow every ***executor to perform work in parallel, Spark breaks up the data into chunks called partitions. A partition is a collection of rows that sit on one physical machine in your cluster***. A DataFrame’s partitions represent how the data is ***physically distributed*** across the cluster of machines during execution. ***If you have one partition, Spark will have a parallelism of only one, even if you have thousands of executors. If you have many partitions but only one executor, Spark will still have a parallelism of only one because there is only one computation resource.***
  - An important thing to note is that with DataFrames you do not (for the most part) manipulate partitions manually or individually. You simply specify high-level transformations of data in the physical partitions, and Spark determines how this work will actually execute on the cluster. Lower-level APIs do exist (via the RDD interface).
  - In Spark, the core data structures are immutable. To “change” a DataFrame, you need to instruct Spark how you would like to modify it to do what you want. These instructions are called ***transformations***. Transformations are the core of how you express your business logic using Spark. There are two types of transformations: 
    - those that specify narrow dependencies, and 
    - those that specify wide dependencies.
  - Transformations consisting of narrow dependencies (we’ll call them ***narrow transformations***) are those for which ***each input partition will contribute to only one output partition***.
  - A wide dependency (or ***wide transformation***) style transformation will have ***input partitions contributing to many output partitions***. You will often hear this referred to as a ***shuffle*** whereby Spark will exchange partitions across the cluster.
  - With narrow transformations, Spark will automatically perform an operation called ***pipelining*** meaning that if we specify multiple filters on DataFrames, they’ll all be performed in-memory. The same cannot be said for shuffles. ***When we perform a shuffle, Spark writes the results to disk.***
  - ***Lazy evaulation*** means that Spark will wait until the very last moment to execute the graph of computation instructions. In Spark, instead of modifying the data immediately when you express some operation, you build up a plan of transformations that you would like to apply to your source data. By waiting until the last minute to execute the code, Spark compiles this plan from your raw DataFrame transformations to a streamlined physical plan that will run as efficiently as possible across the cluster. This provides immense benefits because Spark can optimize the entire data flow from end to end. An example of this is something called ***predicate pushdown*** on Dataframes. If we build a large Spark job but specify a filter at the end that only requires us to fetch one row from our source data, the most efficient way to execute this is to access the single record that we need. Spark will actually optimize this for us by pushing the filter down automatically.
  - An '***action'*** instructs Spark to compute a result from a series of transformations.
  - Spark UI: The Spark UI displays information on the state of your Spark jobs, its environment, and cluster state. It’s very useful, especially for tuning and debugging.
  - ***Schema inference***, which means that we want Spark to take a best guess at what the schema of our DataFrame should be. To get the schema information, Spark reads in a little bit of the data and then attempts to parse the types in those rows according to the types available in Spark. Eg:

```
flightData2015 = spark\
                .read\
                .option("inferSchema", "true")\
                .option("header", "true")\
                .csv("/data/flight-data/csv/2015-summary.csv")
```

  - We can call ***explain*** on any Dataframe object to see the DataFrame’s lineage (or how Spark will execute this query). Eg: flightData2015.sort("count").explain()
  - By ***default, when we perform a shuffle, Spark outputs 200 shuffle partitions***. You can change it via: spark.conf.set("spark.sql.shuffle.partitions", "5")
  - Spark can run the same transformations, ***regardless of the language***, in the exact same way. 
  - With Spark SQL, you can register any DataFrame as a table or view (a temporary table) and query it using pure SQL. ***There is no performance difference between writing SQL queries or writing DataFrame code, they both “compile” to the same underlying plan that we specify in DataFrame code***. You can make any DataFrame into a table or view with one simple method call: flightData2015.createOrReplaceTempView("flight_data_2015")

```
# in Python
sqlWay = spark.sql("""
SELECT DEST_COUNTRY_NAME, count(1)
FROM flight_data_2015
GROUP BY DEST_COUNTRY_NAME
""")

dataFrameWay = flightData2015\
  .groupBy("DEST_COUNTRY_NAME")\
  .count()
  
sqlWay.explain()
dataFrameWay.explain()

Notice that these plans compile to the exact same underlying plan, i.e:
== Physical Plan ==
    *HashAggregate(keys=[DEST_COUNTRY_NAME#182], functions=[count(1)])
    +- Exchange hashpartitioning(DEST_COUNTRY_NAME#182, 5)
       +- *HashAggregate(keys=[DEST_COUNTRY_NAME#182], functions=[partial_count(1)])
          +- *FileScan csv [DEST_COUNTRY_NAME#182] ...
          
This execution plan is a directed acyclic graph (DAG) of transformations, each resulting in a new immutable DataFrame, on which we call an action to generate a result.
```

---------------------------------

- Chapter 3: A Tour of Spark’s Toolset
  - ***Spark-submit does one thing: it lets you send your application code to a cluster and launch it to execute there***. Upon submission, the application will run until it exits (completes the task) or encounters an error. ***You can do this with all of Spark’s support cluster managers including Standalone, Mesos, and YARN***.
  - spark-submit offers several controls with which you can specify the resources your application needs as well as how it should be run and its command-line arguments.

```
./bin/spark-submit \
      --master local \
      ./examples/src/main/python/pi.py 10
      
By changing the master argument of spark-submit, we can also submit the same application to a cluster running Spark’s standalone cluster manager, Mesos or YARN.
```

  - Type-Safe Structured APIs: Spark’s structured API called Datasets, for writing statically typed code in Java and Scala. ***The Dataset API is not available in Python and R, because those languages are dynamically typed.***
  - The Dataset API gives users the ability to assign a Java/Scala class to the records within a Data‐ Frame and manipulate it as a collection of typed objects, similar to a Java ArrayList or Scala Seq. The APIs available on Datasets are type-safe, meaning that you cannot accidentally view the objects in a Dataset as being of another class than the class you put in initially. This makes Datasets especially attractive for writing large applications.

```
Eg: 
// in Scala
case class Flight(DEST_COUNTRY_NAME: String, ORIGIN_COUNTRY_NAME: String, count: BigInt) 
val flightsDF = spark.read.parquet("/data/flight-data/parquet/2010-summary.parquet/") 
val flights = flightsDF.as[Flight]

// sample parquet would look like usual: 
DEST_COUNTRY_NAME	ORIGIN_COUNTRY_NAME		count
United States			Romania				15
United States			Croatia				1
United States			Ireland				344
// in Scala

flights.filter(flight_row => flight_row.ORIGIN_COUNTRY_NAME != "Canada") .map(flight_row => flight_row)
.take(5)
```

  - Other concepts: Spark Streaming, MLLib for ML models, etc. Lower-Level APIs are RDDs: ***Virtually everything in Spark is built on top of RDDs***. SparkR is a tool for running R on Spark. 

---------------------------------

- Chapter 4: Structured API Overview
  - ***Structured API*** are a tool for manipulating all sorts of data, from unstructured log files to semi-structured CSV files and highly structured Parquet files. These APIs refer to three core types of distributed collection APIs:
    - Datasets
    - DataFrames
    - SQL tables and views
  - The majority of the Structured APIs apply to both batch and streaming computation.
  - ***Spark is a distributed programming model in which the user specifies transformations. Multiple transformations build up a directed acyclic graph of instructions. An action begins the process of executing that graph of instructions, as a single job, by breaking it down into stages and tasks to execute across the cluster. The logical structures that we manipulate with transformations and actions are DataFrames and Datasets. To create a new DataFrame or Dataset, you call a transformation. To start computation or convert to native language types, you call an action.***
  - Spark has two notions of structured collections: DataFrames and Datasets. To Spark, DataFrames and Datasets represent immutable, lazily evaluated plans that specify what operations to apply to data residing at a location to generate some output. 
  - Tables and views are basically the same thing as DataFrames. We just execute SQL against them instead of DataFrame code.
  - A ***schema*** defines the column names and types of a DataFrame. You can define schemas manually or read a schema from a data source (often called ***schema on read***).
  - Internally, ***Spark uses an engine called Catalyst*** that maintains its own type information through the planning and processing of work.
  - ***Spark types map directly to the different language APIs that Spark maintains and there exists a lookup table for each of these in Scala, Java, Python, SQL, and R***. Even if we use Spark’s Structured APIs from Python or R, the majority of our manipulations will operate strictly on Spark types, not Python types.
  - For example, the following code does not perform addition in Scala or Python; it ***actually performs addition purely in Spark***:

```
# in Python
    df = spark.range(500).toDF("number")
    df.select(df["number"] + 10)
This addition operation happens because Spark will convert an expression written in an input language to Spark’s internal Catalyst representation of that same type information. It then will operate on that internal representation.
```

  - In essence, within the Structured APIs, there are two more APIs, the “untyped” DataFrames and the “typed” Datasets. DataFrames are untyped is slightly inaccurate; they have types, but Spark maintains them completely and only checks whether those types line up to those specified in the schema at runtime. Datasets, on the other hand, check whether types conform to the specification at compile time. Datasets are only available to Java Virtual Machine (JVM)–based languages (Scala and Java). 
  - ***DataFrames are simply Datasets of Type Row. The “Row” type is Spark’s internal representation of its optimized in-memory format for computation***. This format makes for highly specialized and efficient computation because rather than using JVM types, which can cause high garbage-collection and object instantiation costs, Spark can operate on its own internal format without incurring any of those costs. This format applies the same efficiency gains to all of Spark’s language APIs.
  - Columns represent a simple type like an integer or string, a complex type like an array or map, or a null value. A row is nothing more than a record of data.
  - Spark’s language bindings: (for Python type reference, similarly other langauge types)

<>Upload img on Python type inference<>

  - ***Overview of Structured API Execution***: 
    - Step 1: Write DataFrame/Dataset/SQL Code and execute it: This code is then submitted to Spark either through the console or via a submitted job. This code then passes through the Catalyst Optimizer, which decides how the code should be executed and lays out a plan for doing so before, finally, the code is run and the result is returned to the user.
    - Step 2: If valid code, Spark converts this to a Logical Plan: This logical plan only represents a set of abstract transformations that do not refer to executors or drivers, it’s purely to convert the user’s set of expressions into the most optimized version. It does this by converting user code into an unresolved logical plan. This plan is unresolved because although your code might be valid, the tables or columns that it refers to might or might not exist. Spark uses the ***catalog***, a repository of all table and DataFrame information, to resolve columns and tables in the analyzer. The analyzer might reject the unresolved logical plan if the required table or column name does not exist in the catalog. If the analyzer can resolve it, the result is passed through the Catalyst Optimizer, a collection of rules that attempt to optimize the logical plan by pushing down predicates or selections. Packages can extend the Catalyst to include their own rules for domain-specific optimizations.
    - Step 3: Spark transforms this Logical Plan to a Physical Plan, checking for optimizations along the way: After successfully creating an optimized logical plan, Spark then begins the physical planning process. The physical plan, often called a ***Spark plan***, specifies how the logical plan will execute on the cluster by generating different physical execution strategies and comparing them through a cost model. An example of the cost comparison might be choosing how to perform a given join by looking at the physical attributes of a given table (how big the table is or how big its partitions are).
    - Step 4: Spark then executes this Physical Plan (RDD manipulations) on the cluster: Physical planning results in a series of RDDs and transformations. This result is why you might have heard ***Spark referred to as a compiler*** —it takes queries in Data‐ Frames, Datasets, and SQL and compiles them into RDD transformations for you.

---------------------------------

- Chapter 5: Basic Structured Operations
  - For adhoc analysis, schema-on-read usually works just fine (***although at times it can be a bit slow with plain-text file formats like CSV or JSON***). However, this can also lead to precision issues like a long type incorrectly set as an integer when reading in a file. When using Spark for production ***Extract, Transform, and Load (ETL), it is often a good idea to define your schemas manually***, especially when working with untyped data sources like CSV and JSON because schema inference can vary depending on the type of data that you read in.
  - If you need to refer to a specific DataFrame’s column, you can use the ***col method*** on the specific DataFrame. As an added benefit, ***Spark does not need to resolve this column itself (during the analyzer phase) because we did that for Spark***: df.col("ABX")
  - When using an expression, the ***expr function*** can actually parse transformations and column references from a string and can subsequently be passed into further transformations. expr("someCol - 5") is the same transformation as performing col("someCol") - 5, or even expr("someCol") - 5.
  - In Spark, each row in a DataFrame is a single record. Spark represents this record as an object of type Row (discussed earlier). Spark manipulates Row objects using column expressions in order to produce usable values. ***Row objects internally represent arrays of bytes***. The byte array interface is never shown to users because we only use column expressions to manipulate them. df.first() - first row
  - You can create rows by manually instantiating a Row object with the values that belong in each column. It’s important to note that only DataFrames have schemas. Rows themselves do not have schemas. This means that if you create a Row manually, you must specify the values in the same order as the schema of the DataFrame to which they might be appended.

```
1) from pyspark.sql import Row
myRow = Row("Hello", None, 1, False)
Accessing data in rows is equally as easy: you just specify the position that you would like. 
# in Python
myRow[0]
myRow[2]
    
2) We can: add/remove, transform rows or columns, as well as change the order of rows based on the values in columns.

3) We can also create DataFrames on the fly by taking a set of rows and converting them to a DataFrame.
# in Python
from pyspark.sql import Row
from pyspark.sql.types import StructField, StructType, StringType, LongType 
myManualSchema = StructType([
      StructField("some", StringType(), True),
      StructField("col", StringType(), True),
      StructField("names", LongType(), False)
    ])
    myRow = Row("Hello", None, 1)
    myDf = spark.createDataFrame([myRow], myManualSchema)
    myDf.show()
    
4) select and selectExpr: You can use them to manipulate columns in your DataFrames. selectExpr allow you to do the DataFrame equivalent of SQL queries on a table of data. 
# in Python
You can select multiple columns select() 
# in Python: df.select("DEST_COUNTRY_NAME", "ORIGIN_COUNTRY_NAME").show(2)
# in SQL: SELECT DEST_COUNTRY_NAME, ORIGIN_COUNTRY_NAME FROM dfTable LIMIT 2

4.1) The alias method on the column:
# in Python: df.select(expr("DEST_COUNTRY_NAME AS destination")).show(2)
# in SQL: SELECT DEST_COUNTRY_NAME as destination FROM dfTable LIMIT 2
# in Python: df.select(expr("DEST_COUNTRY_NAME AS destination")).show(2) 
# in SQL: SELECT DEST_COUNTRY_NAME as destination FROM dfTable LIMIT 2

4.2) In this case, the preceding operation changes the column name back to its original name: 
# in Python: df.select(expr("DEST_COUNTRY_NAME as destination").alias("DEST_COUNTRY_NAME")).show(2)

5) Because select followed by a series of expr is such a common pattern, Spark has a shorthand for doing this efficiently using selectExpr: 
# in Python: df.selectExpr("DEST_COUNTRY_NAME as newColumnName", "DEST_COUNTRY_NAME").show(2)

5.1) We can treat selectExpr as a simple way to build up complex expressions that create new DataFrames. In fact, we can add any valid non-aggregating SQL statement, and as long as the columns resolve, it will be valid.
Other eg: 
# in Python: df.selectExpr(
"*", # all original columns
"(DEST_COUNTRY_NAME = ORIGIN_COUNTRY_NAME) as withinCountry")\ .show(2)
# in SQL: SELECT *, (DEST_COUNTRY_NAME = ORIGIN_COUNTRY_NAME) as withinCountry FROM dfTable LIMIT 2
Above will give below output: 
Giving an output like:
+-----------------+-------------------+-----+-------------+
|DEST_COUNTRY_NAME|ORIGIN_COUNTRY_NAME|count|withinCountry|
+-----------------+-------------------+-----+-------------+
|    United States|            Romania|   15|        false|
|    United States|            Croatia|    1|        false|
+-----------------+-------------------+-----+-------------+

5.2) With select expression, we can also specify aggregations over the entire DataFrame by taking advantage of the functions that we have. 
# in Python: df.selectExpr("avg(count)", "count(distinct(DEST_COUNTRY_NAME))").show(2) 
# in SQL: SELECT avg(count), count(distinct(DEST_COUNTRY_NAME)) FROM dfTable LIMIT 2

6) Sometimes, we need to pass explicit values into Spark that are just a value (rather than a new column). The way we do this is through literals.
from pyspark.sql.functions import lit 
# in Python: df.select(expr("*"), lit(1).alias("One")).show(2)
# in SQL: SELECT *, 1 as One FROM dfTable LIMIT 2

7) There’s also a more formal way of adding a new column to a DataFrame, and that’s by using the withColumn method on our DataFrame.
# in Python: df.withColumn("numberOne", lit(1)).show(2)
# in SQL: SELECT *, 1 as numberOne FROM dfTable LIMIT 2

7.1) Notice that the withColumn function takes two arguments: the column name and the expression that will create the value for that given row in the DataFrame. Other eg: 
df.withColumn("withinCountry", expr("ORIGIN_COUNTRY_NAME == DEST_COUNTRY_NAME")).show(2)

8) Renaming columns: df.withColumnRenamed("DEST_COUNTRY_NAME", "dest").columns

9) One thing that you might come across is reserved characters like spaces or dashes in column names.
Handling these means escaping column names appropriately. In Spark, we do this by using backtick (`) characters. 
# in Python: 
dfWithLongColName.selectExpr(
        "`This Long Column-Name`",
        "`This Long Column-Name` as `new col`").show(2) 
    dfWithLongColName.createOrReplaceTempView("dfTableLong")
# in SQL: SELECT `This Long Column-Name`, `This Long Column-Name` as `new col` FROM dfTableLong LIMIT 2

10) By default Spark is case insensitive, but: # in SQL: set spark.sql.caseSensitive true

11) Drop multiple columns: dfWithLongColName.drop("ORIGIN_COUNTRY_NAME", "DEST_COUNTRY_NAME")

12) Changing columns type: 
# Python: df.withColumn("count2", col("count").cast("long")) 
# SQL: SELECT *, cast(count as long) AS count2 FROM dfTable

13) To filter rows, we create an expression that evaluates to true or false. There are two methods to perform this operation: you can use 'where' or 'filter' and they both will perform the same operation and accept the same argument types when used with DataFrames. 
Way 1 Python: df.filter(col("count") < 2).show(2)
Way 2 Python: df.where("count < 2").show(2)
SQL: SELECT * FROM dfTable WHERE count < 2 LIMIT 2

13.1) Multiple filters: 
Python: df.where(col("count") < 2).where(col("ORIGIN_COUNTRY_NAME") != "Croatia").show(2)
SQL: SELECT * FROM dfTable WHERE count < 2 AND ORIGIN_COUNTRY_NAME != "Croatia" LIMIT 2

14) Distinct rows: 
Python: df.select("ORIGIN_COUNTRY_NAME", "DEST_COUNTRY_NAME").distinct().count() 
SQL: ELECT COUNT(DISTINCT(ORIGIN_COUNTRY_NAME, DEST_COUNTRY_NAME)) FROM dfTable

15) Random samples or fraction of rows: 
seed=5
withReplacement = False
fraction = 0.5
df.sample(withReplacement, fraction, seed).count()

16) Random splits can be helpful when you need to break up your DataFrame into a ran‐ dom “splits” of the original DataFrame. This is often used with machine learning algorithms to create training, validation, and test sets.
# in Python: dataFrames = df.randomSplit([0.25, 0.75], seed) dataFrames[0].count() > dataFrames[1].count() # False

17) To append to a DataFrame, you must union the original DataFrame along with the new DataFrame. To union two DataFrames, you must be sure that they have the same schema and number of columns; otherwise, the union will fail. Unions are currently performed based on location, not on the schema. This means that columns will not automatically line up the way you think they might.
Python: df.union(newDF).where("count = 1").where(col("ORIGIN_COUNTRY_NAME") != "United States").show()

18) Sort: There are two equivalent operations to do this sort and orderBy that work the exact same way.
Way 1: df.sort("count").show(5)
Way 2: df.orderBy("count", "DEST_COUNTRY_NAME").show(5) or df.orderBy(col("count"), col("DEST_COUNTRY_NAME")).show(5)
To be more explicit: 
# in Python: 
from pyspark.sql.functions import desc, asc
df.orderBy(expr("count desc")).show(2)
df.orderBy(col("count").desc(), col("DEST_COUNTRY_NAME").asc()).show(2)
# in SQL: SELECT * FROM dfTable ORDER BY count DESC, DEST_COUNTRY_NAME ASC LIMIT 2

19) Limiting records to dispay from df: df.limit(5).show() or SELECT * FROM dfTable LIMIT 6
```

  - Another important optimization opportunity is to partition the data according to some frequently filtered columns, which control the physical layout of data across the cluster including the partitioning scheme and the number of partitions.
    - ***Repartition*** will incur a full shuffle of the data, regardless of whether one is necessary. This means that you should typically only repartition when the future number of partitions is greater than your current number of partitions or when you are looking to partition by a set of columns:

```
df.rdd.getNumPartitions() # 1
or - df.repartition(5)
Repartitioning based on column and total patitions: 
df.repartition(5, col("DEST_COUNTRY_NAME"))
```

  - ***Spark maintains the state of the cluster in the driver***. There are times when you’ll want to collect some of your data to the driver in order to manipulate it on your local machine.
    - Thus far, we did not explicitly define this operation. However, we used several differ‐ ent methods for doing so that are effectively all the same. collect gets all data from the entire DataFrame, take selects the first N rows, and show prints out a number of rows nicely in below example:

```
# in Python
collectDF = df.limit(10)
collectDF.take(5) # take works with an Integer count collectDF.show() # this prints it out nicely collectDF.show(5, False)
collectDF.collect()
```
  - There’s an additional way of collecting rows to the driver in order to iterate over the entire dataset. The method toLocalIterator collects partitions to the driver as an iterator. This method allows you to iterate over the entire dataset partition-by- partition in a serial manner: collectDF.toLocalIterator()
  - ***Any collection of data to the driver can be a very expensive opera‐ tion! If you have a large dataset and call collect, you can crash the driver. If you use toLocalIterator and have very large partitions, you can easily crash the driver node and lose the state of your application. This is also expensive because we can operate on a one-by-one basis, instead of running computation in parallel.***

---------------------------------

- Chapter 6: Working with Different Types of Data
  -  About filtering and working with different types of data... 

```
Some examples: 
Eg1: 
from pyspark.sql.functions import instr
DOTCodeFilter = col("StockCode") == "DOT"
priceFilter = col("UnitPrice") > 600
descripFilter = instr(col("Description"), "POSTAGE") >= 1 df.withColumn("isExpensive", DOTCodeFilter & (priceFilter | descripFilter))\
      .where("isExpensive")\
      .select("unitPrice", "isExpensive").show(5)
      
Eg2: 
df.selectExpr(
"CustomerId",
"(POWER((Quantity * UnitPrice), 2.0) + 5) as realQuantity").show(2)
-- in SQL
SELECT customerId, (POWER((Quantity * UnitPrice), 2.0) + 5) as realQuantity FROM dfTable

Eg3: To round off
from pyspark.sql.functions import lit, round, bround 
df.select(round(lit("2.5")), bround(lit("2.5"))).show(2)
-- in SQL
SELECT round(2.5), bround(2.5)

Eg4: Correlation between columns
from pyspark.sql.functions import corr df.stat.corr("Quantity", "UnitPrice") df.select(corr("Quantity", "UnitPrice")).show()
-- in SQL
SELECT corr(Quantity, UnitPrice) FROM dfTable

Eg5: Compute some stats
# in Python: df.describe().show()

Eg6: 
The initcap function will capitalize every word in a given string when that word is separated from another by a space.
from pyspark.sql.functions import initcap df.select(initcap(col("Description"))).show()
-- in SQL
SELECT initcap(Description) FROM dfTable

Eg7:
from pyspark.sql.functions import lower, upper df.select(col("Description"),
        lower(col("Description")),
        upper(lower(col("Description")))).show(2)
-- in SQL
SELECT Description, lower(Description), Upper(lower(Description)) FROM dfTable

Eg8:
Another trivial task is adding or removing spaces around a string. You can do this by using lpad, ltrim, rpad and rtrim, trim:
from pyspark.sql.functions import lit, ltrim, rtrim, rpad, lpad, trim df.select(
        ltrim(lit("    HELLO    ")).alias("ltrim"),
        rtrim(lit("    HELLO    ")).alias("rtrim"),
        trim(lit("    HELLO    ")).alias("trim"),
        lpad(lit("HELLO"), 3, " ").alias("lp"),
        rpad(lit("HELLO"), 10, " ").alias("rp")).show(2)
-- in SQL
SELECT ltrim(' HELLLOOOO '), rtrim(' HELLLOOOO '), trim(' HELLLOOOO '), lpad('HELLOOOO ', 3, ' '), rpad('HELLOOOO ', 10, ' ')
FROM dfTable

Eg9:
Searching for the existence of one string in another or replacing all mentions of a string with another value. This is often done with a tool called regular expressions that exists in many programming languages.
from pyspark.sql.functions import regexp_replace regex_string = "BLACK|WHITE|RED|GREEN|BLUE" df.select(
      regexp_replace(col("Description"), regex_string, "COLOR").alias("color_clean"),
      col("Description")).show(2)
-- in SQL
SELECT
regexp_replace(Description, 'BLACK|WHITE|RED|GREEN|BLUE', 'COLOR') as color_clean, Description
FROM dfTable

Eg10:
This simple feature can often help you programmatically generate columns or Boolean filters in a way that is simple to understand and extend.
# in Python
from pyspark.sql.functions import expr, locate simpleColors = ["black", "white", "red", "green", "blue"] def color_locator(column, color_string):
return locate(color_string.upper(), column)\ .cast("boolean")\
.alias("is_" + c)
selectedColumns = [color_locator(df.Description, c) for c in simpleColors]
selectedColumns.append(expr("*")) # has to a be Column type df.select(*selectedColumns).where(expr("is_white OR is_red"))\
      .select("Description").show(3, False)

Eg11: 
Date & Timestamp related examples: 
from pyspark.sql.functions import current_date, current_timestamp 
dateDF = spark.range(10)\
      .withColumn("today", current_date())\
      .withColumn("now", current_timestamp())
    dateDF.createOrReplaceTempView("dateTable")
    
Eg11.1: Adding dates: 
from pyspark.sql.functions import date_add, date_sub 
dateDF.select(date_sub(col("today"), 5), date_add(col("today"), 5)).show(1)
-- in SQL
SELECT date_sub(today, 5), date_add(today, 5) FROM dateTable

Eg11.2: Subtracting dates: 
from pyspark.sql.functions import datediff, months_between, to_date 
dateDF.withColumn("week_ago", date_sub(col("today"), 7))\
      .select(datediff(col("week_ago"), col("today"))).show(1)

Eg11.3: The to_date function allows you to convert a string to a date, optionally with a specified format.
dateDF.select(
        to_date(lit("2016-01-01")).alias("start"),
        to_date(lit("2017-05-22")).alias("end"))\
      .select(months_between(col("start"), col("end"))).show(1)
-- in SQL
SELECT to_date('2016-01-01'), months_between('2016-01-01', '2017-01-01'), datediff('2016-01-01', '2017-01-01')
FROM dateTable

Eg11.4: 
from pyspark.sql.functions import to_timestamp cleanDateDF.select(to_timestamp(col("date"), dateFormat)).show()
-- in SQL
SELECT to_timestamp(date, 'yyyy-dd-MM'), to_timestamp(date2, 'yyyy-dd-MM') FROM dateTable2

Eg11.5: 
-- in SQL
SELECT cast(to_date("2017-01-01", "yyyy-dd-MM") as timestamp)

Eg12: 
Spark includes a function to allow you to select the first non-null value from a set of columns by using the coalesce function.
There are several other SQL functions that you can use to achieve similar things: ifnull, nullIf, nvl, and nvl2
from pyspark.sql.functions import coalesce 
df.select(coalesce(col("Description"), col("CustomerId"))).show()
-- in SQL
SELECT
ifnull(null, 'return_value'), nullif('value', 'value'),
nvl(null, 'return_value'), nvl2('not_null', 'return_value', "else_value")
FROM dfTable LIMIT 1

Eg13: Drop, which removes rows that contain nulls.
df.na.drop("any")
SELECT * FROM dfTable WHERE Description IS NOT NULL

Eg14: Fill function, you can fill one or more columns with a set of values.
df.na.fill("All Null values become this string")

Eg15:
df.na.replace([""], ["UNKNOWN"], "Description")

Eg16: You can use asc_nulls_first, desc_nulls_first, asc_nulls_last, or desc_nulls_last to specify where you would like your null val‐ ues to appear in an ordered DataFrame.
```

  - ***Spark will not throw an error if it cannot parse the date; rather, it will just return null. This can be a bit tricky in larger pipelines because you might be expecting your data in one format and getting it in another.***
  - ***Nulls are a challenging part of all programming, and Spark is no exception. When we declare a column as not having a null time, that is not actually enforced. To reiterate, when you define a schema in which all columns are declared to not have null values, Spark will not enforce that and will happily let null values into that column. The nullable signal is simply to help Spark SQL optimize for handling that column. If you have null val‐ ues in columns that should not have null values, you can get an incorrect result or see strange exceptions that can be difficult to debug. There are two things you can do with null values: you can explicitly drop nulls or you can fill them with a value (globally or on a per-column basis).***

```
Complex types can help you organize and structure your data in ways that make more sense for the problem that you are hoping to solve. There are three kinds of complex types: structs, arrays, and maps.
1) 
You can think of structs as DataFrames within DataFrames. Eg: 
complexDF = df.select(struct("Description", "InvoiceNo").alias("complex"))
2) 
The first task is to turn our Description column into a complex type, an array. We do this by using the split function and specify the delimiter:
from pyspark.sql.functions import split 
df.select(split(col("Description"), " ")).show(2)
-- in SQL
SELECT split(Description, ' ') FROM dfTable
+---------------------+
|split(Description,  )|
+---------------------+
| [WHITE, HANGING, ...|
| [WHITE, METAL, LA...|
+---------------------+
We can also query the values of the array using Python-like syntax:
df.select(split(col("Description"), " ").alias("array_col")).selectExpr("array_col[0]").show(2)
-- in SQL
SELECT split(Description, ' ')[0] FROM dfTable This gives us the following result:
+------------+
|array_col[0]|
+------------+
| WHITE      |
| WHITE      |
+------------+
For array length: df.select(size(split(col("Description"), " "))).show(2) # shows 5 and 3
If array contains a value: 
df.select(array_contains(split(col("Description"), " "), "WHITE")).show(2)
-- in SQL
SELECT array_contains(split(Description, ' '), 'WHITE') FROM dfTable
To convert a complex type into a set of rows (one per value in our array), we need to use the explode function: 
df.withColumn("splitted", split(col("Description"), " ")).withColumn("exploded", explode(col("splitted"))).select("Description", "InvoiceNo", "exploded").show(2)
-- in SQL
SELECT Description, InvoiceNo, exploded
FROM (SELECT *, split(Description, " ") as splitted FROM dfTable) LATERAL VIEW explode(splitted) as exploded
+--------------------+---------+--------+
|         Description|InvoiceNo|exploded|
+--------------------+---------+--------+
|WHITE HANGING HEA...|   536365|   WHITE|
|WHITE HANGING HEA...|   536365| HANGING|
+--------------------+---------+--------+
3) 
Maps are created by using the map function and key-value pairs of columns.
 in Python
from pyspark.sql.functions import create_map df.select(create_map(col("Description"), col("InvoiceNo")).alias("complex_map"))\
.show(2)
-- in SQL
SELECT map(Description, InvoiceNo) as complex_map FROM dfTable WHERE Description IS NOT NULL
This produces the following result:
+--------------------+
|         complex_map|
+--------------------+
|Map(WHITE HANGING...|
|Map(WHITE METAL L...|
You can query them by using the proper key. A missing key returns null:
df.select(map(col("Description"), col("InvoiceNo")).alias("complex_map")).selectExpr("complex_map['WHITE METAL LANTERN']").show(2)
+--------------------------------+
|complex_map[WHITE METAL LANTERN]|
+--------------------------------+
|                            null|
|                          536365|
+--------------------------------+
You can also explode map types, which will turn them into columns. 
```

<>Upload img on explode()<>

  - Spark has some unique support for working with JSON data. You can operate directly on strings of JSON in Spark and parse from JSON or extract JSON objects.

```
You can use the get_json_object to inline query a JSON object, be it a dictionary or array.
jsonDF.select(get_json_object(col("jsonString"), "$.myJSONKey.myJSONValue[1]") as "column", json_tuple(col("jsonString"), "myJSONKey")).show(2)
Here’s the equivalent in SQL:
    jsonDF.selectExpr(
      "json_tuple(jsonString, '$.myJSONKey.myJSONValue[1]') as column").show(2)

You can also turn a StructType into a JSON string by using the to_json function:
df.selectExpr("(InvoiceNo, Description) as myStruct")\
      .select(to_json(col("myStruct")))

This function also accepts a dictionary (map) of parameters that are the same as the JSON data source. 
Etc etc... 
```
  - ***UDFs (User Defined Functions)*** can take and return one or more columns as input. Although you can write UDFs in Scala, Python, or Java, there are performance considerations that you should be aware of.
    - When you use the function, there are essentially two different things that occur. If the function is written in Scala or Java, you can use it within the Java Virtual Machine (JVM). This means that there will be little performance penalty aside from the fact that you can’t take advantage of code generation capabilities that Spark has for built-in functions. 
    - If the function is written in Python, something quite different happens. Spark starts a Python process on the worker, serializes all of the data to a format that Python can understand (remember, it was in the JVM earlier), executes the function row by row on that data in the Python process, and then finally returns the results of the row operations to the JVM and Spark. 
      - ***Starting this Python process is expensive, but the real cost is in seri‐ alizing the data to Python. This is costly for two reasons: it is an expensive computation, but also, after the data enters Python, Spark cannot manage the memory of the worker. This means that you could potentially cause a worker to fail if it becomes resource constrained (because both the JVM and Python are competing for memory on the same machine). We recommend that you write your UDFs in Scala or Java—the small amount of time it should take you to write the function in Scala will always yield significant speed ups, and on top of that, you can still use the function from Python.***

```
Eg consider the function: 
udfExampleDF = spark.range(5).toDF("num") 
def power3(double_value):
  return double_value ** 3 power3(2.0)
  
Now that we’ve created these functions and tested them, we need to register them with Spark so that we can use them on all of our worker machines. Spark will serialize the function on the driver and transfer it over the network to all executor processes. This happens regardless of language.
Eg:
from pyspark.sql.functions import udf 
power3udf = udf(power3)
or udfExampleDF.selectExpr("power3(num)").show(2)

You can also use UDF/UDAF creation via a Hive syntax. o allow for this, first you must enable Hive support when they create their SparkSession (via SparkSession.builder().enableHiveSupport()). Then you can register UDFs in SQL. 
```

---------------------------------

- Chapter 7: Aggregations
  - Aggregating is the act of collecting something together and is a cornerstone of big data analytics. In an aggregation, you will specify a key or grouping and an aggregation function that specifies how you should transform one or more columns.
  - Spark allows us to create the following groupings types:
    - The simplest grouping is to just summarize a complete DataFrame by perform‐ ing an aggregation in a select statement.
    - A ***“group by”*** allows you to specify one or more keys as well as one or more aggregation functions to transform the value columns.
    - A ***“window”*** gives you the ability to specify one or more keys as well as one or more aggregation functions to transform the value columns. However, the rows input to the function are somehow related to the current row.
    - A ***“grouping set”*** which you can use to aggregate at multiple different levels. Grouping sets are available as a primitive in SQL and via rollups and cubes in DataFrames.
    - A ***“rollup”*** makes it possible for you to specify one or more keys as well as one or more aggregation functions to transform the value columns, which will be summarized hierarchically.
    - A ***“cube”*** allows you to specify one or more keys as well as one or more aggrega‐ tion functions to transform the value columns, which will be summarized across all combinations of columns.
  - Basic aggregations apply to an entire DataFrame.
  - Some functions: count, countDistinct, approx_count_distinct, first and last, min and max, sum, sumDistinct, avg.
  - Spark performs the formula for the sample standard deviation or variance if you use the variance or stddev functions.
  - Skewness and kurtosis are both measurements of extreme points in your data. Skew‐ ness measures the asymmetry of the values in your data around the mean, whereas kurtosis is a measure of the tail of data. These are both relevant specifically when modeling your data as a probability distribution of a random variable. 
  - Correlation measures the Pearson correlation coefficient, which is scaled between –1 and +1. The covariance is scaled according to the inputs in the data.
  - In Spark, you can perform aggregations not just of numerical values using formulas, you can also perform them on complex types. For example, we can collect a list of values present in a given column or only the unique values by collecting to a set. Eg: `df.agg(collect_set("Country"), collect_list("Country")).show()`
  - We can also do grouping, grouping with expressions (Eg: `df.groupBy("InvoiceNo").agg(count("Quantity").alias("quan"), expr("count(Quantity)")).show()`), grouping with maps. 
  - We can also perform window functions. Eg: `windowSpec = Window.partitionBy("CustomerId", "date").orderBy(desc("Quantity")).rowsBetween(Window.unboundedPreceding, Window.currentRow)`
  - Grouping sets: An aggregation across multiple groups. We achieve this by using grouping sets. Eg: `SELECT CustomerId, stockCode, sum(Quantity) FROM dfNoNull GROUP BY customerId, stockCode GROUPING SETS((customerId, stockCode)) ORDER BY CustomerId DESC, stockCode DESC`. 
    - ***Grouping sets depend on null values for aggregation levels. If you do not filter-out null values, you will get incorrect results. This applies to cubes, rollups, and grouping sets.***
    - ***The GROUPING SETS operator is only available in SQL. To perform the same in Data‐ Frames, you use the rollup and cube operators—which allow us to get the same results.***
  - A ***rollup*** is a multidimensional aggregation that performs a vari‐ ety of group-by style calculations for us.
  - A ***cube*** takes the rollup to a level deeper. Rather than treating elements hierarchically, a cube does the same thing across all dimensions.
  - Grouping Metadata... 
  - Pivots make it possible for you to convert a row into a column. 
  - ***User-defined aggregation functions (UDAFs)*** (note it is slightly different from UDF) are a way for users to define their own aggregation functions based on custom formulae or business rules. You can use UDAFs to compute custom calculations over groups of input data (as opposed to sin‐ gle rows). Spark maintains a single AggregationBuffer to store intermediate results for every group of input data.

---------------------------------

- Chapter 8: Joins
  - A join brings together two sets of data. There are a variety of different join types available in Spark for you to use:
    - ***Inner joins*** (keep rows with keys that exist in the left and right datasets)
    - ***Outer joins*** (keep rows with keys in either the left or right datasets)
    - ***Left outer joins*** (keep rows with keys in the left dataset)
    - ***Right outer joins*** (keep rows with keys in the right dataset)
    - ***Left semi joins*** (keep the rows in the left, and only the left, dataset where the key appears in the right dataset)
    - ***Left anti joins*** (keep the rows in the left, and only the left, dataset where they do not appear in the right dataset)
    - ***Natural joins*** (perform a join by implicitly matching the columns between the two datasets with the same names)
      - ***Implicit is always dangerous; The following query will give us incorrect results because the two DataFrames/tables share a col‐ umn name (id), but it means different things in the datasets. You should always use this join with caution.***
    - ***Cross (or Cartesian) joins*** (match every row in the left dataset with every row in the right dataset)

```
Eg: 
1) Inner join
joinType = "inner"
person.join(graduateProgram, joinExpression, joinType).show()
-- in SQL
SELECT * FROM person INNER JOIN graduateProgram ON person.graduate_program = graduateProgram.id

2) Complex dtype join
from pyspark.sql.functions import expr person.withColumnRenamed("id", "personId").join(sparkStatus, expr("array_contains(spark_status, id)")).show()
-- in SQL
SELECT * FROM (select id as personId, name, graduate_program, spark_status FROM person) INNER JOIN sparkStatus ON array_contains(spark_status, id)
```
  - ***Handling Duplicate Column Names when Joining:***
    - When you have two keys that have the same name, probably the easiest fix is to change the join expression from a Boolean expression to a string or sequence. This automatically removes one of the columns for you during the join: `person.join(gradProgramDupe,"graduate_program").select("graduate_program").show()`. 
    - Another approach is to drop the offending column after the join: `person.join(gradProgramDupe, joinExpr).drop(person.col("graduate_program")).select("graduate_program").show()`.
    - (Or) We can avoid this issue altogether if we rename one of our columns before the join. 
  - ***How Spark Performs Joins:***
    - To understand this, you need to know the two core resources at play: 
      - node-to-node communication strategy (shuffle join) and 
      - per node computation strategy (broadcast join)
    - Spark approaches cluster communication in two different ways during joins. It either incurs a ***shuffle join***, which results in an all-to-all communication or a ***broadcast join***.
    - Some of these internal optimizations are likely to change over time with new improvements to the cost-based optimizer and improved communication strategies.
    - The core foundation of our simplified view of joins is that in Spark you will have either a big table or a small table. Although this is obviously a spectrum (and things do happen differently if you have a “medium-sized table”), but for easier explanation. 
    - ***When you join a big table to another big table, you end up with a shuffle join.***
      - In a shuffle join, every node talks to every other node and they share data according to which node has a certain key or set of keys (on which you are joining). These joins are expensive because the network can become congested with traffic, especially if your data is not partitioned well.
    - When the table is small enough to fit into the memory of a single worker node, with some breathing room of course, we can optimize our join. Although we can use a big table–to–big table communication strategy, it can often be more efficient to ***use a broadcast join***. 
      - What this means is that we will replicate our small DataFrame onto every worker node in the cluster (be it located on one machine or many). ***Now this sounds expensive. However, what this does is prevent us from performing the all-to-all communication during the entire join process***. Instead, ***we perform it only once at the beginning and then let each individual worker node perform the work*** without having to wait or communicate with any other worker node. ***At the beginning of this join will be a large communication, just like in the previous type of join. However, immediately after that first, there will be no further communication between nodes.*** This means that joins will be performed on every single node individually, making CPU the biggest bottleneck. explain() query for such a case looks like: 

```
      == Physical Plan ==
      *BroadcastHashJoin [graduate_program#40], [id#5....
      :- LocalTableScan [id#38, name#39, graduate_progr...
      +- BroadcastExchange HashedRelationBroadcastMode(....
         +- LocalTableScan [id#56, degree#57, departmen....
```
  - ***The SQL interface also includes the ability to provide hints to perform joins. These are not enforced,*** however, so the optimizer might choose to ignore them. You can set one of these hints by using a special comment syntax. MAPJOIN, BROADCAST, and BROAD CASTJOIN all do the same thing and are all supported:

```
Eg: 
-- in SQL
SELECT /*+ MAPJOIN(graduateProgram) */ * FROM person JOIN graduateProgram
ON person.graduate_program = graduateProgram.id
```
  - ***This doesn’t come for free either: if you try to broadcast something too large, you can crash your driver node (because that collect is expensive).*** This is likely an area for optimization in the future.
  - When performing joins with small tables, it’s usually best to let Spark decide how to join them. You can always force a broadcast join if you’re noticing strange behavior.

---------------------------------

- Chapter 9: Data Sources
  - Spark has six “core” data sources and hundreds of external data sources written by the community: CSV, JSON, Parquet, ORC, JDBC/ODBC connections, Plain-text files. Spark has numerous community-created data sources. Here’s just a small sample: Cassandra, HBase, MongoDB, AWS Redshift, etc. 
  - The core structure for reading data is as follows: DataFrameReader.format(...).option("key", "value").schema(...).load()
  - There are a variety of ways in which you can set options; for example, you can build a map and pass in your configurations. 
  - Similarly, we have different write modes... can be checked....
  - In writing parquet files, even though there are only two options, you can still encounter problems if you’re working with incompatible Parquet files. 
    - ***Be careful when you write out Parquet files with different versions of Spark (especially older ones) because this can cause significant headache.***
  - Reading/Writing from SQL Databases; Eg: 

```
Eg: To connect to a sql db from spark and query: 
driver = "org.sqlite.JDBC"
path = "/data/flight-data/jdbc/my-sqlite.db"
url = "jdbc:sqlite:" + path
tablename = "flight_info"
```
  - As we create this DataFrame, it is no different from any other: you can query it, transform it, and join it without issue. You’ll also notice that there is already a schema, as well. That’s because ***Spark gathers this information from the table itself and maps the types to Spark data types.***
  - Spark makes a best-effort attempt to filter data in the database itself before creating the DataFrame.
  - ***Spark can’t translate all of its own functions into the functions available in the SQL database in which you’re working. Therefore, sometimes you’re going to want to pass an entire query into your SQL that will return the results as a DataFrame.***
  - Spark has an underlying algorithm that can read multiple files into one partition, or conversely, read multiple partitions out of one file, depending on the file size and the “splitability” of the file type and compression. The same flexibility that exists with files, ***also exists with SQL databases except that you must configure it a bit more manually.*** What you can ***configure, is the ability to specify a maximum number of partitions to allow you to limit how much you are reading and writing in parallel:***

```
# in Python
    dbDataFrame = spark.read.format("jdbc")\
      .option("url", url).option("dbtable", tablename).option("driver",  driver)\
      .option("numPartitions", 10).load()  
```

  - ***You can explicitly push predicates down into SQL databases through the connection itself. This optimization allows you to control the physical location of certain data in certain partitions by specifying predicates.***
  - ***Spark predicate push down to database allows for better optimized Spark queries.*** 
    - A ***predicate*** is a condition on a query that returns true or false, typically located in the WHERE clause. A predicate push down filters the data in the database query, reducing the number of entries retrieved from the database and improving query performance. By default the Spark Dataset API will automatically push down valid WHERE clauses to the database.
  - Splittable File Types and Compression: Certain file formats are fundamentally “splittable.” This can improve speed because it makes it possible for Spark to avoid reading an entire file, and access only the parts of the file necessary to satisfy your query. Additionally if you’re using something like Hadoop Distributed File System (HDFS), splitting a file can provide further optimization if that file spans multiple blocks. In conjunction with this is a need to manage compression. Not all compression schemes are splittable. ***How you store your data is of immense consequence when it comes to making your Spark jobs run smoothly. We recommend Parquet with gzip compression.***
  - ***Reading Data in Parallel***: Multiple executors cannot read from the same file at the same time necessarily, but they can read different files at the same time. In general, this means that when you read from a folder with multiple files in it, each one of those files will become a partition in your DataFrame and be read in by available executors in parallel (with the remaining queueing up behind the others).
  - ***Writing Data in Parallel***: The number of files or data written is dependent on the number of partitions the DataFrame has at the time you write out the data. By default, one file is written per partition of the data. This means that although we specify a “file,” it’s actually a number of files within a folder, with the name of the specified file, with one file per each partition that is written.
  - ***Partitioning (partitionBy)*** is a tool that allows you to control what data is stored (and where) as you write it. When you write a file to a partitioned directory (or table), you basically encode a column as a folder. Eg: `csvFile.limit(10).write.mode("overwrite").partitionBy("DEST_COUNTRY_NAME").save("/tmp/partitioned-files.parquet")`
    - This is probably the ***lowest-hanging optimization that you can use when you have a table that readers frequently filter by before manipulating.*** For instance, date is particularly common for a partition because, downstream, often we want to look at only the previous week’s data (instead of scanning the entire list of records). This can provide massive speedups for readers.
  - ***Bucketing*** is another file organization approach with which you can control the data that is specifically written to each file. This can ***help avoid shuffles later when you go to read the data because data with the same bucket ID*** will all be grouped together into one physical partition. 
    - Rather than partitioning on a specific column (which might write out a ton of directories), it’s probably worthwhile to explore bucketing the data instead. This will create a certain number of files and organize our data into those “buckets”.
  - Although Spark can work with all of these types, not every single type works well with every data file format. For instance, ***CSV files do not support complex types,*** whereas Parquet and ORC do.
  - Managing file sizes is an important factor ***not so much for writing data but reading it later on.*** When you’re writing lots of small files, there’s a significant metadata over‐head that you incur managing all of those files. ***Spark especially does not do well with small files,*** although many file systems (like HDFS) don’t handle lots of small files well, either. You might hear this referred to as the ***“small file problem.”*** The opposite is also true: you don’t want files that are too large either, because it becomes inefficient to have to read entire blocks of data when you need only a few rows.
    - Spark 2.2 introduced a new ***method for controlling file sizes in a more automatic way.*** We saw previously that the number of output files is a derivative of the number of partitions we had at write time (and the partitioning columns we selected). Now, you can take advantage of another tool in order to limit output file sizes so that you can target an optimum file size. You can use the maxRecordsPerFile option and specify a number of your choosing. For example, if you set an option for a writer as df.write.option("maxRecordsPerFile", 5000), Spark will ensure that files will contain at most 5,000 records.

- Chapter 10: Spark SQL
  - With Spark SQL you can run SQL queries against views or tables organized into databases. SQL or Structured Query Language is a domain-specific language for expressing relational operations over data.
  - ***Before Spark’s rise, Hive was the de facto big data SQL access layer.*** Originally developed at Facebook, Hive became an incredibly popular tool across industry for performing SQL operations on big data. In many ways it helped propel Hadoop into different industries because analysts could run SQL queries. Although Spark began as a general processing engine with Resilient Distributed Datasets (RDDs), a large cohort of users now use Spark SQL.
  - With the release of Spark 2.0, its authors created a superset of Hive’s support, writing a native SQL parser that supports both ANSI-SQL as well as HiveQL queries.
  - ***Spark SQL is intended to operate as an online analytic processing (OLAP) database, not an online transaction processing (OLTP) database.*** This means that it is not intended to perform extremely low-latency queries. Even though support for in-place modifications is sure to be something that comes up in the future, it’s not something that is currently available.
  - Spark SQL has a great relationship with Hive because it can connect to Hive metastores. ***The Hive metastore is the way in which Hive maintains table information for use across sessions.*** With Spark SQL, you can connect to your Hive metastore (if you already have one) and access table metadata to reduce file listing when accessing information. This is popular for users who are migrating from a legacy Hadoop environment and beginning to run all their workloads using Spark.
  - You can connect to hive metastore using the options here: spark.sql.hive.metastore... 
  - The highest level abstraction in Spark SQL is the Catalog. ***The Catalog is an abstraction for the storage of metadata about the data stored in your tables as well as other helpful things like databases, tables, functions, and views.*** The catalog is available in the org.apache.spark.sql.catalog.Catalog package and contains a number of helpful functions for doing things like listing tables, databases, and functions. 
  - To do anything useful with Spark SQL, you first need to define tables. Tables are logically equivalent to a DataFrame in that they are a structure of data against which you run commands. 
  - ***The core difference between tables and DataFrames is this: you define DataFrames in the scope of a programming language, whereas you define tables within a database.*** 
  - One important note is the concept of ***managed versus unmanaged tables.*** Tables store two important pieces of information. The data within the tables as well as the data about the tables; that is, the metadata. 
    - You can have Spark manage the metadata for a set of files as well as for the data. When you define a table from files on disk, you are defining an unmanaged table. 
    - When you use saveAsTable on a DataFrame, you are creating a managed table for which Spark will track of all of the relevant information.
    - This will read your table and write it out to a new location in Spark format. You can see this reflected in the new explain plan.
  - Creating table: CREATE TABLE flights (DEST_COUNTRY_NAME STRING, ORIGIN_COUNTRY_NAME STRING, count LONG) USING JSON OPTIONS (path '/data/flight-data/json/2015-summary.json')
  - The specification of the ***USING syntax*** in the above example is of significant importance. If you do not specify the format, Spark will default to a Hive SerDe configuration. This has performance implications for future readers and writers because ***Hive SerDes are much slower than Spark’s native serialization.***
  - Spark will manage the table’s metadata; however, the files are not managed by Spark at all. You create this table by using the CREATE EXTERNAL TABLE statement: CREATE EXTERNAL TABLE hive_flights (DEST_COUNTRY_NAME STRING, ORIGIN_COUNTRY_NAME STRING, count LONG) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LOCATION '/data/flight-data-hive/'
  - Describing Table Metadata: DESCRIBE TABLE flights_csv
  - View the partitioning scheme for the data: SHOW PARTITIONS partitioned_flights
  - Refreshing Table Metadata: Maintaining table metadata is an important task to ensure that you’re reading from the most recent set of data. There are two commands to refresh table metadata. 
    - ***REFRESH TABLE*** refreshes all cached entries (essentially, files) associated with the table. If the table were previously cached, it would be cached lazily the next time it is scanned: REFRESH table partitioned_flights
    - Another related command is ***REPAIR TABLE***, which refreshes the partitions maintained in the catalog for that given table. This command’s focus is on collecting new partition information—an example might be writing out a new partition manually and the need to repair the table accordingly: MSCK REPAIR TABLE partitioned_flights
  - Dropping Tables: DROP TABLE IF EXISTS flights_csv;
  - Dropping unmanaged tables: No data will be removed but you will no longer be able to refer to this data by the table name.
  - Just like DataFrames, you can ***cache and uncache tables.*** You simply specify which table you would like using the following syntax:
    - CACHE TABLE flights 
    - Here’s how you uncache them: UNCACHE TABLE FLIGHTS
  - A view specifies a set of transformations on top of an existing table—***basically just saved query plans***, which can be convenient for organizing or reusing your query logic. Spark has several different notions of views. Views can be global, set to a database, or per session.
    - CREATE VIEW just_usa_view AS SELECT * FROM flights WHERE dest_country_name = 'United States'
    - You can also have: CREATE TEMP VIEW, CREATE GLOBAL TEMP VIEW, CREATE OR REPLACE TEMP VIEW, etc. 
    - A view is effectively a transformation and Spark will perform it only at query time. Effectively, views are equivalent to creating a new DataFrame from an existing DataFrame.
    - Similarly, you can drop views: DROP VIEW IF EXISTS just_usa_view;
  - Also, you can create, set databases in spark, etc. 
  - Oftentimes, you might need to ***conditionally replace values in your SQL queries.*** You can do this by using a case...when...then...end style statement. This is essentially the equivalent of programmatic if statements:

```
SELECT
CASE WHEN DEST_COUNTRY_NAME = 'UNITED STATES' THEN 1
WHEN DEST_COUNTRY_NAME = 'Egypt' THEN 0
ELSE -1 END
FROM partitioned_flights
```

  - There are ***three core complex types in Spark SQL: structs, lists, and maps.***
    - Structs are more akin to maps. They provide a way of creating or querying nested data in Spark. To create one, you simply need to wrap a set of columns (or expressions) in parentheses: CREATE VIEW IF NOT EXISTS nested_data AS SELECT (DEST_COUNTRY_NAME, ORIGIN_COUNTRY_NAME) as country, count FROM flights
      - You can query individual columns within a struct—all you need to do is use dot syntax: SELECT country.DEST_COUNTRY_NAME, count FROM nested_data
    - There are several ways to create an array or list of values. You can use the collect_list function, which creates a list of values. You can also use the function collect_set, which creates an array without duplicate values. These are both aggregation functions and therefore can be specified only in aggregations: SELECT DEST_COUNTRY_NAME as new_name, collect_list(count) as flight_counts, collect_set(ORIGIN_COUNTRY_NAME) as origin_set FROM flights GROUP BY DEST_COUNTRY_NAME 
      - You can query lists by position by using a Python-like array query syntax: SELECT DEST_COUNTRY_NAME as new_name, collect_list(count)[0] FROM flights GROUP BY DEST_COUNTRY_NAME
  - To see a list of functions in Spark SQL, you use the SHOW FUNCTIONS statement in sql. Eg: SHOW FUNCTIONS LIKE "collect*";
  - As we know Spark gives you the ability to define your own functions and use them in a distributed manner (UDFs):

```
def power3(number:Double): Double = number * number * number 
spark.udf.register("power3", power3(_:Double):Double)
SELECT count, power3(count) FROM flights
```

  - With subqueries, you can specify queries within other queries. This makes it possible for you to specify some sophisticated logic within your SQL. In Spark, there are two fundamental subqueries: 
    - Correlated subqueries use some information from the outer scope of the query in order to supplement information in the subquery. 
    - Uncorrelated subqueries include no information from the outer scope. 
      - Using uncorrelated scalar queries, you can bring in some supplemental information that you might not have previously. For example, if you wanted to include the maximum value as its own column from the entire counts dataset, you could do this (below example check):
    -  Each of these queries can return one (scalar subquery) or more values. Spark also includes support for predicate subqueries, which allow for filtering based on values.

```
Uncorrelated predicate subqueries
Eg: SELECT * FROM flights
WHERE origin_country_name IN (SELECT dest_country_name FROM flights
GROUP BY dest_country_name ORDER BY sum(count) DESC LIMIT 5)

Correlated predicate subqueries
SELECT * FROM flights f1
WHERE EXISTS (SELECT 1 FROM flights f2
WHERE f1.dest_country_name = f2.origin_country_name) AND EXISTS (SELECT 1 FROM flights f2
WHERE f2.dest_country_name = f1.origin_country_name)

Uncorrelated scalar queries: 
SELECT *, (SELECT max(count) FROM flights) AS maximum FROM flights
```

---------------------------------

- Chapter 11: Datasets
  - We already worked with DataFrames, which are Datasets of type Row, and are available across Spark’s different languages. ***Datasets are a strictly Java Virtual Machine (JVM) language feature that work only with Scala and Java***. Using Datasets, you can define the object that each row in your Dataset will consist of.
  - We discussed that Spark has types like StringType, BigIntType, Struct Type, and so on. ***Those Spark-specific types map to types available in each of Spark’s languages like String, Integer, and Double.*** When you use the DataFrame API, you do not create strings or integers, but ***Spark manipulates the data for you by manipulating the Row object.***
  - When you use the Dataset API, for every row it touches, this domain specifies type, ***Spark converts the Spark Row format to the object you specified (a case class or Java class). This conversion slows down your operations but can provide more flexibility. You will notice a hit in performance but this is a far different order of magnitude from what you might see from something like a user-defined function (UDF) in Python, because the performance costs are not as extreme as switching programming languages,*** but it is an important thing to keep in mind.
  - When to Use Datasets:
    - When the operation(s) you would like to perform cannot be expressed using DataFrame manipulations
    - When you want or need ***type-safety***, and you’re willing to accept the cost of performance to achieve it.  Operations that are not valid for their types, say subtracting two string types, will fail at compilation time not at runtime. If correctness and bulletproof code is your highest priority, at the cost of some performance, this can be a great choice for you.
  - Creating Datasets:
    - You simply specify your class and then you’ll encode it when you come upon your DataFrame (which is of type Dataset<Row>):

```
Using java encoders
import org.apache.spark.sql.Encoders;
public class Flight implements Serializable{ String DEST_COUNTRY_NAME;
String ORIGIN_COUNTRY_NAME;
Long DEST_COUNTRY_NAME;
}
Dataset<Flight> flights = spark.read
.parquet("/data/flight-data/parquet/2010-summary.parquet/")
.as(Encoders.bean(Flight.class));
```

  - Other things covered: Action, Transformation, Filtering, Mapping, Joins, Grouping, Aggregations
  - By specifying a function, we are forcing Spark to evaluate this function on every row in our Dataset. This can be very resource intensive. ***For simple filters it is always preferred to write SQL expressions***. This will greatly reduce the cost of filtering out the data while still allowing you to manipulate it as a Dataset later on.

- Chapter 12: Resilient Distributed Datasets (RDDs)
  - Previous part of the book covered Spark’s Structured APIs. ***You should heavily favor these APIs in almost all scenarios.*** That being said, there are times when higher-level manipulation will not meet the business or engineering problem you are trying to solve. For those cases, you might need to use Spark’s lower-level APIs, specifically the Resilient Distributed Dataset (RDD), the SparkContext, and distributed shared variables like accumulators and broadcast variables.
  - There are two sets of low-level APIs: 
    - there is one for manipulating distributed data (RDDs), and
    - for distributing and manipulating distributed shared variables (broadcast variables and accumulators).
  - When to Use the Low-Level APIs: 
    - You need some functionality that you cannot find in the higher-level APIs; for example, ***if you need very tight control over physical data placement across the cluster.***
    - You need to maintain some legacy codebase written using RDDs.
    - You need to do some custom shared variable manipulation.
  - ***When you’re calling a DataFrame transformation, it actually just becomes a set of RDD transformations.*** This understanding can make your task easier as you begin debugging more and more complex workloads.
  - A ***SparkContext*** is the entry point for low-level API functionality. You access it through the SparkSession, which is the tool you use to perform computation across a Spark cluster: spark.sparkContext
  - RDDs were the primary API in the Spark 1.X series and are still available in 2.X, but they are not as commonly used. 
  - ***In short, an RDD represents an immutable, partitioned collection of records that can be operated on in parallel. Unlike DataFrames though, where each record is a structured row containing fields with a known schema, in RDDs the records are just Java, Scala, or Python objects of the programmer’s choosing.***
    - RDDs give you complete control because every record in an RDD is a just a Java or Python object. You can store anything you want in these objects, in any format you want. This gives you great power, but ***not without potential issues. Every manipulation and interaction between values must be defined by hand,*** meaning that you must “reinvent the wheel” for whatever task you are trying to carry out. 
  - Also, ***optimizations are going to require much more manual work,*** because Spark does not understand the inner structure of your records as it does with the Structured APIs. For instance, Spark’s Structured APIs automatically store data in an optimizied, compressed binary format, so to achieve the same space-efficiency and performance, you’d also need to implement this type of format inside your objects and all the low-level operations to compute over it. Likewise, optimizations like reordering filters and aggregations that occur automatically in Spark SQL need to be implemented by hand. 
  - Internally, each RDD is characterized by five main properties: 
    - A list of partitions
    - A function for computing each split
    - A list of dependencies on other RDDs
    - Optionally, a Partitioner for key-value RDDs (e.g., to say that the RDD is hash- partitioned)
    - Optionally, a list of preferred locations on which to compute each split (e.g., block locations for a Hadoop Distributed File System [HDFS] file)
  - The RDD APIs are available in Python as well as Scala and Java. For Scala and Java, the performance is for the most part the same, the large costs incurred in manipulating the raw objects. ***Python, however, can lose a substantial amount of performance when using RDDs. Running Python RDDs equates to running Python user-defined functions (UDFs) row by row.***
  - Because Python doesn’t have Datasets—it has only DataFrames—you will get an RDD of type Row: Eg: spark.range(10).rdd
  - To create an RDD from a collection, you will need to ***use the parallelize method on a SparkContext (within a SparkSession).***
    - This turns a single node collection into a parallel collection. When creating this parallel collection, you can also explicitly state the number of partitions into which you would like to distribute this array. In this case below, we are creating two partitions:

```
myCollection = "Spark The Definitive Guide : Big Data Processing Made Simple".split(" ")
words = spark.sparkContext.parallelize(myCollection, 2)
```

  - Then learned about creating RDD from data sources. Then functions like: Transformations (distinct, filter, map, flatmap, sort, random splits), Actions (reduce, count - countApprox, countApproxDistinct, countByValue, countByValueApprox, first, max/min, take), Saving RDD as file.
  - The same principles apply for caching RDDs as for DataFrames and Datasets. You can either cache or persist an RDD. ***By default, cache and persist only handle data in memory.***
  - Spark originally grew out of the Hadoop ecosystem, so it has a fairly tight integration with a variety of Hadoop tools. ***A sequenceFile is a flat file consisting of binary key– value pairs.*** It is extensively used in MapReduce as input/output formats.
  - ***Checkpointing: This feature is not available in Dataframe API. It is the act of saving an RDD to disk so that future references to this RDD point to those intermediate partitions on disk rather than recomputing the RDD from its original source.*** This is similar to caching except that it’s not stored in memory, only disk. This can be helpful when performing iterative computation.
  - The ***pipe method*** is probably one of Spark’s more interesting methods. With pipe, you can return an RDD created by piping elements to a forked external process. The resulting RDD is computed by executing the given process once per partition. We can use a simple example and pipe each partition to the command wc. Each row will be passed in as a new line, so if we perform a line count, we will get the number of lines, one per partition: words.pipe("wc -l").collect(). In this case, we could say get five lines per partition.
  - Then learned about: mapPartitions, foreachPartition, ***Glom (It is an interesting function that takes every partition in your dataset and converts them to arrays.*** This can be useful if you’re going to collect the data to the driver and want to have an array for each partition. However, this can cause serious stability issues because if you have large partitions or a large number of partitions, it’s simple to crash the driver).

- Chapter 13: Advanced RDDs
  - Covered advanced topics related to RDDs.
  - There are many methods on RDDs that require you to put your data in a key–value format. A hint that this is required is that the method will include <some-operation> ByKey. Whenever you see ***ByKey*** in a method name, it means that you can perform this only on a PairRDD type. The easiest way is to just map over your current RDD to a basic key–value structure. This means having two values in each record of your RDD: Eg: words.map(lambda word: (word.lower(), 1))
  - Other things learned: keyBy, Mapping over Values, Extracting Keys and Values, lookup, sampleByKey. 
  - You can perform aggregations on plain RDDs or on PairRDDs, depending on the method that you are using. 

```
Eg:
chars = words.flatMap(lambda word: word.lower()) KVcharacters = chars.map(lambda letter: (letter, 1)) def maxFunc(left, right):
return max(left, right) def addFunc(left, right):
return left + right
nums = sc.parallelize(range(1,31), 5)
```

  - Other stuff learned: countByKey, groupByKey, reduceByKey, aggregate, aggregateByKey, combineByKey, foldByKey, ***CoGroups (It give you the ability to group together up to three key–value RDDs together in Scala and two in Python.*** This joins the given values by key. This is effectively just a group-based join on an RDD. When doing this, you can also specify a number of out‐ put partitions or a custom partitioning function to control exactly how this data is distributed across the cluster.)

```
Example of using CoGroups:
import random
distinctChars = words.flatMap(lambda word: word.lower()).distinct() 
charRDD = distinctChars.map(lambda c: (c, random.random())) 
charRDD2 = distinctChars.map(lambda c: (c, random.random())) 
charRDD.cogroup(charRDD2).take(5)
```

  - Other stuffL RDDs have much the same joins as we saw in the Structured API: Inner Join, fullOuterJoin, leftOuterJoin, rightOuterJoin, cartesian
    - ***Also: Zip join*** (Note that it isn’t really a join at all, but it does combine two RDDs, so it’s worth labeling it as a join) allows you to “zip” together two RDDs, assuming that they have the same length. This creates a PairRDD. The two RDDs must have the same number of partitions as well as the same number of elements.
  - With RDDs, you have control over how data is exactly physically distributed across the cluster. 
    - ***coalesce***: Effectively collapses partitions on the same worker in order to avoid a shuffle of the data when repartitioning.
    - ***repartition***: Operation allows you to repartition your data up or down but performs a shuffle across nodes in the process. 
    - ***repartitionAndSortWithinPartitions***: This operation gives you the ability to repartition as well as specify the ordering of each one of those output partitions.
  - ***Custom Partitioning: This ability is one of the primary reasons you’d want to use RDDs.*** Custom partitioners are not available in the Structured APIs because they don’t really have a logical counterpart. They’re a low-level, implementation detail that can have a significant effect on whether your jobs run successfully. 
    - The canonical example to motivate custom partition for this operation is PageRank whereby we seek to control the layout of the data on the cluster and avoid shuffles.
    - In short, the sole goal of custom partitioning is to even out the distribution of your data across the cluster so that you can work around problems like data skew.
    - To perform custom partitioning you need to implement your own class that extends Partitioner.
    - Spark has two built-in Partitioners that you can leverage off in the RDD API:
      - a Hash Partitioner for discrete values and 
      - a RangePartitioner for continuous values. 
    - Spark’s Structured APIs will already use these, although we can use the same thing in RDD.
    - Although the hash and range partitioners are useful, they’re fairly rudimentary. At times, you will need to perform some very low-level partitioning because you’re working with very large data and large key skew. 
    - ***Key skew*** simply means that some keys have many, many more values than other keys. You want to break these keys as much as possible to improve parallelism and prevent OutOfMemoryErrors during the course of execution.
    - One instance might be that you need to partition more keys if and only if the key matches a certain format. For instance, we might know that there are two customers in your dataset that always crash your analysis and we need to break them up further than other customer IDs. In fact, these two are so skewed that they need to be operated on alone, whereas all of the others can be lumped into large groups. This is obviously a bit of a caricatured example, but you might see similar situations in your data, as well:

```
// in Scala
import org.apache.spark.Partitioner
class DomainPartitioner extends Partitioner {
def numPartitions = 3
def getPartition(key: Any): Int = {
val customerId = key.asInstanceOf[Double].toInt
if (customerId == 17850.0 || customerId == 12583.0) {
return 0 }else{
return new java.util.Random().nextInt(2) + 1 }
} }
keyedRDD
.partitionBy(new DomainPartitioner).map(_._1).glom().map(_.toSet.toSeq.length) .take(5)
```
  
  - Then we have the ***issue of Kryo serialization.*** 
    - ***Any object that you hope to parallelize (or function) must be serializable.***
    - The default serialization can be quite slow. Spark can use the Kryo library (version 2) to serialize objects more quickly. Kryo is significantly faster and more compact than Java serialization (often as much as 10x), but ***does not support all serializable types and requires you to register the classes you’ll use in the program in advance*** for best performance.
    - You can use Kryo by initializing your job with a SparkConf and setting the value of "spark.serializer" to "org.apache.spark.serializer.KryoSerializer".
    - The only reason Kryo is not the default is because of the custom registration requirement, but we recommend trying it in any network-intensive application. Since Spark 2.0.0, we internally use Kryo serializer when shuffling RDDs with simple types, arrays of simple types, or string type. Spark automatically includes Kryo serializers for the many commonly used core Scala classes covered in the AllScalaRegistrar from the Twitter chill library. To register your own custom classes with Kryo, use the registerKryoClasses method.

---------------------------------

- Chapter 14: Distributed Shared Variables
  - In addition to the Resilient Distributed Dataset (RDD) interface, the second kind of low-level API in Spark is two types of “distributed shared variables”: 
    - ***Broadcast variables***: Broadcast variables are a way you can share an immutable value efficiently around the cluster without encapsulating that variable in a function closure. The normal way to use a variable in your driver node inside your tasks is to simply reference it in your function closures (e.g., in a map operation), but this can be inefficient, especially for large variables such as a lookup table or a machine learning model. The reason for this is that when you use a variable in a closure, it must be deserialized on the worker nodes many times (one per task). Moreover, if you use the same variable in multiple Spark actions and jobs, it will be re-sent to the workers with every job instead of once. 
      - ***These variables that are cached on every machine in the cluster instead of serialized with every single task.*** The canonical use case is to pass around a large lookup table that fits in memory on the executors and use that in a function. This value is immutable and is lazily replicated across all nodes in the cluster when we trigger an action: Eg: suppBroadcast = spark.sparkContext.broadcast(supplementalData)

      <>attach image for ref<>
      
    - ***Accumulators***: They are a way of updating a value inside of a variety of transformations and ***propagating that value to the driver node in an efficient and fault-tolerant way.*** Accumulators provide a mutable variable that a Spark cluster can safely update on a per-row basis. You can use these for debugging purposes (say to track the values of a certain variable per partition in order to intelligently use it over time) or to create low-level aggregation. Accumulator variables are “added” to only through an associative and commutative operation and can therefore be efficiently supported in parallel. You can use them to implement counters (as in MapReduce) or sums. Spark natively supports accumulators of numeric types, and programmers can add support for new types.
      - For accumulator updates performed inside actions only, Spark guarantees that each task’s update to the accumulator will be applied only once, meaning that restarted tasks will not update the value. In transformations, you should be aware that each task’s update can be applied more than once if tasks or job stages are reexecuted. Accumulators do not change the lazy evaluation model of Spark. If an accumulator is being updated within an operation on an RDD, its value is updated only once that RDD is actually computed (e.g., when you call an action on that RDD or an RDD that depends on it). Consequently, accumulator updates are not guaranteed to be executed when made within a lazy transformation like map(). Eg: accChina = spark.sparkContext.accumulator(0)
      - Accumulators can be both named and unnamed. Named accumulators will display their running results in the Spark UI, whereas unnamed ones will not.
      - Although Spark does provide some default accumulator types, sometimes you might want to build your own custom accumulator. In order to build a custom accumulator you need to subclass the AccumulatorV2 class.

      <>attach image for ref<>

---------------------------------

- Chapter 15: How Spark Runs on a Cluster
  - (How spark runs on a cluster) The ***Spark driver***: 
    - The driver is the process “in the driver seat” of your Spark Application. It is the controller of the execution of a Spark Application and maintains all of the state of the Spark cluster (the state and tasks of the executors). It must interface with the cluster manager in order to actually get physical resources and launch executors.
    - At the end of the day, this is just a process on a physical machine that is responsible for maintaining the state of the application running on the cluster.
  - The ***Spark executors***:
    - Spark executors are the processes that perform the tasks assigned by the Spark driver. Executors have one core responsibility: take the tasks assigned by the driver, run them, and report back their state (success or failure) and results. Each Spark Application has its own separate executor processes.
  - The ***cluster manager***: 
    - The Spark Driver and Executors do not exist in a void, and this is where the cluster manager comes in. The cluster manager is responsible for maintaining a cluster of machines that will run your Spark Application(s). Somewhat confusingly, a cluster manager will have its own “driver” (sometimes called master) and “worker” abstractions. The core difference is that these are tied to physical machines rather than processes (as they are in Spark).
    - When it comes time to actually run a Spark Application, we request resources from the cluster manager to run it. Depending on how our application is configured, this can include a place to run the Spark driver or might be just resources for the execu‐ tors for our Spark Application. Over the course of Spark Application execution, the cluster manager will be responsible for managing the underlying machines that our application is running on.
    - Spark currently supports three cluster managers: ***a simple built-in standalone cluster manager, Apache Mesos, and Hadoop YARN***. However, this list will continue to grow...
  - An execution mode gives you the power to determine where the aforementioned resources are physically located when you go to run your application. You have three modes to choose from:
    - ***Cluster mode***: Cluster mode is probably the most common way of running Spark Applications. In cluster mode, a user submits a pre-compiled JAR, Python script, or R script to a cluster manager. The cluster manager then launches the driver process on a worker node inside the cluster, in addition to the executor processes. This means that the cluster manager is responsible for maintaining all Spark Application–related processes.
    - ***Client mode***: Client mode is nearly the same as cluster mode except that the Spark driver remains on the client machine that submitted the application. This means that the client machine is responsible for maintaining the Spark driver process, and the cluster manager maintains the executor processes. The driver is running on a machine outside of the cluster but that the workers are located on machines in the cluster.
    - ***Local mode***: Local mode is a significant departure from the previous two modes: it runs the entire Spark Application on a single machine. It achieves parallelism through threads on that single machine. This is a common way to learn Spark, to test your applications, or experiment iteratively with local development. However, we do not recommend using local mode for running production applications.
  - ***The Life Cycle of a Spark Application (Outside)***: 
    - The first step is for you to submit an actual application. ***This will be a pre-compiled JAR or library***. At this point, you are executing code on your local machine and you’re going to make a request to the cluster manager driver node. Here, we are explicitly asking for resources for the Spark driver process only. We assume that the cluster manager accepts this offer and places the driver onto a node in the cluster. The client process that submitted the original job exits and the application is off and running on the cluster.
    - To do this, you’ll run something like the following command in your terminal: `./bin/spark-submit --class <main-class> --master <master-url> --deploy-mode cluster --conf <key>=<value> ... # other options`
    - Now that the driver process has been placed on the cluster, it begins running user code.
    - This code must include a SparkSession that initializes a Spark cluster (e.g., driver + executors). The SparkSession will subsequently communicate with the cluster manager asking it to launch Spark executor processes across the cluster. 
    - The number of executors and their relevant configurations are set by the user via the command-line arguments in the original spark-submit call.
    - The cluster manager responds by launching the executor processes (assuming all goes well) and sends the relevant information about their locations to the driver process. After everything is hooked up correctly, we have a “Spark Cluster” as you likely think of it today.
    - Now that we have a “Spark Cluster,” Spark goes about its merry way executing code.  
    - The driver and the workers communicate among themselves, executing code and moving data around. The driver schedules tasks onto each worker, and each worker responds with the status of those tasks and success or failure. 
    - After a Spark Application completes, the driver processs exits with either success or failure. The cluster manager then shuts down the executors in that Spark cluster for the driver. At this point, you can see the success or failure of the Spark Application by asking the cluster manager for this information.
  - ***The Life Cycle of a Spark Application (Inside)***: 
    - The first step of any Spark Application is creating a SparkSession. In many interactive modes, this is done for you, but in an application, you must do it manually.
    - After you have a SparkSession, you should be able to run your Spark code. From the SparkSession, you can access all of low-level and legacy contexts and configurations accordingly, as well. Note that the ***SparkSession class was only added in Spark 2.X. Older code you might find would instead directly create a SparkContext and a SQLContext for the structured APIs***.
    - A SparkContext object within the SparkSession represents the connection to the Spark cluster. This class is how you communicate with some of Spark’s lower-level APIs, such as RDDs. It is commonly stored as the variable sc in older examples and documentation. Through a SparkContext, you can create RDDs, accumulators, and broadcast variables, and you can run code on the cluster. For the most part, you should not need to explicitly initialize a SparkContext; you should just be able to access it through the SparkSession. ***In previous versions of Spark, the SQLContext and HiveContext provided the ability to work with DataFrames and Spark SQL and were commonly stored as the variable sqlContext in examples, documentation, and legacy code. As a historical point, Spark 1.X had effectively two contexts. The SparkContext and the SQLContext. These two each performed different things. The former focused on more fine-grained control of Spark’s central abstractions, whereas the latter focused on the higher-level tools like Spark SQL. In Spark 2.X, the community combined the two APIs into the centralized SparkSession that we have today.*** However, both of these APIs still exist and you can access them via the SparkSession. 
    - After you initialize your SparkSession, it’s time to execute some code.

    ```
        from pyspark.sql import SparkSession
        spark = SparkSession.builder.master("local").appName("Word Count")\
              .config("spark.some.config.option", "some-value")\
              .getOrCreate()
    ```
    
    - As you saw earlier, Spark code essentially consists of transformations and actions. How you build these is up to you—whether it’s through SQL, low-level RDD manipulation, or machine learning algorithms. Say when you run a piece of code, your action triggers one complete Spark job. If you explain() it, will look like:

    ```
        == Physical Plan ==
        *HashAggregate(keys=[], functions=[sum(id#15L)])
        +- Exchange SinglePartition
         +- *HashAggregate(keys=[], functions=[partial_sum(id#15L)])
            +- *Project [id#15L]
               +- *SortMergeJoin [id#15L], [id#10L], Inner
                  :- *Sort [id#15L ASC NULLS FIRST], false, 0
                  :  +- Exchange hashpartitioning(id#15L, 200)
        +- *Project [(id#7L * 5) AS id#15L]
           +- Exchange RoundRobinPartitioning(5)
        +- *Range (2, 10000000, step=2, splits=8)
                         +- Exchange hashpartitioning(id#10L, 200)
                            +- Exchange RoundRobinPartitioning(6)
                               +- *Range (2, 10000000, step=4, splits=8)
    ```
    - In general, there should be one Spark job for one action. Actions always return results. Each job breaks down into a series of stages, the number of which depends on how many shuffle operations need to take place.

    ```
    A job breakdown may look like: 
    • Stage 1 with 8 Tasks
    • Stage 2 with 8 Tasks
    • Stage 3 with 6 Tasks
    • Stage 4 with 5 Tasks
    • Stage 5 with 200 Tasks
    • Stage 6 with 1 Task       
    ```
    - ***Stages in Spark represent groups of tasks that can be executed together to compute the same operation on multiple machines.*** In general, Spark will try to pack as much work as possible (i.e., as many transformations as possible inside your job) into the same stage, but the engine starts new stages after operations called shuffles. A shuffle represents a physical repartitioning of the data—for example, sorting a DataFrame, or grouping data that was loaded from a file by key (which requires sending records with the same key to the same node). This type of repartitioning requires coordinating across executors to move data around. Spark starts a new stage after each shuffle, and keeps track of what order the stages must run in to compute the final result.
      - In the job we looked at earlier, the first two stages correspond to the range that you perform in order to create your DataFrames. By default when you create a DataFrame with range, it has eight partitions. The next step is the repartitioning. This changes the number of partitions by shuffling the data. These DataFrames are shuffled into six partitions and five partitions, corresponding to the number of tasks in stages 3 and 4.
      - Stages 3 and 4 perform on each of those DataFrames and the end of the stage repre‐ sents the join (a shuffle). Suddenly, we have 200 tasks. This is because of a Spark SQL configuration. The spark.sql.shuffle.partitions default value is 200, which means that when there is a shuffle performed during execution, it outputs 200 shuffle partitions by default. You can change this value, and the number of output partitions will change.
      - ***A good rule of thumb is that the number of partitions should be larger than the number of executors on your cluster,*** potentially by multiple factors depending on the workload.
      - Each task corresponds to a combination of blocks of data and a set of transformations that will run on a single executor. If there is one big partition in our dataset, we will have one task. If there are 1,000 little partitions, we will have 1,000 tasks that can be executed in parallel. A task is just a unit of computation applied to a unit of data (the partition). Partitioning your data into a greater number of partitions means that more can be executed in parallel.
    - Execution Details: Spark automatically ***pipelines stages and tasks*** that can be done together, such as a map operation followed by another map operation. 
      - An important part of what makes Spark an “in-memory computation tool” is that unlike the tools that came before it (e.g., MapReduce), Spark performs as many steps as it can at one point in time before writing data to memory or disk. 
      - One of the key optimizations that ***Spark performs is pipelining, which occurs at and below the RDD level. With pipelining, any sequence of operations that feed data directly into each other, without needing to move it across nodes, is collapsed into a single stage of tasks that do all the operations together.*** For example, if you write an RDD-based program that does a map, then a filter, then another map, these will result in a single stage of tasks that immediately read each input record, pass it through the first map, pass it through the filter, and pass it through the last map function if needed. This pipelined version of the computation is much faster than writing the intermediate results to memory or disk after each step. The same kind of pipelining happens for a DataFrame or SQL computation that does a select, filter, and select.
      - Second, for all shuffle operations, Spark writes the data to stable storage (e.g., disk), and can reuse it across multiple jobs. This is called ***Shuffle Persistence***. When Spark needs to run an operation that has to move data across nodes, such as a reduce-by-key operation (where input data for each key needs to first be brought together from many nodes), the engine can’t perform pipelining anymore, and instead it performs a cross-network shuffle. Spark always executes shuffles by first having the “source” tasks (those sending data) write shuffle files to their local disks during their execution stage. Then, the stage that does the grouping and reduction launches and runs tasks that fetch their corresponding records from each shuffle file and performs that computa‐ tion (e.g., fetches and processes the data for a specific range of keys). Saving the shuffle files to disk lets Spark run this stage later in time than the source stage (e.g., if there are not enough executors to run both at the same time), and also lets the engine re-launch reduce tasks on failure without rerunning all the input tasks.
        - One side effect you’ll see for shuffle persistence is that running a new job over data that’s already been shuffled does not rerun the “source” side of the shuffle. Because the shuffle files were already written to disk earlier, Spark knows that it can use them to run the later stages of the job, and it need not redo the earlier ones. In the Spark UI and logs, you will see the pre-shuffle stages marked as “skipped”. This automatic optimization can save time in a workload that runs multiple jobs over the same data, but of course, for even better performance you can perform your own caching with the DataFrame or RDD cache method, which lets you control exactly which data is saved and where. 

---------------------------------

- Chapter 16: Developing Spark Applications
  - Writing spark application, Testing it: Input data resilience, Business logic resilience and evolution, Resilience in output and atomicity... 
  - Testing your Spark code using a unit test framework like JUnit or ScalaTest is relatively easy because of Spark’s local mode—just create a local mode SparkSession as part of your test harness to run it.
  - Different options in spark submit or launching application. 
  - Spark includes a number of different configurations; The majority of configurations fall into the following categories: Application properties, Runtime environment, Shuffle behavior, Spark UI, Compression and serialization, Memory management, Execution behavior, Networking, Scheduling, Dynamic allocation, Security, Encryption, Spark SQL, Spark streaming, SparkR. 
  - Spark provides three locations to configure the system:
    - Spark properties control most application parameters and can be set by using a ***SparkConf object***
    - Java system properties
    - Hardcoded configuration files

<put image of application properties> 

  - Other stuff: Runtime Properties, Execution Properties, Configuring Memory Management, Configuring Shuffle Behavior, Environmental Variables...
  - ***By default, Spark’s scheduler runs jobs in FIFO fashion.*** If the jobs at the head of the queue don’t need to use the entire cluster, later jobs can begin to run right away, but if the jobs at the head of the queue are large, later jobs might be delayed significantly.
  - It is also possible to configure fair sharing between jobs. Under ***fair sharing***, Spark assigns tasks between jobs in a round-robin fashion so that all jobs get a roughly equal share of cluster resources. This means that short jobs submitted while a long job is running can begin receiving resources right away and still achieve good response times without waiting for the long job to finish. This mode is best for multi‐user settings. ***To enable the fair scheduler,*** set the spark.scheduler.mode property to FAIR when configuring a SparkContext. The fair scheduler also supports grouping jobs into pools, and setting different scheduling options, or weights, for each pool. This can be useful to create a high-priority pool for more important jobs or to group the jobs of each user together and give users equal shares regardless of how many concurrent jobs they have instead of giving jobs equal shares. This approach is modeled after the Hadoop Fair Scheduler. Without any intervention, newly submitted jobs go into a default pool, but jobs pools can be set by adding the spark.scheduler.pool local property to the SparkContext in the thread that’s submitting them. This is done as follows (assuming sc is your SparkContext): `sc.setLocalProperty("spark.scheduler.pool", "pool1")`. After setting this local property, all jobs submitted within this thread will use this pool name. ***The setting is per-thread to make it easy to have a thread run multiple jobs on behalf of the same user.*** If you’d like to clear the pool that a thread is associated with, set it to null.
  - Spark should work similarly with all the supported cluster managers; However, customizing the setup means understanding the intricacies of each of the cluster management systems. The hard part is deciding on the cluster manager (or choosing a managed service). 
    - Spark has three officially supported cluster managers: Standalone mode, Hadoop YARN, Apache Mesos. Naturally, each of these cluster managers has an opinionated view toward management, and so there are trade-offs and semantics that you will need to keep in mind. 
    - Spark’s standalone cluster manager is a lightweight platform built specifically for Apache Spark workloads. Using it, you can run multiple Spark Applications on the same cluster. 
    - The main disadvantage of the standalone mode is that it’s more limited than the other cluster managers—in particular, your cluster can only run Spark. It’s probably the best starting point if you just want to quickly get Spark run‐ ning on a cluster, however, and you do not have experience using YARN or Mesos.
    - Hadoop YARN is a framework for job scheduling and cluster resource management. Even though Spark is often (mis)classified as a part of the “Hadoop Ecosystem,” in reality, Spark has little to do with Hadoop. Spark does natively support the Hadoop YARN cluster manager but it requires nothing from Hadoop itself. You can run your Spark jobs on Hadoop YARN by specifying the master as YARN in the spark-submit command-line arguments. Just like with standalone mode, there are a number of knobs that you are able to tune according to what you would like the cluster to do. The number of knobs is naturally larger than that of Spark’s standalone mode because Hadoop YARN is a generic scheduler for a large number of different execution frameworks.
    - For the most part, Mesos intends to be a datacenter scale-cluster manager that manages not just short-lived applications like Spark, but long-running applications like web applications or other resource interfaces. Mesos is the heaviest-weight cluster manager, simply because you might choose this cluster manager only if your organization already has a large-scale deployment of Mesos, but it makes for a good cluster manager nonetheless.

---------------------------------

- Chapter 17: Deploying Spark
  - There are two high-level options for where to deploy Spark clusters: 
    - deploy in an on-premises cluster or in the public cloud. 
    - Deploying Spark to an on-premises cluster is sometimes a reasonable option, especially for organizations that already manage their own datacenters. As with everything else, there are trade-offs to this approach. An on-premises cluster gives you full control over the hardware used, meaning you can optimize performance for your specific workload. However, it also introduces some challenges, especially when it comes to data analytics workloads like Spark. First, with on-premises deployment, your cluster is fixed in size, whereas the resource demands of data analytics work‐ loads are often elastic. If you make your cluster too small, it will be hard to launch the occasional very large analytics query or training job for a new machine learning model, whereas if you make it large, you will have resources sitting idle. Second, for on-premises clusters, you need to select and operate your own storage system, such as a Hadoop file system or scalable key-value store. This includes setting up georeplication and disaster recovery if required. If you are going to deploy on-premises, the best way to combat the resource utilization problem is to use a cluster manager that allows you to run many Spark applica‐ tions and dynamically reassign resources between them, or even allows non-Spark applications on the same cluster. All of Spark’s supported cluster managers allow multiple concurrent applications, but YARN and Mesos have better support for dynamic sharing and also additionally support non-Spark workloads. Handling resource shar‐ ing is likely going to be the biggest difference your users see day to day with Spark on-premise versus in the cloud: in public clouds, it’s easy to give each application its own cluster of exactly the required size for just the duration of that job.
    - While early big data systems were designed for on-premises deployment, the cloud is now an increasingly common platform for deploying Spark. The public cloud has several advantages when it comes to big data workloads. First, resources can be launched and shut down elastically, so you can run that occasional “monster” job that takes hundreds of machines for a few hours without having to pay for them all the time. Even for normal operation, you can choose a different type of machine and cluster size for each application to optimize its cost performance—for example, launch machines with Graphics Processing Units (GPUs) just for your deep learning jobs. Second, public clouds include low-cost, georeplicated storage that makes it easier to manage large amounts of data.
    - Many companies looking to migrate to the cloud imagine they’ll run their applications in the same way that they run their on-premises clusters. All the major cloud providers (Amazon Web Services [AWS], Microsoft Azure, Google Cloud Platform [GCP], and IBM Bluemix) include managed Hadoop clusters for their customers, which provide HDFS for storage as well as Apache Spark. This is actually not a great way to run Spark in the cloud, however, because by using a fixed-size cluster and file system, you are not going to be able to take advantage of elasticity. Instead, it is generally a better idea to use global storage systems that are decoupled from a specific cluster, such as Amazon S3, Azure Blob Storage, or Google Cloud Storage and spin up machines dynamically for each Spark workload. 
    - With decoupled compute and storage, you will be able to pay for computing resources only when needed, scale them up dynamically, and mix different hardware types. Basically, keep in mind that running Spark in the cloud need not mean migrating an on-premises installation to virtual machines: you can run Spark natively against cloud storage to take full advantage of the cloud’s elasticity, cost-saving benefit, and management tools without having to manage an on-premise computing stack within your cloud environment.
    - Several companies provide “cloud-native” Spark-based services, and all installations of Apache Spark can of course connect to cloud storage. Databricks, the company started by the Spark team from UC Berkeley, is one example of a service provider built specifically for Spark in the cloud. 
  - Other stuff: Configuring Spark on YARN Applications, Secure Deployment Configurations, Cluster Networking Configurations, Application Scheduling...

---------------------------------

- Chapter 18: Monitoring and Debugging
  - At some point, you’ll need to monitor your Spark jobs to understand where issues are occuring in them.
  - Let’s review the ***spark components we can monitor***:
    - Spark Applications and Jobs 
    - JVM
      - JVM utilities such as jstack for providing stack traces, jmap for creating heap-dumps, jstat for report‐ ing time–series statistics, and jconsole for visually exploring various JVM proper‐ ties are useful for those comfortable with JVM internals. You can also use a tool like jvisualvm to help profile Spark jobs. Some of this information is provided in the Spark UI, but for very low-level debugging, the aforementioned tools can come in handy.
    - OS/Machine 
      - The JVMs run on a host operating system (OS) and it’s important to monitor the state of those machines to ensure that they are healthy. This includes monitoring things like CPU, network, and I/O. These are often reported in cluster-level monitoring solutions; however, there are more specific tools that you can use, including dstat, iostat, and iotop.
    - Cluster 
      - Some popular cluster-level monitoring tools include Ganglia and Prometheus
    - Driver 
      - This is where all of the state of your application lives, and you’ll need to be sure it’s running in a stable manner. If you could monitor only one machine or a single JVM, it would definitely be the driver.
    - Queries, Jobs, Stages, and Tasks
    - Spark Logs (One challenge, however, is that Python won’t be able to integrate directly with Spark’s Java-based logging library. Using Python’s logging module or even simple print statements will still print the results to standard error, however, and make them easy to find. To change Spark’s log level, simply run the following command: `spark.sparkContext.setLogLevel("INFO")`)
    - Spark UI: 
      - The Spark UI provides a visual way to monitor applications while they are running as well as metrics about your Spark workload, at the Spark and JVM level. In addition to the Spark UI, you can also access Spark’s status and metrics via a REST API. For the most part this API exposes the same information presented in the web UI, except that it doesn’t include any of the SQL-related information (can get via API). Normally, the Spark UI is only available while a SparkContext is running, so how can you get to it after your application crashes or ends? To do this, ***Spark includes a tool called the Spark History Server that allows you to reconstruct the Spark UI and REST API, provided that the application was configured to save an event log***.
  - There are two main things you will want to monitor: 
    - the processes running your application (at the level of CPU usage, memory usage, etc.), and 
    - the query execution inside it (e.g., jobs and tasks).
  - Other stuff: Discuss on debugging techiniques, errors one may get (OOM, unexpected Null, serialization error, etc)

---------------------------------

- Chapter 19: Performance Tuning
  - There are a variety of different parts of Spark jobs that you might want to optimize, and it’s valuable to be specific. Following are some of the areas:
    - Code-level design choices (e.g., RDDs versus DataFrames)
    - Data at rest
    - Joins
    - Aggregations
    - Data in flight
    - Individual application properties
    - Inside of the Java Virtual Machine (JVM) of an executor
    - Worker nodes
    - Cluster and deployment properties (And many more)
  - Scala versus Java versus Python versus R: 
    - This question is nearly impossible to answer in the general sense because a lot will depend on your use case. 
    - ***Spark’s Structured APIs are consistent across languages in terms of speed and stability.***
  - DataFrames versus SQL versus Datasets versus RDDs:
    - ***Across all languages, DataFrames, Datasets, and SQL are equivalent in speed.*** This means that if you’re using DataFrames in any of these languages, performance is equal. 
    - ***However, if you’re going to be defining UDFs, you’ll take a performance hit writing those in Python or R,*** and to some extent a lesser performance hit in Java and Scala. If you want to optimize for pure performance, it would behoove you to try and get back to DataFrames and SQL as quickly as possible. Although all DataFrame, SQL, and Dataset code compiles down to RDDs, Spark’s optimization engine will write “better” RDD code than you can manually and certainly do it with orders of magnitude less effort. Additionally, you will lose out on new optimizations that are added to Spark’s SQL engine every release.
    - Lastly, ***if you want to use RDDs, we definitely recommend using Scala or Java.*** If that’s not possible, we recommend that you restrict the “surface area” of RDDs in your application to the bare minimum. That’s because when Python runs RDD code, it’s serializes a lot of data to and from the Python process. This is very expensive to run over very big data and can also decrease stability.
  - (Discussed earlier) ***When you’re working with custom data types, you’re going to want to serialize them using Kryo because it’s both more compact and much more efficient than Java serialization.***
  - Cluster Configurations:
    - This area has huge potential benefits but is probably one of the more difficult to prescribe because of the variation across hardware and use cases. 
    - Cluster/application sizing and sharing, Dynamic allocation (Spark provides a mechanism to dynamically adjust the resources your application occupies based on the workload, spark.dynamicAllocation.enabled to true)
  - Scheduling: 
    - Scheduling optimizations do involve some research and experimentation, and unfortunately there are not super quick fixes beyond ***setting spark.scheduler.mode to FAIR to allow better sharing of resources across multiple users, or setting --max-executor-cores, which specifies the maximum number of executor cores that your application will need.***
  - Data at Rest: 
    - More often that not, when you’re saving data it will be read many times as other folks in your organization access the same datasets in order to run different analyses. ***Making sure that you’re storing your data for effective reads later on is absolutely essential*** to successful big data projects.
    - This involves choosing your storage system, choosing your data format, and taking advantage of features such as data partitioning in some storage formats.
  - File-based long-term data storage: 
    - ***Generally you should always favor structured, binary types to store your data, especially when you’ll be accessing it frequently.*** Although files like ***“CSV” seem well-structured, they’re very slow to parse,*** and often also full of edge cases and pain points. 
    - ***The most efficient file format you can generally choose is Apache Parquet.*** Parquet stores data in binary files with column-oriented storage, and also tracks some statistics about each file that make it possible to quickly skip data not needed for a query. It is well integrated with Spark through the built-in Parquet data source.
  - Splittable file types and compression:
    - Whatever file format you choose, you should make sure it is “splittable”, which means that different tasks can read different parts of the file in parallel. 
    - When we read in the file, all cores were able to do part of the work. That’s because the file was splittable. If we didn’t use a splittable file type— say something like a malformed JSON file—we’re going to need to read in the entire file on a single machine, greatly reducing parallelism.
    - ***The main place splittability comes in is compression formats. A ZIP file or TAR archive cannot be split, which means that even if we have 10 files in a ZIP file and 10 cores, only one core can read in that data because we cannot parallelize access to the ZIP file. This is a poor use of resources. In contrast, files compressed using gzip, bzip2, or lz4 are generally splittable*** if they were written by a parallel processing framework like Hadoop or Spark.
  - Table partitioning:
    - Table partitioning refers to storing files in separate directories based on a key, such as the date field in the data. Storage managers like Apache Hive support this concept, as do many of Spark’s built-in data sources. 
    - Partitioning your data correctly allows Spark to skip many irrelevant files when it only requires data with a specific range of keys. For instance, if users frequently filter by “date” or “customerId” in their queries, partition your data by those columns. This will greatly reduce the amount of data that end users must read by most queries, and therefore dramatically increase speed.
    - The one downside of partitioning, however, is that ***if you partition at too fine a granularity, it can result in many small files, and a great deal of overhead trying to list all the files in the storage system.***
    - Bucketing: 
      - Bucketing your data allows Spark to “pre-partition” data according to how joins or aggregations are likely to be performed by readers. This can improve performance and stability because data can be consistently distributed across partitions as opposed to skewed into just one or two. For instance, if joins are frequently performed on a column immediately after a read, you can use bucketing to ensure that the data is well partitioned according to those values. This can help prevent a shuffle before a join and therefore help speed up data access. 
      - Bucketing generally works hand-in-hand with partitioning as a second way of physically splitting up data.
  - File count: 
    - If there are lots of small files, you’re going to pay a price listing and fetching each of those individual files. For instance, if you’re reading a data from Hadoop Distributed File System (HDFS), this data is managed in blocks that are up to 128 MB in size (by default). This means if you have 30 files, of 5 MB each, you’re going to have to potentially request 30 blocks, even though the same data could have fit into 2 blocks (150 MB total).
    - ***Having lots of small files is going to make the scheduler work much harder to locate the data and launch all of the read tasks.*** This can increase the network and scheduling overhead of the job. Having fewer large files eases the pain off the scheduler but it will also make tasks run longer. In this case, though, you can always launch more tasks than there are input files if you want more parallelism—Spark will split each file across multiple tasks assuming you are using a splittable format. In general, we recommend sizing your files so that they each contain at least a few tens of megabytes of data.
    - To control how many records go into each file, you can specify the maxRecordsPerFile option to the write operation.
  - Data locality:
    - Another aspect that can be important in shared cluster environments is data locality. Data locality basically specifies a preference for certain nodes that hold certain data, rather than having to exchange these blocks of data over the network. If you run your storage system on the same nodes as Spark, and the system supports locality hints, Spark will try to schedule tasks close to each input block of data. For example HDFS storage provides this option. There are several configurations that affect locality, but it will generally be used by default if Spark detects that it is using a local storage system. 
  - Statistics collection: 
    - Spark includes a cost-based query optimizer that plans queries based on the properties of the input data when using the structured APIs. However, to allow the cost-based optimizer to make these sorts of decisions, you need to collect (and maintain) statistics about your tables that it can use. There are two kinds of statistics: table-level and column-level statistics. 
    - Statistics collection is available only on named tables, not on arbitrary DataFrames or RDDs. 
    - To collect table-level statistics, you can run the following command: ANALYZE TABLE table_name COMPUTE STATISTICS
    - To collect column-level statistics, you can name the specific columns: ANALYZE TABLE table_name COMPUTE STATISTICS FOR COLUMNS column_name1, column_name2, ...
    - Column-level statistics are slower to collect, but provide more information for the cost-based optimizer to use about those data columns. Both types of statistics can help with joins, aggregations, filters, and a number of other potential things 
  - Shuffle Configurations: 
    - Configuring Spark’s external shuffle service can often increase performance because it allows nodes to read shuffle data from remote machines even when the executors on those machines are busy (e.g., with garbage collection). 
    - In addition, for RDD-based jobs, the serialization format has a large impact on shuffle performance—always prefer Kryo over Java serialization.
  - Memory Pressure and Garbage Collection: 
    - During the course of running Spark jobs, the executor or driver machines may struggle to complete their tasks because of a lack of sufficient memory or “memory pressure.” This may occur when an application takes up too much memory during execution or when garbage collection runs too frequently or is slow to run as large numbers of objects are created in the JVM and subsequently garbage collected as they are no longer used. 
    - ***One strategy for easing this issue is to ensure that you’re using the Structured APIs as much as possible.*** These will not only increase the efficiency with which your Spark jobs will execute, but it will also greatly reduce memory pressure because JVM objects are never realized and Spark SQL simply performs the computation on its internal format.
    - To further tune garbage collection, you first need to understand some basic information about memory management in the JVM:
      - Java heap space is divided into two regions: Young and Old. The Young genera‐ tion is meant to hold short-lived objects whereas the Old generation is intended for objects with longer lifetimes.
      - The Young generation is further divided into three regions: Eden, Survivor1, and Survivor2.
      - Here’s a simplified description of the garbage collection procedure:
        - When Eden is full, a minor garbage collection is run on Eden and objects that are alive from Eden and Survivor1 are copied to Survivor2.
        - The Survivor regions are swapped.
        - If an object is old enough or if Survivor2 is full, that object is moved to Old.
        - Finally, when Old is close to full, a full garbage collection is invoked. This involves tracing through all the objects on the heap, deleting the unreferenced ones, and moving the others to fill up unused space, so it is generally the slowest garbage collection operation.
      - The goal of garbage collection tuning in Spark is to ensure that only long-lived cached datasets are stored in the Old generation and that the Young generation is sufficiently sized to store all short-lived objects. This will help avoid full garbage collections to collect temporary objects created during task execution. 
      - You can specify garbage collection tuning flags for executors by setting spark.executor.extraJavaOptions in a job’s configuration. And more details...
  - Direct Performance Enhancements:
    - Parallelism: The first thing you should do whenever trying to speed up a specific stage is to increase the degree of parallelism. In general, we recommend having at least two or three tasks per CPU core in your cluster if the stage processes a large amount of data. You can set this via the spark.default.parallelism property as well as tuning the spark.sql.shuffle.partitions according to the number of cores in your cluster.
    - Improved Filtering: Another frequent source of performance enhancements is moving filters to the earliest part of your Spark job that you can. 
    - Repartitioning and Coalescing: Repartition calls can incur a shuffle. However, doing some can optimize the overall execution of a job by balancing data across the cluster, so they can be worth it. In general, you should try to shuffle the least amount of data possible. For this reason, if you’re reducing the number of overall partitions in a DataFrame or RDD, first try coalesce method, which will not perform a shuffle but rather merge partitions on the same node into one partition.
    - Custom partitioning
    - User-Defined Functions (UDFs): ***In general, avoiding UDFs is a good optimization opportunity. UDFs are expensive because they force representing data as objects in the JVM and sometimes do this multiple times per record in a query. You should try to use the Structured APIs as much as possible to perform your manipulations simply because they are going to perform the transformations in a much more efficient manner than you can do in a high-level language.***
    - Temporary Data Storage (Caching): 
      - In applications that reuse the same datasets over and over, one of the most useful optimizations is caching. Caching will place a DataFrame, table, or RDD into temporary storage (either memory or disk) across the executors in your cluster, and make subsequent reads faster. ***Although caching might sound like something we should do all the time, it’s not always a good thing to do. That’s because caching data incurs a serialization, deserialization, and storage cost.*** For example, if you are only going to process a dataset once (in a later transformation), caching it will only slow you down.
      - Caching is a lazy operation, meaning that things will be cached only as they are accessed. The RDD API and the Structured API differ in how they actually perform caching.
      - ***When we cache an RDD, we cache the actual, physical data (i.e., the bits). The bits. When this data is accessed again, Spark returns the proper data. This is done through the RDD reference. However, in the Structured API, caching is done based on the physical plan. This means that we effectively store the physical plan as our key (as opposed to the object reference) and perform a lookup prior to the execution of a Structured job.***
  - Joins: Joins are a common area for optimization. Equi-joins are the easiest for Spark to optimize at this point and therefore should be preferred wherever possible. Beyond that, simple things like trying to use the filtering ability of inner joins by changing join ordering can yield large speedups. Additionally, using broadcast join hints can help Spark make intelligent planning decisions when it comes to creating query plans avoiding Cartesian joins or even full outer joins is often low-hanging fruit for stability and optimizations because these can often be optimized into different filtering style joins when you look at the entire data flow instead of just that one particular job area. 
  - Aggregations: For the most part, there are not too many ways that you can optimize specific aggregations beyond filtering data before the aggregation having a sufficiently high number of partitions. However, if you’re using RDDs, controlling exactly how these aggregations are performed (e.g., using reduceByKey when possible over groupByKey) can be very helpful and improve the speed and stability of your code.
  - Broadcast Variables: We touched on broadcast joins and variables in previous chapters, and these are a good option for optimization. The basic premise is that if some large piece of data will be used across multiple UDF calls in your program, you can broadcast it to save just a single read-only copy on each node and avoid re-sending this data with each job.

---------------------------------

- Chapter 20: Stream Processing Fundamentals
  - Apache Spark has a long history of high-level support for streaming. In 2012, the project incorporated Spark Streaming and its DStreams API, one of the first APIs to enable stream processing using high-level functional operators like map and reduce. Hundreds of organizations now use DStreams in production for large real-time applications, often processing terabytes of data per hour. Much like the Resilient Distributed Dataset (RDD) API, however, the DStreams API is based on relatively low-level operations on Java/Python objects that limit opportunities for higher-level optimization. Thus, in 2016, the Spark project added Structured Streaming, a new streaming API built directly on DataFrames that supports both rich optimizations and significantly simpler integration with other DataFrame and Dataset code. The Structured Streaming API was marked as stable in Apache Spark 2.2.
  - ***Stream processing is the act of continuously incorporating new data to compute a result.*** In stream processing, the input data is unbounded and has no predetermined beginning or end. It simply forms a series of events that arrive at the stream process‐ ing system (e.g., credit card transactions, clicks on a website, or sensor readings from Internet of Things [IoT] devices). User applications can then compute various queries over this stream of events (e.g., tracking a running count of each type of event or aggregating them into hourly windows). The application will output multiple versions of the result as it runs, or perhaps keep it up to date in an external “sink” system such as a key-value store.
  - Although streaming and batch processing sound different, in practice, they often need to work together. For example, streaming applications often need to join input data against a dataset written periodically by a batch job, and the output of streaming jobs is often files or tables that are queried in batch jobs.
  - 6 common use cases with varying requirements from the underlying stream processing system: Notifications and alerting, Real-time reporting, Incremental ETL, Update data to serve in real time, Real-time decision making, Online machine learning
  - Stream processing is essential in two cases. 
    - First, stream processing enables lower latency: when your application needs to respond quickly (on a timescale of minutes, seconds, or milliseconds), you will need a streaming system that can keep state in memory to get acceptable performance. Many of the decision making and alerting use cases we described fall into this camp. 
    - Second, stream processing can also be more efficient in updating a result than repeated batch jobs, because it automatically incrementalizes the computation. For example, if we want to compute web traffic statistics over the past 24 hours, a naively implemented batch job might scan all the data each time it runs, always processing 24 hours’ worth of data. In contrast, a streaming system can remember state from the previous computation and only count the new data. 
  - To summarize, the challenges: 
    - Processing out-of-order data based on application timestamps (also called event time)
    - Maintaining large amounts of state
    - Supporting high-data throughput
    - Processing each event exactly once despite machine failures
    - Handling load imbalance and stragglers
    - Responding to events at low latency
    - Joining with external data in other storage systems
    - Determining how to update output sinks as new events arrive
    - Writing data transactionally to output systems
    - Updating your application’s business logic at runtime
  - Stream Processing Design Points: 
    - ***Record-at-a-Time Versus Declarative APIs***: The simplest way to design a streaming API would be to just pass each event to the application and let it react using custom code. Streaming that provide this kind of record-at-a-time API just give the user a collection of “plumbing” to connect together into an application. With a record-at-a-time API, you are responsible for tracking state over longer time periods, dropping it after some time to clear up space, and responding differently to duplicate events after a failure. Programming these systems correctly can be quite challenging. At its core, low-level APIs require deep expertise to be develop and maintain.As a result, many newer streaming systems provide declarative APIs, where your application specifies what to compute but not how to compute it in response to each new event and how to recover from failure. Spark’s original DStreams API, for exam‐ ple, offered functional API based on operations like map, reduce and filter on streams. Internally, the DStream API automatically tracked how much data each operator had processed, saved any relevant state reliably, and recovered the computation from fail‐ ure when needed. Systems such as Google Dataflow and Apache Kafka Streams pro‐ vide similar, functional APIs. Spark’s Structured Streaming actually takes this concept even further, switching from functional operations to relational (SQL-like) ones that enable even richer automatic optimization of the execution without programming effort. 
    - ***Event Time Versus Processing Time***: For the systems with declarative APIs, a second concern is whether the system natively supports event time. Event time is the idea of processing data based on timestamps inserted into each record at the source, as opposed to the time when the record is received at the streaming application (which is called processing time). In particular, when using event time, records may arrive to the system out of order (e.g., if they traveled back on different network paths), and different sources may also be out of sync with each other (some records may arrive later than other records for the same event time). If your application collects data from remote sources that may be delayed, such as mobile phones or IoT devices, event-time processing is crucial: without it, you will miss important patterns when some data is late. In contrast, if your application only processes local events (e.g., ones generated in the same datacenter), you may not need sophisticated event-time processing. When using event-time, several issues become common concerns across applications, including tracking state in a manner that allows the system to incorporate late events, and determining when it is safe to output a result for a given time window in event time (i.e., when the system is likely to have received all the input up to that point). Because of this, many declarative systems, including Structured Streaming, have “native” support for event time integrated into all their APIs, so that these concerns can be handled automatically across your whole program.
    - ***Continuous Versus Micro-Batch Execution***: In continuous processing-based systems, each node in the system is continually listening to messages from other nodes and outputting new updates to its child nodes. Continuous processing has the advantage of offering the lowest possible latency when the total input rate is relatively low, because each node responds immediately to a new message. However, continuous processing systems generally have lower maximum throughput, because they incur a significant amount of overhead per-record (e.g., calling the operating system to send a packet to a downstream node). In addition, continous systems generally have a fixed topology of operators that cannot be moved at runtime without stopping the whole system, which can introduce load balancing issues. In contrast, micro-batch systems wait to accumulate small batches of input data (say, 500 ms’ worth), then process each batch in parallel using a distributed collection of tasks, similar to the execution of a batch job in Spark. Micro-batch systems can often achieve high throughput per node because they leverage the same optimizations as batch systems (e.g., vectorized processing), and do not incur any extra per-record overhead. Thus, they need fewer nodes to process the same rate of data. Micro-batch systems can also use dynamic load balancing techniques to handle changing workloads (e.g., increasing or decreasing the number of tasks). The downside, however, is a higher base latency due to waiting to accumulate a micro-batch. 

---------------------------------

- Chapter 21: Structured Streaming Basics
  - The main idea behind Structured Streaming is to treat a stream of data as a table to which data is continuously appended. The job then periodically checks for new input data, process it, updates some internal state located in a state store if needed, and updates its result. A cornerstone of the API is that you should not have to change your query’s code when doing batch or stream processing—you should have to spec‐ ify only whether to run that query in a batch or streaming fashion.
  - Internally, Structured Streaming will automatically figure out how to “incrementalize” your query, i.e., update its result efficiently whenever new data arrives, and will run it in a fault-tolerant fashion.
  - Core Concepts: 
    - Structured Streaming maintains the same concept of transformations and actions that we have seen throughout this book.
    - Structured Streaming supports several input sources for reading in a streaming fashion. As of Spark 2.2, the supported input sources are as follows: Apache Kafka 0.10, Files on a distributed file system like HDFS or S3 (Spark will continuously read new files in a directory), A socket source for testing
    - Just as sources allow you to get data into Structured Streaming, sinks specify the destination for the result set of that stream. Sinks and the execution engine are also responsible for reliably tracking the exact progress of data processing. Here are the supported output sinks as of Spark 2.2: Apache Kafka 0.10, Almost any file format, A foreach sink for running arbitary computation on the output records, A console sink for testing, A memory sink for debugging
      - Note: Defining a sink for our Structured Streaming job is only half of the story. We define an ***output mode***, similar to how we define output modes in the static Structured APIs. The supported output modes are as follows: 
        - Append (only add new records to the output sink)
        - Update (update changed records in place)
        - Complete (rewrite the full output)
      - One important detail is that certain queries, and certain sinks, only support certain output modes.
    - Output modes define how data is output, ***triggers*** define when data is output — that is, when Structured Streaming should check for new input data and update its result. By default, Structured Streaming will look for new input records as soon as it has finished processing the last group of input data, giving the lowest latency possible for new results. However, this behavior can lead to writing many small output files when the sink is a set of files. Thus, Spark also supports triggers based on processing time (only look for new data at a fixed interval). In the future, other types of triggers may also be supported.
    - Structured Streaming also has support for event-time processing (i.e., processing data based on timestamps included in the record that may arrive out of order).
      - Event-time means time fields that are embedded in your data. This means that rather than processing data according to the time it reaches your system, you process it according to the time that it was generated, even if records arrive out of order at the streaming application due to slow uploads or network delays. 
      - Expressing event-time processing is simple in Structured Streaming. Because the system views the input data as a table, the event time is just another field in that table, and your application can do grouping, aggregation, and windowing using standard SQL operators. However, under the hood, Structured Streaming can take some special actions when it knows that one of your columns is an event-time field, including optimizing query execution or determining when it is safe to forget state about a time window. Many of these actions can be controlled using watermarks. 
      - ***Watermarks are a feature of streaming systems that allow you to specify how late they expect to see data in event time***. For example, in an application that processes logs from mobile devices, one might expect logs to be up to 30 minutes late due to upload delays. Systems that support event time, including Structured Streaming, usually allow setting watermarks to limit how long they need to remember old data. Watermarks can also be used to control when to output a result for a particular event time window (e.g., waiting until the watermark for it has passed).
  - Other stuff...

---------------------------------

- Chapter 22: Event-Time and Stateful Processing
  - One of the more difficult operations in record-at-a-time systems is removing duplicates from the stream. Almost by definition, you must operate on a batch of records at a time in order to find duplicates—there’s a high coordination overhead in the processing system. Deduplication is an important tool in many applications, especially when messages might be delivered multiple times by upstream systems. 
  - A perfect example of this are Internet of Things (IoT) applications that have upstream producers generating messages in nonstable network environments, and the same message might end up being sent multiple times. Your downstream applications and aggregations should be able to assume that there is only one of each message.
  - Essentially, Structured Streaming makes it easy to take message systems that provide at-least-once semantics, and convert them into exactly-once by dropping duplicate messages as they come in, based on arbitrary keys. ***To de-duplicate data, Spark will maintain a number of user specified keys and ensure that duplicates are ignored.***
  - Just like other stateful processing applications, you need to specify a watermark to ensure that the maintained state does not grow infinitely over the course of your stream.
  - Other stuff... 

---------------------------------

- Chapter 23: Structured Streaming in Production.
  - Not much to add... 

---------------------------------

Later chapters related to ML/Data Science, skipped...

---------------------------------
---------------------------------

