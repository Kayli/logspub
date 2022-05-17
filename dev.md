# notes related to software development

## basics

- structured programming
  - forbids arbitrary jumps in code
  - defines which points in code are legitimate to jump to
    - nowadays these structures are called methods, functions, switch statements, loops, etc.


## modelling languages and tools

- universal modelling language
- mermaid https://mermaid.live/
  - declarative uml diagrams, similar to websequencediagrams
  - supports: flow charts, sequence diagrams, class diagrams, erd diagrams
  - vscode plugin


## parser generators/combinators

- grammar standards
  - ebnf (w3c grammar notation, extended backus–naur form)

- antlr
  - industry standard tool to generate parsers
  - antlr is its own grammar standard
  - supports many languages for generated parsers

- parsec
  - parser combinator in python
  - source code https://github.com/sighingnow/parsec.py/blob/master/src/parsec/__init__.py
  - some examples https://github.com/sighingnow/parsec.py/tree/master/examples


## programming languages

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
    - problems: oop paradigms are not supported and fanboys will never admit this is an issue


      

## verified compilers

- CompCert 
  - C verified compiler, 
  - provides high-assurance for almost all of the C language (ISO C 2011)
  - generates efficient code for the PowerPC, ARM, RISC-V and x86 processors


## mobile

- microsoft maui
  - dotnet multiplatform application user interface
  - cross-platform, native ui
  - platforms: windows, mac, ios, android
  - supports blazor components


## ide

- visual studio: slow and bloated
- vscode
  - useful extensions
    - draw.io integration: unofficial extension integrates Draw.io (also known as diagrams.net)
    - markdown preview mermaid support: adds mermaid diagram and flowchart support to vs code's builtin markdown preview

- jetbrains
  - rider: for .net developers
  - pycharm: for python developers


## software testing

- automation frameworks
  - functional
    - selenium
  - load/performance
    - jmeter
    - k6.io


## patterns

- forbidden dependency test [^3]
  - enforces constraints on project structure
  - implementations: dependency-cruiser (nodejs)


## references

[^1]: https://github.com/hmemcpy/milewski-ctfp-pdf/ (category theory for programmers)
[^2]: https://stackoverflow.com/questions/9611904/haskell-lists-arrays-vectors-sequences
[^3]: https://www.youtube.com/watch?v=TqfbAXCCVwE
[^4]: https://youtu.be/szHV6RdQdg8?t=1088
