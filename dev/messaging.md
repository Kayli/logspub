# notes about messaging in distributed systems and related information [1]

## basics

- messaging benefits
  - remote communication via object serialization
  - platform/language integration
  - async communication 
  - buffer messages in case of overloaded receiver
  - reliable communication
  - disconnected operation
  - mediation role of messaging system
  - thread management: consumers often assigned dedicated threads


## schema

- defines constraints on the structure and content of data structures
- compatibility types
  - backward-compatible
    - consumers using new schema version are able to read previous version schema messages
  - forward compatible
    - consumers using previous schema version are able to read next version schema messages
  - full compatibility (backward + forward)
  - transitive
    - means that the new schema is checked against all previous schema versions
    - non-transitive means that the new schema is checked against the last schema version only

- schema registry
  - component that helps with schema verification before publishing message to a pipe
  - implementations
    - confluence schema registry
    - hive metastore
    - karapace from aiven
    - apicurio from ibm
  
- standards
  - json schema (.schema.json)
  - xml schema (.xsd)
  - protobuf (.proto)
    - RPC and serialization framework
  - apache thrift (.thrift)
    - RPC and serialization framework
    - is statically typed
      - implies a benefit from the better performance of generated code
  - apache avro (.avsc)
    - supports dynamic typing
  - parquet?
  - orc (optimized row columnar)


## enterprise integration patterns

- integration styles
  - file transfer
  - shared database
  - remote procedure invocation
  - messaging: applications communicate by sending messages via message channels

- other useful patterns
  - message
    - command message: ask receiver to perform some operation
    - event message: notifies receivers about some change in a system
    - document message: passes data from sender to receiver(s)
  
  - message channel: often called a queue
    - datatype channel: carries message only of a specific type
    - point-to-point channel (queue): exactly one receiver will receive a message
    - publish-subscribe channel (topic): broadcasting an event to all interested receivers
    - dead letter queue and poison pill/message
  
  - endpoints
    - channel adapter: connect message channel and application without modifying its code
    - message endpoint: connect message channel and application by modifying its code
    - message receiver
      - polling consumer
      - event-driven consumer
      - competing consumers: parallel multithreaded consumption of messages
        - competing transactional clients: risk of waste due to rollbacks
      - message dispatcher: implements custom parallel consumption logic
      - selective consumer
      - durable subscriber: ensures messages not lost while endpoint is disconnected
      - idempotent receiver: correctly handles duplicate messages
  
  - conversation
    - request-reply: useful when wrapping async system into a sync interface
    - scatter-gather

  - canonical data model: unified contract for messages
  - message bus: canonical data model + messaging infrastructure
  
  - message translator: mapper

  - message store

  - routing
    - splitter
    - aggregator
    - message filter
    - ordering
      - message group [2]
        - local message order: order is preserved within a group of messages
        - global message order: order is preserved for all messages in a channel
      - resequencer: sorts out of order messages 


## kafka

- typical components
  - broker
    - expose producer and consumer apis
    - kafka 'broker', 'server', 'node', 'storage node' all refer to the same concept and are synonyms
  - producer: publishes events
  - consumer: subscribes and consumes events

- can preserve immutable log of events
  - retention time can be configured based on number, size or ttl of objects

- topic: named container for similar events

- partitioning
  - messages without a key will be distributed to nodes in a round-robin manner
  - asigning a key makes messages with the same key to end up on same partition
  - whenever a topic is created, the partitions are divided among the cluster nodes
    - each partition has a leader node and replica nodes (see replication factor)
    - producers write to the leader node and kafka internally replicates the data on the replica nodes
    - consumers consume data of a partition from its leader node

- kafka connect
  - provides ecosystem of pluggable connectors
  - kafka connectors
    - source connector acts as a producer
    - sink connector acts as a consumer
    - declarative approach, no need to write boilerplate code
    - allows to transfer data from source connector to sink
    - runs in client process, is not a part of a broker
    - allows to define smts - single message transformers
  - you can have a cluster of connect workers moving data around

- kafka streams
  - is a complete stream-processing system
  - define processor topology dag
    - source processor
    - stream processors
    - sink processor
  - Serdes (сёрдей) 
    - is an object encapsulating serializer/deserializer logic
    - existing serializers for primitive types as well as for avro, protobuf, json
  - KStream is a stream in which every element represents a separate event
  - KTable
    - is an update stream in which elements can represent a new event or an update to the existing one
    - shardes the data between all running Kafka Streams instances
  - GlobalKTable
    - similar to KTable
    - has a full copy of all data on each instance
  - support for joins, time windows, stream time (opposed to wall-clock time), unit testing

- fault tolerant cluster
  - powered by apache zookeeper
  - in newer versions zookeeper will be swapped by quorum controller
    - this allows cluster to be composed only of kafka nodes

- exactly once delivery semantics [3] [4]
  - the producer send operation is now idempotent (set “enable.idempotence=true”)
  - atomic writes across multiple partitions through the new transactions api
    - this helps when publishing a message into multiple topic which are hosted on different cluster nodes

- consumer lag
  - is an indicator of how much lag there is between kafka producers and consumers
  - indicates how far behind is your consumer compared to the latest produced message in the topic the consumer is reading from

- cloud products
  - azure hdinsight kafka (managed native kafka service in azure)
  - azure event hub (supports kafka api)
  - amazon managed streaming for apache kafka (msk)


## terminology

- dag: directed acyclic graph


## references

[1]: https://www.enterpriseintegrationpatterns.com
[2]: https://youtu.be/QhfuzEkN3Ck?t=1806
[3]: https://kafka.apache.org/documentation/#semantics
[4]: https://www.confluent.io/blog/enabling-exactly-once-kafka-streams/