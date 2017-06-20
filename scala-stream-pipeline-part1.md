# Creating Scala Streaming Pipeline
 
## 1 Apache Kafka
[Official Documentation](https://kafka.apache.org){:target="_blank"}

Apache Kafka is a distributed streaming platform, or at least is how the documentation defines it.
So, basically allows you to publish and subscribe to a stream of events (or hwo they call them, records)
categorised in topics.

### 1.1 Some definitions

1. **Record** each one of the entries registered in this streams, this ones are composed by an *key*, *timestamp* and the value.
1. **Topic** this is the category where a specific type of records get stream into. The topics are distributed in
different partitions of ordered, immutable squence of records that are constantly appended, and that are remove only after a
configured period of time. The records within a partition get a sequential id call offset.
Thanks to this we can have multiple clients for this data, and is the client that needs to control the offset that it is consuming.
1. **Producer** Needs to decide in which partition for the given topic needs to publish the message.
1. **Consumer** This ones are identified with a consumer name group, this is to allow to decide if multiple consumers are
sharing the same offset, or instead (when different group) they consume the same messages as the other group... So, we can
either parallelised the consumption of the stream or simply do different things consuming the same topic at a different rate.


### 1.2 Some exciting numbers

2 Million Writes Per Second (On Three Cheap Machines)
https://engineering.linkedin.com/kafka/benchmarking-apache-kafka-2-million-writes-second-three-cheap-machines


### 1.3 Kafka Guarantees

1. Recrods in a topic's partition will be appended on the same order they are sent, they will keep the offset in order
and so, they will be log on the same order. This is great where compared with some Messaging Queue System that do not
warrant the order. This makes Kafka a great candidate to keep in sync data between different services, and one of the
reason that has been quite popular during the adoption of microservices.
1. Consumers are guaranteed to consume the messages on the same order as they are log
1. Finally, given a replication factor of N it guarantees that can tolerate N-1 server failures.
