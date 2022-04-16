# notes about distributed systems and related topics

## basics

- use docker and kubernetes to decompose and modularize applications


## patterns [^2]

- event notification
  - pubsub using events
  - notify system about state change in a decoupled manner
  - disadvantages: harder to track effects of a change

- event-carried state transfer
  - requirement for the event to contain all necessary information to reconstruct state after change
  - disadvantages: events may become heavy

- event sourcing
  - asynchrony complicates things, but it is not a reuquirement for es

- cqrs
  - commands and queries have different state representations
  - simplifies representation, increases performance
  - disadvantages: likely data duplication, eventual consistency


## antipatterns

- vague/meaningless terms
  - service-oriented architecture, event-driven architecture

- integration database

- using bleeding edge technological stack
  - very risky for big projects

- beware of bias and heuristics
  - evaluate tech/architectural decisions for each specific business case
    - unless you had exactly the same combo of context + task in the past with now known solution

## abstraction for cloud infrastructure

- must have layer to decouple from specific vendors

- dapr (distributed application runtime) [^1]
  - unified wrapper for typical cloud services
  - rpc, configuration, instrumentation
  - pubsub
    - can use redis for pubsub
      - run in 'append only file' mode with fsync at every query to provide stong guarantees
  - key-value store
    - use to store shared configuration


## references

[^1]: https://www.youtube.com/watch?v=-4sHUvfk2Eg
[^2]: https://www.youtube.com/watch?v=STKCRSUsyP0 (martin fowler goto 2017)
