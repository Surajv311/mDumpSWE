
# Airflow

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


----------------------------------------------------------------------





















