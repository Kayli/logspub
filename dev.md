# notes related to software development

## basics

- structured programming
  - forbids arbitrary jumps in code
  - defines which points in code are legitimate to jump to
    - nowadays these structures are called methods, functions, switch statements, loops, etc.

- lambda calculus is one of the origins of functional programming

- pure function
  - one that has no side-effects
  - has referential transparency
    - always returns same result when called with same parameters
- prefix function
  - usual named function that is placed before arguments
- infix function
  - is like '+' or '*' operators that is placed between 


## modelling languages and tools

- universal modelling language
- mermaid https://mermaid.live/
  - declarative uml diagrams, similar to websequencediagrams
  - supports: flow charts, sequence diagrams, class diagrams, erd diagrams
  - vscode plugin


## functional programming languages

- classic functional programming [^1]
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
  - lisp

- modern fp: closure, fsharp, scala


## imperative/hybrid programming languages

- javascript and typescript
  - don't natively support named function parameters on a call site


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

- microsoft
  - notepad (just kidding)
  - visual studio: slow and bloated
  - vscode
    - opensource
    - very promising one, a joy to work in, hope they won't fuck this one up
    - useful extensions
      - draw.io integration: unofficial extension integrates Draw.io (also known as diagrams.net)
      - markdown preview mermaid support: adds mermaid diagram and flowchart support to vs code's builtin markdown preview
    - to increase scrolll buffer in terminal set the following option [^5]
      - "terminal.integrated.scrollback": 1000 

- jetbrains
  - rider: for .net developers
  - pycharm: for python developers
  - intellij idea: java
  - fleet: in public preview as of oct 2022, polyglot ide

- unix: vim, emacs


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


## recursion

- base case: a terminating scenario that does not use recursion to produce an answer
- recursive step: a set of rules that reduces all successive cases toward the base case

- mutual recursion: when more than one function call one another recursively [^4]


## unicode

- basic multilingual plane (bmp)
  - utf16: use of 16 bits allows direct representation of 65,536 unique characters

- supplementary character: is a character located beyond the bmp

- surrogate
  - unicode reserves the codepoints that match the ranges of the high and low pairs as invalid
  - they are sometimes called surrogates but they are not characters, they don't mean anything by themselves

- surrogate pair
  - for UTF-16, a "surrogate pair" is required to represent a single supplementary character
  - backward compatibility mechanism


## algorithms

- big O notation
  - defines worst-case scenario time complexity
  - non-dominant terms are dropped if they are composed by addition
    - if your algorithm does something that takes log time and then something that takes linear time, complexity will be linear
  - you can't drop terms if they are composed by multiplication
    - if your algorithm does something that takes linear t
  - examples
    - constant     O(1)
    - log:         O(log n)
    - linear:      O(n)
    - log-linear:  O(n * log n)
    - quadratic:   O(n^2)
    - polynomial:  O(n^const) ???
    - exponential: O(2^n)
    - factorial:   O(n!)

- popular ones
  - binary search

- stable vs unstable sorting algorithms
  - unstable may change order of values with same keys, where stable guarantees initial order
  - starts to matter when you sorting objects


## useful resources

- rosetta code https://rosettacode.org/wiki/Rosetta_Code
  - programming chrestomathy site
  - presents solutions to the same task in as many different languages as possible, to demonstrate how languages are similar and different, and to aid a person with a grounding in one approach to a problem in learning another


## references

[^1]: https://github.com/hmemcpy/milewski-ctfp-pdf/ (category theory for programmers)
[^2]: https://stackoverflow.com/questions/9611904/haskell-lists-arrays-vectors-sequences
[^3]: https://www.youtube.com/watch?v=TqfbAXCCVwE
[^4]: https://youtu.be/LYIn_Ewpq-E?t=2205
[^5]: https://stackoverflow.com/questions/39881395/visual-studio-code-scroll-back-buffer