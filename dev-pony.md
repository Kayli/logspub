# notes related to pony programming language

- type-safe
    - with safety math proof, but what it practically means?
      - most likely that some math person looked at math model and approved it
      - so, whats been approved is not even an implementation of that model
  - object-oriented
  - compiled ahead of time using LLVM
  - actor
    - is like a class with specifics
    - can have behaviours, which are async functions
    - single message queue
    - back pressure problem
      - automatically deprioritise actors that send messages to "loaded queues"
    - has its own heap
  - exception safe
    - exceptions are always handled
  - dealing with hard concurrency problems is the main area for which Pony has been designed
  - reference capabilities (rcaps)
  - inspired by: erlang, elixir, akka, haskell, scala, python



Foreign Function Interface (FFI)
