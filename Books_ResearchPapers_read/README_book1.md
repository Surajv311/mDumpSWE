## Spark: The Definitive Guide: Big Data Processing Made Simple (Matei Zaharia)

#### Interesting points/notes:

- Note that in some places, I've googled/chatgpt'd few terms/reordered explanations and added here in the README for understanding. 

- Chapter 1:
  - Apache Spark is a unified computing engine and a set of libraries for parallel data processing on computer clusters.
  - For example, if you load data using a SQL query and then evaluate a machine learning model over it using Spark’s ML library, the engine can combine these steps into one scan over the data. The combination of general APIs and high-performance execution, no matter how you combine them, makes Spark a powerful platform for interactive and production applications. At the same time that Spark strives for unification, it carefully limits its scope to a computing engine. By this, we mean that Spark handles loading data from storage systems and performing computation on it, not permanent storage as the end itself. However, Spark neither stores data long term itself, nor favors one over another. The key motivation here is that most data already resides in a mix of storage systems. Data is expensive to move so Spark focuses on performing computations over the data, no matter where it resides. Spark’s focus on computation makes it different from earlier big data software platforms such as Apache Hadoop. ***Hadoop included both a storage system (the Hadoop file system, designed for low-cost storage over clusters of commodity servers) and a computing system (MapReduce), which were closely integrated together***. However, this choice makes it difficult to run one of the systems without the other. For most of their history, computers became faster every year through processor speed increases: the new processors each year could run more instructions per second than the previous year’s. As a result, applications also automatically became faster every year, without any changes needed to their code. This trend led to a large and established ecosystem of applications building up over time, most of which were designed to run only on a single processor. These applications rode the trend of improved processor speeds to scale up to larger computations and larger volumes of data over time. ***Unfortunately, this trend in hardware stopped around 2005: due to hard limits in heat dissipation, hardware developers stopped making individual processors faster, and switched toward adding more parallel CPU cores all running at the same speed***. This change meant that suddenly applications needed to be modified to add parallelism in order to run faster, which set the stage for new programming models such as Apache Spark. 
  - On top of that, the technologies for storing and collecting data did not slow down appreciably in 2005, when processor speeds did. ***The cost to store 1 TB of data continues to drop by roughly two times every 14 months***, meaning that it is very inexpensive for organizations of all sizes to store large amounts of data. Moreover, many of the technologies for collecting data (sensors, cameras, public datasets, etc.) continue to drop in cost and improve in resolution. For example, camera technology continues to improve in resolution and drop in cost per pixel every year, to the point where a 12-megapixel webcam costs only $3 to $4; this has made it inexpensive to collect a wide range of visual data, whether from people filming video or automated sensors in an industrial setting. Moreover, cameras are themselves the key sensors in other data collection devices, such as telescopes and even gene-sequencing machines, driving the cost of these technologies down as well.
  - The end result is a world in which collecting data is extremely inexpensive—many organizations today even consider it negligent not to log data of possible relevance to the business—but processing it requires large, parallel computations, often on clusters of machines. Moreover, in this new world, the software developed in the past 50 years cannot automatically scale up, and neither can the traditional programming models for data processing applications, creating the need for new programming models. It is this world that Apache Spark was built for.
  - ***Apache Spark began at UC Berkeley in 2009*** as the Spark research project, which was first published the following year in a paper entitled “Spark: Cluster Computing with Working Sets” by ***Matei Zaharia***, Mosharaf Chowdhury, Michael Franklin, Scott Shenker, and Ion Stoica of the UC Berkeley AMPlab. 

- Chapter 2:
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

- Chapter 3:
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

- Chapter 4: 
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

- Chapter 5: 
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

- Chapter 6: 
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

- Chapter 7: 
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

- Chapter 8: 
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

- Chapter 9: 
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

- Chapter 10: 
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

- Chapter 11: 
  - 





















































---------------------------------