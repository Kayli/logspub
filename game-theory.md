# Game theory and related topics

## basics

- runaway selection (fisherian runaway)
  - examples
    - sexually dimorphic phenotypic traits such as behavior expressed by a particular sex
    - evolution of ostentatious male ornamentation by persistent, directional female choice
      - initially the ornament signalled greater potential fitness (the likelihood of leaving more descendants), so preference for the ornament had a selective advantage
      - subsequently, if strong enough, female preference for exaggerated ornamentation in mate selection could be enough to undermine natural selection even when the ornament has become non-adaptive


## infinite games

- theory-of-mind agent games
  - how recursive (fractal?) models related to that


## simultaneous games

- atomic games (examples are so so)
  - coordination
    - 2 american drivers on a narrow road
    - shelling point: go right
  - battle of sexes
    - american and english driver
    - agreement
  - chicken
    - two arrogant drivers
  - prisoners dilemma
    - scheduling contract work for payment
    - could be nice to pay late, could be nice to deliver work late


## sequential games

- game tree
  - a useful way of reasoning about game and possible strategies
    - applicable to finite deterministic non-cooperative sequential games only
  - set of paths from root to terminal vertices in such tree represent possible strategies
  - rollback
    - a way of reasoning about the best strategy for a player
    - procedure
      - player choses strategies that include path that represents current state of a game
      - player selects terminal vertices of the paths represented by previously selected strategies
      - player picks vertex with the best payoff
      - player starts following strategy leading to selected vertex
  - rollback equilibrium
    - best strategy profile
    - right way to play sequential game of perfect information

- subgame
  - a subset of a game
  - a game tree of a subgame is a subtree of a game

- first mover advantage
  - true only if
    - all players perfectly rational
      - all have the same information about game
      - game rules and payoffs don't change
  - is actually a 'first mover highly probable advantage'
    - as there is a small chance that there is no advantage at all
      - when potential payoffs are the same for all players

- strategy profile
  - set of strategies that correspond to your actions in current and all possible future game states

- signalling and signal jamming
  - important parts of a game theory

- nash equilibrium
  - situation when no player will gain from unilaterally changing strategy
    - if everybody else is playing nash equilibrium, its rational to play it too
  - important to have one, otherwise
    - players will change their strategies whenever they like
    - game will be harder, more computationally expensive to play
  - not necessarily a best strategy, but can be viewed as an attractor where players 'stuck'
  - synonyms: focal point, schelling point 
    - at least they are used interchangeably in this article
    - https://www.lesswrong.com/posts/yJfBzcDL9fBHJfZ6P/nash-equilibria-and-schelling-points

- pareto efficiency 
  - situation where no individual or preference criterion can be better off without making at least 
    one individual or preference criterion worse off
  - related to nash equilibrium

- pareto superiority - an economic situation in which an exchange can be made that benefits someone 
  and injures no one, see https://www.legal-lingo.net/pareto-superiority/
  

## fundamentals

- game information types
  - perfect
    - full history of the game is known to all players
    - players know each other moves and state (figures, hand cards, etc)
    - example: chess
  - imperfect
    - history of the game and state of players is unknown or partially known
    - example: poker

- strategies
  - pure - defined deterministically, no randomness involved
  - mixed - involves stochastic (randomish) decision making in its rules
  - dominant - the best player can do no matter what other players doing

- game types
  - sequential vs simultaneous
    - sequential
      - time matters in this model
      - can use a 'game tree' concept
    - simultaneous (static)
      - players don't know what other players are doing
        - so that time dimension can be collapsed
  - cooperative vs non-cooperative
    - imply possibility of binding agreements between players
    - betrayal
  - finite vs infinite
  - deterministic vs stochastic
  - perfect vs imperfect information
    - perfect is when each player, when making any decision, is perfectly informed of all the events
      that have previously occurred
  
- lotteries 
  - are inherently inefficient for scenarios like redistribution of radio frequency spectums among companies
    - goals:
      - raising money while efficiently distributing spectrum ranges
        - silly question: raising money for what? 
          - i guess for financing auctions and related research ...
      - tried to avoid monopolies and redistribute resources to minority businesses
      - hired a bunch of game throrists ppl to design auction in order to settle on Schelling point
      - raised 400 billion dollars from the auction
  - ideas for scifi shorts: 
    - lotteries are efficient enough for 
      - milking citizens not familiar with math/stats/probability theory sciences
      - providing socially acceptible way for giving someone a big pile of cash (for whatever reasons)
        - the one who verifies fairness of a lottery is in control of triggering such scenario when needed
    
- threats, promises, commitments can be a part of the game as well

- coopetition 
  - one of the game theoretical models
  - act of cooperation between competing companies
  - businesses that engage in both competition and cooperation are said to be in coopetition
  - common in the technology industry, particularly between software and hardware firms.
  - are statistical models that consider the ways in which synergy can be created by partnering with competitors
  - aim of coopetition, and the model itself, is to move the market from a zero-sum game, where a single winner takes all, 
    to an environment in which the end result benefits the whole and makes everyone more profitable
  - develops understanding that leads to knowing which forces will make the players compete and which forces 
    will make them cooperate, and to what capacity
    
- attrition warfare (война на истощение) - is a military strategy consisting of belligerent attempts to win a war by 
  wearing down the enemy to the point of collapse through continuous losses in personnel and material
- books written 
  - "the strategy of conflict" by Thomas Schelling (1960)
    - Schelling won a nobel price for economics for his works

- sample game #2
  - there is an auction, you can bid to get 100$
  - the one who wins the auction - pays their bid and gets 100$
  - the second bidder should pay their bid as well, while getting nothing
  - game has a very high chance of attracting bids higher than 100$ 
  
- sample game #1
  - start with 100$
  - players: you and 100 other people of unknown identities
  - possible actions 
      - push a button
      - do not push a button
  - rules
    - if you push and no one else does - other players lose 2$
    - if you push and some other players push
      - you lose 2$ times number of other players who pushed the button
      - losses cut in half
  - properties
    - symmetric 
      - meaning that this game, its rules and its properties are 
        - known to everyone else
        - the same for everyone else
  - typical lines of reasoning
    - i'll be crazy to push, because we all know if no one is pushing everyone will get a 100$
    - i have to push in self-defence, as there are 100 people that i don't know playing this, someone is likely going to push
    - i'm not going to push because it is a morally right thing to do
    - i'll push to stir things up, we'll see what happens, 100$ is not that much money
    - i'll push, as if others push and i don't - everyone else will be ahead of me (competitive)
  - among those lines of reasoning, which ones are rational?
  - instance of a game structure called 'the tragedy of the commons'
    - other instances: global warming, overfishing, traffic conjestion

- game usually has
  - players
  - strategies
    - each player has a set of strategies, how they will respond
    - specifies what decision you will make in evey possible situation that you may find yourself
  - payoffs
    - specify how reward will be distributed among players
  - common knowledge
    
- game theory - is a study of strategic interactions among the rational decision makers



## references

- tgc game theory course by prof Scott P. Stevens 
