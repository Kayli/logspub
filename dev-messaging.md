# notes about messaging in distributed systems and related information [^1]

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


## enterprise integration patterns

- main patterns
  - file transfer
  - shared database
  - remote procedure invocation
  - messaging: applications communicate by sending messages via message channels

- other useful patterns
  - message channel: often called a queue
    - datatype channel: carries message only of a specific type
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
  - canonical data model: unified contract for messages
  - message translator: mapper
  - command message: ask receiver to perform some operation
  - event message: notifies receivers about some change in a system
  - document message: passes data from sender to receiver(s)
  - message endpoint
  - request-reply: useful when wrapping async system into a sync interface
  - message store


## references

[^1]: https://www.enterpriseintegrationpatterns.com
