# notes about distributed systems and related topics

## basics

- use docker and kubernetes to decompose and modularize applications
- explore enterprise integration patterns and frameworks implementing them ;)
- prefer cloud-vendor-neutral technologies
- ensure homogenety of tools across teams
  - rpc: common language between services to establish unified contract for interaction
  - ci/cd
- encourage team autonomy, freedom and responsibility
  - splitting the ownership of the code is an important part of ms architecture
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
  - buses should be trivial to use

- transactional outbox [^4]
  - safely save messages into a database before sending them asynchronously
  - sending is usually done by some other service

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

- destructive testing automation
  - chaos monkey approach
  - simulate regularily
    - instances failure
    - whole region failures 


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
