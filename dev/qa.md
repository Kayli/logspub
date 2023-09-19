# notes related to quality assurance practices in software

## basics

- synthetic testing (synthetic monitoring, proactive monitoring)
  - is a method of understanding a user’s experience of your application
  - is a way to identify performance issues with key user journeys and application endpoints before they degrade user experience
  - connect to test servers (usually in different locations around the world) and use behavioral scripts to simulate the typical actions of end-users

- functional testing
  - tests individual features or functions of the software application
  - ensures that functions are working as per the specified functional requirements
  - does not imply that you are testing a function (method) of your module or class
  - subtypes
    - smoke testing, sanity testing
    - regression testing
    - usability testing

- non-functional testing
  - tests software application's non-functional aspects, such as performance, usability, security, scalability, and compatibility

- phases of testing
  - unit testing
  - integration testing
  - system testing 
    - conducted on a complete integrated system to evaluate the system's compliance with its specified requirements

- build verification test
  - is a set of tests run on every new build
  - verifies that build is testable before it is released to test team for further testing
  - runs core functionality test cases that ensure application is stable and can be tested thoroughly


## test doubles

- definition: object that substitutes one of the components in integration testing

- main purposes
  - setup initial conditions and dynamic behaviour for test scenarios
  - isolate SUT from external dependencies

- can be of several different types
  - stub: dumbest of three, always returns same values
  - spy: like stub, but also records calls
  - fake: can have some logic based on input parameters
  - mock: most advanced, allows dynamic configuration of simulated behaviour, verification policies, flexible assertion constraints and other cool stuff


## clusters

- failure scenarios
  - more than half of the cluster nodes lose connection with the cluster, resulting in quorum loss
    - cluster recovery process may be involved
    - it better be automated and tested beforehand


## performance testing

- load testing: performance assessment under given average load
- stress testing: system stability under extreme conditions
- soak testing: reliability over a longer period of time
- spike Testing: simulates huge spike of load on a very short period of time


## frameworks

- jmeter
- selenium
- nunit, xunit
- mockoon https://github.com/mockoon/mockoon/
  - mocking framework written in typescript
  - provides npm packages to run as mock server

