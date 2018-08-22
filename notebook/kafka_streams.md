# Kafka streams
java library
Deeply coupled to kafka
Declarative - don't need deep knowledge of network or producer consumer API

SERDE - serializer/deserrializer
* Gives you infinite stream of "strings" for instance

Aggregators transform streams into k-table (?)
 * (mutable table)
 * Still an infinite stream of values

 Donstream consumers realize they get updates to the k-table
* This is like getting a changelog stream from a relational database
* You ask for a value as it was at a given time (defaulting to now)
* But more changes might/will come along later

A change to the keys in a stream causes a repartition.  This is expensive because it involved network I/O to write the new key/value pairs to a topic and read them back out.

Streams handles divvying up work (paritions) into tasks and spreads them across threads.
