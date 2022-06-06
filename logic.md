# topics related to logic

## basics [^1]

- truth-functional propositional logic
  - formulas are interpreted as having precisely one of two possible truth values, 
    the truth value of true or the truth value of false
  - principle of bivalence and the law of excluded middle are upheld

- inferences: are steps in reasoning, moving from premises to logical consequences

- and (conjunction) 
  - notated as '∧', mnemonic: 'cap', same number of letters as word 'and'
- or (disjunction)
  - notated as 'v', mnemonic 'versus'
- exclusive or (xor, intensional disjunction) 
  - notated as '⊕', mnemonic 'cross' like x in 'exclusive'
  - P ⊕ Q ≡ (P ∨ Q) ∧ (∼(P ∧ Q)) 

- hypothesis (antecedent, protasis)
  - first half of a hypothetical proposition, whenever the if-clause precedes the then-clause

- conclusion (consequent)
  - second half of a hypothetical proposition

- contraposition
  - inference of going from a conditional statement into its logically equivalent contrapositive
  - contrapositive of P → Q is ¬Q → ¬P

- conversion: Q → P is conversion of P → Q

- logical biconditional P <-> Q
  - means that P implies Q and Q implies P
  - alternative notations: iff, <=>, =, an equivalence sign (≡), EQV
  - sometimes known as the material biconditional, is the logical connective used to conjoin two 
    statements P and Q to form the statement "P if and only if Q"


## rules of inference

- transformatiion rules [^2]
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


## references

[^1]: wikipedia
[^2]: https://math.stackexchange.com/questions/1201492/is-the-modus-ponens-is-an-axiom-in-formal-logic
