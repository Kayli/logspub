# notes on topics related to logic

## basics

- logic
  - is the study of correct reasoning

- types
  - formal logic
    - is the science of deductively valid inferences or logical truths
    - uses formal language
    - studies how conclusions follow from premises due to the structure of arguments alone, independent of their topic and content
    - examples: algebraic logic, boolean logic

  - informal logic
    - examines arguments expressed in natural language
    - associated with informal fallacies, critical thinking, and argumentation theory
    - wikipedia says that bayesian logic is informal (but why???) 
    - approaches
      - pragmatic or dialogical approach
        - composed of arguments as speech acts occuring in a context which affects the standards of right and wrong arguments
        - dialogues are games of persuasion
          - each player has the goal of convincing the opponent of their own conclusion
          - arguments are the moves of the game
          - winning move 
            - is a successful argument 
              - that takes the opponent's commitments as premises
              - and shows how one's own conclusion follows from them
          - fallacy
            - is a violation of the standards of proper argumentative rules


## propositional logic, boolean algebra

- is a truth-functional propositional logic
- formulas are interpreted as having precisely one of two possible truth values, 
  the truth value of true l the truth value of false
- principle of bivalence and the law of excluded middle are upheld

- inferences: are steps in reasoning, moving from premises to logical consequences

- and (conjunction)
  - notated as '∧', mnemonic: 'cap', same number of letters as word 'and'
- or (disjunction)
  - notated as 'v', mnemonic 'versus'
- exclusive or (xor, intensional disjunction)
  - notated as '⊕', mnemonic 'cross' like x in 'exclusive'
  - P ⊕ Q ≡ (P ∨ Q) ∧ (∼(P ∧ Q))

- conditional (implication, if)
  - notated as '->', '=>'
  - consists of 
    - hypothesis (antecedent, protasis)
      - first half of a hypothetical proposition, whenever the if-clause precedes the then-clause
    - conclusion (consequent)
      - second half of a hypothetical proposition

- contraposition
  - inference of going from a conditional statement into its logically equivalent contrapositive
  - contrapositive of P → Q is ¬Q → ¬P

- conversion: Q → P is conversion of P → Q

- biconditional (iff)
  - means that P implies Q and Q implies P
  - alternative notations: iff, <->, <=>, =, an equivalence sign (≡), EQV
  - sometimes known as the material biconditional, is the logical connective used to conjoin two
    statements P and Q to form the statement "P if and only if Q"

- iff vs equivalence [3]
  - P ↔ Q (iff) is statement that could be either true or false
  - but P ≡ Q means that P ↔ Q is always a true biconditional
    - meaning that P and Q have the same value no matter what

- syllogism ‘with’ + ‘to reason’


## rules of inference

- transformatiion rules [2]
  - carnap brings [axioms and rules of inference] under the common term "transformatiion rules", 
    by considering the axioms as the result of transformation from zero premises 

- modus ponens (implication elimination or affirming the antecedent)
    - it is a rule of inference, deductive
    - P implies Q. P is true, therefore Q must also be true
    - also known as
      - modus ponendo ponens (Latin for "method of putting by placing")
      - implication elimination
      - affirming the antecedent

- modus tollens (denying the consequent)
  - if P, then Q. Not Q. Therefore, not P.
  - pretty much the same as contraposition: if a statement is true, then so is its contrapositive


## proofs

- definition
  - mathematical proof is an inferential argument for a mathematical statement
  - it shows that the stated assumptions logically guarantee the conclusion
  - may use other previously established statements, such as theorems
    - but can, in principle, be constructed using only certain basic or original assumptions
      known as axioms, along with the accepted rules of inference

- axiom or postulate
  - fundamental assumption regarding the object of study, that is accepted without proof

- definition
  - gives the meaning of a word or a phrase in terms of known concepts

- typical process: definitions -> axioms -> proofs


## truth

- see 'theories of truth' in philosophy.md


## references

[2]: https://math.stackexchange.com/questions/1201492/is-the-modus-ponens-is-an-axiom-in-formal-logic
[3]: https://math.stackexchange.com/questions/2432462/whats-the-difference-between-biconditional-iff-and-logical-equivalence/
