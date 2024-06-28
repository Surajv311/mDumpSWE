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
  - Spark’s language bindings: (image below - for Python type reference, similarly other langauge types)

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
  -  






---------------------------------