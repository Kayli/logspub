# notes about distributed systems and related topics

## basics

- use docker and kubernetes to decompose and modularize applications
- explore enterprise integration patterns and frameworks implementing them ;)
- prefer cloud-vendor-neutral technologies


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
  - buses should be trivial to use

- end-to-end ownership of a service [^3]
  - closed loop: architect -> design -> develop -> review -> test -> deploy -> run -> support -> architect ...
  - teams are loosely coupled, each iterating their own process


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


## kubernetes k8s

- to run locally 
  - minikube (cli only)
  - rancher desktop (cli+gui)
    - kim is a wrapper for docker commands

- key entities
  - node
    - controller
    - worker
  - pod
  - service
    - takes care of service discovery, allowing to expose fixed ip and dns endpoint
    - see selector and load-balancer mechanisms
    - when a pod is run on a node, the kubelet adds a set of environment variables for each active service
  - replica set
    - defines how many pod instances we need across cluster
  - deployment
    - yaml with desired state
    - defines/configures pods and replica sets via deployment controller
    - abstraction on top of pods
  - volume
    - local or remote storage for stateful apps
  - stateful set
    - provides replication services for volumes

- databases
  - etcd
    - distrubuted key-value store 
    - uses raft consensus algorithm to elect master node for writes

  - kubegres [^5]
    - postgresql cluster operator
    - manages fail-over 
    - has a data backup option allowing to dump PostgreSql data regularly in a given volume

- patterns
  - sidecar
    - there are 2 containers in a single pod
      - main app
      - sidecar
    - goal: augment functionality of main app in some way


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


## tracing tools

- packet sniffers
  - wireshark: tcp/udp traffic

- http(s)
  - fiddler: for http traffic
  - mitmproxy: has python api


## testing

- faking service dependencies: hoverfly and others

- performance/load testing
  - tools: jmeter, gatling, jmeter, flood.io

- security testing
  - findsecbugs, bdd-security, arachni, gauntlt, serverspec, docker bench for security, clair

- destructive testing automation: chaos monkey approach


## security

- static vulnerability analysis for docker images
  - snyk, etc.


## infrastructure as code

- https://medium.com/style-theory-engineering/infrastructure-as-code-kubernetes-a2f050389f26


## data

- cassandra
  - nosql
  - sypports async replication of data across regions


## some techs to uncover

- databases: cassandra
- security testing: findsecbugs, bdd-security, arachni, gauntlt, serverspec, docker bench for security, clair
- performance/load testing: gatling, jmeter, flood.io


## references

[^1]: https://www.youtube.com/watch?v=-4sHUvfk2Eg
[^2]: https://www.youtube.com/watch?v=STKCRSUsyP0 (martin fowler goto 2017)
[^3]: https://www.youtube.com/watch?v=57UK46qfBLY
