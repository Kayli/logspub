# notes on apache spark and related software [1]

## basics

- is an open-source unified analytics engine for large-scale data processing
- the most popular opensource platform for data science
- written in scala, has scala shell for interacting with data

- pyspark
  - bindings/adapters for spark, uses py4j under the hood
  - heavily influenced by pandas

- supports 'schema on read'
  - allows to derive schema by sampling only small fraction of data


## spark cluster architecture

- driver program: provides context for user operation

- cluster manager
  - coordination of worker nodes based on user request
  - responsible for orchestrating components of the cluster
  - default spark cluster manager, alternatives are:
    - hadoop yarn
    - elastic mapreduce (aws)
    - apache mesos
    - kubernetes

- worker nodes
  - executor
    - process launched for particular spark application on a worker node
    - multiple executors can run on the same worker node

- data sources
  - hdfs, sql, nosql, etc.
  - azure datalake gen1 gen2: emulate hdfs, but implement it more efficiently for the azure cloud


## spark components

- spark core: provides shared functionality for all other components
- spark streaming: realtime data
- spark sql: treat your data like in a data warehouse
- mllib: ml algorithms, like pearson correlation
- graphx
  - implements network theory algorithms
  - used to query network/graph data


## important abstractions

- facades: objects that we use to interact with most other things
  - SparkContext
    - allows to load data directly from 
      - hdfs
      - json, csv
      - compressed file formats
      - was used in earlier versions (< 2.0) of Spark or Pyspark
  - SparkSession
      - in later versions of spark (>= 2.0)
      - combined class for all different contexts we used to have prior to 2.0
        - instead of SparkContext, SQLContext, HiveContext etc.
      - entry point for programming with DataFrame and Dataset

- rdd (resilient distributed dataset)
  - fault-tolerant collection of elements that can be operated on in parallel
  - supports partitioning
    - partitions by 128MB blocks of data by default
    - slices and partitions are synonyms in the context of rdd
  
  - support two types of operations
    - transformations: create a new dataset from an existing one
      - map: like Select in linq
      - flatmap: like SelectMany in linq
      - filter: like Where in linq
      - distinct: like Distinct in linq
      - sample: returns random sample of data
      - union, intersection, subtract, cartesian
      - more others ...
    
    - actions: return a value to the driver program after running a computation on the dataset
      - collect
      - count
      - countByValue
      - take
      - top
      - reduce
      - more others ...

  - api analogous to iqueryable in dotnet in some ways

- dataframe
  - analogous to table abstraction in sql
  - provides api for interacting with data

- datasets and dataframes
  - refer to kinda same api? difference is not crystal clear
  - are often used interchangeably

- koalas
  - foss library that offers pandas api with spark backend
  - covers more than 60% of pandas api


## query optimizations [2]

- spark uses two engines to optimize and run the queries: catalyst and tungsten
- catalyst
  - generates an optimized physical query plan from the logical query plan
  - enables
    - adding new optimization techniques and features to Spark SQL
    - external developers to extend the optimizer
      - e.g. adding data source specific rules, support for new data types, etc.
  - ast tree transformation phases
    - analysis
    - logical optimization
      - predicate pushdown
      - column pruning (projection pruning)
      - constant folding


## deployment

- localhost deployment using kind and kubernetes
  - spark operator, argocd and argo workflows to create a spark application workflow solution on kubernetes and uses gitops to propagate the changes
  - is cloud-agnostic
  - see article for more details: https://medium.com/empathyco/running-apache-spark-on-kubernetes-2e64c73d0bb2
  - spark k8s operator on gcp https://github.com/GoogleCloudPlatform/spark-on-k8s-operator


## spark history

- project started around 2009 with mesos in uc berkley
- 2014, spark 1 release
  - becomes a top-level project within apache foundation
  - spark sql was introduced
- 2016, spark 2 release
  - unifying DataFrame and Dataset apis
  - performance improvements
- 2017: integration with azure via databricks
- 2020, spark 3 release
  - adaptive query execution: automatically optimizes query execution based on data characteristics and hardware resources
  - pandas udf api that allows users to apply custom python functions to spark dataframes


## databricks

- commercial product
- was created by developers of apache spark and uses apache spark under the hood
- complete development environment designed to get up and running quickly
- designed for large size team collaboration
- can't run on-premise, designed to run in the cloud
- leverages foss technologies under the hood
  - spark, koalas, delta lake, redash, mlflow

- user interface
  - notebooks ide interface (similar to jupiter notebooks)
  - supports: python, r, scala, sql
  - clusters maintanence
  - sharing of clusters and notebooks
  - custom libraries installation

- workspace
  - contains all compute resources needed to support databricks
    - file storage
    - vms to run databricks user interface
    - some other stuff

- delta lake: file-based open-source data storage format and project
  - high-performance acid table storage over cloud object stores
  - notable features
    - acid transaction guarantees
      - only optimistic concurrency control, no locks
      - snapshot isolation on reads and write-serializable isolation on writes
    - scalable data and metadata handling (petabyte-scale tables)
    - audit history and time-travel
      - transaction log, reverting transactions, reproducing experiments
    - schema enforcement and evolution
    - support for deletes, updates and merges
    - unified streaming and batch data processing
    - supports parquet open storage format via parquet tables
    - can store data in
      - aws s3
      - google cloud storage
      - adls (azure data lake storage gen2) 
        - is a set of capabilities dedicated to big data analytics, built on azure blob storage
      - alibaba, hdfs
    - data ingestion third-party adapters
    - data querying third-party adapters
  - delta files and delta tables
    - parquet files: open, fast, columnar storage
    - plus additional metadata layer
      - data versioning
      - transaction logs (enables acid transactions)
  - limitaions
    - pks and fks are implemented but can't be enforced
      - performance considerations are the main reason
      - also the whole pk/fk functionality is still in 'public preview' (as of oct 2023)
    - multitable transactions are not supported
      - applications that modify multiple tables commit transactions to each table in a serial fashion

- photon: execution engine (among several others available)
  - databricks-native query engine
  - support for query languages
    - databricks sql
    - spark sql

- redash
  - allows to connect and query your data sources using intuitive query editor
  - offers snappy interactive web-interface
  - alows building dashboards to visualize data and share them with others


## terminology

- py4j: enables python programs running in a python interpreter to dynamically access java objects in a java virtual machine

- delta live tables (dlt)
  - are equivalent conceptually to materialized views


## references

[1]: https://www.youtube.com/watch?v=ChISx0-cMpU&list=PL7_h0bRfL52qWoCcS18nXcT1s-5rSa1yp
[2]: https://www.linkedin.com/pulse/catalyst-tungsten-apache-sparks-speeding-engine-deepak-rajak/