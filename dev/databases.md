# notes about data formats, management system and related stuff

## basics

- datalake
  - centralized repository
  - designed to store, process, and secure large amounts of data 
  - supports structured, semistructured, and unstructured data
  - no transactional support

- datamesh
  - usually faster than datalake
  - realtime data access
  - gather data from many disconnected systems for instant processing


## some popular databases

- types
  - relational: sqlite, postgresql, mysql, mssql, oracle
  - aggregate
    - document: mongodb, raven, couch
    - key-value: riak, redis, etcd
  - graph: neo4j, dgraph
  - column: cassandra, hbase, duckdb, kudu
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

- relational database strategies [3]
  - with downtime
    - run db up-migration script using automatic migrations framework
    - down-migration scripts are not that useful in practice
  - without downtime
    - migrate new version of app to db schema compatible with old application
    - switch to new version of application
    - remove compatability artifacts of migration left after the first step
  
- document database strategies [4]
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
      - allows nested selectors into json column [2]
- dotnet
  - entity framework
  - nhibernate


## relational

- sqlite
  - gui tools: dbbrowser

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
  - has 2 auth modes
    - sql server authentication
    - windows authentication

  - get row counts for all tables in a database
    ```sql
      DECLARE @TableRowCounts TABLE ([TableName] VARCHAR(128), [RowCount] INT) ;
        INSERT INTO @TableRowCounts ([TableName], [RowCount])
        EXEC sp_MSforeachtable 'SELECT ''?'' [TableName], COUNT(*) [RowCount] FROM ?' ;
        SELECT [TableName], [RowCount]
        FROM @TableRowCounts
        ORDER BY [RowCount] desc
      GO
    ```
  
  - search for arbitrary string in stored procedures
    ```sql
      SELECT name
        FROM   sys.procedures
        WHERE  Object_definition(object_id) LIKE '%my-search-string%'
    ```
- snowflake
- bigquery
- redshift
- synapse


## object relational mappers (orms)

- python
  - sqlalchemy
    - allow returning data from disconnected entities (closed session)
      - session.expire_on_commit = False
    - sqlite+pysqlite does not support Decimal objects natively
      - possible loss of data
    - json types
      - PostgreSQL, SQLite as of version 3.9
      - supports JSON SQL operations
      - allows nested selectors into json column [2]

- dotnet
  - entity framework
  - nhibernate


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

- benefits of columnar representation
  - multiple values of the same type (columns) are clustered together
    - enables a better querying performance
      - as we're requesting a subset of the columns more often


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
        - "is intended to be read and written in streams" [1]


## open formats

- apache parquet
  - on-disk storage format
  - columnar
  - enables optimizations
    - if you know max value, you can use fewer bits to represent it (not just 16, 32, 64)?
  
- apache arrow
  - in-memory storage format
  - columnar
  - language-agnostic in-memory representation
  - optimized for
    - nested data structures
    - pipelining, simd, cache locality
  - arrow flight framework: wrapper around grpc to make serialization more efficient with arrow
  - good for working with parquet-stored data
  - deeper pandas integrations are on the roadmap
  - supports .arrow file format which then can be used to memory-map using os mechanisms
    - os often maps file in a lazy-load manner, significantly speeding up access

- apache orc: free and open-source column-oriented data storage format
- apache avro: row-based storage format
- rcfile: mix of row-store and column-store approaches


## relational algebra 

- bag (multiset)
  - is like a set, but an element may appear more than once

- define operators
  - that transform one or more input relations into an output relation
  - accept relations as input and produce relations as output

- fundamental operators
  - selection(σ): analogous to selecting rows filtered by predicate
  - projection(π): analogous to selecting rows with data from only specified columns
  - union(u)
  - set difference(-)
  - set intersection(∩)
  - rename(ρ)
  - cartesian product(x)


## sql syntax

- "having" clause
  - used when filtering is needed for aggregate functions on grouped results


## useful tools

- dbeaver https://dbeaver.io
  - free and opensource community edition
  - supports many databases, on-premise and cloud, all in one interface


## terminology

- time to glass
  - time between the moment when an event happens and the point when a platform issues an alert

- dataframe
  - generic term, not a specific implementation
  - a data structure representing a chunk of data
  - also an api for interacting with that data
    - use imperative/procedural constructs
    - offer access to internal structure
    - expose operations outside of traditional relational algebra
    - have stateful semantics
  - examples
    - in r dataframe is a part of the language
    - in python its a library like pandas

- predicate pushdown
  - using predicates to read only required data
  - comparing to reading it all and then applying predicate on higher layers

- projection pushdown
  - reading only data for columns user requested in their query
  - example: if your projection selects only 3 columns out of 10, then less columns will be passed from the storage to Spark and if your storage is columnar (e.g. Parquet, not Avro) and the non selected columns are not a part of the filter, then these columns won't even have to be read.



## references

[1]: https://en.wikipedia.org/wiki/YAML
[2]: https://stackoverflow.com/questions/31197813/sqlalchemy-filtering-nested-json-data-in-postgresql-jsonb
[3]: https://www.youtube.com/watch?v=ka-PLyjV3AI
[4]: https://mongodb.github.io/mongo-csharp-driver/2.4/reference/bson/mapping/schema_changes/
[5]: https://youtu.be/QhfuzEkN3Ck?t=935
