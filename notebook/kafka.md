Kafka
-----

Distributed log
  log as DB

  "Confluent" built on top of kafka -> more commercial offering

Real time event processing

One at a time

Message queue

### Terms

Producer/consumer/connector/stream processors

Consumers pull messages from the partitions

A topic is split into partitions (replication/availability)

In general working with kafka, the producer and consumer API need to be aware of partitions (if you care about ordered delivery)

broker is a node

Zookeeper consensus mechanism of the distributed system

### partitions
(num) partitions = num of parallel processes

The topic doesn't exist in any one place
The leader is the leader of a partition (not a topic)

partitions tend to be replicating, but it's purely for backup.  Like RAID,

Kafka does in order message delivery by partition

### Stream processors give guarantees on the producer/consumers
 - a stream consumer will keep state (what message I'm on) back as a kafka topic so it can be killed/replaced

Kafka Stream or Apache Storm


### You can build anything on top of kakfa
- db
- message queue
- stream processing
