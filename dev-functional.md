# notes on functional programming [^1]

- basics
  - pure function
    - one that has no side-effects
    - has referential transparency
      - always returns same result when called with same parameters
  - prefix function
    - usual named function that is placed before arguments
  - infix function
    - is like '+' or '*' operators that is placed between 
  

## haskell

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



## references

[^1]: https://github.com/hmemcpy/milewski-ctfp-pdf/ (category theory for programmers)
[^2]: https://stackoverflow.com/questions/9611904/haskell-lists-arrays-vectors-sequences
