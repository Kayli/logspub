# notes related to software development

## source control

- git
  - foss, written in shell + c
  - recursively git latest version
    > git submodule update --recursive --remote

- mercurial
  - foss, written in python
  - repository https://www.mercurial-scm.org/repo/hg/


## modelling languages and tools

- universal modelling language
- mermaid https://mermaid.live/
  - declarative uml diagrams, similar to websequencediagrams
  - supports: flow charts, sequence diagrams, class diagrams, erd diagrams


## programming languages

- pony
  - type-safe
    - with safety math proof, but what it practically means? 
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


- classic functional programming [^1]
  - basics
    - lambda calculus is one of the origins of functional programming
    - pure function
      - one that has no side-effects
      - has referential transparency
        - always returns same result when called with same parameters
    - prefix function
      - usual named function that is placed before arguments
    - infix function
      - is like '+' or '*' operators that is placed between 
  - haskell
    - evaluation of statements is lazy by default
    - function call
      - example: myfuncname p1 p2 p3
      - you can call prefix functions as infix, by putting backticks around their names
        - usually you write: div 5 10
        - but using infix notation you can write: 5 `div` 10
    - Int and Integer are different types
      - Int is int64 and Integer is a dynamic range integer
    - type class
      - is a constraint (or interface) for types
      - defines operations allowed on variables of this type
    - sequential data [^2]
      - lists
        - standard way to represent sequences
        - implemented as singly-linked list under the hood
        - ϴ(n) to append or access elements by index
      - Data.Sequence 
        - based on finger trees
        - ϴ(log n) access to the middle of the sequence and inserting new values
      - Data.Vector
        - something like std::vector in C++
        - ϴ(log n) access elements by index
    - important topics
      - type classes
      - functors
      - applicative functors
      - monoids
      - monades
    - questions
      - purity and halting problem: are they even connected?
        - look up termination analysis articles
    - problems: oop paradigms are not supported and fanboys will never admit this is a problem


## verified compilers

- CompCert 
  - C verified compiler, 
  - provides high-assurance for almost all of the C language (ISO C 2011)
  - generates efficient code for the PowerPC, ARM, RISC-V and x86 processors


## mobile

- microsoft maui
  - dotnet multiplatform app user interface
  - cross-platform, native ui
  - platforms: windows, mac, ios, android


## references

[^1]: https://github.com/hmemcpy/milewski-ctfp-pdf/ (category theory for programmers)
[^2]: https://stackoverflow.com/questions/9611904/haskell-lists-arrays-vectors-sequences
