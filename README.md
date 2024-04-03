# mDumpSWE

Collection of interesting articles/newsletters/blogs/videos - related to software engineering, I've surfed online and learned about. Thank you internet and chatgpt. Creating a repo for my memory dump. I've tried to add as many references from where I read the articles about, but may have missed few. 

Abbrevations in doc hyperlinked: 
- `_vl`: video reference link
- `_al`: article/page reference link

------------------------
Add these things: 

A Web Server is a server capable of receiving HTTP requests, interpreting them, processing the corresponding HTTP Responses and sending them to the appropriate clients (Web Browsers). Example: Apache Web Server. Read more about Web Servers and their working>>


https://stackoverflow.com/questions/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe?rq=1

The try block lets you test a block of code for errors.
The **except** block lets you handle the error. - Its like catch block
The else block lets you execute code when there is no error.
The finally block lets you execute code, regardless of the result of the try- and except blocks.


Of course! Let's simplify it with an analogy:
Imagine you're a chef running a restaurant kitchen. Your job is to cook meals (handle requests) for customers (web users) who come to your restaurant (website). You have two different ways of managing your kitchen:
The WSGI Kitchen (Traditional):
In the WSGI kitchen, you work on one dish (request) at a time, from start to finish, without interruption.
When a customer (web user) orders a meal (sends a request), you start preparing it immediately and don't move on to the next order until you're done with the current one.
This approach works well for most meals but can be inefficient if you have a lot of orders coming in at once, as you might spend a lot of time waiting for one order to finish before starting the next.
The ASGI Kitchen (Modern and Flexible):
In the ASGI kitchen, you have the option to work on multiple dishes (requests) simultaneously, even if they're at different stages of preparation.
When a customer orders a meal, you start preparing it but can also handle other orders at the same time. For example, you might start marinating chicken for one dish while grilling steak for another.
This approach allows you to be more efficient and handle a higher volume of orders, especially if some dishes require longer cooking times or if you have special requests like making a dessert while the main course is still cooking.
Now, let's relate this analogy back to web development:
WSGI (Traditional): This is like the traditional kitchen where you handle one request at a time. When a web user sends a request to your website, the server processes it from start to finish before moving on to the next request. Frameworks like Flask and Django work this way.
ASGI (Modern and Flexible): This is like the modern kitchen where you can handle multiple requests simultaneously, even if they're at different stages of processing. ASGI servers can handle long-lived connections, real-time updates, and high concurrency. Frameworks like FastAPI, Starlette, and Quart are designed to work with ASGI servers.
In essence, ASGI allows web servers to handle requests more efficiently, especially for real-time applications or when dealing with a large number of concurrent users.
WSGI (Web Server Gateway Interface):
WSGI is a specification for how web servers communicate with Python web applications or frameworks.
In WSGI, the web server receives an HTTP request from a client (like a web browser) and forwards it to a WSGI application.
The WSGI application is a Python callable (such as a function or object) that processes the request and returns an HTTP response.
WSGI applications typically follow a synchronous execution model, meaning they handle one request at a time and block until the request is completed.
Most traditional Python web frameworks, like Flask and Django, are built on top of WSGI.
ASGI (Asynchronous Server Gateway Interface):
ASGI is an evolution of WSGI designed to support asynchronous and real-time web applications.
ASGI provides a more flexible protocol that can handle both synchronous and asynchronous processing of HTTP requests.
In ASGI, the web server receives an HTTP request and forwards it to an ASGI application, which can be either synchronous or asynchronous.
ASGI applications can handle multiple requests concurrently and are well-suited for long-lived connections, such as WebSockets and server-sent events.
ASGI servers support asynchronous frameworks like Quart, FastAPI, and Starlette, as well as traditional synchronous frameworks with ASGI adapters.
In technical terms, WSGI and ASGI are specifications that define how Python web applications interact with web servers. WSGI follows a synchronous execution model, while ASGI supports both synchronous and asynchronous processing of HTTP requests, making it more versatile for modern web applications. ASGI enables real-time communication and better scalability, especially for applications with high concurrency or long-lived connections.
is wsgi a load balancer then?
No, WSGI is not a load balancer. WSGI (Web Server Gateway Interface) is a specification for how web servers communicate with Python web applications or frameworks. It defines the protocol for handling HTTP requests and responses between the web server and the Python application.
A load balancer, on the other hand, is a separate component of a network infrastructure that distributes incoming network traffic across multiple servers. Its purpose is to improve the performance, reliability, and scalability of web applications by evenly distributing the workload among multiple servers.
While WSGI defines how a Python web application interacts with a web server, a load balancer sits in front of multiple servers and routes incoming requests to the appropriate server based on various criteria, such as server availability, response time, or server load.
In a typical web application deployment, a load balancer would sit in front of multiple web servers running WSGI-compliant applications. The load balancer distributes incoming requests across these servers to ensure efficient utilization of resources and high availability of the application. Each web server then communicates with the Python application through the WSGI interface.

https://en.wikipedia.org/wiki/Common_Gateway_Interface
https://docs.python.org/2/howto/webservers.html
https://stackoverflow.com/questions/69641363/how-to-run-fastapi-app-on-multiple-ports


No, a virtual environment created using pip does not encapsulate the entire operating system ecosystem. Instead, it isolates Python packages and dependencies within a specific directory, allowing you to manage and install packages independently of the system-wide Python installation.

This was done because data stored in a RAM is volatile than that stored in a physical server. In contrast, Spark copies most of the data from a physical server to RAM; this is called “in-memory” operation. It reduces the time required to interact with servers and makes Spark faster than the Hadoop's MapReduce system.

spark why faster than hadoop - because ram - in memery processing 
singleton class - when is it comproised - synchronised keyword, double lock mechanism... java is 


ssl certificate

https://medium.com/@AbbasPlusPlus/docker-port-mapping-explained-c453dfb0ae39

requests library does all the tcp thing , networking thing under the hood. it has abstracted a lot of things

https://stackoverflow.com/questions/2829528/whats-the-scope-of-a-variable-initialized-in-an-if-statement


green thread vs virtual thread java

------------------------

Table of contents (rough overview): 
- [mDumpSWE](#mdumpswe)
    - [Understand\_read\_again\_summarise](#understand_read_again_summarise)
    - [Kafka](#kafka)
    - [Airflow](#airflow)
    - [Dask](#dask)
    - [Spark](#spark)
    - [Hadoop](#hadoop)
    - [Sqoop](#sqoop)
    - [Databricks](#databricks)
    - [Snowflake](#snowflake)
    - [Pinot](#pinot)
    - [MultiThreading\_Synchronous\_Asynchronous\_Programming](#multithreading_synchronous_asynchronous_programming)
    - [CPU\_Intensive\_vs\_IO\_Bound\_Processes](#cpu_intensive_vs_io_bound_processes)
    - [Concurrency\_vs\_Parallelism](#concurrency_vs_parallelism)
    - [Threads\_vs\_Process](#threads_vs_process)
    - [CPU\_Threads\_vs\_Cores](#cpu_threads_vs_cores)
    - [Generators\_Iterables\_Coroutines](#generators_iterables_coroutines)
    - [Python](#python)
      - [aiohttp library](#aiohttp-library)
      - [asyncio library](#asyncio-library)
      - [concurrent.futures.ThreadPoolExecutor library](#concurrentfuturesthreadpoolexecutor-library)
      - [Basic Data structures](#basic-data-structures)
      - [Context Managers](#context-managers)
      - [Try catch block](#try-catch-block)
      - [Python Global Interpreter Lock](#python-global-interpreter-lock)
      - [Function annotations](#function-annotations)
      - [Classmethod and Staticmethod](#classmethod-and-staticmethod)
      - [Others](#others)
    - [Java](#java)
      - [Java Int vs int](#java-int-vs-int)
      - [Java virtual threads](#java-virtual-threads)
      - [Java enum](#java-enum)
      - [JIT Compiler](#jit-compiler)
      - [Others](#others-1)
    - [AWS\_Services](#aws_services)
      - [EC2 Spot Instances](#ec2-spot-instances)
      - [Redshift](#redshift)
      - [Redshift Spectrum](#redshift-spectrum)
      - [AWS Glue Catalogue](#aws-glue-catalogue)
      - [AWS RDS and Aurora](#aws-rds-and-aurora)
      - [AWS ECS Task, Task Definition \& Service](#aws-ecs-task-task-definition--service)
      - [AWS ECR](#aws-ecr)
      - [Misc infos:](#misc-infos)
    - [Database\_internals](#database_internals)
      - [Timeseries DB](#timeseries-db)
    - [SQL Functions](#sql-functions)
    - [Linux\_internals\_and\_commands](#linux_internals_and_commands)
    - [Webhooks\_APIs\_Websockets](#webhooks_apis_websockets)
    - [HTTP Request](#http-request)
    - [HTTP\_1\_vs\_HTTP\_2](#http_1_vs_http_2)
    - [Docker](#docker)
    - [TCP vs UDP](#tcp-vs-udp)
    - [gRPC\_REST\_GraphQL](#grpc_rest_graphql)
    - [JSON vs Protobuf](#json-vs-protobuf)
    - [Git](#git)
    - [cURL](#curl)
    - [Data\_transformation\_info](#data_transformation_info)
      - [JSON explode vs JSON normalize](#json-explode-vs-json-normalize)
      - [Dataframe Index](#dataframe-index)
      - [Dataframe Reset Index](#dataframe-reset-index)
    - [SAML](#saml)
    - [Opensource\_Github\_repos\_knowledge\_extraction](#opensource_github_repos_knowledge_extraction)
      - [donnemartin/system-design-primer \_al](#donnemartinsystem-design-primer-_al)
      - [surajv311/myCS-NOTES \_al](#surajv311mycs-notes-_al)
    - [Info\_Miscellaneous](#info_miscellaneous)


--------------------------


### Understand_read_again_summarise

https://www.linkedin.com/posts/hnaser_in-the-beginning-for-the-os-to-write-to-activity-7163388923916861441-t1vw?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_the-big-win-of-using-threads-instead-of-processes-activity-7161147178546069506-yehp?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_fragmentation-is-a-very-interesting-topic-activity-7156142414989037568-6C96?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_today-i-learned-how-the-linux-option-netipv4-activity-7150555792662740992-w8fL?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_i-just-learned-that-in-addition-to-the-mapping-activity-7148454941404110848-8m4D?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_i-am-fascinated-by-gos-compiler-escape-analysis-activity-7144747978224746496-z-YZ?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_glad-mongo-fixed-this-in-62-so-prior-to-activity-7135553971066175489-nwm7?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_why-does-it-take-time-for-dns-to-resolve-activity-7134793549526528001-xjL0?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_a-connection-pool-is-always-a-good-idea-especially-activity-7134109245909725184-qaUE?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_graphql-was-invented-by-facebook-mainly-because-activity-7127490321701056513-DSxX?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_the-recent-cloudflare-api-outage-on-november-activity-7126989541537677312-upGW?utm_source=share&utm_medium=member_desktop
https://www.linkedin.com/posts/hnaser_http3-is-taking-over-the-world-but-consider-activity-7116186211039285248-Bae7?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_i-got-asked-how-vpn-works-on-x-so-here-is-activity-7110641803984322560--ONA?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_fun-networking-fact-http-related-pglocks-activity-7108275178979160064-gAVu?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_its-fascinating-to-know-how-jit-just-in-activity-7101992901496229888-_777?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_postgres-has-weak-locks-those-are-table-activity-7078250396678303744-p6WU?utm_source=share&utm_medium=member_desktop

https://www.linkedin.com/posts/hnaser_normally-when-you-write-to-disk-the-writes-activity-7067253338395852800-r2JY?utm_source=share&utm_medium=member_desktop

https://bugs.mysql.com/bug.php?id=109595

https://www.youtube.com/watch?v=lCb5BkJOOVI&list=PLQnljOFTspQU0ICDe-cL1EwXC4GDSayKY&index=43

https://medium.com/@hnasr/the-journey-of-a-request-to-the-backend-c3de704de223

https://blog.jcole.us/2014/04/16/the-basics-of-the-innodb-undo-logging-and-history-system/

https://medium.com/@hnasr/how-slow-is-select-8d4308ca1f0c

https://medium.com/@hnasr/what-happens-when-databases-crash-74540fd97ea9

https://www.linkedin.com/pulse/how-troubleshoot-long-postgres-startup-nikolay-samokhvalov/

https://keefmck.blogspot.com/2023/04/why-ssds-lie-about-flush.html?m=1

https://tontinton.com/posts/scheduling-internals/

https://stackoverflow.com/questions/1518711/how-does-free-know-how-much-to-free

https://blog.allegro.tech/2024/03/kafka-performance-analysis.html

https://www.youtube.com/watch?v=d86ws7mQYIg


--------------------------

### Kafka

Kafka is a distributed messaging system providing fast, highly scalable and redundant messaging through a pub-sub model. Apache Kafka was developed by LinkedIn but is now under the Apache foundation. It is written in Scala and Java. It is primarily used to build real-time streaming data pipelines and applications that adapt to the data streams.

The basic architecture of Kafka is organised around a few key terms: topics, producers, consumers, and brokers. 

- All Kafka messages are organised into **topics**. If you wish to send a message you send it to a specific topic and if you wish to read a message you read it from a specific topic. 
- A **consumer** pulls messages off of a Kafka topic while **producers** push messages into a Kafka topic. 
- Lastly, Kafka, as a distributed system, runs in a cluster. Each node in the cluster is called a Kafka **broker**. 
- Kafka topics are divided into a number of **partitions**. Each partition can be placed on a separate machine to allow for multiple consumers to read from a topic in parallel. 
- Each message within a partition has an identifier called its **offset**. The offset the ordering of messages as an immutable sequence. Kafdrop can be used to view the Kafka brokers/ topics/ consumers, etc. AWS has a service called MSK which can be used for Kafka service.   
- In Kafka, a **consumer group** is a group of one or more consumers that work together to consume messages from one or more partitions of a topic. When multiple consumers are part of a consumer group, Kafka automatically assigns partitions to each consumer within the group, ensuring that each partition is consumed by only one consumer at a time. This allows for horizontal scaling of consumers and high availability of data processing.
- Kafka batch size vs buffer memory: 
  - batch.size: The maximum amount of data that can be sent in a single request. If batch.size is (32*1024) that means 32 KB can be sent out in a single request.
  - buffer.memory: if Kafka Producer is not able to send messages(batches) to Kafka broker (Say broker is down). It starts accumulating the message batches in the buffer memory (default 32 MB). Once the buffer is full, It will wait for "max.block.ms" (default 60,000ms) so that buffer can be cleared out. Then it's throw exception.

[Kafka internals _al](https://engineering.cred.club/kafka-internals-47e594e3f006)

**Schema registry in Kafka**: Kafka, at its core, only transfers data in byte format. There is no data verification that’s being done at the Kafka cluster level. In fact, Kafka doesn’t even know what kind of data it is sending or receiving; whether it is a string or integer. 

Due to the decoupled nature of Kafka, producers and consumers do not communicate with each other directly, but rather information transfer happens via Kafka topic. At the same time, the consumer still needs to know the type of data the producer is sending in order to deserialize it. 

Imagine if the producer starts sending bad data to Kafka or if the data type of your data gets changed. Your downstream consumers will start breaking. We need a way to have a common data type that must be agreed upon. That’s where Schema Registry comes into the picture. 

It is an application that resides outside of your Kafka cluster and handles the distribution of schemas to the producer and consumer by storing a copy of schema in its local cache. With the schema registry in place, the producer, before sending the data to Kafka, talks to the schema registry first and checks if the schema is available. If it doesn’t find the schema then it registers and caches it in the schema registry. Once the producer gets the schema, it will serialize the data with the schema and send it to Kafka in binary format prepended with a unique schema ID. When the consumer processes this message, it will communicate with the schema registry using the schema ID it got from the producer and deserialize it using the same schema. If there is a schema mismatch, the schema registry will throw an error letting the producer know that it’s breaking the schema agreement.

[Schema registry Kafka _al](https://medium.com/slalom-technology/introduction-to-schema-registry-in-kafka-915ccf06b902)

**Kafka consumer commits**: 
  - A kafka offset is a unique identifier for each message within a kafka partition. It helps consumers keep track of their progress like how many messages each consumer has already consumed from a partition so far and where to start next from. Please note, offset is unique only within a partition, not across partitions.
  - A consumer can either chose to automatically commit offsets periodically or chose to commit it manually for special use cases. Different ways to commit: 
    - Auto commit is the simplest way to commit offsets by just setting enable.auto.commit property to true. In this case, kafka consumer client will auto commit the largest offset returned by the poll() method every 5 seconds. We can set auto.commit.interval.ms property to change this default 5 seconds interval.
      - Caution with auto commit : With auto commit enabled, kafka consumer client will always commit the last offset returned by the poll method even if they were not processed. For example, if poll returned messages with offsets 0 to 1000, and the consumer could process only up to 500 of them and crashed after auto commit interval. Next time when it resumes, it will see last commit offset as 1000, and will start from 1001. This way it ended up losing message offsets from 501 till 1000. Hence with auto commit, it is critical to make sure we process all offsets returned by the last poll method before calling it again. Sometimes auto commit could also lead to duplicate processing of messages in case consumer crashes before the next auto commit interval. Hence kafka consumer provides APIs for developers to take control in their hand when to commit offsets rather than relying on auto commit by setting enable.auto.commit to false which we will discuss next. 
    - Manual synchronous commit: One downside of this synchronous commit is that it may have an impact on the application throughput as the application gets blocked until the broker responds to the commit request. 
    - Manual asynchronous commit: With asynchronous commit API, we just send the commit request and carry on. Here the application is not blocked due to asynchronous call nature. One more way asynchronous commit differs from synchronous commit is that synchronous keep on retrying as long as there is no fatal error, while asynchronous does not retry even if it fails otherwise it could lead to duplicate processing. In case of failures, asynchronous relies on the next commit to cover for it.
      - Usually its a good programming practice to leverage both synchronous and asynchronous commits, sample code snippet below. 
    - One can also do Manual commit for specific offsets. 

[Kafka commit strategies _al](https://quarkus.io/blog/kafka-commit-strategies/), [Kafka commit types _al](https://medium.com/@rramiz.rraza/kafka-programming-different-ways-to-commit-offsets-7bcd179b225a), 
[Kafka in nutshell _al](https://sookocheff.com/post/kafka/kafka-in-a-nutshell/)

------------------------------

### Airflow
Apache Airflow is an open-source workflow management platform for data engineering pipelines. It is used for the scheduling and orchestration of data pipelines or workflows. Orchestration of data pipelines refers to the sequencing, coordination, scheduling, and managing complex data pipelines from diverse sources. Airflow installation generally consists of the following components:

- **Scheduler**: It controls and manages all the task. It’s like a master node. It will schedule next task based on how many workers are free or decide when to kill a task. Also, Schedular is a single point of failure. If the Schedular fails then the tasks wouldn’t be executed. 
- **Workers**: Execute the assigned tasks. Eg: **Celery workers**. Celery is a task management system that you can use to distribute tasks across different machines or threads. It allows you to have a task queue and can schedule and process tasks in real-time. This task queue is monitored by workers which constantly look for new work to perform. When you run a celery worker, it creates one parent process to manage the running tasks. This process handles the book keeping features like sending/receiving queue messages, registering tasks, killing hung tasks, tracking status, etc. [Celery concepts animated _vl](https://www.youtube.com/watch?v=TzVkED3y3Ig)
- **Executor**: Executor is used by Scheduler. It’s a message queuing process that is tightly bound to the Scheduler and determines the worker processes that actually execute each scheduled task.
- **Web Server**: This is a handy user interface to inspect, trigger and debug the behaviour of DAGs and tasks, it’s basically the Airflow UI.
- **DAG**: DAG or Directed Acyclic Graphs are nothing but workflows in Airflow are collections of tasks that have directional dependencies. A directory of DAG files, read by the scheduler and executor (and any workers the executor has)
- **Metastore**: This database stores information regarding the state of tasks. Database updates are performed using an abstraction layer implemented in SQLAlchemy. This abstraction layer cleanly separates the function of the remaining components of Airflow from the database. Usually MySQL or PostgreSQL are used for this.
- **Operators**: An Operator determines what will be executed when the DAG runs. They can be considered as templates or blueprints that contain the logic for a predefined task, that we can define declaratively inside an Airflow DAG. Eg:

```
BashOperator: It is used to execute a bash command.
PythonOperator: It is used to run the python callable or python function.
EmailOperator: It is used to send emails to the receiver.
MySqlOperator: It is used to run the SQL query for MySql Database.
Sensor: waits for a certain time, for a condition to be satisfied.
S3ToHiveOperator: It transfers data from Amazon S3 to Hive.
HttpOperator: It is used to trigger an HTTP endpoint, etc.  
```

- [Priority weight of tasks in Airflow DAG _al](https://stackoverflow.com/questions/55145641/can-we-set-priority-weight-per-task-in-airflow)

- [Duplicate messages Kafka consumer _al](https://stackoverflow.com/questions/29647656/effective-strategy-to-avoid-duplicate-messages-in-apache-kafka-consumer)

- Note: Kafka Streams API functions as an embeddable library, negating the necessity to construct clusters whereas **Apache Flink** operates as a data processing framework utilizing a cluster model. The two major streaming platforms are Apache Flink and Kafka. [flink vs kafka _al](https://medium.com/@BitrockIT/apache-flink-and-kafka-stream-a-comparative-analysis-f8cb5b946ec3). Kafka Stream manages windowing based on event time and processing time. Apache Flink manages flexible windowing based on event time, processing time, and ingestion time. Apache Flink is a fully-stateful framework that can store the state of the data during processing, making it ideal for applications that require complex calculations or data consistency. Kafka Streams is a partially-stateful framework and it is ideal for applications that require low latency or to process large amounts of data.

------------------------------

### Dask

Dask is a parallel and distributed computing library that scales the existing Python and PyData ecosystem. Dask scales Python code from multi-core local machines to large distributed clusters in the cloud. 

Dask consists of three main components: a **client**, a **scheduler**, and one or more **workers** (they communicate using messages): 

- As an engineer, you’ll communicate directly with the Dask Client. It sends instructions to the scheduler and collects results from the workers.
- The Scheduler is the midpoint between the workers and the client. It tracks metrics, and allows the workers to coordinate. 
- The Workers are threads, processes, or separate machines in a cluster. They execute the computations from the computation graph. Each worker contains a ThreadPool that it uses to evaluate tasks as requested by the scheduler. It stores the results of these tasks locally and serves them to other workers or clients on demand, it can also reach out to other workers to gather the necessary dependencies if needed. 

A **Dask graph** is a dictionary mapping keys to computations:
```
{'x': 1,
 'y': 2,
 'z': (add, 'x', 'y'), // Computation function
 'w': (sum, ['x', 'y', 'z']), // Some computation being performed 
 'v': [(sum, ['w', 'z']), 2]}
```
- A key is any hashable value that is not a task. 
- A task is a tuple (allowed duplicates, ordered, immutable i.e we can not make any changes in it) with a callable first element. Tasks represent atomic units of work meant to be run by a single worker. 

The size of the Dask graph depends on two things:
- The number of tasks.
- The size of each task.

```
Having either lots of smaller tasks or some overly large tasks can lead to the same outcome: the size in bytes of the serialized task graph becomes too big for the Scheduler to handle. 
```

After we create a dask graph, we use a scheduler to run it. The entry point for all schedulers is a get function. Dask currently implements a few different schedulers (Single machine & Distributed Schedular - 2 family of schedular):

```
dask.threaded.get: a scheduler backed by a **thread pool**
dask.multiprocessing.get: a scheduler backed by a **process pool**
dask.get: a synchronous scheduler, good for debugging
distributed.Client.get: a distributed scheduler for executing graphs on multiple machines. This lives in the external distributed project.
```

- In dask this function: map_partitions(func, *args[, meta, ...]) Apply Python function on each DataFrame partition.
- [Dask df best practices _al](https://docs.dask.org/en/latest/dataframe-best-practices.html), in short: Reduce and then use pandas, Use the Index, Avoid Full-Data Shuffling, Persist Intelligently, Repartition to Reduce Overhead, Joins, Use Parquet format data. 
- [Strategy to partition dask df _al](https://stackoverflow.com/questions/44657631/strategy-for-partitioning-dask-dataframes-efficiently)

------------------------------

### Spark 

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

------------------------------

### Hadoop 

Hadoop architecture comprises four key components: 

- **HDFS** (Hadoop Distributed File System for distributed storage):
The **NameNode** serves as the master in a Hadoop cluster, overseeing the **DataNodes** (slaves). Its primary role is to manage metadata, such as transaction logs tracking user activity. The NameNode instructs DataNodes on operations like creation, deletion, and replication. DataNodes, acting as slaves, are responsible for storing data in the Hadoop cluster. It’s recommended to have DataNodes with high storage capacity to accommodate a large number of file blocks. In Hadoop, data is stored in blocks, each typically set to a default size of 128 MB or 256 MB. This block size ensures efficient storage and processing of large datasets. Replication in HDFS ensures data availability and fault tolerance. By default, Hadoop sets a replication factor of 3, creating copies of each file block for backup purposes. Rack Awareness in Hadoop involves the physical grouping of nodes in the cluster. This information is used by the NameNode to select the closest DataNode, reducing network traffic and optimizing read/write operations.
- **MapReduce** (for distributed processing): MapReduce process involves a client that submits a job to the Hadoop MapReduce Manager. The job is then divided into job parts (smaller tasks) by the Hadoop MapReduce Master. Input data is processed through Map() and Reduce() functions, resulting in output data. The Map function breaks down data into key-value pairs, which are then further processed by the Reduce function. Multiple clients can continuously submit jobs for processing. The map reduce functions are idempotent, i.e: output remains constant irrespective of multiple runs. [Map Reduce function _vl](https://www.youtube.com/watch?v=cHGaQz0E7AU)
- **YARN** (Yet Another Resource Negotiator): YARN, or Yet Another Resource Negotiator, is a vital component in the Hadoop framework, overseeing resource management and job scheduling. It separates these functions, employing a global Resource Manager and ApplicationMasters for individual applications. The NodeManager monitors container resource usage, providing data for efficient allocation of CPU, memory, disk, and connectivity by the ResourceManager. Features: multi-tenancy, scalability, cluster-utilization, etc. [Hadoop architecture _al](https://www.interviewbit.com/blog/hadoop-architecture/)

------------------------------

### Sqoop

Sqoop is a tool designed for efficiently transferring bulk data between Apache Hadoop and structured datastores such as relational databases. Sqoop has two main functions: importing and exporting. Importing transfers structured data into HDFS; exporting moves this data from Hadoop to external databases in the cloud or on-premises. Importing involves Sqoop assessing the external database’s metadata before mapping it to Hadoop. Sqoop undergoes a similar process when exporting data; it parses the metadata before moving the actual data to the repository. [Sqoop basics _al](https://www.guru99.com/introduction-to-flume-and-sqoop.html)

------------------------------

### Databricks

Databricks is a unified, open analytics platform for building, deploying, sharing, and maintaining enterprise-grade data, analytics, and AI solutions at scale. The Databricks Lakehouse Platform integrates with cloud storage and security in your cloud account, and manages and deploys cloud infrastructure on your behalf.

Databricks has two different types of clusters: 
- Interactive clusters are used to analyse data with notebooks, thus give you much more visibility and control. This should be used in the development phase of a project. 
- Job clusters are used to run automated workloads using the UI or API. Jobs can be used to schedule Notebooks, they are recommended to be used in Production for most projects and that a new cluster is created for each run of each job. Cluster nodes have a single driver node and multiple worker nodes. 

The driver and worker nodes can have different instance types, but by default they are the same. A driver node runs the main function and executes various parallel operations on the worker nodes. The worker nodes read and write from and to the data sources. 

The driver node maintains state information of all notebooks attached to the cluster. The driver node also maintains the SparkContext, interprets all the commands you run from a notebook or a library on the cluster, and runs the Apache Spark master that coordinates with the Spark executors. 

A cluster consists of one driver node and zero or more worker nodes. You can pick separate cloud provider instance types for the driver and worker nodes, although by default the driver node uses the same instance type as the worker node. Different families of instance types fit different use cases, such as memory-intensive or compute-intensive workloads. Databricks worker nodes run the Spark executors and other services required for proper functioning clusters. When you distribute your workload with Spark, all the distributed processing happens on worker nodes. 

Databricks runs one executor per worker node. Therefore, the terms executor and worker are used interchangeably in the context of the Databricks architecture.

**Query Federation in Databricks**: Query federation allows Databricks to execute queries against data served by other Databricks metastores as well as many third-party database management systems (DBMS) such as PostgreSQL, mySQL, AWS Redshift and Snowflake. To query data from another system you must: Create a foreign connection., etc. Simply put, from databricks UI itself you can run queries over external/third-party db post necessary connections are set up. 

------------------------------

### Snowflake 

Snowflake is a cloud data warehouse that can store and analyze all your data records in one place. It can automatically scale up/down its compute resources to load, integrate, and analyze data. Snowflake supports both transformation during (ETL) or after loading (ELT).

Snowflake uses OLAP (Online Analytical Processing) as a foundational part of its database schema and acts as a single, governed, and immediately queryable source for your data.

- **Star vs Snowflake vs OBT Schema**:
  - In **star schema**, The fact tables and the dimension tables are contained. It's design is simple but may have high data redundancy.
  - In **snowflake schema**, The fact tables, dimension tables as well as sub dimension tables are contained. It's design is complex & has more foreign keys but less data redundancy. To simply put, Snowflake schema is a more detailed & branched out version of star schema. 
  - **One big table** is a concept in which data is stored in a single table rather than being partitioned across multiple tables. This approach can offer several advantages, including simpler data management, faster query performance, and easier scalability. [Star vs Snowflake schema _vl](https://www.youtube.com/watch?v=hQvCOBv_-LE&ab_channel=codebasics) 

------------------------------

### Pinot 
It is a column-oriented, open-source, distributed data store written in Java. Pinot is designed to execute OLAP (online analytical processing) queries with low latency.

------------------------------

### MultiThreading_Synchronous_Asynchronous_Programming

```
An analogy usually helps. You are cooking in a restaurant. An order comes in for eggs and toast.
Synchronous: you cook the eggs, then you cook the toast.
Asynchronous, single threaded: you start the eggs cooking and set a timer. You start the toast cooking, and set a timer. While they are both cooking, you clean the kitchen. When the timers go off you take the eggs off the heat and the toast out of the toaster and serve them.
Asynchronous, multithreaded: you hire two more cooks, one to cook eggs and one to cook toast. Now you have the problem of coordinating the cooks so that they do not conflict with each other in the kitchen when sharing resources. And you have to pay them.
```

When you execute something synchronously, you wait for it to finish before moving on to another task. When you execute something asynchronously, you can move on to another task before it finishes.

**Threading** is about workers; **asynchrony** is about tasks.

Asynchronous programming might be more powerful and efficient when coupled with multiple threads or processes, it can still provide advantages in certain scenarios:
- I/O-Bound Operations: In a single-threaded, multi-core environment, asynchronous programming is particularly effective for I/O-bound tasks, such as network requests, file I/O, and database queries. When one task is waiting for I/O, the CPU can switch to executing other tasks. This allows the program to use the available cores more efficiently and keep the CPU busy even when some tasks are blocked.
- Concurrency and Responsiveness: Asynchronous programming allows the application to remain responsive even when dealing with I/O-bound tasks. In a multi-core system, the event loop can manage multiple tasks concurrently, ensuring that one blocked task doesn't prevent others from making progress.
- Scalability: Even though you have a single thread, the application can scale to utilize multiple cores effectively. If you have a pool of tasks, the event loop can distribute these tasks across multiple cores, enabling better resource utilization.
- Simplified Concurrency Handling: Asynchronous programming still provides a simpler approach to managing concurrency compared to traditional multi-threading or multiprocessing. It eliminates the need to manage low-level synchronization primitives, reducing the risk of race conditions and other synchronization issues.
- Resource Utilization: Asynchronous programming can help maximize resource utilization, such as network connections and memory. While one task is waiting for I/O, other tasks can execute, making better use of available resources.

Consider below scenarios: 
- Single Thread, Single Core:
  - In this scenario, both synchronous and asynchronous code won't have significant benefits in terms of parallelism. Asynchronous code could still provide benefits in terms of responsiveness, managing I/O-bound tasks efficiently, and simplifying concurrency handling.
- Single Thread, Multiple Cores:
  - While a single thread can't fully utilize multiple cores for CPU-bound tasks due to the Global Interpreter Lock (GIL) in CPython, asynchronous code can help make better use of the CPU time by interleaving tasks during I/O operations. Asynchronous programming can still offer benefits in responsiveness, managing I/O-bound tasks, and concurrency handling.
- Multiple Threads, Multiple Cores:
  - Using multiple threads in a multi-core environment can allow you to better utilize CPU resources. Asynchronous code, combined with multiple threads, can help manage I/O-bound tasks efficiently and provide better parallelism for tasks running in different threads. However, the GIL can still limit the true parallelism for CPU-bound tasks in CPython.
- Multiple Processes, Multiple Cores:
  - Using multiple processes in a multi-core environment enables parallelism without the GIL limitations. Asynchronous code can still help manage I/O-bound tasks efficiently within each process. Additionally, asynchronous code within each process can provide responsiveness and handle concurrency more easily.

In all these above scenarios, asynchronous code can provide benefits in terms of managing I/O-bound tasks, responsiveness, and simplifying concurrency handling. However, when it comes to fully utilizing multiple cores for CPU-bound tasks, asynchronous code in combination with multiple threads or processes is more effective. [Asynchronous and synchronous execution _al](https://stackoverflow.com/questions/748175/asynchronous-vs-synchronous-execution-what-is-the-difference)

------------------------------

### CPU_Intensive_vs_IO_Bound_Processes

- **CPU-intensive tasks** involve complex calculations, mathematical operations, data processing, or simulations that consume a substantial amount of CPU time. Examples include scientific simulations, data encryption/decryption, video/audio encoding/decoding, and certain data analysis tasks. In Python, CPU-intensive tasks can be challenging to parallelize effectively due to the Global Interpreter Lock (GIL) in CPython, which can limit the concurrency of CPU-bound operations when using threads. In such cases, you might consider using multiprocessing or other techniques for parallelism.
- **Thread-Intensive (I/O-Bound)** processes are characterized by tasks that spend a significant amount of time waiting for I/O operations to complete, such as reading/writing to files, making network requests, or interacting with databases. Thread-intensive tasks are often I/O-bound, meaning that the program spends more time waiting for I/O operations than it does actively processing data. Using threads to manage I/O-bound tasks can improve concurrency and overall system responsiveness by allowing other threads to continue execution while some are waiting for I/O. Examples include web servers handling multiple client connections simultaneously, data retrieval from multiple remote sources, and GUI applications that need to remain responsive while performing background tasks. I/O-bound operations are often considered more thread-intensive due to their characteristics and the way they interact with the system resources. Reasons:
  - Blocking Nature: Many I/O operations are inherently blocking, which means they can cause a thread to wait for external resources (e.g., network data, disk I/O) to become available. During this waiting period, the thread is effectively idle, and the system may benefit from switching to another thread to perform useful work.
  - Concurrency: To achieve concurrency in I/O-bound tasks, one common approach is to use multiple threads, each handling a different I/O operation simultaneously. This allows you to overlap waiting times for I/O operations and potentially reduce the overall execution time.
  - Resource Utilization: When a thread is blocked on an I/O operation, it's not actively using the CPU core. In a multi-threaded application, other threads can be scheduled to run on the same core, making better use of available CPU resources.
  - Scalability: Threads are relatively lightweight compared to processes, making them a suitable choice for managing multiple I/O-bound tasks concurrently. A single process can have many threads, allowing for high scalability in handling I/O operations.
  - Responsiveness: In scenarios where responsiveness is crucial, such as in GUI applications or web servers, offloading I/O-bound tasks to separate threads can ensure that the main thread (responsible for user interaction) remains responsive.
  - However, it's important to note that while threads are suitable for managing I/O-bound tasks, they may not be the best choice for CPU-bound tasks due to potential Global Interpreter Lock (GIL) limitations in certain Python implementations (e.g., CPython). In such cases, you might consider using multiprocessing or other concurrency approaches.
- In summary, CPU-intensive processes focus on tasks that demand significant computational resources, while thread-intensive processes deal with tasks that involve a lot of waiting for external resources.

------------------------------

### Concurrency_vs_Parallelism
- **Concurrency** is when two or more tasks can start, run, and complete in overlapping time periods. It doesn't necessarily mean they'll ever both be running at the same instant. For example, multitasking on a single-core machine.
- **Parallelism** is when tasks literally run at the same time, e.g., on a multicore processor.
- Concurrent and parallel are effectively the same principle, both are related to tasks being executed simultaneously although we can say that parallel tasks should be truly multitasking, executed "at the same time" (multiple threads of execution executing simultaneously) whereas concurrent could mean that the tasks are sharing the execution thread while still appearing to be executing in parallel (managing multiple threads of execution).

Example: 
- Concurrency is like a person juggling balls with only 1 hand. Regardless of how it seems the person is only holding at most one ball at a time. Parallelism is when the juggler uses both hands.
- Concurrency is two lines of customers ordering from a single cashier (lines take turns ordering); Parallelism is two lines of customers ordering from two cashiers (each line gets its own cashier).

- As a note: Asynchronous methods aren't directly related to the previous two concepts, asynchrony is used to present the impression of concurrent or parallel tasking but effectively an asynchronous method call is normally used for a process that needs to do work away from the current application and we don't want to wait and block our application awaiting the response. 
  - Eg: For example, getting data from a database could take time but we don't want to block our UI waiting for the data. The async call takes a call-back reference and returns execution back to your code as soon as the request has been placed with the remote system. Your UI can continue to respond to the user while the remote system does whatever processing is required, once it returns the data to your call-back method then that method can update the UI (or handoff that update) as appropriate. From the user perspective, it appears like multitasking but it may not be.

[Concurrency & Parallellism _al](https://stackoverflow.com/questions/1050222/what-is-the-difference-between-concurrency-and-parallelism), [Concurrency, Parallellism, Asynchronous methods _al](https://stackoverflow.com/questions/4844637/what-is-the-difference-between-concurrency-parallelism-and-asynchronous-methods), [Concurrency, parallellism, threads, process, etc. _al](https://medium.com/swift-india/concurrency-parallelism-threads-processes-async-and-sync-related-39fd951bc61d)

------------------------------

### Threads_vs_Process
Process means any program is in execution. Thread means a segment of a process. The process takes more time to terminate. The thread takes less time to terminate. Process takes more time for creation. It takes less time for creation. 

Processes and threads can be considered similar, but a big difference is that a process is much larger than a thread. For that reason, it is not good to have switching between processes. There is too much information in a process that would have to be saved and reloaded each time the CPU decides to switch processes. A thread on the other hand is smaller and so it is better for switching. A process may have multiple threads that run concurrently, meaning not at the same exact time, but run together and switch between them. The context switching here is better because a thread won't have as much information to store/reload.

Another explanation: 

Firstly, a program is an executable file. 

It contains the code, or a set of processor instructions, that is stored as a file on disk. When the code in a program is loaded into memory and executed by the processor, it becomes a process. An active process also includes the  resources the program needs to run. These resources are managed  by the operating system. Some examples are processor registers, program counters, stack pointers, memory pages assigned to  the process for its heap and stack, etc. There is an important property of a process that is worth mentioning. Each process has its own memory address space. One process cannot corrupt the  memory space of another process. This means that when one process malfunctions, other processes keep running. Chrome is famous for taking advantage of this process isolation by running each tab in its own process. When one tab misbehaves due to a bug or a malicious attack, other tabs are unaffected. 

A thread is the unit of execution within a process. 

A process has at least one thread. It is called the main thread. It is not uncommon for a  process to have many threads. Each thread has its own stack. Earlier we mentioned registers, program counters,  and stack pointers as being part of a process. It is more accurate to say that those things belong to a thread. 

Threads within a process share a memory address space. It is possible to communicate between threads using that shared memory space. However, one misbehaving thread could bring down the entire process. The operating system run a thread or process on a CPU by context switching. During a context switch, one process is switched out of the CPU so another process can run. The operating system stores the  states of the current running process so the process can be restored  and resume execution at a later point. It then restores the previously saved states of a different process and resumes execution for that process. Context switching is expensive. It involves saving and loading of registers, switching out memory pages, and updating various kernel data structures. Switching execution between threads also requires context switching. 

It is generally faster to switch context  between threads than between processes. There are fewer states to track, and more importantly, since threads share the same memory address space, there is no need to switch out virtual memory pages, which is one of the most expensive operations during a context switch. 

Context switching is so costly there are other mechanisms to try to minimize it. Some examples are fibers and coroutines. These mechanisms trade complexity for even lower context-switching costs. In general, they are cooperatively scheduled, that is, they must yield control for others to run. In other words, the application itself handles task scheduling. It is the responsibility of the application to make sure a long-running task is broken up by yielding periodically. 
[Process vs Thread _al](https://stackoverflow.com/questions/200469/what-is-the-difference-between-a-process-and-a-thread), [Process vs Thread _vl](https://www.youtube.com/watch?v=4rLW7zg21gI)

------------------------------

### CPU_Threads_vs_Cores
- Core is an individual physical processing unit, while threads are virtual sequences of instructions. Think of threads as conveyor belts of products that are being sent to the worker (which is the core).
- Hardware on the CPU is a physical core & a logical core is more like code it exists, i.e threads.
- If a CPU has more threads than cores, say 4 cores, 8 threads so 2 threads per core, in such case, the core would be context switching between each thread to process the task. It cannot process both at the same time, some downtime will be there due to switching. This is also an example of what we call - concurrent execution.

[Cores vs threads _vl](https://www.youtube.com/watch?v=hwTYDQ0zZOw), [Cores, threads difference in graphic design](https://www.youtube.com/watch?v=VCUvknmi5QA)

------------------------------

### Generators_Iterables_Coroutines

- A **generator** function is a type of function that uses the **yield** keyword to create an **iterator**. It generates values lazily one at a time, allowing you to iterate over a potentially infinite sequence without storing the entire sequence in memory. Generators are memory-efficient and useful when you need to produce a stream of values on-the-fly. Generators are run with normal iteration (e.g., using for loops) and produce values one by one. 
  - **Iterable** is anything like a list or set or range or dict-view, with a built-in protocol for visiting each element inside the list/ set in a certain order. If the compiler detects the yield keyword anywhere inside a function, that function no longer returns via the return statement. Instead, it immediately returns a lazy 'pending list' 'object' called a generator. 
    - A generator is iterable. Basically, whenever the yield statement is encountered, the function pauses and saves its state, then emits "the next return value in the 'list'" according to the python iterator protocol. We lose the convenience of a container, but gain the power of a series that's computed as needed, and arbitrarily long. Yield is lazy, it puts off computation. A function with a yield in it doesn't actually execute at all when you call it. It returns an iterator object that remembers where it left off. Each time you call next() on the iterator (this happens in a for-loop) execution inches forward to the next yield. return raises StopIteration and ends the series (this is the natural end of a for-loop). Yield is versatile. Data doesn't have to be stored all together, it can be made available one at a time. It can be infinite. As an analogy, return and yield are twins. return means 'return and stop' whereas 'yield` means 'return, but continue'. [Yield in python _al](https://stackoverflow.com/questions/231767/what-does-the-yield-keyword-do-in-python). Eg:

```
def countdown(n):
    while n > 0:
        yield n
        n -= 1
for num in countdown(5):
    print(num)
```

- A **coroutine** function is an asynchronous function that uses the **async** and **await** keywords to manage asynchronous operations. Coroutines can be paused and resumed, allowing other coroutines or tasks to execute while waiting for I/O operations. Inside a coroutine, you can use the await keyword to indicate points where the coroutine can pause and allow other tasks to run. They are particularly useful for I/O-bound operations, such as network requests, where waiting for external resources can lead to inefficiencies. Coroutines are run within an event loop using asyncio and can pause and resume during execution. Eg:

```
import asyncio
async def fetch_data(url):
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            return await response.text()

async def main():
    url = "https://example.com"
    data = await fetch_data(url)
    print(data)

if __name__ == "__main__":
    asyncio.run(main())
```

In summary, yield is used in generator functions to produce a sequence of values lazily, while await is used in asynchronous coroutines to pause the execution of the coroutine while waiting for an asynchronous operation to complete. generators for lazy iteration and coroutines for efficient asynchronous programming.

------------------------------

### Python 

#### aiohttp library

aiohttp is a popular asynchronous HTTP client/server framework for Python. It allows you to make asynchronous HTTP requests and build asynchronous web applications. It is particularly useful in scenarios where you want to perform I/O-bound operations without blocking the execution of other tasks. Key features of aiohttp include:
- Asynchronous I/O: aiohttp is designed to work with Python's asyncio framework, allowing you to write asynchronous code that can efficiently handle multiple concurrent connections and I/O operations.
- Client-Side: On the client side, aiohttp provides an asynchronous HTTP client that allows you to make asynchronous HTTP requests to external APIs, websites, or other HTTP servers. This is especially useful for scenarios where you need to make multiple requests concurrently without blocking the program's execution.
- Server-Side: On the server side, aiohttp enables you to build asynchronous web applications using the aiohttp.web module. This allows you to handle incoming HTTP requests asynchronously, making it possible to handle a large number of concurrent connections efficiently.
- WebSocket Support: aiohttp also supports WebSockets, which are a communication protocol that enables two-way communication between the client and the server over a single, long-lived connection.
- Middleware and Routing: aiohttp provides features for adding middleware to the request processing pipeline and defining URL routing to handle different endpoints in your application.

Eg: In this example, the fetch_data coroutine asynchronously makes an HTTP request using aiohttp and then prints the response text. The main coroutine is run using asyncio.run() to initiate the asynchronous execution:

```
import aiohttp
import asyncio

async def fetch_data(url):
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            return await response.text()

async def main():
    url = "https://example.com"
    data = await fetch_data(url)
    print(data)
if __name__ == "__main__":
    asyncio.run(main())

```

#### asyncio library

asyncio is a Python library that provides support for asynchronous programming, allowing you to write concurrent code that can efficiently handle multiple tasks without the need for explicit threading or multiprocessing. 

It's particularly useful for I/O-bound operations, such as networking or file I/O, where waiting for external resources can create bottlenecks. At its core, asyncio is built around the concept of coroutines, which are a form of lightweight, cooperative multitasking. 

When you use asyncio to call multiple API endpoints, you can perform non-blocking I/O operations. This means that when one API call is waiting for a response, your code can continue to execute other tasks, making efficient use of the event loop. Multiple API calls can be executed concurrently within a single event loop, and you can await their results as they complete.
asyncio is well-suited for I/O-bound operations, such as network requests and file I/O.

Few terms: 
- event loop (responsible for managing the execution of coroutines, scheduling tasks, and handling events)
- tasks (objects that represent the execution of a coroutine within the event loop. You can create tasks to run coroutines concurrently, and the event loop will manage their execution and Tasks can be created explicitly using asyncio.create_task())
- await keyword
- callbacks & futures (asyncio also provides a way to work with callbacks using Future - it represents a potential result of a coroutine, and you can attach callbacks to it that will be executed when the result is available)
- I/O operations (when a coroutine encounters an I/O operation like reading from a socket, it can await that operation without blocking the event loop, making the most efficient use of resources)
- Concurrency (managing many tasks efficiently) not parallelism (simultaneously executing tasks on multiple cores).

Example: In below code; Tasks 1 and 2 initiate API requests and await the responses concurrently. While Tasks 1 and 2 are waiting for their respective API responses, Task 3 starts its local processing. Once Tasks 1 and 2 receive their API responses, they continue and print the data. Task 3 completes its local processing after a 2-second delay. This demonstrates how different tasks can execute concurrently, and the event loop switches between them, making efficient use of time.

```
async def fetch_data(url, task_name):
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            data = await response.text()
            print(f"{task_name} fetched data from {url}: {data}")

async def process_local_data(task_name):
    # Simulate some local processing or computation
    await asyncio.sleep(2)
    print(f"{task_name} completed local processing")

async def main():
    urls = [
        ("https://jsonplaceholder.typicode.com/posts/1", "Task 1"),
        ("https://jsonplaceholder.typicode.com/posts/2", "Task 2")
    ]
    # Create tasks for fetching data
    data_fetch_tasks = [fetch_data(url, task_name) for url, task_name in urls]
    # Create a task for local processing
    local_processing_task = process_local_data("Task 3")
    # Run all tasks concurrently
    await asyncio.gather(local_processing_task, *data_fetch_tasks)

if __name__ == "__main__":
    asyncio.run(main())
```

[asyncio history _vl](https://www.youtube.com/playlist?list=PLhNSoGM2ik6SIkVGXWBwerucXjgP1rHmB), 
[asyncio gather _al](https://www.educative.io/answers/what-is-asynciogather), 
[asyncio python _al](https://superfastpython.com/python-asyncio/)

#### concurrent.futures.ThreadPoolExecutor library

ThreadPoolExecutor is part of the concurrent.futures module and provides a way to run functions concurrently using threads.
When you use ThreadPoolExecutor, you create a pool of worker threads, and each task you submit is executed in a separate thread. This allows you to parallelize CPU-bound tasks.

Unlike asyncio, ThreadPoolExecutor does not inherently provide non-blocking I/O. When you make API calls using ThreadPoolExecutor, each call blocks the calling thread until it receives a response. This may lead to less efficient CPU usage in I/O-bound scenarios. ThreadPoolExecutor is well-suited for CPU-bound operations where you want to parallelize tasks that do not involve waiting for external resources.

In summary, asyncio is designed for asynchronous programming and excels at I/O-bound operations with non-blocking behavior, while ThreadPoolExecutor is more suitable for CPU-bound tasks where parallelism is needed but not necessarily non-blocking behavior. The choice between them depends on your specific use case and whether you need true asynchronous behavior or parallelism.

Example: In below code; fetch_data and process_local_data are functions that fetch data from URLs and perform local processing, respectively. In the main function, we create a list of URLs with their associated task names. We create a ThreadPoolExecutor with a maximum of 2 worker threads. We submit tasks to the executor using executor.submit(). We wait for all tasks to complete using future.result(). This code achieves concurrency using threads, where Tasks 1 and 2 fetch data concurrently, and Task 3 performs local processing. The ThreadPoolExecutor manages the thread pool for us.

```
def fetch_data(url, task_name):
    response = requests.get(url)
    data = response.text
    print(f"{task_name} fetched data from {url}: {data}")

def process_local_data(task_name):
    # Simulate some local processing or computation
    import time
    time.sleep(2)
    print(f"{task_name} completed local processing")

def main():
    urls = [
        ("https://jsonplaceholder.typicode.com/posts/1", "Task 1"),
        ("https://jsonplaceholder.typicode.com/posts/2", "Task 2")
    ]
    # Create a ThreadPoolExecutor with 2 threads
    with ThreadPoolExecutor(max_workers=2) as executor:
        # Submit tasks for fetching data
        data_fetch_tasks = [executor.submit(fetch_data, url, task_name) for url, task_name in urls]
        # Submit the local processing task
        local_processing_task = executor.submit(process_local_data, "Task 3")
        # Wait for all tasks to complete
        for future in data_fetch_tasks + [local_processing_task]:
            future.result()

if __name__ == "__main__":
    main()
```

Note: You can combine asyncio with ThreadPoolExecutor to achieve asynchronous programming with multi-threading for certain use cases. This can be particularly useful when you have both I/O-bound and CPU-bound tasks that need to run concurrently.

Example: 

```
async def io_bound_task():
    # Perform I/O-bound task (e.g., make HTTP requests)
    await asyncio.sleep(1)
    print("I/O-bound task completed")

def cpu_bound_task():
    # Perform CPU-bound task (e.g., heavy computation)
    import time
    time.sleep(1)
    print("CPU-bound task completed")

async def main():
    # Create a ThreadPoolExecutor with 2 threads
    with ThreadPoolExecutor(max_workers=2) as executor:
        # Submit CPU-bound tasks to the ThreadPoolExecutor
        cpu_tasks = [executor.submit(cpu_bound_task) for _ in range(2)]
        # Await asyncio tasks for I/O-bound operations
        await asyncio.gather(io_bound_task(), io_bound_task())

if __name__ == "__main__":
    asyncio.run(main())
```

#### Basic Data structures

- List [], Tuple (), Set {}, Dictionary {“”:””,“”:_,..}
- The list allows duplicate elements. Tuple allows duplicate elements. The Set will not allow duplicate elements. The dictionary doesn’t allow duplicate keys.

```
Example: [1, 2, 3, 4, 5]
Example: (1, 2, 3, 4, 5)
Example: {1, 2, 3, 4, 5}
Example: {1: “a”, 2: “b”, 3: “c”, 4: “d”, 5: “e”}
```

  - A list is mutable i.e we can make any changes in the list. And ordered. 
  - A tuple is immutable i.e we can not make any changes in the tuple. And ordered. 
  - A set is mutable i.e we can make any changes in the set, but elements are not duplicated. And unordered. 
  - A dictionary is mutable, but Keys are not duplicated. And ordered (Python 3.7x) 

#### Context Managers 

In any programming language, the usage of resources like file operations or database connections is very common. But these resources are limited in supply. Therefore, the main problem lies in making sure to release these resources after usage. If they are not released then it will lead to resource leakage and may cause the system to either slow down or crash. It would be very helpful if users have a mechanism for the automatic setup and teardown of resources. In Python, it can be achieved by the usage of context managers which facilitate the proper handling of resources. Managing resources properly is often a tricky problem. It requires both a setup phase and a teardown phase. The latter phase requires you to perform some cleanup actions, such as closing a file, releasing a lock, or closing a network connection. If you forget to perform these cleanup actions, then your application keeps the resource alive. This might compromise valuable system resources, such as memory and network bandwidth.

A context manager is an object that supports the context management protocol, which means it defines methods __enter__() and __exit__(). When you use a context manager with the with statement, it automatically calls __enter__() before entering the block and __exit__() after exiting the block. This allows you to perform setup and cleanup actions in a convenient and reliable way. The contextlib module provides utilities for working with context managers. The contextlib.contextmanager decorator allows you to define a generator function that serves as a context manager. This decorator simplifies the creation of context managers by handling the __enter__() and __exit__() methods for you. In summary, the with statement is used to invoke the context manager's __enter__() and __exit__() methods, while contextlib provides utilities, such as the contextmanager decorator, to create context managers more easily.

```
In this case: 
file = open("hello.txt", "w")
file.write("Hello, World!")
file.close()
```

This implementation doesn’t guarantee the file will be closed if an exception occurs during the .write() call. In this case, the code will never call .close(), and therefore your program might leak a file descriptor. In Python, you can use two general approaches to deal with resource management. You can wrap your code in: try … finally construct

The Python 'with' construct creates a runtime context that allows you to run a group of statements under the control of a context manager. It is the primary method used to call a context manager. Eg: with SomeContextManager as context_variable:`. 

A with statement does not create a scope (like if, for and while do not create a scope either). As a result, Python will analyze the code and see that you made an assignment in the with statement, and thus that will make the variable local (to the real scope). A with statement is only used for context management purposes. It forces (by syntax) that the context you open in the with is closed at the end of the indentation.

[Scope of with statement _al](https://stackoverflow.com/questions/45100271/scope-of-variable-within-with-statement?rq=1)
[Context manager python _al](https://realpython.com/python-with-statement/)
[enter exit functions _al](https://stackoverflow.com/questions/1984325/explaining-pythons-enter-and-exit ), 
[context manager python _al](https://www.pythonmorsels.com/what-is-a-context-manager/),
[python with statement _al](https://stackoverflow.com/questions/3012488/what-is-the-python-with-statement-designed-for)

#### Try catch block 
- Try: This block will test the excepted error to occur 
- Except:  Here you can handle the error 
- Else: If there is no exception then this block will be executed 
- Finally: Finally block always gets executed either exception is generated or not

#### Python Global Interpreter Lock

The GIL, is a mutex (or a lock) that allows only one thread to hold the control of the Python interpreter. 

As a note: Before the interpreter takes over, Python performs three other steps: lexing, parsing, and compiling. Together, these steps transform the source code from lines of text into byte code containing instructions that the interpreter can understand. The interpreter's job is to take these code objects and follow the instructions. [How python interpretor works _al](https://stackoverflow.com/questions/70514761/how-does-python-interpreter-actually-interpret-a-program)

This means that only one thread can be in a state of execution at any point in time. The impact of the GIL isn’t visible to developers who execute single-threaded programs, but it can be a performance bottleneck in CPU-bound and multi-threaded code.

Problem which GIL solved: Python uses **reference counting** for memory management. It means that objects created in Python have a reference count variable that keeps track of the number of references that point to the object. When this count reaches zero, the memory occupied by the object is released. The problem was that this reference count variable needed protection from race conditions where two threads increase or decrease its value simultaneously. If this happens, it can cause either leaked memory that is never released or, even worse, incorrectly release the memory while a reference to that object still exists. This can cause crashes or other “weird” bugs in your Python programs. This reference count variable can be kept safe by adding locks to all data structures that are shared across threads so that they are not modified inconsistently. But adding a lock to each object or groups of objects means multiple locks will exist which can cause another problem—Deadlocks (deadlocks can only happen if there is more than one lock). Another side effect would be decreased performance caused by the repeated acquisition and release of locks. The GIL is a single lock on the interpreter itself which adds a rule that execution of any Python bytecode requires acquiring the interpreter lock. This prevents deadlocks (as there is only one lock) and doesn’t introduce much performance overhead. But it effectively makes any CPU-bound Python program single-threaded. The GIL, although used by interpreters for other languages like Ruby, is not the only solution to this problem. Some languages avoid the requirement of a GIL for thread-safe memory management by using approaches other than reference counting, such as garbage collection. On the other hand, this means that those languages often have to compensate for the loss of single threaded performance benefits of a GIL by adding other performance boosting features like JIT compilers.

Reason why GIL chosen: A lot of extensions were being written for the existing C libraries whose features were needed in Python. To prevent inconsistent changes, these C extensions required a thread-safe memory management which the GIL provided. The GIL is simple to implement and was easily added to Python. It provides a performance increase to single-threaded programs as only one lock needs to be managed. C libraries that were not thread-safe became easier to integrate. And these C extensions became one of the reasons why Python was readily adopted by different communities. As you can see, the GIL was a pragmatic solution to a difficult problem that the CPython developers faced early on in Python’s life.

Impact on multi thread python programs: When you look at a typical Python program—or any computer program for that matter—there’s a difference between those that are CPU-bound in their performance and those that are I/O-bound. CPU-bound programs are those that are pushing the CPU to its limit. This includes programs that do mathematical computations like matrix multiplications, searching, image processing, etc. I/O-bound programs are the ones that spend time waiting for Input/Output which can come from a user, file, database, network, etc. I/O-bound programs sometimes have to wait for a significant amount of time till they get what they need from the source due to the fact that the source may need to do its own processing before the input/output is ready, for example, a user thinking about what to enter into an input prompt or a database query running in its own process. Hence whether you run a program leveraging single thread or multi-thread, the runtime would be same. 

Why GIL not removed yet: The developers of Python receive a lot of complaints regarding this but a language as popular as Python cannot bring a change as significant as the removal of GIL without causing backward incompatibility issues. Removing the GIL would have made Python 3 slower in comparison to Python 2 in single-threaded performance and you can imagine what that would have resulted in. You can’t argue with the single-threaded performance benefits of the GIL. So the result is that Python 3 still has the GIL. But Python 3 did bring a major improvement to the existing GIL— We discussed the impact of GIL on “only CPU-bound” and “only I/O-bound” multi-threaded programs but what about the programs where some threads are I/O-bound and some are CPU-bound? In such programs, Python’s GIL was known to starve the I/O-bound threads by not giving them a chance to acquire the GIL from CPU-bound threads. This was because of a mechanism built into Python that forced threads to release the GIL after a fixed interval of continuous use and if nobody else acquired the GIL, the same thread could continue its use. The problem in this mechanism was that most of the time the CPU-bound thread would reacquire the GIL itself before other threads could acquire it. This was researched by David Beazley. This problem was fixed in Python 3.2 in 2009 by Antoine Pitrou who added a mechanism of looking at the number of GIL acquisition requests by other threads that got dropped and not allowing the current thread to reacquire GIL before other threads got a chance to run. 

How to deal: The most popular way is to use a multi-processing approach where you use multiple processes instead of threads. Each Python process gets its own Python interpreter and memory space so the GIL won’t be a problem. Python has a multiprocessing module which lets us create processes easily. [Python GIL _al](https://realpython.com/python-gil/)

Hence in short, 
- Pros: The GIL ensures thread safety in CPython by allowing only one running thread at a time to execute Python bytecode (thereby, no deadlock, race conditions, etc.)
- Cons: High intense CPU task threads are impacted as GIL allows only for single thread execution at any point of time. 
Multiple threads within a ThreadPool are subject to the global interpreter lock (GIL), whereas multiple child processes in the Pool are not subject to the GIL.

The GIL only affects threads within a single process. The multiprocessing module is in fact an alternative to threading that lets Python programs use multiple cores. [Python GIL _vl](https://www.youtube.com/watch?v=XVcRQ6T9RHo), [Does Py need GIL _vl](https://www.youtube.com/watch?v=EYgDP8cYlLo&ab_channel=CodePersist)

#### Function annotations

Python is a dynamically typed language instead of a statically typed language. This means that instead of defining data types beforehand, they are determined at runtime based on the values variables contain. Annotations are merely added as information for the one reading the code. Python does not inherently implement checks on annotations. Eg: 

```
def addition(num1: int, num2: float) -> float:
    return num1 + num2

def testing():
    a: int = 78
    b: float = 34.5
    addition(a, b)

if __name__ == "__main__":
    testing()
```

[Annotations _al](https://www.educative.io/answers/how-annotations-are-used-in-python)

#### Classmethod and Staticmethod 

- In Python, classmethod and staticmethod are two types of methods that can be defined inside a class. They both have special behaviors and use cases compared to regular instance methods.
- @classmethod: A class method is a method that is bound to the class itself rather than to any specific instance of the class. It takes the class (cls) as its first parameter instead of the instance (self). You denote a class method using the @classmethod decorator. The primary use case for class methods is to define methods that operate on the class itself, rather than on instances of the class. These methods can be used as alternative constructors or to access or modify class-level attributes. Example:

```
class MyClass:
    class_attr = 0

    @classmethod
    def class_method(cls):
        return cls.class_attr

# Calling class method
print(MyClass.class_method())  # Output: 0
```

- @staticmethod: A static method is a method that doesn't depend on the instance or the class. It behaves like a regular function but belongs to the class's namespace. It does not take either the instance (self) or the class (cls) as its first parameter. You denote a static method using the @staticmethod decorator. Static methods are typically used when a method does not need to access or modify any instance or class attributes. They are often used for utility functions that logically belong to the class but do not require access to any instance or class variables. Example:

```
class MyClass:
    @staticmethod
    def static_method(x, y):
        return x + y

# Calling static method
print(MyClass.static_method(3, 4))  # Output: 7
```

- In summary: Use @classmethod when you want a method to operate on the class itself and have access to class-level attributes.
Use @staticmethod when you want a method that does not depend on instance or class state and behaves like a regular function but belongs to the class's namespace.

#### Others 

- Use Pytest to test Python unit tests code: https://docs.pytest.org/en/7.1.x/how-to/usage.html
- What does __name__ == "__main__" do?: It allows you to execute code when the file runs as a script. In other words, remember in C++ code we had main() function, when we ran the file, the default function used to execute. Similar analogy. [init main info _al](https://stackoverflow.com/questions/419163/what-does-if-name-main-do)
- [Python logging causing latencies? _al](https://stackoverflow.com/questions/24791395/python-logging-causing-latencies)
- Inner functions: A function which is defined inside another function is known as inner function or nested function. Nested functions are able to access variables of the enclosing scope. Inner functions are used so that they can be protected from everything happening outside the function. [Inner functions _al](https://www.geeksforgeeks.org/python-inner-functions/)
- init function, self object, constructor: Self represents the instance of the class. By using the **self**  we can access the attributes and methods of the class in Python. **Constructors** are used to initializing the object’s state. The task of constructors is to initialize(assign values) to the data members of the class when an object of the class is created. The Default **__init__** Constructor used in Python. [Python init tutorial _vl](https://www.youtube.com/watch?v=WIP3-woodlU&ab_channel=Telusko)

```
class mynumber:
  def __init__(self, value):
    self.value = value
  def print_value(self):
    print(self.value)
    obj1 = mynumber(17)
    obj1.print_value()
```

- `getattr() function`: The getattr() function is used to access the attribute value of an object and also gives an option of executing the default value in case of unavailability of the key. [getattr in py _al](https://www.geeksforgeeks.org/python-getattr-method/)
- `isinstance() function`: The isinstance() function returns True if the specified object is of the specified type, otherwise False. If the type parameter is a tuple, this function will return True if the object is one of the types in the tuple. Eg: isinstance(object, type)
- `*args` and `**kwargs` are special keyword which allows function to take variable length argument. 
  - `*args` passes variable number of non-keyworded arguments and on which operation of the tuple can be performed.

```
def adder(*num):
    sum = 0
    for n in num:
        sum = sum + n
    print("Sum:",sum)

adder(3,5)
adder(4,5,6,7)
adder(1,2,3,5,6)
```

  - `**kwargs` passes variable number of keyword arguments dictionary to function on which operation of a dictionary can be performed.

```
def intro(**data):
    print("\nData type of argument:",type(data))
    for key, value in data.items():
        print("{} is {}".format(key,value))

intro(Firstname="Sita", Lastname="Sharma", Age=22, Phone=1234567890)
intro(Firstname="John", Lastname="Wood", Email="johnwood@nomail.com", Country="Wakanda", Age=25, Phone=9876543210)
```

- StringIO Module in Python is an in-memory file-like object. This object can be used as input or output to the most function that would expect a standard file object. Eg: 

```
from io import StringIO  

string ='Hello and welcome to GeeksForGeeks.'
 
# Using the StringIO method to set as file object.
file = StringIO(string) 
 
# Retrieve the entire content of the file.
print(file.getvalue())
```

[stringio python _al](https://www.geeksforgeeks.org/stringio-module-in-python/)

- Positional arguments and keyword arguments to functions python: 

```
rectangle_area(1, 2) # positional arguments
rectangle_area(width=2, height=1) # keyword arguments
```

- Single quotes vs double quotes in Python - There is no difference. 
- [Integer cache maintained by Python interpretor _al](https://stackoverflow.com/questions/15171695/whats-with-the-integer-cache-maintained-by-the-interpreter)

```
Consider running in python shell: 

>>> a = 1
>>> b = 1
>>> a is b
True
>>> a = 257
>>> b = 257
>>> a is b
False

But if it is run in a py file (or joined with semi-colons), the result is different:
>>> a = 257; b = 257; a is b
True

Why so?
Python caches integers in the range [-5, 256], so integers in that range are usually but not always identical. What you see for 257 is the Python compiler optimizing identical literals when compiled in the same code object. When typing in the Python shell each line is a completely different statement, parsed and compiled separately, but if its in a file - the behaviour is different. 
```

- `'wb'` in Python code: The wb indicates that the file is opened for writing in binary mode. When writing in binary mode, Python makes no changes to data as it is written to the file. In text mode (when the b is excluded as in just w or when you specify text mode with wt), however, Python will encode the text based on the default text encoding. Additionally, Python will convert line endings (\n) to whatever the platform-specific line ending is, which would corrupt a binary file like an exe or png file. Text mode should therefore be used when writing text files (whether using plain text or a text-based format like CSV), while binary mode must be used when writing non-text files like images. [wb in python _al](https://stackoverflow.com/questions/2665866/what-does-wb-mean-in-this-code-using-python)

------------------------------

### Java 

#### Java Int vs int 
- The key difference between the Java int and Integer types is that an int simply represents a whole number, while an Integer has additional properties and methods. 
- The Integer class is an Object while an int is a primitive type. The Integer class allows conversion to float, double, long and short, while the int doesn’t.
- The Integer is compared with .equals while the int uses two equal signs, == .

[Java Int vs int _al](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/int-vs-Integer-java-difference-comparison-primitive-object-types)

#### [Java virtual threads](https://medium.com/@RamLakshmanan/java-virtual-threads-easy-introduction-44d96b8270f8)
Java virtual threads is a new feature introduced in JDK 19. It has potential to improve an applications availability, throughput and code quality on top of reducing memory consumption.
Let’s walkthrough a typical lifecycle of a thread:

1. Thread is created in a thread pool
2. Thread waits in the pool for a new request to come
3. Once the new request comes, the thread picks up the request and it makes a backend Database call to service this request.
4. Thread waits for response from the backend Database
5. Once response comes back from the Database, the thread processes it, and sends back the response to customer
6. Thread is returned back to the thread pool

Step #2 to #6 will repeat until the application is shutdown. If you notice, the thread is actually doing real work only in step #3 and #5. In all other steps(i.e., step #1, step #2, step #4, step #6), it is basically waiting(or doing nothing). In most applications, a significant number of threads predominantly waits during most of its lifetime.

In the previous release of JVM(Java Virtual Machine), there was only one type of thread. It’s called as ‘classic’ or ‘platform’ thread. Whenever a platform thread is created, an operating system thread is allocated to it. Only when the platform thread exits(i.e., dies) the JVM, this operating system thread is free to do other tasks. Until then, it cannot do any other tasks. Basically, there is a 1:1 mapping between a platform thread and an operating system thread.

According to this architecture, OS thread will be unnecessarily locked down in step #1, step #2, step #4, step #6 of the thread’s life cycle, even though it’s not doing anything during these steps. Since OS threads are precious and finite resources, it’s time is extensively wasted in this platform threads architecture.

In order to efficiently use underlying operating system threads, virtual threads have been introduced in JDK 19. In this new architecture, a virtual thread will be assigned to a platform thread (aka carrier thread) only when it executes real work. As per the above-described thread’s life cycle, only during step #3 and step #5 virtual thread will be assigned to the platform thread(which in turn uses OS thread) for execution. In all other steps, virtual thread will be residing as objects in the Java heap memory region just like any of your application objects. Thus, they are lightweight and more efficient.

#### Java enum

The Enum in Java is a data type which contains a fixed set of constants. Eg: 

```
class EnumExample1{  
//defining the enum inside the class  
public enum Season { WINTER, SPRING, SUMMER, FALL }  
//main method  
public static void main(String[] args) {  
//traversing the enum  
for (Season s : Season.values())  
System.out.println(s);  
}}  
```

#### JIT Compiler 
Bytecode is one of the most important features of java that aids in cross-platform execution. The way of converting bytecode to native machine language for execution has a huge impact on its speed of it. 

These bytecodes have to be interpreted or compiled to proper machine instructions depending on the instruction set architecture. Moreover, these can be directly executed if the instruction architecture is bytecode based. Interpreting the bytecode affects the speed of execution. 

In order to improve performance, JIT compilers interact with the Java Virtual Machine (JVM) at run time and compile suitable bytecode sequences into native machine code. While using a JIT compiler, the hardware is able to execute the native code, as compared to having the JVM interpret the same sequence of bytecode repeatedly and incurring overhead for the translation process. This subsequently leads to performance gains in the execution speed, unless the compiled methods are executed less frequently. 

The JIT compiler is able to perform certain simple optimizations while compiling a series of bytecode to native machine language. Some of these optimizations performed by JIT compilers are data analysis, reduction of memory accesses by register allocation, translation from stack operations to register operations, elimination of common sub-expressions, etc. 

The greater the degree of optimization done, the more time a JIT compiler spends in the execution stage. Therefore it cannot afford to do all the optimizations that a static compiler is capable of, because of the extra overhead added to the execution time and moreover its view of the program is also restricted.

#### Others

- Jackson Object Mapper method can be used to serialize any Java value as a byte array.
- The Java Persistence API (JPA) is used to persist data between Java object and relational database. 
- Object Relational Mapping (ORM) is a functionality which is used to develop and maintain a relationship between an object and relational database by mapping an object state to database column. It is capable to handle various database operations easily such as inserting, updating, deleting etc.
- Garbage Collection is process of reclaiming the runtime unused memory automatically. Java garbage collection is an automatic process.

------------------------------

### AWS_Services

#### EC2 Spot Instances

A Spot Instance is an instance that uses spare EC2 capacity that is available for less than the On-Demand price. Because Spot Instances enable you to request unused EC2 instances at steep discounts, you can lower your Amazon EC2 costs significantly. The hourly price for a Spot Instance is called a Spot price. The Spot price of each instance type in each Availability Zone is set by Amazon EC2, and is adjusted gradually based on the long-term supply of and demand for Spot Instances. Your Spot Instance runs whenever capacity is available. [Spot instances _al](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-spot-instances.html)

#### Redshift

Redshift is a clustered data warehouse and each cluster can house multiple databases. As expected, each database contains multiple objects like tables, views, stored procedures, etc. It is logical to expect that the data tables are stored across multiple nodes.

A node is a compute unit with dedicated CPUs, memory and disk. Redshift has two types of nodes: **Leader** and **Compute**. The Leader node manages data distribution and query execution across Compute nodes. Data is stored on Compute nodes only. 
Slice is logical partition for disk storage. Each node has multiple slices which allow parallel access and processing across slices on each node. The number of slices per node depends on the node instance types. [Redshift architecture _al](https://towardsdatascience.com/amazon-redshift-architecture-b674513eb996)

In Redshift, Vacuum is a resource-intensive operation. Re-sorts rows and reclaims space in either a specified table or all tables in the current database. Users can access tables while they are being vacuumed. You can perform queries and write operations while a table is being vacuumed, but when data manipulation language (DML) commands and a vacuum run concurrently, both might take longer. If you run UPDATE and DELETE statements during a vacuum, system performance might be reduced. VACUUM DELETE temporarily blocks update and delete operations. [Redshift Vacuum performance _al](https://repost.aws/knowledge-center/redshift-vacuum-performance). 

According to Redshift Documentation, You can only add one column in each ALTER TABLE statement. Only way to add multiple columns is executing multiple ALTER TABLE statements.

In Redshift, max limit to a varchar/jsonvarchar datatype is 65535 bytes. In PostgreSQL, where we have this data type called **Text** which can store unlimited char values. 

Note that, 
- **'Tag'** is a reserved word in Redshift, if you like to use reserved words as column names or aliases you need to use delimited identifiers (double quotes). Hence to create column in a table with name tag, instead of using this: alter table schema.tablename add column tag varchar(100), you have to use this: alter table schema.tablename add column "tag" varchar(100)
- A table's **distkey** is the column on which it's distributed to each node. Rows with the same value in this column are guaranteed to be on the same node. 
- A table's **sortkey** is the column by which it's sorted within each node.

#### Redshift Spectrum 

Using Amazon Redshift Spectrum, you can efficiently query and retrieve structured and semistructured data from files in Amazon S3 without having to load the data into Amazon Redshift tables. Redshift Spectrum queries employ massive parallelism to run very fast against large datasets. Much of the processing occurs in the Redshift Spectrum layer, and most of the data remains in Amazon S3. Multiple clusters can concurrently query the same dataset in Amazon S3 without the need to make copies of the data for each cluster.

Redshift Spectrum resides on dedicated Amazon Redshift servers that are independent of your cluster. Based on the demands of your queries, Redshift Spectrum can potentially use thousands of instances to take advantage of massively parallel processing. 
You create Redshift Spectrum tables by defining the structure for your files and registering them as tables in an external data catalog. The external data catalog can be AWS Glue, the data catalog that comes with Amazon Athena, or your own Apache Hive metastore. You can create and manage external tables either from Amazon Redshift using data definition language (DDL) commands or using any other tool that connects to the external data catalog. Changes to the external data catalog are immediately available to any of your Amazon Redshift clusters.

Spectrum (Redshift) tables access data from S3 and uses almost infinite resources to read data. Cost of querying depends on size of data being read. Hence they are costly. 

#### AWS Glue Catalogue

It is a centralized metadata repository for all your data assets across various data sources. It provides a unified interface to store and query information about data formats, schemas, and sources. An AWS Glue crawler automatically discovers and extracts metadata from a data store, and then it updates the AWS Glue Data Catalog accordingly.

#### AWS RDS and Aurora

- Amazon Aurora (Aurora) is a fully managed relational database engine that's compatible with MySQL and PostgreSQL. 
- Amazon Relational Database Service (Amazon RDS) is a web service that makes it easier to set up, operate, and scale a relational database in the AWS Cloud [Amazon RDS Docs _al](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html). 

While RDS provides good performance for most workloads, Aurora generally offers better performance due to its architecture optimizations. But not always true. [Amazon RDS Aurora vs RDS MySQL vs MySQL on EC2 _al](https://stackoverflow.com/questions/46401830/amazon-rds-aurora-vs-rds-mysql-vs-mysql-on-ec2), [Optimize write performance for AWS Aurora instance _al](https://stackoverflow.com/questions/46383763/optimize-write-performance-for-aws-aurora-instance/46384196). 

If you have secondary indexes and have high write traffic, Aurora is not suitable. Though it may change in future. AWS RDS is the managed database solution which provides support for multiple database options Amazon Aurora, PostgreSQL, MySQL, MariaDB, Oracle, and Microsoft SQL Server. When you consider Amazon Aurora in RDS, it differs from the rest of the engines because, its new and fully implemented by Amazon from ground up. 

You choose Aurora MySQL or Aurora PostgreSQL as the DB engine option when setting up new database servers through Amazon RDS. Aurora takes advantage of the familiar Amazon Relational Database Service (Amazon RDS) features for management and administration. [PostgreSQL vs. Aurora PostgreSQL _al](https://www.linkedin.com/pulse/postgresql-vs-aurora-choosing-right-database-your-aws-barry-o-connell-mgare/) 

- ExportTaskAlreadyExistsFault error comes in RDS when you trigger export of snapshot data of an RDS instance (having db's, tables) multiple times. 

#### AWS ECS Task, Task Definition & Service

- ECS task definition is: The task definition is a text file, in JSON format, that describes one or more containers, that form your application. It can be thought of as a blueprint for your application. The Task definition allows you to specify which Docker image to use, which ports to expose, how much CPU and memory to allot, how to collect logs, and define environment variables. 
- A Task is created when you run a Task directly, which launches container(s) (defined in the task definition) until they are stopped or exit on their own, at which point they are not replaced automatically. Running Tasks directly is ideal for short-running jobs, perhaps as an example of things that were accomplished via CRON.
- A Service is used to guarantee that you always have some number of Tasks running at all times. If a Task's container exits due to an error, or the underlying EC2 instance fails and is replaced, the ECS Service will replace the failed Task. This is why we create clusters so that the service has plenty of resources in terms of CPU, memory and network ports to use. To us it doesn't really matter which instance Tasks run on so long as they run. A Service configuration references a Task definition. A Service is responsible for creating Tasks.
- [Memory reservations, soft & hard limit in ECS _al](https://aws.amazon.com/blogs/containers/how-amazon-ecs-manages-cpu-and-memory-resources/)

[ECS task and task definition _al](https://stackoverflow.com/questions/42960678/what-is-the-difference-between-a-task-and-a-service-in-aws-ecs)
[ECS task and task definition _vl](https://www.youtube.com/watch?v=5uJUmGWjRZY)

#### AWS ECR

Amazon Elastic Container Registry (Amazon ECR) is an AWS managed container image registry service that is secure, scalable, and reliable. Amazon ECR supports private repositories with resource-based permissions using AWS IAM. [Docs _al](https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html)


#### Misc infos: 

- With **Amazon S3 Select**, you can use structured query language (SQL) statements to filter the contents of an Amazon S3 object and retrieve only the subset of data that you need.
- Boto3 makes it easy to integrate your Python application, library, or script with AWS services including Amazon S3, Amazon EC2, Amazon DynamoDB, and more. [boto3 client vs resource vs session _al](https://stackoverflow.com/questions/42809096/difference-in-boto3-between-resource-client-and-session)
  - boto3.client interface provides a low-level, service-specific API. It exposes methods and parameters that closely mirror the AWS service APIs.
  - boto3.resource interface provides a higher-level, object-oriented API. It abstracts away many of the low-level details and provides a more Pythonic and object-oriented way to work with AWS services.
  - Session stores configuration information (primarily credentials and selected region) & allows you to create service clients and resources

------------------------

### Database_internals

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

------------------------------

### SQL Functions

- Joins in SQL: INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL JOIN. Syntax: `SELECT table1.column1,table1.column2,table2.column1,.... FROM table1 JOIN table2 ON table1.matching_column = table2.matching_column;`. Here, table1: First table, table2: Second table, matching_column: Column common to both the tables.
- Order of execution in SQL: 

```
FROM [MyTable]
ON [MyCondition]
JOIN [MyJoinedTable]
WHERE [...]
GROUP BY [...]
HAVING [...]
SELECT [...]
ORDER BY [...]
```

- Aggregate Functions in sql: COUNT(), SUM(), AVG(), MIN(), MAX().
- Window/ Analytic Functions in sql: ORDER BY, PARTITION BY, RANK(), DENSE_RANK(), ROW_NUMBER(), LEAD(), LAG(). [Window functions sql example _vl](https://www.youtube.com/watch?v=Ww71knvhQ-s&ab_channel=techTFQ) Eg: 

Consider a table named employees with the following data:

| emp_id | emp_name | department |
| :----: | :------: | :--------: |
|   1    |  Alice   |     HR     |
|   1    |   Bob    |     HR     |
|   1    | Charlie  |   Sales    |
|   1    |  David   |   Sales    |
|   1    |   Eve    | Marketing  |

For: `SELECT emp_name, department, RANK() OVER (ORDER BY department) AS dept_rank FROM employees;`
`RANK()`: RANK() is a window function that assigns a unique rank to each row within the partition of a result set. It assigns the same rank to rows with the same values and leaves gaps between ranks when there are ties.
Output: 
| emp_id  | emp_name  | dept_rank |
| :-----: | :-------: | :-------: |
|  Alice  |    HR     |     1     |
|   Bob   |    HR     |     1     |
| Charlie |   Sales   |     3     |
|  David  |   Sales   |     3     |
|   Eve   | Marketing |     5     |

For: `SELECT emp_name, department, DENSE_RANK() OVER (ORDER BY department) AS dept_dense_rank FROM employees;`
`DENSE_RANK()`: DENSE_RANK() is similar to RANK() but it doesn't leave gaps between ranks when there are ties. It assigns consecutive ranks to rows with the same values, so there are no gaps in the ranking sequence.
Output: 
| emp_id  | emp_name  | dept_dense_rank |
| :-----: | :-------: | :-------------: |
|  Alice  |    HR     |        1        |
|   Bob   |    HR     |        1        |
| Charlie |   Sales   |        2        |
|  David  |   Sales   |        2        |
|   Eve   | Marketing |        3        |

For: `SELECT emp_name, department, ROW_NUMBER() OVER (ORDER BY emp_name) AS row_num FROM employees;`
`ROW_NUMBER()`: ROW_NUMBER() is a window function that assigns a unique sequential integer to each row within the partition of a result set. It does not handle ties; each row receives a distinct number, starting from 1 and incrementing by 1 for each row.
Output: 
| emp_id  | emp_name  | row_num |
| :-----: | :-------: | :-----: |
|  Alice  |    HR     |    1    |
|   Bob   |    HR     |    2    |
| Charlie |   Sales   |    3    |
|  David  |   Sales   |    4    |
|   Eve   | Marketing |    5    |

For: `SELECT emp_name, department, RANK() OVER () AS rank_all FROM employees;`
`OVER()`: OVER() is a clause used with window functions to define the window or set of rows that the function operates on. It specifies the partitioning and ordering of the rows in the result set for the window function to process. If used without any specific partitioning or ordering, it considers the entire result set as a single partition.
Output: 
| emp_id  | emp_name  | rank_all |
| :-----: | :-------: | :------: |
|  Alice  |    HR     |    1     |
|   Bob   |    HR     |    1     |
| Charlie |   Sales   |    3     |
|  David  |   Sales   |    3     |
|   Eve   | Marketing |    5     |

For: `SELECT emp_name, department, RANK() OVER (PARTITION BY department ORDER BY emp_name) AS dept_rank FROM employees;`
`OVER() PARTITION BY`: OVER() PARTITION BY is used to partition the result set into distinct subsets (partitions) based on the values of one or more columns. It divides the result set into groups, and the window function is applied separately to each group. Within each partition, the window function operates on the rows based on the specified ordering (or the default ordering if not specified).
Output: 
| emp_id  | emp_name  | dept_rank |
| :-----: | :-------: | :-------: |
|  Alice  |    HR     |     1     |
|   Bob   |    HR     |     2     |
| Charlie |   Sales   |     1     |
|  David  |   Sales   |     2     |
|   Eve   | Marketing |     1     |

For: `SELECT emp_name, department, ROW_NUMBER() OVER (PARTITION BY department ORDER BY emp_name) AS dept_row_num FROM employees;`
`ROW_NUMBER() OVER() PARTITION BY`: ROW_NUMBER() OVER() PARTITION BY combines the functionality of ROW_NUMBER() and OVER() PARTITION BY. It assigns a unique sequential integer to each row within each partition of the result set. The numbering starts from 1 for each partition, and rows are ordered within each partition as specified.
Output: 
| emp_id  | emp_name  | dept_row_num |
| :-----: | :-------: | :----------: |
|  Alice  |    HR     |      1       |
|   Bob   |    HR     |      2       |
| Charlie |   Sales   |      1       |
|  David  |   Sales   |      2       |
|   Eve   | Marketing |      1       |

For: `SELECT emp_name, department, ROW_NUMBER() OVER (PARTITION BY department ORDER BY emp_name) AS dept_row_num FROM employees;`
`ROW_NUMBER() OVER PARTITION BY ORDER BY`: Similar to ROW_NUMBER() OVER() PARTITION BY, but with an added ORDER BY clause. It assigns a unique sequential integer to each row within each partition, ordered by the specified column(s). The numbering starts from 1 for each partition, and rows are ordered within each partition according to the specified ordering.
Output: 
| emp_id  | emp_name  | dept_row_num |
| :-----: | :-------: | :----------: |
|  Alice  |    HR     |      1       |
|   Bob   |    HR     |      2       |
| Charlie |   Sales   |      1       |
|  David  |   Sales   |      2       |
|   Eve   | Marketing |      1       |

- SQL UPSERT command: It’s “update” and “insert.” In the context of relational databases, an upsert is a database operation that will update an existing row if a specified value already exists in a table, and insert a new row if the specified value doesn't already exist.
- SQL clause "GROUP BY 1" mean: It means to group by the first column of your result set regardless of what it's called. You can do the same with ORDER BY.
- SQL CHECK constraint: It is used to specify the condition that must be validated in order to insert data into a table. Eg: 

```
CREATE TABLE Orders (
order_id INT PRIMARY KEY, amount INT CHECK (amount > 0));
```

- Keys in SQL: 
  - A **primary key** uniquely identifies each record in a database table. Any individual key that does this can be called a **candidate key**, but only one can be chosen by database engineers as a primary key. 
  - A **composite key** is composed of two or more attributes that collectively uniquely identify each record. 
  - A **foreign key** in a database table is taken from some other table and applied in order to link database records back to that foreign table. The foreign key in the database table where it resides is actually the primary key of the other table.
  - For more details, my notes: [cs_core_notes _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/DBMS/dbms%20(5).jpg)
- `SELECT CURRENT_TIMESTAMP()` - Return the current date and time. 
- The `TRUNCATE` statement removes all data from a table but leaves the table structure intact. The `DELETE` statement is used to remove rows from a table one by one. The `DROP` statement deletes the entire table, including all data and the table structure. [difference truncate, delete, drop _al](https://stackoverflow.com/questions/32499763/what-is-the-difference-between-truncate-drop-and-delete-of-tables-and-when-to)
- LIKE Operator: We use the SQL LIKE operator with the WHERE clause to get a result set that matches the given string pattern. Eg: `SELECT * FROM Customers WHERE country LIKE 'UK';`
- `WITH` Clause: A WITH clause defines a temporary data set whose output is available to be referenced in subsequent queries. Eg: 

```
WITH cte_quantity
AS
(SELECT
    SUM(Quantity) as Total
FROM OrderDetails
GROUP BY ProductID) 
SELECT
    AVG(Total) average_product_quantity
FROM cte_quantity;
```

- Order of execution of ORDER BY and LIMIT in a MySQL query: A SQL LIMIT will in all databases always work on the result of a query, so it will first run the query with the ORDER BY and that result will then be limited.

------------------------------

### Linux_internals_and_commands

- `grep -i "UNix" geekfile.txt`: Case insensitive search
- `grep -c "unix" geekfile.txt`: Displaying the count of number of matches
- `grep -l "unix" *` (or) `grep -l "unix" f1.txt f2.txt f3.xt f4.txt`: Display the file names that matches the pattern
- `grep -w "unix" geekfile.txt`: Checking for the whole words in a file
- `cat <file_name>`: View file content
- `:q!`: Exit vim terminal 
- `:wq!`: Save and exit vim terminal 
- `:%d`: Clear all contents of a file 
- `:set nu`: Will put index numbers in file opened via vim
- `vi ~/.bash_profile`: Opens the .bash_profile file in the vi text editor. This file typically contains settings and configurations for the Bash shell.
- `vi .bash_history`: Opens the .bash_history file in the vi text editor. This file contains a history of commands that have been executed in the current user's Bash shell.
- `top`: The top command displays real-time information about system processes. It provides a dynamic view of system resource usage, including CPU and memory usage, as well as information about running processes. Users can monitor the processes, their resource consumption, and manage them interactively.
- `fdisk -l`: The fdisk command is used for disk partitioning and disk management on Unix-like systems. The -l option lists information about all available disks and their partitions. This command is typically used to view the current disk layout and partitioning scheme of the system.
- `ps -ef`: The ps command is used to display information about running processes on Unix-like systems. The -ef options stand for "everyone" (-e) and "full-format" (-f), which together instruct ps to display information about all processes in a detailed format. This includes information such as the process ID (PID), the terminal associated with the process, the user running the process, CPU and memory usage, and the command being executed.
- `ls -l <dir path else it lists current path files>`: Lists files and directories in the specified directory (or the current directory if none is specified) with detailed information, including permissions, ownership, size, and modification date.
- `ls -lrt`: Lists files and directories in the current directory in long format (-l) sorted by modification time in reverse order (-r for reverse, -t for time).
- `pwd`: Prints the current working directory.
- `ls -la`: Lists all files (including hidden files) and directories in the current directory in long format, showing detailed information, including hidden files (-a for all).
- `su``: Allows switching to another user account. If no username is specified, it defaults to the superuser (root) account.
- `su root`: Switches to the root user account.
- `whoami`: Displays the username of the current user.
- `which python`: Displays path where executable file of python is located.
- `top`: Displays real-time information about system processes, including CPU and memory usage.
- `set | grep AWS_KEY`: Displays environment variables (set) and filters the output to show lines containing AWS_KEY using grep.
- `screen -ls`: Lists currently running screen sessions.
- `screen -S vikas`: Starts a new screen session with the name vikas.
- `find ~ -name aws_credentials`: Searches for files named aws_credentials in the user's home directory (~).
- `grep -iR AWS_KEY *`: Searches recursively (-R) for occurrences of AWS_KEY in files in the current directory and its subdirectories (*).
- `exit`: Exits the current shell or session.
- `grep -iR access <path>`: Searches recursively for occurrences of access in files within the specified path.
- `echo $ec2`: Prints the value of the environment variable ec2.
- `pip install -U s3fs=0.4.0`: Installs or upgrades the s3fs Python package to version 0.4.0 using pip.
- `cd ./venvs`: Changes the current directory to venvs, which is located in the current directory (.).
- `df -h`: The df command is used to display disk space usage on Unix-like systems. The -h option stands for "human-readable" and formats the output in a more easily understandable way, showing sizes in kilobytes, megabytes, gigabytes, etc., rather than in raw bytes.
- `du psycopg2-2.9.3.tar.gz`: Displays the disk usage of the psycopg2-2.9.3.tar.gz file.
- `du -sh psycopg2-2.9.3.tar.gz`: Displays the disk usage of the psycopg2-2.9.3.tar.gz file in a human-readable format (-h) and summarizes the total (-s).
- `du -sh *`: Displays the disk usage of all files and directories in the current directory in a human-readable format and summarizes the total.
- `du -sh * | sort -h`: Displays the disk usage of all files and directories in the current directory in a human-readable format, summarizes the total, and sorts the output numerically and in a human-readable way (-h).
- `conda list`: Lists installed packages and their versions using Conda, a package manager for Python.
- `echo $PATH`: It prints out the value of the PATH environment variable. 
- `sudo -su user`: It is short for sudo -s -u user. The -s option means to run the shell specified in the environment variable SHELL if this has been set, or else the user's login shell. The -u user option means to run the command as the specified user rather than root. 
- `sudo su user`: It will use sudo to run the command su user as the root user. The su command will then invoke the login shell of the specified username. The su user command could be run without the use of sudo, but by running it as root it will not require the password of the target user.
- `rm /path/to/directory/*`: To remove all non-hidden files* in a directory 
- `rm -r /path/to/directory/*`: To remove all non-hidden files and sub-directories (along with all of their contents) in a directory
- `rm -rf "/path/to the/directory/"*`: Force removal of files

Note: [Shell scripts best practices _al](https://stackoverflow.com/questions/78497/design-patterns-or-best-practices-for-shell-scripts)

- [How a Linux system boots up, from the power button being pressed to the operating system being loaded _vl](https://www.youtube.com/watch?v=XpFsMB6FoOs): 
  - The boot process starts with the BIOS or UEFI, which prepares the computer’s hardware for action.
  - UEFI offers faster boot times and better security features compared to BIOS.
  - The power-on self-test (POST) checks the hardware before fully turning on the system.
  - The boot loader locates the operating system kernel, loads it into memory, and starts running it.
  - Systemd is the parent of all other processes on Linux and handles various tasks to get the system booted and ready to use.

------------------------------

### Webhooks_APIs_Websockets 

- An **API** is a messenger that delivers your request to the provider you're requesting it from and then responds to you. ​​APIs are request-based, meaning that they operate when requests come from 3rd party apps.
- **Webhook**, also called reverse API, web callback, or an HTTP push API, is a way for an app to provide other applications with real-time information. It delivers data as an event happens or almost immediately. Webhooks are event-based, meaning they will run when a specific event occurs in the source app. ​​To use a real-world analogy, APIs would be likened to you repeatedly calling a retailer to ask if they've stocked up on a brand of shoes you like. Webhooks would then ask the retailer to contact you whenever they have the shoes in stock, which frees up time on both sides. 
- **Websockets** are different, it is an open connection. With WebSockets, a persistent connection (means, continuous polling) is established between the client and server, enabling real-time data transfer in both directions. This is particularly useful for applications that require continuous, low-latency communication, such as online games or chat applications.

------------------------------

### HTTP Request

HTTP is a method for encoding and transporting data between a client and a server. It is a request/response protocol: clients issue requests and servers issue responses with relevant content and completion status info about the request. HTTP is self-contained, allowing requests and responses to flow through many intermediate routers and servers that perform load balancing, caching, encryption, and compression.

HTTP is an application layer protocol relying on lower-level protocols such as TCP and UDP.

In general, an HTTP request is divided into 3 parts: 
- A request line: We place the HTTP method to be used, the URI of the request and the HTTP protocol to be used. HTTP methods indicate what kind of action our client wants to perform, whether he wants to read a resource, or if he wants to send information to the API, etc. The URI refers to the address where the resource is located. And the HTTP protocol refers to which HTTP protocol will be used, this is because there are several versions of the HTTP protocol, at the time of writing this post, the most common protocol is HTTP/1.1, however, there are other more recent revisions , like the HTTP/2.0 revision. Eg: `GET /api/authors HTTP/1.1` - means we are requesting a resource from endpoint. 
- A set of header fields: Headers are metadata that are sent in the request to provide information about the request. Each header is specified with a name, then two points, and then followed by the value of that header. Eg: `Host: en.wikipedia.org`, or `Cache-Control: no-cache`. The Host and Cache-Control headers are standard headers, which already have a well-defined purpose. However, we are free to use our own custom headers.  
- A body, which is optional: The Request Body is where we put additional information that we are going to send to the server. In the body of the request we are free to place virtually whatever we want. From the username and password of a person trying to login to our system, to the answers of a complex form of a survey. The body is quite important, because it represents, in many cases, the content per se that one wants to transmit. We note that GET requests do not use a body, because one does not tend to send many complex data when reading information. In the case of the POST method, we usually use the body of the request to place what we want to send. Eg: `Hello`

Clubbing all examples: 

```
HTTP Request: GET /api/autores HTTP/1.1
Headers: 
Host: en.wikipedia.org
Cache-Control: no-cache
Example of Request body for POST request: 
{
    "Name": "Test",
    "Age": 123
}
```

[Anatomy of HTTP request _al](https://gavilan.blog/2019/01/03/anatomy-of-an-http-request/)

When the client sends us an HTTP request, server responds with an HTTP response. The HTTP response also has its own structure, which is quite similar to the structure of the request. These parts are: `Status line`, `Header`, `Body (optional)`. Eg:

``` 
HTTP/1.1 200 OK
Date: Thu, 29 Mar 2024 19:43:07 IST
Server: gws
Accept-Ranges: bytes
Content-Length: 68894
Content-Type: text/html; charset=UTF-8
<!doctype html><html …
```

------------------------------

### HTTP_1_vs_HTTP_2

- HTTP stands for hypertext transfer protocol, and it is the basis for almost all web applications. More specifically, HTTP is the method computers and servers use to request and send information. For instance, when someone navigates to cloudflare.com on their laptop, their web browser sends an HTTP request to the Cloudflare servers for the content that appears on the page. Then, Cloudflare servers send HTTP responses with the text, images, and formatting that the browser displays to the user.
- The first usable version of HTTP was created in 1997. Because it went through several stages of development, this first version of HTTP was called HTTP/1.1. This version is still in use on the web. In 2015, a new version of HTTP called HTTP/2 was created. In particular, HTTP/2 is much faster and more efficient than HTTP/1.1. One of the ways in which HTTP/2 is faster is in how it prioritizes content during the loading process.
- In the context of web performance, prioritization refers to the order in which pieces of content are loaded. Suppose a user visits a news website and navigates to an article. Should the photo at the top of the article load first? Should the text of the article load first? Should the banner ads load first? Prioritization affects a webpage's load time. For example, certain resources, like large JavaScript files, may block the rest of the page from loading if they have to load first. More of the page can load at once if these render-blocking resources load last. In HTTP/2, developers have hands-on, detailed control over prioritization. This allows them to maximize perceived and actual page load speed to a degree that was not possible in HTTP/1.1. HTTP/2 offers a feature called weighted prioritization. This allows developers to decide which page resources will load first, every time. In HTTP/2, when a client makes a request for a webpage, the server sends several streams of data to the client at once, instead of sending one thing after another. This method of data delivery is known as multiplexing. Developers can assign each of these data streams a different weighted value, and the value tells the client which data stream to render first.
- Other differences: 
  - Multiplexing: HTTP/1.1 loads resources one after the other, so if one resource cannot be loaded, it blocks all the other resources behind it. In contrast, HTTP/2 is able to use a single TCP connection to send multiple streams of data at once so that no one resource blocks any other resource. HTTP/2 does this by splitting data into binary-code messages and numbering these messages so that the client knows which stream each binary message belongs to.
  - Server push: Typically, a server only serves content to a client device if the client asks for it. However, this approach is not always practical for modern webpages, which often involve several dozen separate resources that the client must request. HTTP/2 solves this problem by allowing a server to "push" content to a client before the client asks for it. The server also sends a message letting the client know what pushed content to expect - eg: Table of contents.
  - Header compression: Small files load more quickly than large ones. To speed up web performance, both HTTP/1.1 and HTTP/2 compress HTTP messages to make them smaller. However, HTTP/2 uses a more advanced compression method called **HPACK** that eliminates redundant information in HTTP header packets. This eliminates a few bytes from every HTTP packet. Given the volume of HTTP packets involved in loading even a single webpage, those bytes add up quickly, resulting in faster loading.
- HTTP/3 is the next proposed version of the HTTP protocol. HTTP/3 does not have wide adoption on the web yet, but it is growing in usage. The key difference between HTTP/3 and previous versions of the protocol is that HTTP/3 runs over QUIC instead of TCP. QUIC is a faster and more secure transport layer protocol that is designed for the needs of the modern Internet.
[http 1.1 and 2.0 _al](https://www.cloudflare.com/en-gb/learning/performance/http2-vs-http1.1/)

------------------------------

### Docker 

- Docker runs on a client-server that is meditated by the daemon that leverages REST APIs to request to perform container-related operations. Podman, on the other hand, does not require a daemon. It uses Pods to manage containers, which helps users to run rootless containers.

------------------------------

### TCP vs UDP 

(From Opensource Github repos knowledge extraction section | system-design-primer):

TCP is a connection-oriented protocol over an IP network. Connection is established and terminated using a handshake. All packets sent are guaranteed to reach the destination in the original order and without corruption through:
- Sequence numbers and checksum fields for each packet
- Acknowledgement packets and automatic retransmission
If the sender does not receive a correct response, it will resend the packets. If there are multiple timeouts, the connection is dropped. TCP also implements flow control and congestion control. These guarantees cause delays and generally result in less efficient transmission than UDP.
To ensure high throughput, web servers can keep a large number of TCP connections open, resulting in high memory usage. It can be expensive to have a large number of open connections between web server threads and say, a memcached server. Connection pooling can help in addition to switching to UDP where applicable.
TCP is useful for applications that require high reliability but are less time critical. Some examples include web servers, database info, SMTP, FTP, and SSH.
Use TCP over UDP when:
- You need all of the data to arrive intact
- You want to automatically make a best estimate use of the network throughput

UDP is connectionless. Datagrams (analogous to packets) are guaranteed only at the datagram level. Datagrams might reach their destination out of order or not at all. UDP does not support congestion control. Without the guarantees that TCP support, UDP is generally more efficient. UDP can broadcast, sending datagrams to all devices on the subnet. This is useful with DHCP because the client has not yet received an IP address, thus preventing a way for TCP to stream without the IP address.
UDP is less reliable but works well in real time use cases such as VoIP, video chat, streaming, and realtime multiplayer games.
Use UDP over TCP when:
- You need the lowest latency
- Late data is worse than loss of data
- You want to implement your own error correction

Note: There is always a layer above TCP. The question is really about how much overhead the stuff above TCP adds. HTTP is relatively chunky because each transmission requires a bunch of header cruft in both the request and the response. It also tends to be used in a stateless mode, whereby each request/response uses a separate TCP session. Keep-alives can ameliorate the session-per-request, but not the headers.

------------------------------

### gRPC_REST_GraphQL

gRPC (Remote Procedure Call) uses Protobufs to encode and send data (.proto file) (It can use other formats like JSON as well). In an RPC, a client causes a procedure to execute on a different address space, usually a remote server. The procedure is coded as if it were a local procedure call, abstracting away the details of how to communicate with the server from the client program. Remote calls are usually slower and less reliable than local calls so it is helpful to distinguish RPC calls from local calls. Popular RPC frameworks include Protobuf, Thrift, and Avro.
- Protocol buffers are Google's language-agnostic, platform-neutral, extensible mechanism for serializing structured data. gRPC uses HTTP2. 
- Also, in other words, **LPC (Local Procedure Call)** vs **RPC (Remote Procedure Call)**: 
  - Host machine invokes a function call in itself, executes & gets the output - LPC
  - Host machine invokes a function call on another machine, executes & gets the output - RPC
- In RPC, there can be issues like: RPC is slower than LPC since it uses the network to invoke the method. Failures can happen, etc. 

REST is an architectural style enforcing a client/server model where the client acts on a set of resources managed by the server. The server provides a representation of resources and actions that can either manipulate or get a new representation of resources. All communication must be stateless and cacheable.

GraphQL is an open source query language that describes how a client should request information through an API.

[gRPC vs REST vs. GraphQL _al](https://www.linkedin.com/pulse/rest-graphql-grpc-comparing-contrasting-modern-api-design-walpita/),
[gRPC over REST _al](https://medium.com/@sankar.p/how-grpc-convinced-me-to-chose-it-over-rest-30408bf42794),
[RPC vs REST _al](https://github.com/donnemartin/system-design-primer?tab=readme-ov-file#rpc-and-rest-calls-comparison),
[Graphql _al](https://www.youtube.com/watch?v=yWzKJPw_VzM),
[gRPC _vl](https://www.youtube.com/watch?v=gnchfOojMk4)

------------------------------

### JSON vs Protobuf

- Protocol Buffers are language-neutral, platform-neutral extensible mechanisms for serializing structured data. Serialization is the process of converting the state of an object, that is, the values of its properties, into a form that can be stored or transmitted.
- JSON is a format that encodes objects in a string. In this context: Serialization means to convert an object into that string, and deserialization is its inverse operation (convert string -> object). When transmitting data or storing them in a file, the data are required to be byte strings, but complex objects are seldom in this format. Serialization can convert these complex objects into byte strings for such use. After the byte strings are transmitted, the receiver will have to recover the original object from the byte string. This is known as deserialization. Say, you have an object: {foo: [1, 4, 7, 10], bar: "baz"} serializing into JSON will convert it into a string: '{"foo":[1,4,7,10],"bar":"baz"}' which can be stored or sent through wire to anywhere. The receiver can then deserialize this string to get back the original object. {foo: [1, 4, 7, 10], bar: "baz"}. [Serialize, Deserialize in json _al](https://stackoverflow.com/questions/3316762/what-is-deserialize-and-serialize-in-json)
- When to use JSON and Protobuf:
  - JSON when: you need or want data to be human readable, data from the service is directly consumed by a web browser, your server side application is written in JavaScript, you aren’t prepared to tie the data model to a schema, the operational burden of running a different kind of network service is too great. 
  - Protobuf for relatively smaller size, guarantees type-safety, prevents schema-violations, gives you simple accessors, fast serialization/deserialization, backward compatibility.

[JSON vs protobuf _al](https://stackoverflow.com/questions/52409579/protocol-buffer-vs-json-when-to-choose-one-over-another)

------------------------------

### Git 

Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency. Under the hood, it's all about pointers. 
Useful links: 
- [Changing base branch git _al](https://stackoverflow.com/questions/10853935/change-branch-base)
- [Squashing commits _al](https://stackoverflow.com/questions/5189560/how-do-i-squash-my-last-n-commits-together)
- [Keep a branch synchronized/updated with master _al](https://stackoverflow.com/questions/16329776/how-to-keep-a-branch-synchronized-updated-with-master)
- [Get changes from master into branch in Git _al](https://stackoverflow.com/questions/5340724/get-changes-from-master-into-branch-in-git)
- [Git branches work _al](https://stackoverflow.blog/2021/04/05/a-look-under-the-hood-how-branches-work-in-git/)
- [Where do git files live _al](https://jvns.ca/blog/2023/09/14/in-a-git-repository--where-do-your-files-live-/)

------------------------------

### cURL 

We often see cURL commands to hit API endpoints in technical docs of any software. It is a command-line tool and library for making HTTP requests and working with URLs. It stands for "Client for URLs" and is often used for testing APIs, making HTTP requests, and performing various web-related tasks from the command line or within scripts. Usage: 
- Quick Testing: curl provides a simple and convenient way to quickly test an API endpoint without the need for a full-fledged programming environment. You can test different HTTP methods, headers, query parameters, and more by constructing a curl command.
- Command-Line Usability: Many developers are comfortable using the command line, and curl offers a way to interact with APIs without needing to write code. This makes it accessible to a wide range of users.
- Examples in Documentation: API documentation often includes curl examples to demonstrate how to make API requests. These examples are generally concise and can be easily copied and modified for testing purposes.
- Cross-Platform: curl is available on various operating systems, including Unix-like systems (Linux, macOS) and Windows, making it a versatile choice for developers working on different platforms.
- HTTP Methods and Options: curl supports various HTTP methods (GET, POST, PUT, DELETE, etc.) and allows you to customize headers, query parameters, and request bodies. This flexibility is useful when exploring API capabilities.
- Debugging: When encountering issues with an API request, you can use curl to inspect the raw request and response data, including headers, to diagnose problems.
- Automation: While it's a command-line tool, curl can also be used within scripts or automation processes to interact with APIs programmatically.
- Example of using curl to make a GET request: `curl -X POST -H "Content-Type: application/json" -d '{"key": "value"}' https://api.example.com/endpoint`
- Note: To convert cURL to Python request, follow this link: [Execute curl command _al](https://stackoverflow.com/questions/25491090/how-to-use-python-to-execute-a-curl-command)

------------------------------

### Data_transformation_info

#### JSON explode vs JSON normalize  

JSON explode creates more rows by expanding a column with lists, while JSON normalize creates more columns by flattening nested JSON objects within a column.

```
Consider the df: 
   id   name       scores
0   1  Alice  [90, 95, 88]
1   2    Bob      [85, 92]

df_exploded = df.explode('scores')

The df_exploded DataFrame after applying JSON explode:
   id   name scores
0   1  Alice     90
0   1  Alice     95
0   1  Alice     88
1   2    Bob     85
1   2    Bob     92

df_normalized = pd.json_normalize(df, 'scores', ['id', 'name'], sep='_')

The df_normalized DataFrame after applying JSON normalize:
   id   name  scores_0  scores_1  scores_2
0   1  Alice        90        95        88
1   2    Bob        85        92       NaN
```

Sidenote: When you use json_normalize to flatten a nested column in a DataFrame, the non-nested columns are not automatically included in the flattened result. json_normalize only operates on the specified nested column and doesn't consider the other columns in the original DataFrame. That's why there is a need to add them back to the flattened DataFrame if you want to retain all the columns from the original DataFrame. In many cases, especially when working with nested JSON data, you might want to perform operations on specific nested columns separately, and you may not need all columns in every operation. Adding the non-nested columns back gives you the flexibility to choose which columns to include in your final DataFrame based on your analysis or processing needs. It allows you to control which columns are present in the flattened DataFrame, which can be especially useful when working with large or complex datasets. In summary, json_normalize focuses on flattening the specified nested column, and if you want to retain non-nested columns, you need to add them back manually to the resulting DataFrame to have a complete view of your data. Eg this code:

```
for col in ist_all_tickets_df.columns.difference(['custom_fields']):
		list_all_tickets_df_normalized[col] = list_all_tickets_df[col]
```

[JSON Flattening _al](https://stackoverflow.com/questions/49822874/i-want-to-flatten-json-column-in-a-pandas-dataframe)

#### Dataframe Index   

In a DataFrame, the "index" refers to the row labels or identifiers that uniquely identify each row of data. It is essentially an ordered set of labels or integers that allows you to access and retrieve rows by their labels.In this example, the index consists of the integers 0, 1, 2, and 3, which correspond to the row positions in the DataFrame. Each row has a unique index label.

```
      Name  Age
0    Alice   25
1      Bob   30
2  Charlie   22
3    David   28

Note:
# Specify a custom index with duplicates

custom_index = ['A', 'B', 'A', 'D']
df = pd.DataFrame(data, index=custom_index)
      Name  Age
A    Alice   25
B      Bob   30
A  Charlie   22
D    David   28
```

In the example, the index labels 'A' are duplicated, as they appear more than once. This is what is meant by a "duplicate index." Duplicate index labels can lead to issues when performing certain operations or transformations on a DataFrame.

#### Dataframe Reset Index   

If you encounter issues related to duplicate indices in your DataFrame, it's often a good practice to reset the index to ensure that it is unique and continuous. 

You can do this using `df.reset_index(drop=True, inplace=True)` as shown in the previous code examples. If you don't use `df.reset_index()` after exploding and flattening the DataFrame, the output would include the old index as a new column in the DataFrame. 

```
   id   name      street         city
0   1  Alice  123 Main St     New York
1   1  Alice    456 Elm St  Los Angeles
0   2    Bob    789 Oak St      Chicago
As you can see, the old index column (0, 1, etc.) is retained as a new column in the DataFrame. This can sometimes lead to confusion, especially if you want to work with a clean DataFrame that starts with an index of 0 and increments sequentially.
```
------------------------------

### SAML  

A SAML (Security Assertion Markup Language) provider is a system that helps a user access a service they need. There are two primary types of SAML providers, service provider, and identity provider.
- A service provider needs authentication from the identity provider to grant authorization to the user.
- An identity provider performs the authentication that the end user is who they say they are and sends that data to the service provider along with the user’s access rights for the service.

Microsoft Active Directory or Azure are common identity providers. Salesforce and other CRM solutions are usually service providers, in that they depend on an identity provider for user authentication.

SAML works by passing information about users, logins, and attributes between the identity provider and service providers. Each user logs in once to Single Sign On with the identify provider, and then the identify provider can pass SAML attributes to the service provider when the user attempts to access those services. The service provider requests the authorization and authentication from the identify provider. Since both of those systems speak the same language – SAML – the user only needs to log in once.

OAuth is a slightly newer standard that was co-developed by Google and Twitter to enable streamlined internet logins. OAuth uses a similar methodology as SAML to share login information. SAML provides more control to enterprises to keep their SSO logins more secure, whereas OAuth is better on mobile and uses JSON.

Facebook and Google are two OAuth providers that you might use to log into other internet sites.

[What is saml _al](https://www.varonis.com/blog/what-is-saml)

------------------

### Opensource_Github_repos_knowledge_extraction 

#### [donnemartin/system-design-primer _al](https://github.com/donnemartin/system-design-primer)

- A service is scalable if it results in increased performance in a manner proportional to resources added. Generally, increasing performance means serving more units of work, but it can also be to handle larger units of work, such as when datasets grow. Another way to look at performance vs scalability: If you have a performance problem, your system is slow for a single user. If you have a scalability problem, your system is fast for a single user but slow under heavy load.

- Latency is the time to perform some action or to produce some result. Throughput is the number of such actions or results per unit of time. Generally, you should aim for maximal throughput with acceptable latency.

- CAP Theorem: Also note that in a distributed computer system, you can only support two of the following guarantees:
  - Consistency - Every read receives the most recent write or an error
  - Availability - Every request receives a response, without guarantee that it contains the most recent version of the information
  - Partition Tolerance - The system continues to operate despite arbitrary partitioning due to network failures

- With multiple copies of the same data, we are faced with options on how to synchronize them so clients have a consistent view of the data. Consistency: Weak (After a write, reads may or may not see it), Eventual (After a write, reads will eventually see it (typically within milliseconds); Data is replicated asynchronously), Strong (After a write, reads will see it; Data is replicated synchronously) 

- There are two complementary patterns to support high availability: 
  - fail-over:
    - In active-passive fail-over, heartbeats are sent between the active and the passive server on standby. If the heartbeat is interrupted, the passive server takes over the active's IP address and resumes service. The length of downtime is determined by whether the passive server is already running in 'hot' standby or whether it needs to start up from 'cold' standby. Only the active server handles traffic. Active-passive failover can also be referred to as master-slave failover.
    - In active-active fail-over, both servers are managing traffic, spreading the load between them. If the servers are public-facing, the DNS would need to know about the public IPs of both servers. If the servers are internal-facing, application logic would need to know about both servers. Active-active failover can also be referred to as master-master failover.
  - replication:
    - In master-slave, master serves reads and writes, replicating writes to one or more slaves, which serve only reads. Slaves can also replicate to additional slaves in a tree-like fashion. If the master goes offline, the system can continue to operate in read-only mode until a slave is promoted to a master or a new master is provisioned. 
    - In master-master, both masters serve reads and writes and coordinate with each other on writes. If either master goes down, the system can continue to operate with both reads and writes.
  - All of above have their own set of advantages/disadvantages.  

- Availability is often quantified by uptime (or downtime) as a percentage of time the service is available. 99.9% availability qualifies to having acceptable downtime of 43m 49.7s/month. In case of 99.99%, acceptable downtime is 4m 23s/month. 
  - If a service consists of multiple components prone to failure, the service's overall availability depends on whether the components are in sequence or in parallel.
    - In sequence: `Availability (Total) = Availability (Foo) * Availability (Bar)`
    - In parallel: `Availability (Total) = 1 - (1 - Availability (Foo)) * (1 - Availability (Bar))`

- Domain Name System (DNS) translates a domain name such as www.example.com to an IP address. DNS is hierarchical, with a few authoritative servers at the top level. Your router or ISP provides information about which DNS server(s) to contact when doing a lookup. Lower level DNS servers cache mappings, which could become stale due to DNS propagation delays. DNS results can also be cached by your browser or OS for a certain period of time, determined by the time to live (TTL).
    - NS record (name server) - Specifies the DNS servers for your domain/subdomain.
    - MX record (mail exchange) - Specifies the mail servers for accepting messages.
    - A record (address) - Points a name to an IP address.
    - CNAME (canonical) - Points a name to another name or CNAME (example.com to www.example.com) or to an A record.
  - Services such as CloudFlare and Route 53 provide managed DNS services. Some DNS services can route traffic through various methods: Weighted round robin, Latency-based, Geolocation-based
  - (Disadvantages): Accessing a DNS server introduces a slight delay, although mitigated by caching described above. And DNS server management could be complex. Also, DNS services have recently come under DDoS attack, preventing users from accessing websites such as Twitter without knowing Twitter's IP address(es).

- Content Delivery Network (CDN) is a globally distributed network of proxy servers, serving content from locations closer to the user. Generally, static files such as HTML/CSS/JS, photos, and videos are served from CDN, although some CDNs such as Amazon's CloudFront support dynamic content. The site's DNS resolution will tell clients which server to contact. Serving content from CDNs can significantly improve performance in two ways:
    - Users receive content from data centers close to them
    - Your servers do not have to serve requests that the CDN fulfills
  - Push CDNs receive new content whenever changes occur on your server. You take full responsibility for providing content, uploading directly to the CDN and rewriting URLs to point to the CDN. You can configure when content expires and when it is updated. Content is uploaded only when it is new or changed, minimizing traffic, but maximizing storage. Sites with a small amount of traffic or sites with content that isn't often updated work well with push CDNs. Content is placed on the CDNs once, instead of being re-pulled at regular intervals.
  - Pull CDNs grab new content from your server when the first user requests the content. You leave the content on your server and rewrite URLs to point to the CDN. This results in a slower request until the content is cached on the CDN. A time-to-live (TTL) determines how long content is cached. Pull CDNs minimize storage space on the CDN, but can create redundant traffic if files expire and are pulled before they have actually changed. Sites with heavy traffic work well with pull CDNs, as traffic is spread out more evenly with only recently-requested content remaining on the CDN.
  - (Disadvantages): CDN costs could be significant depending on traffic, although this should be weighed with additional costs you would incur not using a CDN. Content might be stale if it is updated before the TTL expires it. CDNs require changing URLs for static content to point to the CDN.

- Load balancers distribute incoming client requests to computing resources such as application servers and databases. In each case, the load balancer returns the response from the computing resource to the appropriate client. Load balancers are effective at:
    - Preventing requests from going to unhealthy servers
    - Preventing overloading resources
    - Helping to eliminate a single point of failure
    - Load balancers can be implemented with hardware (expensive) or with software such as HAProxy.
  - Additional benefits include:
    - SSL termination - Decrypt incoming requests and encrypt server responses so backend servers do not have to perform these potentially expensive operations
    - Session persistence - Issue cookies and route a specific client's requests to same instance if the web apps do not keep track of sessions. Note that to protect against failures, it's common to set up multiple load balancers, either in active-passive or active-active mode.
  - Load balancers can route traffic based on various metrics, including: Random, Least loaded, Session/cookies, Round robin or weighted round robin, Layer 4, Layer 7. 
  - Layer 4 load balancers look at info at the transport layer to decide how to distribute requests. Generally, this involves the source, destination IP addresses, and ports in the header, but not the contents of the packet. Layer 4 load balancers forward network packets to and from the upstream server, performing Network Address Translation (NAT).
  - Layer 7 load balancers look at the application layer to decide how to distribute requests. This can involve contents of the header, message, and cookies. Layer 7 load balancers terminate network traffic, reads the message, makes a load-balancing decision, then opens a connection to the selected server. For example, a layer 7 load balancer can direct video traffic to servers that host videos while directing more sensitive user billing traffic to security-hardened servers.
  - Load balancers can also help with horizontal scaling, improving performance and availability. But disadvantages for horizontal scaling is: It introduces complexity and involves cloning servers - hence servers should be stateless: they should not contain any user-related data like sessions or profile pictures and sessions can be stored in a centralized data store such as a database (SQL, NoSQL) or a persistent cache (Redis, Memcached); Downstream servers such as caches and databases need to handle more simultaneous connections as upstream servers scale out
  - (Disadvantages): The load balancer can become a performance bottleneck if it does not have enough resources or if it is not configured properly. Introducing a load balancer to help eliminate a single point of failure results in increased complexity. A single load balancer is a single point of failure, configuring multiple load balancers further increases complexity.

- Reverse Proxy: It is a web server that centralizes internal services and provides unified interfaces to the public. Requests from clients are forwarded to a server that can fulfill it before the reverse proxy returns the server's response to the client.
  - (Benefits): Increased security - Hide information about backend servers, blacklist IPs, limit number of connections per client; Increased scalability and flexibility - Clients only see the reverse proxy's IP, allowing you to scale servers or change their configuration; SSL termination - Decrypt incoming requests and encrypt server responses so backend servers do not have to perform these potentially expensive operations; Compression - Compress server responses; Caching - Return the response for cached requests Static content - Serve static content directly like html/css, photos, videos. 
  - Deploying a load balancer is useful when you have multiple servers. Often, load balancers route traffic to a set of servers serving the same function. Reverse proxies can be useful even with just one web server or application server, opening up the benefits described in the previous section. Solutions such as NGINX and HAProxy can support both layer 7 reverse proxying and load balancing.
  - [Reverse proxy vs API Gateway vs Load Balancer _vl](https://www.youtube.com/watch?v=RqfaTIWc3LQ)

- Microservices: Can be described as a suite of independently deployable, small, modular services. Each service runs a unique process and communicates through a well-defined, lightweight mechanism to serve a business goal. Pinterest, for example, could have the following microservices: user profile, follower, feed, search, photo upload microservices, etc.

- Caching improves page load times and can reduce the load on your servers and databases. In this model, the dispatcher will first lookup if the request has been made before and try to find the previous result to return, in order to save the actual execution. Databases often benefit from a uniform distribution of reads and writes across its partitions. Popular items can skew the distribution, causing bottlenecks. Putting a cache in front of a database can help absorb uneven loads and spikes in traffic.
  - We can have caching at: Client, Web server, Database, CDN, Application, Database query level, Object level caching.
  - When to update the cache: 
    - Cache-aside: The application is responsible for reading and writing from storage. The cache does not interact with storage directly. In short: Look for entry in cache -> resulting in a cache miss -> Load entry from the database -> Add entry to cache -> Return entry. Cache-aside is also referred to as lazy loading. Only requested data is cached, which avoids filling up the cache with data that isn't requested.
    - Write-through: The application uses the cache as the main data store, reading and writing data to it, while the cache is responsible for reading and writing to the database. In short: Application adds/updates entry in cache -> Cache synchronously writes entry to data store -> Return
    - Write-behind (write-back): In write-behind, the application does the following, In short: Add/update entry in cache -> Asynchronously write entry to the data store -> thereby improving write performance
    - Refresh-ahead: You can configure the cache to automatically refresh any recently accessed cache entry prior to its expiration. Refresh-ahead can result in reduced latency vs read-through if the cache can accurately predict which items are likely to be needed in the future.
    - All have their own set of advantages, disadvantages. 

- Asynchronism
  - Message queues receive, hold, and deliver messages. If an operation is too slow to perform inline, you can use a message queue with the following workflow:
      - An application publishes a job to the queue, then notifies the user of job status
      - A worker picks up the job from the queue, processes it, then signals the job is complete
    - The user is not blocked and the job is processed in the background. During this time, the client might optionally do a small amount of processing to make it seem like the task has completed. For example, if posting a tweet, the tweet could be instantly posted to your timeline, but it could take some time before your tweet is actually delivered to all of your followers.
    - Eg: Redis is useful as a simple message broker but messages can be lost. RabbitMQ is popular but requires you to adapt to the 'AMQP' protocol and manage your own nodes. Amazon SQS is hosted but can have high latency and has the possibility of messages being delivered twice.
  - Tasks queues receive tasks and their related data, runs them, then delivers their results. They can support scheduling and can be used to run computationally-intensive jobs in the background. Celery has support for scheduling and primarily has python support.
  - Back pressure: If queues start to grow significantly, the queue size can become larger than memory, resulting in cache misses, disk reads, and even slower performance. Back pressure can help by limiting the queue size, thereby maintaining a high throughput rate and good response times for jobs already in the queue. Once the queue fills up, clients get a server busy or HTTP 503 status code to try again later. Clients can retry the request at a later time, perhaps with exponential backoff.


#### [surajv311/myCS-NOTES _al](https://github.com/Surajv311/myCS-NOTES)

- [Horizontal vs Vertical scaling _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/SYSTEM_DESIGN/sd%20(1).jpg) 
- [2 phase vs 3 phase commit _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/SYSTEM_DESIGN/sd%20(10).jpg) 
- [Pub-Sub model _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/SYSTEM_DESIGN/sd%20(11).jpg) 
- [Cascading failure in Distributed Systems, CDN _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/SYSTEM_DESIGN/sd%20(13).jpg) 
- [Forward Proxy, Reverse Proxy _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/SYSTEM_DESIGN/sd%20(16).jpg) 
- [Service Mesh _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/SYSTEM_DESIGN/sd%20(17).jpg) 
- [How DNS works? _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/SYSTEM_DESIGN/sd%20(19).jpg) 
- [Consistent hashing _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/SYSTEM_DESIGN/sd%20(2).jpg) 
- [L4 and L7 load balancing _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/SYSTEM_DESIGN/sd%20(20).jpg) 
- [System Design Algos _al](https://github.com/Surajv311/myCS-NOTES/blob/main/CS_CORE-NOTES/SYSTEM_DESIGN/sd%20(22).jpg) 

- Paxos is an algorithm that enables a distributed set of computers (for example, a cluster of distributed database nodes) to achieve consensus over an asynchronous network.
- A split brain situation occurs when a distributed system, such as Elasticsearch, loses communication between its nodes. This can happen for a variety of reasons, such as network issues, hardware failures, or software bugs.
- Cross-origin resource sharing (CORS) is a mechanism for integrating applications. CORS defines a way for client web applications that are loaded in one domain to interact with resources in a different domain.
- A Bloom filter is a space-efficient probabilistic data structure that is used to test whether an element is a member of a set.
- Forward Proxy (Proxies on behalf of clients), Reverse Proxy(Proxies on behalf of servers)
- Service Mesh: In short, it manages communication between microservices. 
- A canary deployment is a progressive rollout of an application that splits traffic between an already-deployed version and a new version, rolling it out to a subset of users before rolling out fully.
- NAT stands for network address translation. It's a way to map multiple private addresses inside a local network to a public IP address before transferring the information onto the internet. Organizations that want multiple devices to employ a single IP address use NAT, as do most home routers.
- A port number is a way to identify a specific process to which an internet or other network message is to be forwarded when it arrives at a server.
- Message/Task queue, Monoliths, Microservices, ACID-BASE, Cache, Sharding, Architectures, etc. also covered in the repo. 

------------------

### Info_Miscellaneous

- **Deduplication** refers to a method of eliminating a dataset's redundant data.
- A **race condition** is an undesirable situation that occurs when a device or system attempts to perform two or more operations at the same time, but because of the nature of the device or system, the operations must be done in the proper sequence to be done correctly.
- **Persistence** denotes a process or an object that continues to exist even after its parent process or object ceases, or the system that runs it is turned off. When a created process needs persistence, non-volatile storage, a hard disk is used instead of volatile memory like RAM.
- **Medallion Architecture** is a data design pattern used to logically organize data in a lakehouse, with the goal of incrementally and progressively improving the structure and quality of data as it flows through each layer of the architecture (from Bronze ⇒ Silver ⇒ Gold layer tables). Medallion architectures are sometimes also referred to as "multi-hop" architectures. [Medallion Architecture _al](https://www.databricks.com/glossary/medallion-architecture)
- A **namespace** is a declarative region that provides a scope to the identifiers (the names of types, functions, variables, etc) inside it.
- [To setup env variables in a jupyternotebook _al](https://ipython.readthedocs.io/en/stable/interactive/magics.html#magic-env): `%env var=val`
-  ['b' character do in front of a string literal _al](https://stackoverflow.com/questions/6269765/what-does-the-b-character-do-in-front-of-a-string-literal): A sequence of bytes. A “byte” is the smallest integer type addressable on a computer, which is nearly universally an octet, or 8-bit unit, thus allowing numbers between 0 and 255.
- The only thing that happens when you run touch on an already existing file is that the file's access and modification timestamps are updated to the current time. Its contents are not lost or modified.
- Setting the shell argument in the `subprocess` library to a true value causes subprocess to spawn an intermediate shell process, and tell it to run the command. In other words, using an intermediate shell means that variables, glob patterns, and other special shell features in the command string are processed before the command is run. Executing shell commands that incorporate unsanitized input from an untrusted source makes a program vulnerable to shell injection, a serious security flaw which can result in arbitrary command execution. For this reason, the use of shell=True is strongly discouraged in cases where the command string is constructed from external input. Hence: 

```
Case 1: 
db_config_create_command = f'touch {file_path}'
result_file_created = subprocess.run(db_config_create_command, shell=True, capture_output=True, text=True) -- Not advisable 

Case 2: 
db_config_create_command = ['touch', f'{file_path}']
subprocess.run(db_config_create_command, shell=False) -- Fine 
```
- Pip python package manager: 
  - `!pip install -r requirements.txt --use-deprecated=legacy-resolver` - For pip dependency issue resolving. 
  - `pip list`: pip list shows all the installed packages.
  - `pip freeze`: pip freeze shows packages installed via pip (or pipenv if using that tool) command in a requirements format.
- Semantic versioning (also known as SemVer) is a versioning system that has been on the rise over the last few years. SemVer is in the form of MajorVersion.MinorVersion.PatchVersion; Eg: 4.7.6. [Semantic version doc _al](https://semver.org/)
- In this code:

```
Code: execution_date = datetime.combine(execution_date.date(), datetime.min.time()) + timedelta(hours=18).
The provided code performs the following actions below:

execution_date.date(): It extracts the date component from the execution_date variable, effectively removing the time component and leaving you with just the date.
datetime.min.time(): This creates a new datetime object with the minimum possible time (00:00:00).
datetime.combine(date, time): This combines the date obtained in step 1 with the time obtained in step 2. Essentially, it sets the time component of the execution_date to 00:00:00, effectively resetting the time to midnight.
timedelta(hours=18): It adds a time delta of 18 hours to the resulting datetime object. This effectively sets the time to 18:00:00 (6:00 PM) on the same date.

So, the overall effect of the code is to take an input execution_date, strip off the time component, and set the time to exactly 6:00 PM (18:00:00) on the same date. The resulting datetime object represents 6:00 PM on the same day as the input execution_date.
```

- The way jupyter kernel works: The main benefit for most users of using the kernel is this workflow that comes from the decoupling model. You can continue to write and execute code while other code is executing. The Jupyter kernel architecture consists of several components that work together to execute code, manage the execution environment, and communicate with the frontend. 
  - The kernel process is a standalone process that runs in the background and executes the code that you write in your notebooks. The kernel process is responsible for running the code and returning the results to the frontend.
  - The kernel manager is a component that manages the lifecycle of the kernel process. It is responsible for starting, stopping, and restarting the kernel process as needed.
  - The kernel gateway is a web server that exposes the kernel's functionality over HTTP. The kernel gateway is used to connect the kernel to the frontend (i.e., the web-based interface that you use to interact with the notebook) over a network connection.
  - The communication between the frontend and the kernel is done using WebSockets and ZeroMQ.

- pip installable parquet-tools - with this package you can view parquet file content/schema on local disk.
- Parquet is a columnar storage format, Avro is row-based. [parquet vs avro _vl](https://www.youtube.com/watch?v=QEjDiIyjFGs), [parquet format pros cons _al](https://stackoverflow.com/questions/36822224/what-are-the-pros-and-cons-of-the-apache-parquet-format-compared-to-other-format)
- API pagination refers to a technique used in API design and development to retrieve large data sets in a structured and manageable manner. When an API endpoint returns a large amount of data, pagination allows the data to be divided into smaller, more manageable chunks or pages. Pagination methods: Offset Pagination, Keyset Pagination, Seek Pagination
- Swagger io is a good option to send API contracts to foreign/ other teams: https://swagger.io/ 
- To print response time of hitting an API in requests library python: 

```
response = requests.post(url, data=post_fields, timeout=timeout)
print(response.elapsed.total_seconds())
```

- Unix time is a date and time representation widely used in computing. It measures time by the number of non-leap seconds that have elapsed since 00:00:00 UTC on 1 January 1970, the Unix epoch. [Convert date to epoch python _al](https://stackoverflow.com/questions/75158409/how-to-convert-a-date-to-unix-epoch-time-in-python)
- [Why is processing a sorted array faster than processing an unsorted array _al](https://stackoverflow.com/questions/11227809/why-is-processing-a-sorted-array-faster-than-processing-an-unsorted-array): It involves concept of Branch prediction. Branch prediction attempts to guess whether a conditional jump will be taken or not. Branch target prediction attempts to guess the target of a taken conditional or unconditional jump before it is computed by decoding and executing the instruction itself. It is a technique to predict the outcome of a conditional operation.
- Multhread crawler in python using [bs4 - beautiful soup package _al](https://www.geeksforgeeks.org/multithreaded-crawler-in-python/). 
- What is P99 latency?: It's 99th percentile. It means that 99% of the requests should be faster than given latency. In other words only 1% of the requests are allowed to be slower. 
- Time-to-live (TTL) is a value for the period of time that a packet, or data, should exist on a computer or network before being discarded.
- Lazy loading is the practice of delaying load or initialization of resources or objects until they’re actually needed to improve performance and save system resources. For example, if a web page has an image that the user has to scroll down to see, you can display a placeholder and lazy load the full image only when the user arrives to its location -  with this you can reduce load time, conserve resources, etc. 
- TOAST in postgres: TOAST (The Oversized-Attribute Storage Technique) is a mechanism in Postgres which stores large column values in multiple physical rows, circumventing the page size limit of 8 KB.
- DRY Principal in programming: Do not repeat yourself 
- [Opensearch shard indexing backpressure](https://opensearch.org/blog/shard-indexing-backpressure-in-opensearch)
- Event reactor pattern: The reactor software design pattern is an event handling strategy that can respond to many potential service requests concurrently. The pattern's key component is an event loop, running in a single thread or process, which demultiplexes incoming requests and dispatches them to the correct request handler.
- [Aqua trivy _al](https://github.com/aquasecurity/trivy) is a useful tool to find vulnerabilities.
- [Pydantic validators _al](https://www.apptension.com/blog-posts/pydantic)
- A language is:
  - **statically typed** if the type of a variable is known at compile time, eg: int a = 5. For some languages this means that you as the programmer must specify what type each variable is; other languages (e.g.: Java, C, C++) offer some form of type inference, the capability of the type system to deduce the type of a variable (e.g.: OCaml, Haskell, Scala, Kotlin). Examples: C, C++, Java, Rust, Go, Scala
  - **dynamically typed** if the type is associated with run-time values, and not named variables/fields/etc. This means that you as a programmer can write a little quicker because you do not have to specify types every time (unless using a statically-typed language with type inference). Examples: Perl, Ruby, Python, PHP, JavaScript, Erlang
- Declarative vs Imperative programming: 
  - Declarative: You set the conditions that trigger the program execution to produce the desired results.

```
Eg: Declarative

mylist = [1,2,3,4,5]
total = sum(mylist)
print(total) 
```

  - Imperative: You describe the step-by-step instructions for how an executed program achieves the desired results.

```
Eg: Imperative

total = 0 
myList = [1,2,3,4,5]
for x in myList:
     total += x
print(total)
```

- TIL that if a function has a lot of arguments it takes a small hit on the call because the stack is used for the arguments instead of CPU registers. Depending on the OS (specifically 64 bit for some reason) anything > 4 goes into the stack. else it goes into the R registers.
- You know I used to think that 99.99% CPU at times or 98% RAM indicate bottlenecks and starved processes but that is not always the case. Your might have a multi-threaded or multi-process backend app that use 98% CPU of all cores at times but all processes are served equally and without any blocking or minimum blocking. You simply crafted the number of processes or threads in your CPU-bound backend workload so it runs efficient, which is what you want. So CPU usage alone isn’t enough to indicate pressure or stalling or blocking. I don’t know about Windows but in Linux, The psi (pressure stall information) is a metric I recently learned that tells you whether “some” or “full” pressure is being experienced, that is processes are being stalled for CPU or RAM. This even applies to RAM, some relational and in-memory databases pre-allocates large memory even though they are not using it showing large RAM usage but it doesn’t indicate that you necessarily need more RAM. SQL Server and memcachd comes to mind. So just because your memory usage is 98% doesn’t mean you necessarily need more RAM.
- What is the Torn Page in SQL Server? It is the inability of the server to fetch a particular data during a transaction. It is caused when an Input/Output header tries to access a page that was written incorrectly to the disk. It reports a message saying 'I/O error (torn page) detected during read'.
- [Backend for frontend pattern _al](https://medium.com/mobilepeople/backend-for-frontend-pattern-why-you-need-to-know-it-46f94ce420b0): You need to think of the user-facing application as being two components — a client-side application living outside your perimeter and a server-side component (BFF) inside your perimeter. BFF is a variant of the API Gateway pattern, but it also provides an additional layer between microservices and each client type separately. Instead of a single point of entry, it introduces multiple gateways. Because of that, you can have a tailored API that targets the needs of each client (mobile, web, desktop, voice assistant, etc.), and remove a lot of the bloat caused by keeping it all in one place. 
- An API gateway manages incoming requests and routes them based on key factors such as request path, headers, and query parameters, among others. It allows for efficient distribution of traffic and ensures proper load balancing among target endpoints.
- [Improve API performance _vl](https://www.youtube.com/watch?v=zvWKqUiovAM): Caching, Connection pool, Avoid N+1 Query Problem, Pagination, JSON Serializers, Payload Compression, Asynchronous logging
- **Serialization** is the process of converting the state of an object into a form that can be persisted or transported. The complement of serialization is **deserialization**, which converts a stream into an object. Together, these processes allow data to be stored and transferred.
- [Stateful vs Stateless _al](https://www.redhat.com/en/topics/cloud-native-apps/stateful-vs-stateless): 
  - Stateful: Stateful applications and processes allow users to store, record, and return to already established information and processes over the internet. In stateful applications, the server keeps track of the state of each user session, and maintains information about the user's interactions and past requests. They can be returned to again and again, like online banking or email. They’re performed with the context of previous transactions and the current transaction may be affected by what happened during previous transactions. For these reasons, stateful apps use the same servers each time they process a request from a user. If a stateful transaction is interrupted, the context and history have been stored so you can more or less pick up where you left off. Stateful apps track things like window location, setting preferences, and recent activity. You can think of stateful transactions as an ongoing periodic conversation with the same person.
  - A stateless process or application, however, does not retain information about the user's previous interactions. There is no stored knowledge of or reference to past transactions. Each transaction is made as if from scratch for the first time. Stateless applications provide one service or function and use a content delivery network (CDN), web, or print servers to process these short-term requests. An example of a stateless transaction would be doing a search online to answer a question you’ve thought of. You type your question into a search engine and hit enter. If your transaction is interrupted or closed accidentally, you just start a new one. Think of stateless transactions as a vending machine: a single request and a response.
- Ephemeral storage, in the context of Kubernetes, is storage tied to the lifecycle of a pod, so when a pod finishes or is restarted, that storage is cleared out.
- A bastion host is a publicly facing server that acts as an entry-point to the system which is protected from the high-end firewall or located in a private server. These servers can only be accessible from the bastion hosts so this would reduce the attack surface area from the outside world. [Private server bastion host _al](https://towardsaws.com/ssh-into-the-private-server-through-bastion-host-f637aa5f5c17), [SSH Proxy bastion _al](https://www.redhat.com/sysadmin/ssh-proxy-bastion-proxyjump)
- Data Warehouses are used by managers, analysts, and other business end-users. Data Lake stores mostly raw unstructured and semi-structured data — telemetry, graphics, logs of user behavior, website metrics, and information systems, as well as other data with different storage formats. They are not yet suitable for daily analytics in BI systems but can be used by Data Scientists to test new business hypotheses using statistical algorithms and Machine Learning methods.

--------------------------------

