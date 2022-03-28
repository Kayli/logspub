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


## proofs

- axiomatic proof
  - deductive derivations of propositions from primitive premisses that are true in some sense of ‘true’
  - they start from given primitive premisses and go down to the proposition to be proved
  - aim is to give a foundation and justification of the proposition
- analytic proof
  - proofs are non-deductive derivations of plausible hypotheses from problems, in some sense of ‘plausible’
  - they start from a given problem and go up to plausible hypotheses
  - aim is to discover plausible hypotheses capable of giving a solution to the problem


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
