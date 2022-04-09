# some random stuff

## april 8

- browsing coq-related stuff
  - recursive function
    - defined using 'Fixpoint' keyword
  - proofs
    - are written using 'tactics'
    - you transform your goal until it can be solved using one of these tactics
  - importent coq types:
      - Prop
        - is meant for propositions
        - it is impredicative
          - meaning that you can instantiate polymorphic functions with polymorphic types
        - erased at run-time
          - meaning you can't pattern match on a Prop value to build a Type value, unless 
            there's only one possibility
      - Set
        - is meant for computation
        - it's predicative
        - remains at run-time
      - Type 
        - is a supertype of both Prop and Set
        - allowing you to write code once that works with both
  - tactics cheatsheet 
    - https://www.cs.cornell.edu/courses/cs3110/2018sp/a5/coq-tactics-cheatsheet.html


## april 5

- instrument vs security [^1]
  - financial instrument is a broader term
    - refers to those traded in money markets, capital markets, FX markets, spot market, and derivatives
  - security refers only to equity or debt instruments. 
    - it has some sort of protection in case there will be liquidity risk. 
  - example
    - foreign exchange markets can't be considered a security because it's very volatile, no guarantee if loss


## references

[^1]: https://www.quora.com/What-is-the-difference-between-financial-instruments-financial-securities
