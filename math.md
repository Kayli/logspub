# some basic math facts that i usually tend to forget


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
  - highest l.e. represents chaoticity of a system


## self-referential systems

- russell's paradox
- godel incompletness theorem 
- halting problem


## lambda calculus

- was introduced by the mathematician alonzo church in the 1930s
- definition
  - formal system in mathematical logic for expressing computation based on 
    - function abstraction
    - application using variable binding and substitution
  - it is a universal model of computation that can be used to simulate any turing machine

- a valid lambda calculus expression is called a "lambda term"


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


## references

[^1]: https://en.wikipedia.org/wiki/Duality_(mathematics)
[^2]: https://www.researchgate.net/publication/225203043
