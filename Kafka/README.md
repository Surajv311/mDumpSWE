
# Kafka

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

[Kafka configurations _al](https://medium.com/@madhur25/meaning-of-at-least-once-at-most-once-and-exactly-once-delivery-10e477fafe16)
- At-most once Configuration: At-most-once means the message will be delivered at-most once. Once delivered, there is no chance of delivering again. If the consumer is unable to handle the message due to some exception, the message is lost. This is because Kafka is automatically committing the last offset used.
- At-least once configuration: At-least once as the name suggests, message will be delivered atleast once. There is high chance that message will be delivered again as duplicate. Let’s say consumer has processed the messages and committed the messages to its local store, but consumer crashes and did not get a chance to commit offset to Kafka before it has crashed. When consumer restarts, Kafka would deliver messages from the last offset, resulting in duplicates.
  - Consumer should now then take control of the message offset commits to Kafka by making the consumer.commitSync() call.
- Exactly-once configuration: Exactly-once as the name suggests, there will be only one and once message delivery. It difficult to achieve in practice.
  - In this case offset needs to be manually managed.


----------------------------------------------------------------------





















