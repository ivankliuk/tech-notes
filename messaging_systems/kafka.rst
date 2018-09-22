Kafka
=====

Apache Kafka is a high-throughput distributed messaging system. (vs RabbitMQ???)
Can be rethought as a distributed commit log.
https://data-flair.training/blogs/kafka-vs-rabbitmq/
https://www.quora.com/What-are-the-differences-between-Apache-Kafka-and-RabbitMQ
https://content.pivotal.io/blog/understanding-when-to-use-rabbitmq-or-apache-kafka

Kafka uses `Apache Zookeeper <https://zookeeper.apache.org/>` to manage its
nodes.

Messaging goals:

- High throughput (terabytes data and more)
- Horizontal scalability
- Reliability and durability
- Loosely coupled producers and consumers

**Terminology**

*Producer/Consumer* (same as publisher/subscriber) are used to publish and
receive messages to a topic respectively.

*Topic* is a central Kafka abstraction. It's a feed or category of messages.

*Broker* (a server per se) receives messages, stores them and send them to the
consumers.

*Cluster* is a grouping of multiple brokers.

*Message* consists of timestamp, identifier and binary payload.

*Offset* allows consumers read messages in own pace and process them
independently. It's like a bookmark and corresponds to the last read message
identifier.

*Message retention policy* is the time to keep messages in the topic regardless
of consumption. It's configurable per topic and default value is 7 days.

*Partition* is a physical representation of a topic as a commit log stored on
one or more brokers. Each partition must fit entirely on a single machine.

*Replication factor* is configured at topic level.