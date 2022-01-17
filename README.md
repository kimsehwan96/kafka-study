# Apache Kafka에 대해서 공부해보자.

## Apache Kafka?

- Data in Motion Platfrom
- Event Streaming Platform

### Event
 Event means everything and data that happens in the business

- click something in the website
- remit
- locational information of the delivery item
- measured industrial values like termostat / pressure / position / feedback / velocity

Event has big data characteristic
- It happens in the every parts of business
- It is literally big 

### other messagin platform

1. AWS SQS (Simple Queue Service)
- Managed Service (It means that we can't use it in on-premise enviroment) 
- Easy to use, Reliable
- Autoscaling (Manged service)

2. Kafka
- Distributed System
- Pub-Sub messaging system
- High-throughput

3. Rabbit MQ
- Message broker
- User friendly
- portable

### Why Kafka?
It's difficult to process large data streaming for exisiting services(MQ) because of its lack of perfomance

### Apache Kafka Feature

1. Transmit event streams stably
2. Write event streams to disk (Persistance)
3. Processing, Analysis event streams (ML, Data Pipeline)

### Where Kafka used

- Messaging System
- IoT (Collect Data from IoT Devices)
- Application Logging
- Realtime Event Stream Processing (Fraud Detection)
- DB Sync (MSA)
- Realtime ETL
- Used wtih Spark, Hadoop, Flink ...

### Quick start

```console
wget https://dlcdn.apache.org/kafka/3.0.0/kafka_2.13-3.0.0.tgz
tar -xzf kafka_2.13-3.0.0.tgz
cd kafka_2.13-3.0.0

# start zookeeper, Soon, zookeeper will no longer be required
bin/zookeeper-server-start.sh config/zookeeper.properties

# start kafka broker service
bin/kafka-server-start.sh config/server.properties
```

## Topic, Partition, Segment

### Topic

Topic is where message save in kafka. (Logical expression)

### Producer

Application that produces message and send to kafka's `topic`.

### Consumer

Application that get message from `topic` for cosumes it.

### Consmer Group

Set of `ConsumerS` that cooperate for consuming message from `topic`

A `Consumer` is in a `Consumer Group`, Consumers in `Consumer Group` are cooperating to process `topic`'s message as distributed and parallel

## Decoupling of Producer and Comsumer

Producer and Consumer don't know each other. Producer and Consumer write and read commit log in its own interval.

`Consumers` belong to different `Consumer Group` have no relationship with each other and they can read commit log which is in other offset.

## Kafka Commit Log

Datastructure that can only append, not change.

Commit Log : Event always append to end of log and it is imutable.

Offset: Position of `Event` in commit log

## Topic Partition, Segment

Partition : Commit Log. A Topic consists of at least one partition. Use multiple partition to improve throughput in distributed paralle system.
