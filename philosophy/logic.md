# notes on logic

- informal logic
  - examines arguments expressed in natural language
  - associated with informal fallacies, critical thinking, and argumentation theory
  - wikipedia says that bayesian logic is informal (but why???) 

- formal logic
  - examples: algebraic logic, boolean logic
  - see math/logic-formal.md for more details

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
    - rhetoric (/ˈrɛtərɪk/): is the art of persuasion


## argumentation [1]

- claim: statement that asserts something to be the case or not to be the case
    - can be
      - true or false
      - percievable or not
      - real or imaginary
      - resolvable or not
      - agreed upon or controversial

    - types
      - facts
        - are objective statement about reality, those that
          - describe the world as it is, independent of personal opinions, beliefs, or perspectives
          - based on empirical evidence, observation, and logical reasoning
        - verifiable and can be confirmed/disproved through repeatable experiments or observations

      - value judgements
        - subjective assessments based on personal beliefs, preferences, or moral principles
        - involve making evaluations about what is good, bad, right, or wrong
        - influenced by cultural, societal, and individual perspectives
        - kinds
          - aesthetic value judgements
            - matters of taste, art, attractiveness
            - typically quite different from person to person, there is no universal right answer
          - practical value judgements: accomplishing ends, getting things done
          - moral value judgements
            - what's right and wrong, good and bad
            - typically should be the same for everyone
            - are a part of cultural/moral convention
        
    - examples
      - water contains two hydrogen atoms
      - we should raise tuition
      - batman will beat spiderman in a battle
      - freedom is good

    - examples of domains
      - moral and ethics: right vs wrong, good vs bad
        - theft or murder are often judged as universally wrong
        - honesty and charity are seen as universally right
      - legal judgments: guilty or not guilty of a charge
        - though there are nuances in the legal process
      - mathematics: a statement is either true or false
        - many judgments about propositions or proofs are bivalent
        - however
          - more advanced math incorporate probability and degrees of belief into math reasoning
          - see fuzzy logic, quantum computing, stochastic processes, bayesean inference
      - formal logic: propositions are either true or false
      - binary classification: spam vs. non-spam emails or binary outcomes in medical tests
        - in data science or machine learning

- issue: a controversial claim
  - composed of claim and counterclaim (the opposite)
  - example: should we raise tuition?

- argument: a set of claims
  - composable, so that they can consist of other arguments
  - claims can be
    - premises: represent support for the conclusion
      - indicator words: because, given, since, in view of
    - conclusion: claim we want to agree on
      - indicator words: it follows that, thus, therefore, so, hence, consequently, this implies that

  - what's not an argument
    - non-controversial claim, one that everyone agrees with
    - a single claim without supporting evidence, premises (other supporting claims)
    - a bunch of unrelated or weekly related claims jumbled all together
    - ceremonial language
      - example: 'Esteemed colleagues, distinguished guests, and fellow citizens, today, as we gather on this auspicious occasion, we stand at the threshold of a new era. It is a moment of great significance ...'
  
  - can be
    - deductive
      - given premises, conclusion is certain
      - can be
        - valid: sound, unsound
        - invalid
      - examples
        - socrates is a man, all man are mortal -> socrates is mortal
        - socrates is in jail, everybody in jail are guilty -> socrates broke the law
    
    - inductive
      - given premises, conclusion is likely 
      - can be
        - strong: cogent, not cogent
        - weak
      - examples
        - socrates is in jail, people in jail usually broke the law -> socrates broke the law


## references

[1]: https://www.youtube.com/playlist?list=PL447DFE6900523895 (FSU lectures: critical thinking)
