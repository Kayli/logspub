# some basic math facts that i usually tend to forget

## basics

- universe of discourse
  - generally refers to the collection of objects being discussed in a specific discourse
  - in model-theoretical semantics, a universe of discourse is the set of entities that a model is based on
  - synonyms: domain of discourse, universal set, universe

- type theory
  - is a formal system in which every "term" has a "type"
  - a "type" in type theory has a role similar to a "type" in a programming language as it dictates 
    - operations that can be performed on a term
    - the possible values variables might be replaced with

- key structural elements
  - calling something a lemma, theorem, or corollary is purely a choice made for organizational purposes
  - theorem
    - a mathematical statement that is proved using rigorous mathematical reasoning
    - in a mathematical paper, this term is often reserved for the most important results
  - lemma
    - a minor result whose sole purpose is to help in proving a theorem
    - it is a stepping stone on the path to proving a theorem
  - corollaries
    - something that follows trivially from any one of a theorem, lemma, or other corollary


## set theory

- zermelo–fraenkel set theory (zf)
  - standard form of axiomatic set theory and as such is the most common foundation of mathematics
  - zfc is zf with has axiom of choice (ac) included

- implementations
  - zfc++ [^3]
  - zfc in coq [^4]


## random notes

- euler's number
  - e^x equals to its own derivative: (d/dx)e^x = e^x

- complex numbers
  - common representation: z = x + iy

- duality [^1]
  - translates 
    - concepts, theorems or mathematical structures 
    - into other concepts, theorems or structures in a one-to-one fashion
    - often (but not always) by means of an involution operation:
      - if the dual of A is B, then the dual of B is A

- lyapunov exponent (lyapunov characteristic exponent) of dynamical system
  - quantity that characterizes the rate of separation of infinitesimally close trajectories
  - highest lyapunov exponent represents chaoticity of a system


## self-referential systems

- russell's paradox
- godel incompletness theorem 
- halting problem


## λ-calculus

- was introduced by the mathematician alonzo church in the 1930s
- definition
  - formal system in mathematical logic for expressing computation based on
    - variable:    a character or string representing a parameter or mathematical/logical value
    - abstraction: function definition in which variable becomes bound in the expression
    - application: applies a function to an argument, using variable binding and substitution
  - it is a universal model of computation that can be used to simulate any turing machine

- a valid lambda calculus expression is called a "lambda term"
- abstraction is a definition of an anonymous function
  - for example: abstraction λx.t taking a single input x and substituting it into the expression t
- application is the act of calling function on some input
  - function application is regarded as left-associative, so that 'stx' means '(st)x'
- variable declaration is not defined in lambda calculus
- functions are taken to be 'first class values'
  - so functions may be used as the inputs, or be returned as outputs from other functions
- primitive functions
  - identity function x -> x
  - constant function x -> y
- data storage
  - it is stored as parameters to a function that does not yet have all the parameters required for application
- numbers(ordinals) and booleans can be expressed as functions
  - for numbers
    - having function f and parameter x
    - function f is applied to x fixed number of times
      - 0 means that f is not applied, 1 means that f applied to x once and so on
  - for booleans
    - having function f and two parameters x and y
    - true value represented as function that always returns x
    - false value represented as function that always returns y


## proofs [^2]

- axiomatic proof
  - deductive derivations of propositions from primitive premisses that are true in some sense of ‘true’
  - they start from given primitive premisses and go down to the proposition to be proved
  - aim is to give a foundation and justification of the proposition
  
- analytic proof
  - proofs are non-deductive derivations of plausible hypotheses from problems, in some sense of ‘plausible’
  - they start from a given problem and go up to plausible hypotheses
    - a problem is any open question
    - a hypothesis is any means that can be used to solve a problem
    - a hypothesis is said to be plausible if and only if it is compatible with the existing data
    - look for some hypothesis that is a sufficient condition for solving the problem
    - hypothesis is obtained from the problem, and possibly other data, by some non-deductive inference
      - inductive, analogical, diagrammatic, metaphorical, metonymical, by generalization, 
        by specialization, by variation of the data, and so on
  - aim is to discover plausible hypotheses capable of giving a solution to the problem
  - hypothesis, in turn, is a problem that must be solved, so the process is recursive a potentially infinite
  - statement of the problem may be modified to a certain extent to make it more precise,
    may even be radically changed as new data emerge, so development of the statement of the problem 
    and the development of the solution of the problem may proceed in parallel

- 2 types of reasoning when working on proofs
  - forward reasoning
    - most common approach in human-generated proofs
    - the proof begins by proving simple statements that are then combined to prove 
      the theorem statement as the last step of the proof
  - backward reasoning
    - the proof begins with the theorem statement as the goal, which is then gradually 
      transformed until every subgoal generated along the way has been proven. 


## theorem provers

- components of a typical prover
  - theorem: thing we want to prove
  - logic, which is a type theory, e.g. calculus of constructions [^5]
  - validity checker
  - language
  - proof assistaint (just a debugger??)

- curry-howard isomorphism
  - defines that programs, properties and proofs are formalized in the 
    same language called calculus of inductive constructions, that is a λ-calculus
    with a rich type system
  - can be seen as an analogy that states that the return type of a function (i.e., the 
    type of values returned by a function) is analogous to a logical theorem, subject to 
    hypotheses corresponding to the types of the argument values passed to the function;
    and that the program to compute that function is analogous to a proof of that theorem

- implementations
  - z3 (smt)
    - most popular, backed by microsoft
    - provides bindings to many languages, including python
    - implements algorithms [^8]
      - dppl
        - complete, backtracking-based search algorithm 
        - used for deciding sat of propositional logic formulae in conjunctive normal form
      - simplex: a popular algorithm for linear programming
      - rewriting: methods of replacing subterms of a formula with other terms [^9]
      - superposition: how to combine different algorithms inside one solver
      - congruence closure
        - operation that determines which terms are equal under substitutivity of equality and a given set of equalities
      - grobner basis: multivariate, non-linear generalization of both 
        - euclid's algorithm for computing polynomial greatest common divisors
        - gaussian elimination for linear systems
      - quantifiers elimination
      - euclidian solver: way to find the greatest common divisor of two positive integers, a and b

  - dreal (smt) [^6][^7]
    - supports a wide range of nonlinear functions
      - including transcendental functions and solutions of lipschitz-continuous ODEs

  - coq (interactive theorem prover, assistaint)  
    
  - isabelle/hol (generic proof assistant) [^10]
    - uses hol syntax (typed lambda calculus) [^11]
    - written in standard ml and scala

  - lean
  - holpy
  - dependent type theory-based
    - agda
    - epigram
    - matita
    - nuprl


## computer algebra systems

- sympy https://github.com/sympy/sympy
  - symbolic and numberic solver, differentiation, integration
  - simplifies statistics calculations introducing 'random variable' type 
  - export to latex
  - supports matplotlib backend


## recursion [^13]

- structural
  - a recursive call is made on a subset of the original input data
  - terminates
- generative
  - a recursive call is made on data that was constructed/calculated from the original input data
  - no guarantee that will terminate


## tutorials

- zfc https://ncatlab.org/nlab/show/ZFC
- isabelle/hol https://www.youtube.com/watch?v=1nEpUoVopT0


## terminology

- qed: quod erat demonstrandum
  - translates from latin as "that which was to be demonstrated"
  - a notation which is often placed at the end of a mathematical proof to indicate its completion

- sat: abbr from satisfiability
  - solve constraints involving(written in) propositional logic

- smt: satisfiability modulo theories
  - solve constraints involving(written in) predicate logic with quantifiers
  - can also solve constraints involving propositional logic
  - name is derived from the fact that these expressions are interpreted within ("modulo") 
    a certain formal theory in first-order logic with equality

- cas: computer algebra system


## references

[^1]: https://en.wikipedia.org/wiki/Duality_(mathematics)
[^2]: https://www.researchgate.net/publication/225203043
[^3]: https://esolangs.org/wiki/ZFC%2B%2B
[^4]: https://github.com/coq-contribs/zfc
[^5]: https://en.wikipedia.org/wiki/Calculus_of_constructions
[^6]: http://dreal.github.io
[^7]: https://stackoverflow.com/questions/51433210/support-of-trigonometric-functions-e-g-cos-tan-in-z3
[^8]: https://www.youtube.com/watch?v=unXzJEc3Pvk
[^9]: https://en.wikipedia.org/wiki/Rewriting
[^10]: https://isabelle.in.tum.de
[^11]: https://www.cl.cam.ac.uk/research/hvg/old/HOL/documentation/hol90.7/syntax.html
[^12]: https://math.stackexchange.com/questions/463362/whats-the-difference-between-theorem-lemma-and-corollary/463365#463365
[^13]: https://stackoverflow.com/questions/14268749/how-does-structural-recursion-differ-from-generative-recursion
