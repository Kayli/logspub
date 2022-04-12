# some random stuff

## april 11

- ideas for marketa project
  - test if state (module variables) are shared between tests in pytest
    - so maybe i can instantiate container just once
      - no, it doesn't make sense, as i need clean state to make sure tests are robust
      - but anyways, i should test how pytest handles global state when running test cases
  
- ideas for scifi shorts
  - biking around, meditating, tracking ppls intentions
  - things observed: ppl sucking up to 
    - 'relationship' triggers
      - tested 2 girls, 1 boy interfaces
    - self image insecurities
      - 'so slow' trigger
      - 'theyre watching me' paranoia trigger
        - random people sitting behind
        - guy walking on the street with cail-somthing yellow-blue trigger hat
        - limbs movements
          - not the first time it happens
            - last time i noticed was at macdonalds several months ago
          - 2 guys were trying to suck up to leg-rocking
    - possible reasons
      - social habit, like testing for vulnerabilities or something
      - trying to take advantage of possible vulnerable psychological states
      - trying to enforce psycho-shell formation
        - so that signals go straight around conscious filters
        - this may be just a genetic/socially induced behaviors that ppl express naturally
          in attempts to communicate with each other on conscious and subconscious levels
    - ill call it 'ubc shit meditation, session 002'
    - i think they, like, just, kinda like, like, they, just like, o my god, like,
      i cant make up my mind like, its like, we're talking like, like, we're so fucked up,
      like, he is like, she is like, we are like full of shit like like ...
    - poor kids don't realize yet 
      - that their gyms that 'help build confidence' can turn them into disabled people 
      - as well as convince to buy all sort of shit that healthy humans don't need
      - they must be lucky to have sane elders behind their backs who protect from all those traps
      - but this doesn't matter, as they are just bioactuators of some rich and not very smart people ;)
        - those ppl cant even make a fucking keybord work properly
          - or its another silly sign of their nonsense-torture-game?
          - past is who we are now, so its pretty stupid to give it up
            - unless you're ready to be exploited left and right
        - yeah, those centaur ppl are as fucked as we all are ... but hey have their stupid digital guns
          - and they think about themselves as great puppeteers ... 
            - but they are as pathetic as those kinds they fuck
            - or they are as pathetic as me, who is writing all this nonsense
              - because the one who is writing it is not me, its just a stupid monkey, a stupid monkey of sorts
    - healthy confindence is a symphony, not all pufffed-up nonsense they see is true confidence
 

## april 10

- links to preserve 
  - coq logic https://www.seas.upenn.edu/~cis500/cis500-f13/sf/Logic.html
  
- looking at lean theorem prover tutorial https://leanprover.github.io/tutorial
  
- looking at https://github.com/bzhan/holpy theorem prover
  - proofs are conducted in natural deduction style
    - sequent and consequent

- looking at paper search engines
  - google scholar 
    - is able to search the database of case law
  - interesting clean searcher of scientific papers without ads (so far)
    - https://www.semanticscholar.org/
    - yellow-blue color scheme attention sucker?
      - paranoia? dark scheme is also attention sucker?
        - no, its just easier on eyes in dark setting as it creates less contrast with environment
      - maybe its some cluster of 'workers' into which some people may fall into
        - one of social engineering techniques
        - conspiracy? definitely! ))

- reading about sociology stuff
  - society as objective reality
    - institutionalization implies division of labor?
      - yes, but the problem usually is in bullshit labor/jobs
      - bullshit is subjective
        - therefore problem lies
          - in physical and cognitive traps that people fall in
          - in individuals
            - constructing such traps with 'malicious' intent
            - falling into traps, not being able to predict their existence and specific manifestations
      - but who is going to identify traps?
        - its a joint effort of hunter/pray game players

    - what is considered 'malicious' in our society?
      - what laws forbid 
        - citizenship form of allegiance
      - what ethical standards forbid
        - such standards usually consequence of allegiance with a certain group

- reflecting on theorem provers stuff

  - alternatives
    - theorem state transformation rules and invariants can be implemented in more 
      modern/approachable programming languages like python, javascript, java, c#, etc.
      - consider reviewing projects
        - https://github.com/bzhan/holpy
        - https://github.com/stepchowfun/theorem-prover
    - maybe we don't need to prove theorems in order to have a very reliable code
      - may strong type system + automated testing in the same language is enough?
      - provers don't provide strong guarantees, they just increase probability of correctness
      - how one can practically test/quantify this?
        - otherwise any claim about correctness is just hypothetical/political

  - typical practical use [^2]
    - take program written in language like 'c'
      - where its easy to fuck up
      - where most devs are too old or uneducated to write automated tests (just kidding)
    - create ast with information that is necessary for verification
      - usually not all code gets verified, but only its critical parts
      - business priorities are likely driving such requirements
    - formalize and enforce policies related to
      - shared resources
        - allocated memory access
      - equivalence relations of binary codes, e.g. on different platform
      

  - exploring imposed artificial barriers on knowledge aquisition
    - bait + trap pattern detected
    - bait
      - nice, intuitive interface and surface-level descriptions of a tool
      - naming may revolve around supressed sexual topics
        - coq tactics, isabelle/hol, etc
        - will likely create subconscious fixation/attraction

    - trap
      - creates an artificial barrier, after which only experts/priests can help
      - sudden departure from intutive didactical techniques at certain point
        - essentially a sunk cost fallacy
        - happens when target is already invested some significant time/resources to 
          aquire partial knowledge about the subject
      - example
        - coq tactics are just a bunch of methods which somehow transform proof state
        - the way methods transform it is presented in cryptic and unapproachable fashion
        - even simple proofs like 'A->B' implication or 'modus ponens' require very deep 
          envolvement in fancy terminological maze
    
    - likely goals
      - rich parents are keeping their kids busy with 'right stuff'
        - kids then are more tamed and submissive
        - kids will join family business without rocking a boat too much
      - subscribe 'lost soul' to some n-year university program (indoctrination, brainwashing)
        - for a huge fee/debt
      - charge 'lost souls' for consulting services
        - hiring a private tutor
        - works best after professors convince victims that they are not smart/educated enough
      - keep poor away from pristine certifications while creating illusion of accessebility

    - proved by reflexivity. haha


## april 9

- browsing coq-related stuff
  - https://stackoverflow.com/questions/52935508/modus-ponens-and-modus-tollens-in-coq
  - tactics official doc https://coq.inria.fr/refman/proof-engine/tactics.html

  - 2 types of reasoning when working on proofs
    - forward reasoning
      - most common approach in human-generated proofs
      - the proof begins by proving simple statements that are then combined to prove 
        the theorem statement as the last step of the proof
    - backward reasoning
      - the proof begins with the theorem statement as the goal, which is then gradually 
        transformed until every subgoal generated along the way has been proven. 
  - coq and its tactics use backward reasoning


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


## april 5, 2022

- instrument vs security [^1]
  - financial instrument is a broader term
    - refers to those traded in money markets, capital markets, FX markets, spot market, and derivatives
  - security refers only to equity or debt instruments. 
    - it has some sort of protection in case there will be liquidity risk. 
  - example
    - foreign exchange markets can't be considered a security because it's very volatile, no guarantee if loss


## references

[^1]: https://www.quora.com/What-is-the-difference-between-financial-instruments-financial-securities
[^2]: http://typetheoryforall.com
