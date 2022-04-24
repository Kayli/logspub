# notes related to pony programming language

## basics [^1]

- type-safe
- object-oriented
- inspired by: erlang, elixir, akka, haskell, scala, python
- compiled ahead of time using LLVM
- exception safe: they are always handled
- trait system (similar to Java 8 interfaces that can have default implementations)
- interface system (similar to Go interfaces, i.e. structurally typed)

## common types

- Bool, U64, I64, F64, String


## type conversions

- concrete types provide methods named similarly to target type for conversion
  - F32(1.0).f64()


## encapsulation

- leading underscore in name defines
  - private variable
  - private function
    - definition of 'private' for functions corresponds to something like 'internal' in csharp,
      meaning that they are scoped by package


## safety

- reference capabilities (rcaps)
  - rcap is a modifier which constraints usage of variables, objects and their members
  - used for dealing with hard concurrency problems, as its the main area for which pony has been designed
  - placing rcap in front of the function requres object on which this method has been called to be of that type

- rcap types
  - box 
    - default receiver reference capability if none is specified
    - means “i need to be able to read from this, but i won’t write to it”
    - for a class function, makes it pure? so the following won't compile:
      > fun ref set_hunger(to: U64 = 0): U64 => _hunger_level = to
  - ref
    - reference type, meaning that the object is mutable
    - for a class function, relaxes access to class members
      > fun ref set_hunger(to: U64 = 0): U64 => _hunger_level = to


- comes with safety math proof
  - but what does it practically mean? most likely that some math person looked at math
    model and approved it. so, whats been approved is not even an implementation of that model
  - also keep in mind that all implementations are buggy, its just a matter of probabilities
  - so, at very least, there is some mathematical rigor associated with language design i guess


## concurrency

- pony is actor-based
  - is like a class with specifics
  - can have behaviours, which are async functions
  - single message queue
  - back pressure problem
    - automatically deprioritises actors that send messages to "loaded queues"
  - has its own heap


## problems

- minor
  - there is no repl as of april 24, 2022


## terms

- foreign function interface (ffi)
  - api for intergation with other ?native? languages


## references

[^1]: https://tutorial.ponylang.io
