# notes related to pony programming language

## basics [^1]

- type-safe
- object-oriented
- compiled ahead of time using LLVM
- exception safe: they are always handled
- inspired by: erlang, elixir, akka, haskell, scala, python


## common types

- String, U64


## encapsulation

- leading underscore in name defines
  - private variable
  - private function
    - definition of 'private' for functions corresponds to something like 'internal' in csharp,
      meaning that they are scoped by package


## concurrency

- pony is actor-based
  - is like a class with specifics
  - can have behaviours, which are async functions
  - single message queue
  - back pressure problem
    - automatically deprioritises actors that send messages to "loaded queues"
  - has its own heap

- dealing with hard concurrency problems is the main area for which Pony has been designed
  - reference capabilities (rcaps)


## safety

- comes with safety math proof
  - but what does it practically mean? most likely that some math person looked at math
    model and approved it. so, whats been approved is not even an implementation of that model
  - also keep in mind that all implementations are buggy, its just a matter of probabilities
  - so, at very least, there is some mathematical rigor associated with language design i guess

## terms

- foreign function interface (ffi)
  - api for intergation with other ?native? languages


## references

[^1]: https://tutorial.ponylang.io