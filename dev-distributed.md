# notes about distributed systems and related topics

## basics

- distributed system consists of multiple apps communicating with each other over the network
  - nowadays such apps referred as 'microservices'
  - most ppl start to realize problems with big chunks of tangled code

- conway’s law
  - application will reflect the social boundaries of the organization that produced it
  - but you may want to build the boundaries the way you want the company to be organized
    - because the way it is organized now may be not optimal


## general design recommendations

- use docker and kubernetes to decompose and modularize applications
- explore enterprise integration patterns and frameworks implementing them
- prefer cloud-vendor-neutral technologies

- consider introducing homogenety of tools across teams
  - rpc: common language between services to establish unified contract for interaction
  - ci/cd

- encourage team autonomy, freedom and responsibility
  - splitting the ownership of the code is an important part of ms architecture

- each microservice own its logic and data under an autonomous lifecycle, with independent deployment per microservice.

- it should be easy to rewrite microservice
  - its normal to do that several times, always adapting to business requirements

- data duplication is okay, when necessary

- if your microservice absolutely have to call other service
  - limit sync call chain to 1 other ms dependency call max
  - consider reversing dependency using events


## patterns [^2]

- event notification
  - pubsub using events
  - notify system about state change in a decoupled manner
  - disadvantages: harder to track effects of a change

- event-carried state transfer
  - requirement for the event to contain all necessary information to reconstruct state after change
  - disadvantages: events may become heavy

- event sourcing
  - asynchrony complicates things, but it is not a reuquirement for es

- cqrs
  - commands and queries have different state representations
  - simplifies representation, increases performance
  - disadvantages: likely data duplication, eventual consistency

- dumb pipes
  - buses should be trivial to use, in that sense they should be 'dumb'
  - if some optimization is possible - thats okay, but pipes should not dictate much
  - ideally they should adapt to demands of the applications they use
    - they should autoconfigure based on usage pattern

- transactional outbox [^4]
  - safely save messages into a database before sending them asynchronously
  - sending is usually done by some other service

- end-to-end ownership of a service [^3]
  - closed loop: architect -> design -> develop -> review -> test -> deploy -> run -> support -> architect ...
  - teams are loosely coupled, each iterating their own process

- micro frontend [^8]
  - react: 'module federation plugin'

- api gateway
  - useful for data aggregation from multiple microservices that own different databases
  - improves security by reducing attack surface
  - should never call another api gateway
  - alternatives: materialized view, cqrs


## antipatterns

- vague/meaningless terms
  - service-oriented architecture, event-driven architecture

- integration database

- using bleeding edge technological stack
  - very risky for big projects

- beware of bias and heuristics
  - evaluate tech/architectural decisions for each specific business case
    - unless you had exactly the same combo of context + task in the past with now known solution
  - make sure to be able to unpack buzzwords in order to understand whats behind the curtain

- rudimentary observability
  - lack of metrics, logging, tracing collection and management
  - significantly hinders investigation of problems

- politics
  - company > team > self
  - happen when
    - you put your priorities higher than team's or company's
    - team puts its priorities higher than company's

- micro frontend anarchy
  - a particularly egregious form of this syndrome is using multiple frontend frameworks 
    - for example, React.js and Angular — in the same "single-page" application. 
  - although this might be technically possible, it is far from advisable when not part of a deliberate transition strategy


## splitting a monolith

- be clear and precise about why you want to rearchitect a project
  - better be supported with metrics when possible, and not just fashion or intuition

- make sure functionality that you want to split out is covered with functional tests
  - this will allow to verify that extracted service works the same way 

- typical reasons 
  - parts of the system need to be deployed independently of others [^11]
  - monolithic release is to slow, too complicated [^11]
  - reducing risks of evolving/rewriting application when its time

- residual monolith
  - you can leave old app in place for infinitely long
  - contains functionality with lowest business value
  - most stable and least changing


## kubernetes k8s

- container orchestrator framework
- see more at at dev-distributed-k8.md


## abstraction for cloud infrastructure

- must have layer to decouple from specific vendors

- dapr (distributed application runtime) [^1]
  - unified wrapper for typical cloud services
  - rpc, configuration, instrumentation
  - pubsub
    - can use redis for pubsub
      - run in 'append only file' mode with fsync at every query to provide stong guarantees
  - key-value store
    - use to store shared configuration


## rpc/apis

- key aspects
  - adoption
  - introspection
  - observability

- load balancing [^6]
  - client-side
  - server-side/proxy: dns, nginx, haproxy, consul, envoy

- solutions
  - rest
    - industry most popular choice for apis
    - cons: lacks standardization
      - therefore unified observability and introspection is hindered across heterogeneous stack

  - graphql
    - queryable apis
    - reduces amount of work required on server side, when you need richer queries support
    - provides introspection over its schema [^5]

  - grpc
    - provides unified way of communication between services
    - simple idl
    - many generators from idl to popular languages
    - grpc-web extends same approach to web-apis as well

  - envoy
    - creates observable service-mesh
    - supports load balancing
    - enables grpc-web
    - implements retries and circuit-breaker patterns


## service mesh

- definition
  - dedicated infrastructure layer for facilitating service-to-service communications between services 
    or microservices, using a proxy

- typical features
  - proxying and monitoring traffic among service nodes
    - deriving a real-time preformance profile of a system
  - augmenting service behaviors
    - traffic rerouting and splitting
    - simulating failures
    - auto-retries
    - circuit-breaker

- popular products: istio, envoy


## pipes

- rabbitmq
- kafka
- nservicebus

- amazon
  - simple queue service (sqs)
    - polling model for subscibers
    - persistance for messages of the subscriber
    - you need a new queue for every subscriber
    - oldest aws messaging service
  - simple notification service (sns)
    - supports fan out (multiple subscribers)
    - but has no persistance for subscribers
  - event bridge
    - newest aws messaging service
    - similar to sns, but provides more service integrations out of the box
  - msk: managed service for kafka
    - you need to only manage scaling manually
  - kinesis: simpler to manage and lower costs than kafka [^9]

- microsoft [^7]
  - azure 
    - event hub
      - can maintain the order of the events in the same partition
      - partitioning allows for multiple parallel logs to be used for the same event hub 
        - therefore multiplying the available raw io throughput capacity
    - event grid
      - doesn’t guarantee the order of the events
      - does not support partitions
      - some features overlap with event hub
    - service bus
      - the messages are pulled out by the receiver & cannot be processed again
      - uses the terminology of queues and topics
      - some features overlap with event hub and event grid
  - service bus for windows
  - msmq (deprecated)


## tracing/monitoring

- if you ever need to ssh into a machine with a service, it likely means that monitoring failed you

- tools
  - packet sniffers
    - wireshark: tcp/udp traffic

  - http(s)
    - fiddler
    - postman
    - mitmproxy: has python api
  
  - service meshes: istio, envoy



## testing

- faking service dependencies: hoverfly and others

- performance/load testing
  - tools: jmeter, gatling, jmeter, flood.io

- security testing
  - findsecbugs, bdd-security, arachni, gauntlt, serverspec, docker bench for security, clair

- destructive testing automation
  - chaos monkey approach
  - simulate regularily
    - instances failure
    - whole region failures 


## security

- static vulnerability analysis for docker images
  - snyk, etc.





## cluster synchronozation protocols

- paxos
  - family of protocols for solving consensus in a network of unreliable or fallible processors

- raft
  - consensus algorithm that is designed to be easy to understand
  - it's equivalent to paxos in fault-tolerance and performance
  - difference is that it's decomposed into relatively independent subproblems, 
    and it cleanly addresses all major pieces needed for practical systems

- zab
  - crash-recovery atomic broadcast algorithm for the zookeeper coordination service

## some techs to uncover

- databases: cassandra
- deployment: spinnaker
- fallback: envoy, hystrix
- security testing: findsecbugs, bdd-security, arachni, gauntlt, serverspec, docker bench, clair
- performance/load testing: gatling, jmeter, flood.io





## terminology

- network operations centers (NOCs)
  - are central locations from which an organization supports its computer network and telecom infrastructure

- site reliability engineering (SRE)
  - can be viewed as a specific implementation of devops
  - responsibilities
    - availability, latency, performance, efficiency, change management, monitoring, emergency response, capacity planning


## references

[^1]: https://www.youtube.com/watch?v=-4sHUvfk2Eg
[^2]: https://www.youtube.com/watch?v=STKCRSUsyP0 (martin fowler goto 2017)
[^3]: https://www.youtube.com/watch?v=57UK46qfBLY
[^4]: https://microservices.io/patterns/data/transactional-outbox.html
[^5]: https://spec.graphql.org/June2018/#sec-Introspection
[^6]: https://medium.com/swlh/scaling-microservices-with-grpc-and-envoy-proxy-part-2-148f589b2a83
[^7]: https://stackoverflow.com/questions/57740782/message-bus-vs-service-bus-vs-event-hub-vs-event-grid
[^8]: https://micro-frontends.org
[^9]: https://www.youtube.com/watch?v=TJS19EuzH2k
[^10]: https://www.semanticscholar.org/paper/Zab%3A-High-performance-broadcast-for-primary-backup-Junqueira-Reed/b02c6b00bd5dbdbd951fddb00b906c82fa80f0b3?p2df
[^11]: https://www.youtube.com/watch?v=9vS7TbgirgY
