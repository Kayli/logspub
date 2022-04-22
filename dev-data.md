# notes about data formats, management system and related stuff

## some popular databases

- types
  - relational: sqlite, postgresql, mysql, mssql, oracle
  - aggregate
    - document: mongodb, raven, couch
    - key-value: riak, redis, etcd
  - graph: neo4j
  - column: cassandra, hbase
  - cloud native
    - amazon RDS, SimpleDB, DynamoDB
    - azure Cosmos DB, SQL Database


## migrations

- relational database strategies [^3]
  - with downtime
    - run db up-migration script using automatic migrations framework
    - down-migration scripts are not that useful in practice
  - without downtime
    - migrate new version of app to db schema compatible with old application
    - switch to new version of application
    - remove compatability artifacts of migration left after the first step
  
- document database strategies [^4]
  - with downtime: write an upgrade script
  - without downtime
    - incrementally update your documents as they are used
      - pitfalls: 
        - queries against a schema where half the documents are version 1 
          and half the documents are version 2 can cause problems, therefore it may be 
          useful to run a migration script in a background to update all documents asap
        - any incremental upgrade code must stay in the code-base until all the documents have been upgraded


## orms

- python
  - sqlalchemy
    - allow returning data from disconnected entities (closed session)
      - session.expire_on_commit = False
    - sqlite+pysqlite does not support Decimal objects natively
      - possible loss of data
    - json types
      - PostgreSQL, SQLite as of version 3.9
      - supports JSON SQL operations
      - allows nested selectors into json column [^2]
- dotnet
  - entity framework
  - nhibernate


## streamable data formats

- motivation
  - wiki articles on a topic suck for unknown reason :/
    - phds were too busy to write that shit in an easily digestible manner ... as usual
    - so i have to write that trivia that follows below

  - data is too large to be transmitted in a one go while partially transmitted data is usable on the receiver side
    - data may be a potentially infinite, e.g. sensor data or stream of digits for PI

- solution
  - data chopped into separate "chunks" to be transmitted while being
    - indifferent to its internal structure
      - stream of bytes chopped based on size of some buffer
    - considering its internal structure, e.g.
      - time series
      - graph vertices and edges

- chunk types
  - network packet
    - formatted unit of data carried by a packet-switched network
    - consists of control information and user data/payload
  - message
    - used by systems that implement publish-subscribe pattern
    - message passing
      - invoking program sends a message to a receiver (process/object)
      - relies on that receiver and its supporting infrastructure to then select and run some appropriate code

- streamable data formats
  - binary
  - human readable
    - yaml
        - "is intended to be read and written in streams" [^1]


## document dbs

- schema versioning pattern

- referencing approaches
  - one-to-one
    - embedded
    - linked: cross-reference in both entities
  - one-to-many
    - embedded in parent
    - array in parent
    - scalar in child

- mongodb supports
  - optional schema validation
  - referential constraints using dbref
    - works across documents, shards and databases within same cluster


## references

[^1]: https://en.wikipedia.org/wiki/YAML
[^2]: https://stackoverflow.com/questions/31197813/sqlalchemy-filtering-nested-json-data-in-postgresql-jsonb
[^3]: https://www.youtube.com/watch?v=ka-PLyjV3AI
[^4]: https://mongodb.github.io/mongo-csharp-driver/2.4/reference/bson/mapping/schema_changes/
