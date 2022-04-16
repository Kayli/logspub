# notes about distributed systems and related topics

## basics

- use docker and kubernetes to decompose and modularize applications



## abstraction for cloud infrastructure

- must have layer to decouple from specific vendors

- dapr (distributed application runtime) [^1]
  - unified wrapper for pubsub, rpc, configuration, instrumentation
  - can use redis for pubsub
    - can be run in 'append only file' mode with fsync at every query to provide stong guarantees


## references

[^1]: https://www.youtube.com/watch?v=-4sHUvfk2Eg
