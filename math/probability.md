# some notes on probability theory

## basics

- median
  - middle number, when those numbers are listed in order from smallest to greatest
  - for odd number of elements its a single number
  - for even number of elements its an average between two middle elements

- mean, simple average: sum of all elements divided by total number of all elements

- random variable
  - can take a continuum of values in a continuous space
  - often described by probability density function (pdf)

- normal distribution, gaussian distribution
  - a type of continuous probability distribution for a real-valued random variable
  - assumes we operate with a scalar value

- multivariate: normal distribution over a vector (not a scalar)

- joint distribution
  - independent
    - p(x,y) = p(x) * p(y)
  - dependent, conditional probability
    - describes relationships between dependent events
    - p(x|y) = p(x,y) / p(y) 
    - reads as probability of event x given that event y already happened

- bayes rule
  - relates conditional of type p(x|y) to its inverse p(y|x)
  - p(x|y) = (p(y|x) * p(x)) / p(y)



## spread

- for a set of values defines how far values diverge from their mean

- mean absolute deviation (MAD), mean absolute error (MAE) [4]
  - it corresponds to "real life" much better than sd
  - is more accurate in sample measurements
  - less volatile than STD since it is a natural weight whereas standard deviation uses the observation itself as its own weight, imparting large weights to large observations, thus overweighing tail events
  - most natural measure of spread

- standard deviation
  - alternative names: sd, sigma, среднеквадратичное отклонение
  - sd = sqrt(variance)
  
- variance
  - alternative names: sigma^2, дисперсия
  - variance = 1/N * sum((x - mean)^2)
  - has the additive property when dealing with random variables [6]
  

## interpretations

- physical
  - related terms: , objective or frequency probabilities
  - are associated with random physical systems
    - examples: roulette wheels, rolling dice and radioactive atoms

- evidential (bayesian)
  - main types
    - classical (Laplace's)
    - subjectivist
    - epistemic (inductive)
  - can be assigned to any statement whatsoever, even when no random process is involved
    - represents its subjective plausibility
    - or the degree to which the statement is supported by the available evidence


## references

- https://en.wikipedia.org/wiki/Probability_interpretations
- https://www.coursera.org/learn/probability-theory-statistics
- https://en.wikipedia.org/wiki/Sunrise_problem
[4]: https://stats.stackexchange.com/questions/118/why-square-the-difference-instead-of-taking-the-absolute-value-in-standard-devia?rq=1