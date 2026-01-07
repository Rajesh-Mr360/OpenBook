Apache Kafka is a distributed event streaming platform designed to handle large volumes of real-time data. It works on the principle of Publish – Subscribe pattern, so instead of publishing records directly to the consumer, producers publish the data to the Kafka topics and Consumers subscribe to those topics to receive and process the data. 

It was originally created by LinkedIn and later open-sourced as Apache software foundation project.

![600](CloudBook/Kafka/Images/Kafka_HLI.png)
## Advantages

- **Scalability:** Kafka can handle high volumes of data, allowing you to scale horizontally by adding more brokers. This scalability ensures that as data demands increase, Kafka can adapt without significant reconfiguration.
- **High Throughput:** Kafka is designed for high-speed data transmission, enabling it to process millions of messages per second. This makes it ideal for applications needing real-time data processing and analysis.
- **Fault Tolerance:** With data replication across multiple brokers, Kafka ensures durability and availability. If one broker fails, another can take over without data loss, enhancing system reliability.

## Series:

1. [[Kafka Architecture]]
