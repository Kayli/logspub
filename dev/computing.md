# notes related to topics about computing


## basics

- processor word
  - size varies: on most modern cpus it either 32 or 64 bits

- integers on 64bit machine/executable
  - unsigned 0 to 2^64-1
  - signed -2^63 to 2^63-1

- model of computation
  - model which describes how an output of a mathematical function is computed given an input
  - categories
    - sequential (fsm, turing machine, etc.)
    - functional (combinatory logic, lambda calculus)
    - concurrent (cellular automata, ideal logic gate, etc)

- abstract machine
  - theoretical computer used for defining a model of computation
  - examples
    - rasp: random-access stored-program machine

- automata theory
  - is the study of
    - abstract machines (automata)
    - the computational problems that can be solved using such machines
  - is closely related to formal language theory

- types of logic
  - combinatorial: does not have memory, a pure function
  - sequential: has memory, maintains internal state


## classes of automata

- combinational logic (combinatorial logic)
  - implemented by boolean circuits
  - output depends not only on the present input

- turing machine
  - sequential mathematical model of computation that defines an abstract machine
  - machine example: 3-state, 2-symbol busy beaver
    - operates on an infinite memory tape divided into discrete "cells"
    - has reading head which can move 1 cell left or 1 cell right
    - can read/write tape symbol
      - min number of distinct symbols is 2: {0, 1}
    - can be in 1 of 4 states: {0,1,2,halt}
      - no idea why 3-state machine actually has 4 states: probably some stupid convention
    - has transition function
      - analogous to assembly language in modern computers
      - composed by rules of the following format
        - having current machine state and read tape symbol
        - do
          - write tape symbol
          - move tape
          - set new (next) state


## cellular automata

- types
  - number of dimensions
  - reversible vs irreversible
  - probabilistic vs deterministic

- garden of eden (goe)
  - is a configuration that has no predecessor
  - it can be the initial configuration of the automaton but cannot arise in any other way

- 2d
  - von neumann neighborhood (4-neighborhood)
  - range-2 "cross neighborhood"
  - moore neighborhood

- universal replicators
  - contributors: von Neumann, Renato Nobili
  - construction
    - is the process by which one configuration generates another
    - some configurations cannot be constructed by any means
  - 2d
    - von neumann universal replicator
      - self-replicating machine consists of three parts
        - "description" of itself ('blueprint' or program for)
        - universal constructor mechanism
          - can read any description 
          - can construct the machine encoded in that description 
        - universal copy machine that can make copies of any description

      - steps
        - construct a new machine encoded in the description using universal constructor
        - use a copy machine to create a copy of that description
          - pass on the copy to the new machine

      - some machines will do this backwards, copying the description and then building a machine


## mechanical models

- symbolic mechanical systems
  - lego life glider https://www.youtube.com/watch?v=NefDntR0R3w


## references

- https://en.wikipedia.org/wiki/Automata_theory
