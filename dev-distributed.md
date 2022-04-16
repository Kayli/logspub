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


## abstraction for cloud infrastructure

- must have layer to decouple from specific vendors

- dapr (distributed application runtime) [^1]
  - unified wrapper for pubsub, rpc, configuration, instrumentation
  - can use redis for pubsub
    - can be run in 'append only file' mode with fsync at every query to provide stong guarantees


## references

[^1]: https://www.youtube.com/watch?v=-4sHUvfk2Eg
[^2]: https://www.youtube.com/watch?v=STKCRSUsyP0 (martin fowler goto 2017)
