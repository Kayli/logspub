# abstract algebra self-learning course notes [1]

## basics

- abstract (modern) algebra is a study of algebraic structures

- not to be confused with universal (general) algebra
  - which studies algebraic structures themselves, not examples ("models") of algebraic structures

- algebraic topology
  - branch of mathematics that uses tools from abstract algebra to study topological spaces 

- common algebraic structures
  - groups, rings, fields
  - modules, vector spaces, topological spaces, lattices, and algebras

- groups, rings, fields can be represented as sets

- morphism
  - structure-preserving function
  - maps one mathematical object (such as a group, a ring, a vector space, or a topological space) to another

- isomorphism [2]
  - inverse function exists between two mathematical objects
  - types
    - bijections: between sets
    - bijective homomorphisms: between groups, rings, fields
    - homeomorphisms: between topological spaces

- category
  - is a collection of objects and morphisms (or arrows) between those objects that satisfy certain axioms

- functor
  - map between categories that preserves the structure of the categories


## useful analogies [2]

- in set theory: functions with domains and codomains tell us how sets interact with each other
- in group theory: group homomorphisms tell us how groups interact with each other
- in topology: continuous functions tell us how topological spaces mapped to each other

- to generalize structures above, we use categories
  - which are collection of of objects and collection of morphisms


## groups

- group theory
  - studies the algebraic structures known as groups
  
- group
  - definition
    - has a set of elements G
    - there is a binary operation defined
      - can be applied to any two elements (operands)
      - common operation signs + (plus), x (cross), * (star, often used as generic operation)
    - group axioms are satisfied
      - has an identity element
        - combining any element with identity element gives you the same element
          - y * e = e * y = y
      - each element has an inverse
        - combining element with its inverse gives you identity element
          - x * x⁻¹ = e
      - elements obey associative property
        - (a * b) * c = a * (b * c)
    - closed under operation ??? 
      - x, y ϵ G => x * y ϵ G
  - types
    - commutative (abelian)
    - non-commutative (non-abelian)

- subgroup
  - H is a subgroup of G when elements of H are a subset elements of G
  - notation
    - H is a subgroup of G is written like H <= G
    - H is a proper subgroup of G is written like H < G
  - to fully understand a group G its useful to take it apart and study its pieces (subgroups)

- order of a group
  - signifies number of elements in a group
  - order 1: trivial group, contains only an identity element
  - order 2: integers mod 2
  - order 3
    - abelian group
    - integers mod 3 under +
    
- isomorphic groups
  - group isomorphism is a function between two groups that sets up a one-to-one correspondence 
    between the elements of the groups in a way that respects the given group operations
  - if there exists an isomorphism between two groups, then the groups are called isomorphic


## references

[1]: socratica youtube channel, playlist "abstract algebra"
[2]: https://youtu.be/igf04k13jZk