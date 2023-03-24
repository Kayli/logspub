# notes about data formats, management system and related stuff

## basics

- database is a stateful application

- time to glass
  - time between the moment when an event happens and the point when a platform issues an alert


## some popular databases

- types
  - relational: sqlite, postgresql, mysql, mssql, oracle
  - aggregate
    - document: mongodb, raven, couch
    - key-value: riak, redis, etcd
  - graph: neo4j, dgraph
  - column: cassandra, hbase
  - full-text search engines
    - apache lucene based: solr and elastic search
    - algolia, meilisearch
  - cloud native
    - amazon rds, simpledb, dynamodb
    - azure cosmos db, sql database
    - newrelic (nrdb)
  - multimodel: faunadb
  - timeseries: influxdb, newrelic (nrdb)


## scaling

- allows to handle larger amounts of traffic (requests)
- types
  - vertical
  - horizontal
    - instead of single server you have set of nodes forming a cluster
    - load balancer distributes requests among cluster nodes
    - nodes can replicate data to increase availability and fault tolerance

- replication types
  - master/slave
    - single master, many readonly replicas
    - only master nodes can handle writes
    - all writes are redirected to a single master node in a cluster
  - multimaster/masterless
    - any node can handle reads and writes


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


## caching

- write-through: write is done synchronously both to the cache and to the backing store
- write-back (write-behind)
  - initially, writing is done only to the cache. 
  - write to the backing store is postponed until the modified content is about to be replaced by another cache block


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


## relational dbs

- sqlite
  - gui tools: dbbrowser

- object relational mappers (orms)
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


## relational

- postgresql
  - binary data storage types
    - bytea data type
      - up to 1 GB of binary data
    - large object
      - stores the binary data in a separate table in a special format
      - refers to that table by storing a value of type oid in your table

- mysql
  - binary data types
    - BLOB ≈ 64KB, MEDIUMBLOB ≈ 16MB and LONGBLOB ≈ 4GB
  - mysql cluster supports sharding
  - supports document storage
  - mariadb is a fork after mysql been aquired by oracle

- mssql
  - can run on linux: https://hub.docker.com/_/microsoft-mssql-server
  - dockerize .dbproj https://medium.com/@stepan.chubanian/dockerize-ms-sql-with-ssdt-on-windows-31c570e8d88d


## document dbs

- schema versioning pattern
  - you can store/retrieve documents with slightly different schemas from the same collection
  - application is responsible for extracting correct data based on schema version field

- referencing approaches
  - one-to-one
    - embedded
    - linked: cross-reference in both entities
  - one-to-many
    - embedded in parent
    - array in parent
    - scalar in child

- mongodb
  - 16mb max document size limit
  - optional schema validation
  - referential constraints using dbref
    - works across documents, shards and databases within same cluster
  - $lookup
    - similar to join in sql
  - guis
    - atlas
      - data explorer
      - allows automating database administration tasks such as database configuration, 
        infrastructure provisioning, patches, scaling events, backups, etc.
    - compass
  - gridfs
    - is a specification for storing and retrieving files that exceed the BSON-document size limit of 16 MB
    - supports sharding


## key-value stores

- classification
  - consistency and partition tolerance (cp)
  - availability and partition tolerance (ap)

- zookeeper
- etcd
  - quite specific to k8
  - uses lmdb, a software library behind the scenes that provides an embedded 
    transactional database in the form of a key-value store


## column stores

- cassandra
  - flexible schemas
  - async replication only
    - eventually consistent
    - it takes some (small) time for writes to propagate across cluster nodes
    - so there is a chance of reading stale data
  - enables fast data aggregations, as its column-based
  - multi-master system by default
    - high availability
    - horizontal scaling
    - high concurrency
  - supports async replication of data across regions
  - cassandra query language (cql)
  - nosql
  - sypports async replication of data across regions


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
    - real-time transport protocol (rtp) 
  - human readable
    - yaml
        - "is intended to be read and written in streams" [^1]


## references

[^1]: https://en.wikipedia.org/wiki/YAML
[^2]: https://stackoverflow.com/questions/31197813/sqlalchemy-filtering-nested-json-data-in-postgresql-jsonb
[^3]: https://www.youtube.com/watch?v=ka-PLyjV3AI
[^4]: https://mongodb.github.io/mongo-csharp-driver/2.4/reference/bson/mapping/schema_changes/
[^5]: https://youtu.be/QhfuzEkN3Ck?t=935
