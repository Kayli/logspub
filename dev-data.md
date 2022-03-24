# notes about data formats, management system and related stuff

## databases

- types
  - relational
    - sqlite
    - postgresql
    - mssql
    - oracle
  - document
    - mongodb
  - graph
    - neo4j
  - cloud native
    - amazon RDS, SimpleDB, DynamoDB
    - azure Cosmos DB, SQL Database


## orms

- sqlalchemy (python)
  - allow returning data from disconnected entities (closed session)
    - session.expire_on_commit = False
  - sqlite+pysqlite does not support Decimal objects natively
    - possible loss of data
  - json types
    - PostgreSQL, SQLite as of version 3.9
    - supports JSON SQL operations
    - allows nested selectors into json column [^2]




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


## references

[^1]: https://en.wikipedia.org/wiki/YAML
[^2]: https://stackoverflow.com/questions/31197813/sqlalchemy-filtering-nested-json-data-in-postgresql-jsonb
