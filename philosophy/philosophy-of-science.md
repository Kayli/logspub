# self learning course notes on philosophy of physical sciences

## basics

- etymology
  - latin verb "to separate one thing from another, to distinguish," or else "to incise" 

- branches of sciences
  - formal sciences
    - the study of formal systems, which use an apriori methodology (as opposed to empirical) 
      - formal systems such as those under the branches of logic and mathematics
      - apriori knowledge is one independent from current experience
    - related to semantic/tarski theory of truth

  - natural sciences
    - the study of natural phenomena
    - branches
      - physical science: cosmology, geology, physics, chemistry, etc
      - life science: biology, zoology, botany, genetics, etc
    - measurements
      - rely on quantitative measurements and precise numerical data

  - social sciences
    - study of human behavior in its social and cultural aspects
    - measurements
      - quantitative: involve numerical data and often include scales, questionnaires, surveys, or experiments
      - qualitative: involve descriptive data and can include interviews, observations, case studies, or content analysis
    - testability?


## basic principles

- fact
  - basic statement established by experiment or observation
  - all facts are true under the specific conditions of the observation

- law
  - principle that can be used to predict the behavior of the natural world
  - describes the patterns we see in large amounts of data, but do not describe why the patterns exist

- hypothesis
  - represents a trial solution to a problem
  - propose explanation for a phenomenon
    - educated guess: provides a suggested solution based on evidence
    - prediction: as an outcome of some experiment
    - explanation: hypotheses can be suggestions about why something is observed
  - scientific hypothesis
    - key attributes
      - testability/falsifiability: may be proven true or false by testing and experimentation
      - parsimony (бережливость): discouraging the postulation of excessive numbers of entities, occam's razor
      - scope: the apparent applicability of the hypothesis to multiple known phenomena
      - fruitfulness: the prospect that the hypothesis may explain further phenomena in the future
      - conservatism: the degree of "fit" with existing recognized knowledge-systems

- theory
  - comprehensive explanation of an important feature of nature supported by facts gathered over time
  - allow scientists to make predictions about as yet unobserved phenomena
  - scientific theory is a hypothesis that
    - has been extensively tested
    - evaluated by the scientific community
    - is strongly supported


## scientific realism

- goal is to uncover objective truth about the world around us
  - therefore progress occurs when theories more accurately represent facts
- objective epistemic basis for evaluating scientific disagreements
- positive epistemic attitude toward the content of our best theories and models
  - recommending belief in both observable and unobservable aspects of the world described by the sciences

- goal of progress usually valued higher than social coherence

- inductive reasoning method
  - the premises are viewed as supplying some evidence
  - but they don't offer full assurance of the truth of the conclusion
  - one's experiences and observations, including what are learned from others, are synthesized to come up with a general truth
  - difference from deductive reasoning
    - conclusion of a deductive argument is certain
    - but the truth of the conclusion of an inductive argument is probable, based upon the evidence given

- inductivism
  - make observations about the world
  - draw inductive inferences about the way the world is
    - such inferences are fallible but nonetheless rational 
- scientific method is an inductive method 

- new organon 1620
  - francis bacon creates a new system of logic he believes to be superior to the old ways of syllogism
    - this is now known as the baconian method
- principia mathematica 1687
  - isaac newton defines laws of motion

- calvinism
  - сalvin clearly believed that science and reason were universal gifts to mankind, and non-Christians were just as capable of discovering scientific truth as Christians. To neglect the discoveries of non-Christians simply because of their lack of faith is, according to Calvin, to be guilty of “sloth”

- deism
  - god created earth but after that no longer had influence on life and not watching it
  - secularism

- logical empiricism, or positivism
  - science mathematically coordinates and predicts sense data, rather than seeking underlying metaphysical realities
  - is a movement whose central thesis was the verification principle

- falsifiability
  - karl popper
  - argued for falsifiability
    - as one of the necessary criteria in verification game of science
  - premises and conclusions(expected behavior) should be verifiable
    - ideally, testing procedure should be offered (described)
  - opposed this to the intuitively similar concept of verifiability
    - verifying the claim "all swans are white" would require assessment of all swans, which is not possible
    - the single observation of a black swan is sufficient to falsify it
      - analogy with software development
        - unit-tests trying to falsify system under test to find inconsistency between actual and expected behaviors
        - but there is no way to prove correctness of your program using this method
          - we just increasing assurance/probability of a correct behavior

- kuhn's rationality of theory choice 
  - book "the structure of scientific revolutions"
  - paradigm shift
    - occurs when enough anomalies are accumulated which are not explainable by current theoretical framework
    - theory that 'wins' must have a higher puzzle-solving power than other alternatives

- conjecture vs hypothesis
  - both of them are statements based on observations, that seem to be true, but have not been proved or disproved yet
  - difference is in level of credibility that explanation is based on
    - hypothesis is testable, and explanation is based on accepted grounds
    - conjecture is proposition based on inconclusive grounds, and sometimes can not be fully tested
  - conjectures, unlike hypothesis, are used in math and hypothesis usualy are used elsewhere
    - if conjecture is proven, it becomes a theorem
    - border between two terms remains blurry, and terms sometimes are used as synonyms
    - 'riemann hypothesis' correctly should be called 'riemann conjecture'

- what is scientific?
  - for example, why "literary theory" is not scientific?
    - valuable and important kind of inquiry
    - yields knowledge
    - verification procedure is significantly modified
      - in comparison to one standardised by modern scientific community
      - no clear validation procedure against reality exists 
        - as even if there is a connection to reality, perception of it is highly subjective
        - meanings are too fluid and crafted to induce multiple equally valid interpretations
      - "prestiege" and "novelty" games are much more important than "verification" game


## epistemic relativism

- scientific theories are not simply discovered, but are constructed within specific historical and cultural contexts
- social dynamics within the scientific community, including power structures and dominant paradigms, can shape what is considered valid or credible knowledge

- in a simplest case, there are two contradictary hypotheses
- and there is no legitimate rational basis to agree about what counts as a good evidence to prefer one over the other
- example: there is no objective reason to prefer one poem over the other
  - as such preference is highly subjective
- social coherence usually valued higher than progress


## other

- reduction
  - ontological: complex system is nothing but an aggregation of its simpler components
  - explanatory: complex system can be explained by the theory governing its components alone

- process philosopy, ontology of becoming, or processism
  - is an approach to philosophy that identifies processes, changes, or shifting relationships as the only true elements of the ordinary, everyday real world. It treats other real elements (examples: enduring physical objects, thoughts) as abstractions from, or ontological dependents on, processes
  - has some parallels with 'event sourcing' approach in software design

- underdetermination thesis of theory by data
  - all evidence necessarily underdetermines any scientific theory
  - example
    - if all that was known was that exactly $10 was spent on apples and oranges, and that apples cost $1 and oranges $2, then one would know enough to eliminate some possibilities (e.g., 6 oranges could not have been purchased), but one would not have enough evidence to know which specific combination of apples and oranges was purchased

- duhem–quine thesis
  - posits that it is impossible to experimentally test a scientific hypothesis in isolation
    - because an empirical test of the hypothesis requires one or more background assumptions 
      - also called auxiliary assumptions or auxiliary hypotheses
      - similar to godel's incompleteness theorem ???
  - unambiguous scientific falsifications are impossible
  - related thesis: bundle of hypotheses
    - as a whole can be tested against the empirical world and be falsified if it fails the test
    - impossible to isolate a single hypothesis in the bundle ('confirmation holism' viewpoint)


## peer review

- conducted by 
  - scientific experts with specialized knowledge on the content of the manuscript
  - by scientists with a more general knowledge base

- anonymity
  - different levels
    - open
    - single-anonymous
    - double-anonymous
  - but it’s not possible to guarantee the anonymity of the author
    - if reviewer was already familiar with their work
    - if reviewer had heard that someone was working on a particular topic

- post-publication peer review: published online asap and then reviews come at later point

- paper should have at least two reviewers before being published in a journal
  - these reviewers are typically experts in the field, but should have no direct affiliation with the authors


## keeping references to original works

- stems from biblical tradition of hyperlinked text?
  - bible as a first hyperlinked text [1]


## random thoughts

- related to following statement
  - verifying the claim "all swans are white" would require assessment of all swans, which is not practically possible
      - but how about: "all known swans are white"?
        - when programming language toolchain emposes parser rules on a user program, entered as a text, it verifies only
          - past(existing) data
          - data passed to it explicitly by user
        - it doens't make any claims about
          - all existing user programs that have ever been entered till this moment
          - data that will be entered in the future

## references

- coursera 'philosophy of sciences: introduction to philosophy of physical sciences' by university of edinburgh
  - professor michela massimi (looks like jernej's relative)
- wiki on falsifiability https://en.wikipedia.org/wiki/Falsifiability
- anjan chakravartty on scientific realism https://plato.stanford.edu/entries/scientific-realism/
[1]: https://youtu.be/HPO1cUXZ8Dk