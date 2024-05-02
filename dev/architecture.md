# notes about software architecture design

## basics

- oop
- solid
- tdd
- design patterns and antipatterns
- ddd


## best practices

- start with an idea, but assume its wrong (be humble) [1]
  - so that when you find where its wrong - you can correct it


## modeling tools

- declarative diagrams 
  - c4 https://c4model.com/
  - websequencediagrams https://www.websequencediagrams.com/
  - mermaid https://mermaid.js.org/intro/


## microservices

- pros
  - each unit is simple
  - independent scaling
  - independent deployment
  - own their own persistence
  - optimal technology stack
  - security boundary
- cons
  - multiple cooperating units
  - exchange in-process for network latencies
  - more sophisticated deployment and monitoring
  - higher overall system complexity

- splitting monolith
  - database
    - functional partitioning
    - sharding
  - graphical user interface
    - microfrontends


## backups

- 3-2-1 backup strategy [2]
  - you should have 3 copies of your data (your production data and 2 backup copies) 
    - on two different media (disk and tape)
    - with one copy off-site for disaster recovery


## references

[1]: https://www.youtube.com/watch?v=Qv92qaIGbDg
[2]: https://youtu.be/QsM6b5yix0U?si=gAsQaGplKvnf3ZIP&t=361