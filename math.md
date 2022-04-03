# some basic math facts that i usually tend to forget

## basics

- universe of discourse
  - generally refers to the collection of objects being discussed in a specific discourse
  - in model-theoretical semantics, a universe of discourse is the set of entities that a model is based on
  - synonyms: domain of discourse, universal set, universe

- qed 
  - is an abbreviation for the latin phrase "quod erat demonstrandum" ("that which was to be demonstrated")
  - a notation which is often placed at the end of a mathematical proof to indicate its completion


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


## automated theorem provers

- provers 
- widely used provers
  - SAT (abbr from satisfiability)
    - solve constraints involving(written in) propositional logic
  - SMT (satisfiability modulo theories)
    - solve constraints involving(written in) predicate logic with quantifiers
    - can also solve constraints involving propositional logic
    - name is derived from the fact that these expressions are interpreted within ("modulo") 
      a certain formal theory in first-order logic with equality

### coq

- commands
  - Theorem
    - aliases: "Lemma", "Remark", "Fact", "Corollary", "Proposition"
    - example: Theorem my_first_proof : (forall A : Prop, A -> A).
  - Proof
    - indicates beginning of the proof, plays similar role as an open curly brace in c
  - Qed
    - ends the proof, plays similar role as a closing curly brace in c

## tutorials

- https://ncatlab.org/nlab/show/ZFC


## references

[^1]: https://en.wikipedia.org/wiki/Duality_(mathematics)
[^2]: https://www.researchgate.net/publication/225203043
[^3]: https://esolangs.org/wiki/ZFC%2B%2B
[^4]: https://github.com/coq-contribs/zfc
