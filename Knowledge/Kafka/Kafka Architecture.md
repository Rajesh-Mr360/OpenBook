There are several essential components that are necessary to create a robust Kafka architecture, such as **Kafka Cluster**, **Producers**, **Consumers**, **Brokers**, **Topics**, **Partitions**, and **Zookeeper**. We will dive into each of these components to gain a high-level understanding of how they work and how they interact with one another.

![600](CloudBook/Kafka/Images/kafka_architecture.png)

---
# Topic

A Kafka topic is a logical name or category to which records (messages) are published by producers and from which records are consumed by consumers. Kafka uses the concept of topics to organize related messages.

A topic is identified by its name. For example, we may have a topic called logs that may contain log messages from our application, and another topic called purchases that may contain purchase data from our application as it happens.

Kafka topics can contain any kind of message in any format, and the sequence of all these messages is called a data stream. Data in Kafka topics is deleted after one week by default (*also called the default message retention period*), and this value is configurable. This mechanism of deleting old data ensures a Kafka cluster does not run out of disk space by recycling topics over time.

*Kafka topics are immutable: once data is written to a partition, it cannot be changed.*

## Partitions

Topics are broken down into a number of partitions. A single topic may have more than one partition, it is common to see topics with 100 partitions. The number of partitions of a topic is specified at the time of topic creation. Partitions are numbered starting from `0` to `N-1`, where `N` is the number of partitions. The figure below shows a topic with three partitions, with messages being appended to the end of each one.

## Offset

The offset is an integer value that Kafka adds to each message as it is written into a partition. Each message in a given partition has a unique offset. Offset numbering for every partition starts at 0 and is incremented for each message sent to a specific Kafka partition. Even though we know that messages in Kafka topics are deleted over time (as seen above), the offsets are not re-used. They continually are incremented in a never-ending sequence.

---
# Producers

Applications that send data into topics are known as Kafka producers. Applications typically integrate a Kafka client library to write to Apache Kafka.

![600](CloudBook/Kafka/Images/Producers.png)

A Kafka producer sends messages to a topic, and messages are distributed to partitions according to a mechanism such as key hashing (more on it below).
For a message to be successfully written into a Kafka topic, a producer must specify a level of acknowledgment (acks). This subject will be introduced in depth in the topic replication section.


---
# Consumers

Once a topic has been created in Kafka and data has been placed in the topic, we can start to build applications that make use of this data stream. Applications that read data from Kafka topics are known as consumers. Consumer continuously polls the Kafka broker using the topic name for new messages. Once the polling loop notices a new message, the message is consumed by the consumer and processing is done on the retrieved message.

Consumers can read from one or more partitions at a time in Apache Kafka, and data is read in order within each partition as shown below.

![600](CloudBook/Kafka/Images/Consumers.png)

A consumer always reads data from a lower offset to a higher offset and cannot read data backwards (due to how Apache Kafka and clients are implemented).

If the consumer consumes data from more than one partition, the message order is not guaranteed across multiple partitions because they are consumed simultaneously, but the message read order is still guaranteed within each individual partition.

By default, Kafka consumers will only consume data that was produced after it first connected to Kafka. Which means that to read historical data in Kafka, one must specify it as an input to the command, as we will see in the practice section.

Kafka consumers are also known to implement a "pull model". This means that Kafka consumers must request data from Kafka brokers in order to get it (instead of having Kafka brokers continuously push data to consumers). This implementation was made so that consumers can control the speed at which the topics are being consumed.

## Consumer Group

Every consumer is always part of a consumer group. A consumer group represents a group of consumer instances that work together to consume messages from the specified topic(s). When a topic is created in Kafka, it can have one or more consumer groups associated with it. The consumer groups maintain the offset information for the partitions they consume.

![600](CloudBook/Kafka/Images/ConsumerGroup.png)

When messages are published to a topic, they are distributed across the partitions in a configurable manner. Each consumer within a consumer group is assigned one or more partitions to read from. Each partition is consumed by only one consumer within a consumer group at a time. This ensures that all messages within a partition are processed in the order they were received. To decide which consumer should read data first and from which partition, consumers within a group use _GroupCoordinator_ and _ConsumerCoordinator_, which assign a consumer to a partition, managed by Kafka Broker.

## Consumer Offset

Typically, Kafka consumers have 3 options to read the message from the partition:
1. From-beginning: Always reads data from the start of the partition.
2. Latest: Reads the messages produced after the consumer started.
3. Specific offset: Reads the messages using a specific offset value.

Consumer offset represents the position or offset within a partition from which a consumer group has consumed messages. In other words, each consumer group maintains its offset for each partition it consumes. The offset helps in determining the next message to read from a specified partition inside the topic. As soon as a consumer reads the message, Kafka automatically increments the offset value and commits the offsets, in a topic known as __consumer_offsets. This helps in case of machine failures. Consumer offsets behave like a bookmark for the consumer to start reading the messages from the point it left off.

---
# Message

Kafka messages are created by the producer. A Kafka message sent from Producer consist of following:

![400](CloudBook/Kafka/Images/Message.png)

- **Key :** Keys are used for grouping relating data. It is optional and can be Null. A key may be a string, number, or any object and then the key is serialized into binary format.
- **Value :** It contains the actual data we want to transmit. Kafka does not interpret the content of the value. It is received and sent as it is. It can be XML, JSON, String, or anything. Kafka does not care and stores everything.
- **Compression Type :** Kafka messages are generally small in size, and sent in a standard data format, such as JSON, Avro, or Protobuf. Additionally, we can further compress them into gzip, lz4, snappy or zstd formats. The compression type can be specified as part of the message. Options are `none`, `gzip`, `lz4`, `snappy`, and `zstd`
- **Headers :** There can be a list of optional Kafka message headers in the form of key-value pairs. It is common to add headers to specify metadata about the message, especially for tracing.
- **Offset/Partition :** Once a message is sent into a Kafka topic, it receives a partition number and an offset id. The combination of _topic+partition+offset_ uniquely identifies the message.
- **Timestamp :** A timestamp is added either by the user or the system in the message.

## Message Serializers

In many programming languages, the key and value are represented as objects, which greatly increases the code readability. However, Kafka brokers expect byte arrays as keys and values of messages. The process of transforming the producer's programmatic representation of the object to binary is **called message serialization**.

As shown below, we have a message with an `Integer` key and a `String` value. Since the key is an integer, we have to use an `IntegerSerializer` to convert it into a byte array. For the value, since it is a string, we must leverage a `StringSerializer`.

## Message De-serializers

_Serialization & Deserialization_
_Data being consumed must be deserialized in the same format it was serialized_ in.

As we have seen before, the data sent by the Kafka producers is [serialized](https://www.conduktor.io/kafka/kafka-producers/). This means that the data received by the Kafka consumers must be correctly deserialized in order to be useful within your application. Data being consumed must be deserialized in the same format it was serialized in. For example:
- If the producer serialized a `String` using `StringSerializer`, the consumer must deserialize it using `StringDeserializer`
- If the producer serialized an `Integer` using `IntegerSerializer`, the consumer must deserialize it using `IntegerDeserializer

## Message Keys

Each event message contains an optional key and a value.

In case the key (`key=null`) is not specified by the producer, messages are distributed evenly across partitions in a topic. This means messages are sent in a round-robin fashion (partition _p0_ then _p1_ then _p2_, etc... then back to _p0_ and so on...).

If a key is sent (`key != null`), then all messages that share the same key will always be sent and stored in the same Kafka partition. A key can be anything to identify a message - a string, numeric value, binary value, etc.

Kafka message keys are commonly used when there is a need for message ordering for all messages sharing the same field. For example, in the scenario of tracking trucks in a fleet, we want data from trucks to be in order at the individual truck level. In that case, we can choose the key to be `truck_id`. In the example shown below, the data from the truck with id _truck_id_123_ will always go to partition _p0._

![600](CloudBook/Kafka/Images/Message_keys.png)

---
# Cluster

A single Kafka Server instance is called a “**Kafka Broker**”. A Kafka Broker acts as a bridge between a producer and a consumer. Kafka brokers store data in a directory on the server disk they run on.

A group of brokers working together is called “**Kafka Cluster**”. Some clusters may contain just one broker, or others may contain three or potentially a hundred or thousands of brokers.  Companies like Netflix and Uber run hundreds or thousands of Kafka brokers to handle their data.

![600](CloudBook/Kafka/Images/Client.png)

A client that wants to send or receive messages through the Kafka cluster may connect to any broker in the cluster. Each broker in the cluster has metadata about all the other brokers, and therefore any broker in the cluster can act as a bootstrap server (the initial connection point used by Kafka clients to connect to the cluster).

The client connects to the provided broker (bootstrap server) and requests metadata about the Kafka cluster, such as the addresses of all the other brokers, the available topics, and the partition information. Once the client has obtained the metadata from the bootstrap server, it can establish connections to other brokers in the cluster as needed for producing or consuming messages.

---

## Message Replication in Kafka

When we send a message to a Kafka topic, it is stored in a partition. By default, each topic has only a single partition. However, each topic can have multiple partitions if configured. Suppose if we store the data in only one partition, and if the broker goes down then there might be a data loss problem. To avoid data loss issues, Kafka uses “_Replication_”.

In a distributed Kafka setup, a partition can be replicated across multiple brokers in the cluster to provide fault tolerance and high availability.

One broker is marked leader, and other brokers are called followers for a specific partition. This designated broker assumes the role of the leader for the topic partition. On the other hand, any additional broker that keeps track of the leader partition is called a follower and it stores replicated data for that partition.

Note that the leader receives and serves all incoming messages from producers and serves them to consumers. Followers do not serve read or write requests directly from producers or consumers. Followers just act as backups and can take over as the leader in case the current leader fails. Therefore, each partition has one leader and multiple followers.

## Replication Factor

While creating a topic, we provide a replication-factor value. *A replication factor of `1` means no replication*, mostly used for development purposes and should be avoided in test and production Kafka clusters. _A replication factor 3 is commonly used_ as it provides the right balance between broker loss and replication overhead.

## Insync Replica

When a partition is replicated across multiple brokers, not all replicas are necessarily in sync with the leader at all times. The in-sync replicas represent the number of replicas that are always up-to-date and synchronized with the partition’s leader. The leader continuously sends messages to the in-sync replicas, and they acknowledge the receipt of those messages.
*The recommended value for ISR is always greater than 1.*

## Message Acknowledgement in Kafka

Kafka producers only write data to the current leader broker for a partition.

Kafka producers must also specify a level of acknowledgment acks to specify if the message must be written to a minimum number of replicas before being considered a successful write.

When `acks=0` producers consider messages as "written successfully" the moment the message was sent without waiting for the broker to accept it at all. If the broker goes offline or an exception happens, we won’t know and will lose data. This is useful for data where it’s okay to potentially lose messages, such as metrics collection, and produces the highest throughput setting because the network overhead is minimized.

![600](CloudBook/Kafka/Images/Msg_Ack.png)

When `acks=1` , producers consider messages as "written successfully" when the message was acknowledged by only the leader. Leader response is requested, but replication is not a guarantee as it happens in the background. If an ack is not received, the producer may retry the request. If the leader broker goes offline unexpectedly but replicas haven’t replicated the data yet, we have a data loss.

When `acks=all`, producers consider messages as "written successfully" when the message is accepted by all in-sync replicas (ISR). The lead replica for a partition check to see if there are enough in-sync replicas for safely writing the message (controlled by the broker setting `min.insync.replicas`). The request will be stored in a buffer until the leader observes that the follower replicas replicated the message, at which point a successful acknowledgement is sent back to the client.

![600](CloudBook/Kafka/Images/Msg_ack2.png)

---

# Zookeeper

How do the Kafka brokers and clients keep track of all the Kafka brokers if there is more than one? The Kafka team decided to use Zookeeper for this purpose. Zookeeper is used for metadata management in the Kafka world. For example:

1. Zookeeper keeps track of which brokers are part of the Kafka cluster.
2. Zookeeper is used by Kafka brokers to determine which broker is the leader of a given partition and topic and perform leader elections.
3. Zookeeper stores configurations for topics and permissions.
4. Zookeeper sends notifications to Kafka in case of changes (e.g. new topic, broker dies, broker comes up, delete topics, etc.…)


## Why Zookeeper was removed ? 

Kafka scaling has hit a performance bottleneck with Zookeeper, which means Kafka has the following limitations with Zookeeper:
1. Kafka clusters only support a limited number of partitions (up to 200,000)
2. When a Kafka broker joins or leaves a cluster, a high number of leader election must happen which can overload Zookeeper and slow down the cluster temporarily.
3. Kafka clusters setup is difficult and depends on another component to setup.
4. Kafka cluster metadata is sometimes out-of-sync from Zookeeper.
5. Zookeeper security is lagging behind Kafka security.


---

### Commit Log

In Apache Kafka, the commit log is an append-only data structure that records all published messages in the order they were received. Each record in the log represents a single message, in the order they are produced, maintaining the message ordering within a partition. Let’s understand the commit log in Kafka using the diagram below.

When the message is produced, the record or log is saved as a file with the “.log” extension. Each partition within the Kafka topic has its own dedicated log file. Therefore, if there are six partitions for a topic, there will be six log files in the file system. These files are commonly referred to as _Partition Commit Logs_.

After the messages are written to the log file, the produced records are then committed. Consequently, only the records that have been committed to the file system are visible to consumers actively polling for new records.

Subsequently, as new records are published to the Kafka Topic, they are appended to the respective log file, and the process continues seamlessly, ensuring that messages are not lost in the event of failures.

Note that although the commit log is an append-only structure, Kafka provides efficient random access to specific offsets within a partition. Consumers can read messages from any offset in a partition, allowing them to replay or skip messages as needed.

### Retention Policy

The retention policy serves as the primary determinant of how long messages will be stored, making it a crucial policy to establish. By default, Kafka retains messages for a period of 168 hours, equivalent to 7 days. This default retention period can be adjusted as needed.

If the log retention period is exceeded, Kafka will automatically delete the corresponding data from the log. This process is controlled by the log.retention.check.interval.ms property, which specifies the interval at which retention checks occur (e.g., 300000 milliseconds).

Also, when the log size reaches a specified threshold, a new log segment is created (as shown in below diagram). The  log.segment.bytes  property determines the size of each log segment, with a default value of 1073741824 bytes (1 gigabyte).

![600](CloudBook/Kafka/Images/Retention_pcy.png)

---

## What if a Kafka broker goes down?

Now an obvious question arises, what if one of our brokers dies? Or what if we have to bring one broker down for maintenance? what happens to the partition of that broker? In the above image, Broker 1001 is the leader of partitions 4 and 1, what if broker 1001 dies? what would happen to these partitions? As we lost broker 1001, it is removed from ISR after 10 seconds if not configured, and Broker 1002, and 1003 still have a copy of data, and can still serve the data. Leader election will happen for partitions 1 and 4. Now partition 1 has broker 1003 and partition 4 has broker 1002 as leaders as they were In Sync with the partition leader earlier. If broker 1001 comes back to life, it will try to become a leader again after replicating the data. This is handled by Kafka itself, there is no manual intervention required. In case of any unforeseen events like hardware failure or for maintenance purposes, if we want to bring the broker down, it is recommended to have at least two brokers in the ISR (the leader + a replica) so no loss of data is guaranteed by Kafka.

I hope this explanation empowers you to explore Kafka! Happy learning! 😊
