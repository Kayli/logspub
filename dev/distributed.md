# notes about distributed systems and related topics

## basics

- distributed system consists of multiple apps communicating with each other over the network
  - most ppl start to realize problems with big chunks of tangled code

- conway’s law
  - application will reflect the social boundaries of the organization that produced it
  - but you may want to build the boundaries the way you want the company to be organized
    - because the way it is organized now may be not optimal

- container orchestrator
  - definition: automated configuration, coordination, and management of containers and supporting infrastructure
  - typical tasks
    - container scheduling/placement
    - failover (containers, nodes, management)
    - load balancing
    - service discovery
    - overlay networks
    - storage (distributed, persistent)
    - secret management
    - scaling, autoscaling
    - cli and rest api
    - deployment configuration as code
    - role-based access control (rbac)
      - a policy-neutral access-control mechanism defined around roles and privileges

- rolling restart
  - the standard procedure for deploying software changes while maintaining availability throughout


## general design recommendations

- use docker and kubernetes to decompose and modularize applications
- explore enterprise integration patterns and frameworks implementing them
- prefer cloud-vendor-neutral technologies

- consider introducing homogenety of tools across teams
  - rpc: common language between services to establish unified contract for interaction
  - ci/cd

- encourage team autonomy, freedom and responsibility
  - splitting the ownership of the code is an important part of ms architecture

- each microservice owns its logic and data under an autonomous lifecycle, with independent deployment per microservice

- it should be easy to rewrite microservice
  - its normal to do that several times, always adapting to business requirements

- data duplication is okay, when necessary

- if your microservice absolutely have to call other service
  - limit sync call chain to 1 other ms dependency call max
  - consider reversing dependency using events


## patterns [2]

- ambassador
  - used in distributed systems or microservices architectures
  - helps in offloading certain responsibilities related to network communication from the main business logic, promoting better separation of concerns

- circuit breaker
  - prevents failures by proxying requests and handling errors of the remote services
  - accumulates error stats and provides canned response when failure treshold is reached

- leader election
  - allows coordination of activities in a cluster by electing a leader node
  - consensus algorithms: paxos, raft, bully

- pubsub
- sharding
- strangler fig: replacing legacy systems with new implementations

- event notification
  - pubsub using events
  - events contain some information about state
  - notify system about state change in a decoupled manner
  - disadvantages: harder to track effects of a change

- event-carried state transfer
  - requirement for the event to contain all necessary information to reconstruct state after change
  - disadvantages: events may become heavy

- event sourcing
  - all events are persisted in event store
  - application state can be fully reconstructed from the sequence of events
  - possible disadvantages
    - storing events can consume 2-3 orders of magnitude more storage than storing state

- schema registry
  - component that helps with schema verification before publishing message to a pipe
  - arbitrates the contract between publishers and subscribers
  - see more at dev-messaging.md

- cqrs
  - commands and queries have different state representations
  - simplifies representation, increases performance
  - disadvantages: likely data duplication, eventual consistency

- dumb pipes
  - buses should be trivial to use, in that sense they should be 'dumb'
  - if some optimization is possible - thats okay, but pipes should not dictate much

- transactional outbox [4]
  - safely save messages into a database before sending them asynchronously
  - sending is usually done by some other service

- end-to-end ownership of a service [3]
  - closed loop: architect -> design -> develop -> review -> test -> deploy -> run -> support -> architect ...
  - teams are loosely coupled, each iterating their own process

- micro frontend [8]
  - for react apps see 'module federation plugin'

- api gateway
  - useful for data aggregation from multiple microservices that own different databases
  - improves security by reducing attack surface
  - can hide infrastructural complexities and provide simpler communication interface
  - should never call another api gateway
  - alternatives: materialized view, cqrs


## antipatterns

- vague/meaningless terms
  - service-oriented architecture
  - event-driven architecture?

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
    - for example, react and angular — in the same "single-page" application. 
  - although this might be technically possible, it is far from advisable when not part of a deliberate transition strategy


## splitting a monolith

- be clear and precise about why you want to rearchitect a project
  - better be supported with metrics when possible, and not just fashion or intuition

- make sure functionality that you want to split out is covered with functional tests
  - this will allow to verify that extracted service works the same way 

- typical reasons 
  - parts of the system need to be deployed independently of others [11]
  - monolithic release is too slow, too complicated [11]
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

- dapr (distributed application runtime) [1]
  - unified wrapper for typical cloud services
  - rpc, configuration, instrumentation
  - pubsub
    - can use redis for pubsub
      - run in 'append only file' mode with fsync at every query to provide stong guarantees
  - key-value store
    - use to store shared configuration
  - telemetry: zipkin, open telemetry


## rpc/apis

- key aspects
  - adoption
  - introspection
  - observability

- load balancing [6]
  - client-side
  - server-side/proxy: dns, nginx, haproxy, consul, envoy

- solutions
  - rest
    - industry most popular choice for apis
    - openapi provides observability and introspection even across heterogeneous stack

  - graphql
    - queryable apis
    - reduces amount of work required on server side, when you need richer queries support
    - provides introspection over its schema [5]

  - grpc
    - provides unified way of communication between services
    - simple idl
    - many generators from idl to popular languages
    - grpc-web extends same approach to web-apis as well
    - supports tls encryption of all traffic

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
  - kinesis: simpler to manage and lower costs than kafka [9]

- microsoft [7]
  - azure 
    - event hub
      - can maintain the order of the events in the same partition
      - partitioning allows for multiple parallel logs to be used for the same event hub 
        - therefore multiplying the available raw io throughput capacity
      - has kafka api
    - event grid
      - doesn’t guarantee the order of the events
      - does not support partitions
      - some features overlap with event hub
    - service bus
      - the messages are pulled out by the receiver & cannot be processed again
      - uses the terminology of queues and topics
      - some features overlap with event hub and event grid
    - hdinsight kafka
      - managed native kafka service in azure
  - service bus for windows
  - msmq (deprecated)


## tracing/monitoring

- elk stack
  - logstash: used for publishing and transforming logs
  - elastic search: used for storing and indexing logs
  - kibana: used as a dashboard on top of elastic search

- if you ever need to ssh into a machine with a service, it likely means that monitoring failed you

- tools
  - packet sniffers
    - wireshark: tcp/udp traffic

  - http(s)
    - fiddler
    - postman
    - mitmproxy: has python api
  
  - service meshes: istio, envoy
  
  - infrastructure monitoring
    - azure monitor/app insights
    - aws cloudwatch
    - k8s prometheus + grafana
    - zabbix


## testing

- faking service dependencies: hoverfly and others

- performance/load testing
  - tools: jmeter, gatling, flood.io

- security testing
  - findsecbugs, bdd-security, arachni, gauntlt, serverspec, docker bench for security, clair

- destructive testing automation
  - chaos monkey approach
  - simulate regularily
    - instances failure
    - whole region failures 


## security

- static vulnerability analysis for docker images
  - snyk, veracode, SonarQube, owasp dependency check, etc.


## high availability

- consistent hashing ring algorithm
  - minimizes number of keys need to be remapped when hash table is resized

- 3 and 5 node clusters make most practical sense [12]
  - they shouldn't be 
    - too far away from each other: cluster performance may degrade
    - too close to each other: so that disaster is likely to influence only one

- cluster synchronozation protocols
  - paxos
    - family of protocols for solving consensus in a network of unreliable or fallible processors
  - raft
    - consensus algorithm that is designed to be easy to understand
    - it's equivalent to paxos in fault-tolerance and performance
    - difference is that it's decomposed into relatively independent subproblems, 
      and it cleanly addresses all major pieces needed for practical systems
  - zab
    - crash-recovery atomic broadcast algorithm for the zookeeper coordination service
  - gossip
    - maintains table with memberid and heartbeat counter for every node
    - periodically sends heartbeat requests to random? nodes in a cluster

- leader election
  - tbd: define scenarios, determine which cluster sync protocols need to elect a leader

- state synchronization
  - merkle tree (hash tree)
    - leafs are usually data blocks
    - can be viewed as commitment scheme, in which the root of the tree is seen as a commitment and leaf nodes may be revealed and proven to be part of the original commitment


## content delivery network (cdn) services

- commercial offerings
  - amazon cloudfront
  - cloudflare
  - akamai
  - microsoft azure cdn

- point of presence server (pop, edge)
  - servers distributed geographically to provide higher latency
  - cache static as well as dynamic content
  - uses either dns or unicast routing

- provide protection against ddos attacks, by distributing content across many nodes, avoiding spof 
- supports automatic minification of js, css and html files


## high performance computing (hpc)

- work performed on clusters of computers often referred as 'nodes'
    - use either high-performance multi-core CPUs or, more likely today, GPUs
  - centralized scheduler manages the parallel computing workload
  - clusters may include 100,000 or more nodes
  - lower-latency, higher-throughput RDMA networking
    - RDMA—remote direct memory access
    - enables one networked computer to access another networked computer’s memory 
      - without involving either computer’s operating system 
      - or interrupting either computer’s processing
- cuda model 
  - can effectively utilize only gpu loads
    - this contrasts with opencl, which can use both gpu and cpu for parallel processing
  - sharing data between multiple gpu devices
    - via shared memory, 'unified addressing' feature
      - 'pinned' memory is a non-pageable memory on the host
      - need to clone data from pageable memory to pinned, before copying to device
    - via events
  - kernel
    - function (void only)
    - launched, usually by the host or sometimes from another kernel
    - executed asynchronously (non blocking the host) on the device
  - device function
    - just a function that runs on cuda-managed device
    - can be called by kernel or other device function
    - can't be called from host
  - computation
    - ilp: instruction-level parallelism
    - stream
      - sequence of kernels or CUDA commands that execute in order
        - possibly issued by different host threads
      - within single 'stream' kernels are executed sequentially
      - you can have multiple streams running in-parallel
    - other primitives: grid, block, warp, thread


## 12 factor app principles [13]

codebase: one codebase tracked in version control, many deploys.
dependencies: explicitly declare and isolate dependencies.
config: store configuration in the environment.
backing services: treat backing services as attached resources.
build, release, run: strictly separate build and run stages.
processes: execute the app as one or more stateless processes.
port binding: export services via port binding.
concurrency: scale out via the process model.
disposability: maximize robustness with fast startup and graceful shutdown.
dev/prod parity: keep development, staging, and production as similar as possible.
logs: treat logs as event streams.
admin processes: run admin/management tasks as one-off processes.



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

- daily active users (DAU)

- hostile multitenancy
  - describes hosting platforms that must provide strict resource governance and security isolation between different customers
  - in contrast, 'enterprise multitenancy' assumes internal customers with good intent and reactive controls


## references

[1]: https://www.youtube.com/watch?v=-4sHUvfk2Eg
[2]: https://www.youtube.com/watch?v=STKCRSUsyP0 (martin fowler goto 2017)
[3]: https://www.youtube.com/watch?v=57UK46qfBLY
[4]: https://microservices.io/patterns/data/transactional-outbox.html
[5]: https://spec.graphql.org/June2018/#sec-Introspection
[6]: https://medium.com/swlh/scaling-microservices-with-grpc-and-envoy-proxy-part-2-148f589b2a83
[7]: https://stackoverflow.com/questions/57740782/message-bus-vs-service-bus-vs-event-hub-vs-event-grid
[8]: https://micro-frontends.org
[9]: https://www.youtube.com/watch?v=TJS19EuzH2k
[10]: https://www.semanticscholar.org/paper/Zab%3A-High-performance-broadcast-for-primary-backup-Junqueira-Reed/b02c6b00bd5dbdbd951fddb00b906c82fa80f0b3?p2df
[11]: https://www.youtube.com/watch?v=9vS7TbgirgY
[12]: https://www.youtube.com/watch?v=PRsB6HzQ_ss
[13]: https://12factor.net/