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

- there isn't a hardcoded limit on the size of a single cell
  - but should be well below the total memory available to an executor
  

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
  - hdfs, sql, nosql, s3, etc.
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
    - obsolette, for backward compatability
    - allows to load data directly from 
      - hdfs
      - json, csv
      - compressed file formats
      - was used in earlier versions (< 2.0) of Spark or Pyspark
    - properties
      - defaultParallelism: gives an estimate of degree parallelism for a cluster

  - SparkSession
      - in later versions of spark (>= 2.0)
      - combined class for all different contexts we used to have prior to 2.0
        - instead of SparkContext, SQLContext, HiveContext etc.
      - entry point for programming with DataFrame and Dataset
      - should be preferred to SparkContext as its newer and more powerful/abstract

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
      - foreach: applies lambda action to every element in a dataset
      - collect: converts distributed dataset into a python array
      - count: counts elements in a dataset
      - countByValue: ?
      - reduce: ?
      - reduceByKey
        - similar to groupby in linq
        - works on key-value pairs (only?)
        - reduces rows grouping them by key
        - applies aggregate function provided by lambda for values inside each group
          - lambda takes 2 elements which are values of 2 different rows or accumulators
      - take: takes specified number of elements from the dataset
      - top
      - saveAsTextFile(filename)
      - more others ...
    - other
      - getNumPartitions: number of partitions rdd has


  - api analogous to iqueryable in dotnet in some ways

- spark dataframe
  - analogous to: table abstraction in sql, pandas dataframe
  - provides api for interacting with data
  - key differences from pandas dataframe
    - partitioned
    - distributed across many nodes
    - no inplace modification: as all dataframes are readonly as well as their underlying rdd
  - useful methods
    - printSchema: shows column datatypes
    - display: shows several samples of data and total rows count 
    - show: shows several samples of data in a copyable text format
    - collect: yields collection of objects
    - select: column-level transformations and projections
      - add new column by multiplying two others:
        >>> df.select(col('*'), (col('amount') * col('units')).alias('total_value'))
    - limit: limits result of a query to certain max number of rows
    - take: returns python array of row objects up to specified number of elements
    - withColumn: adds or replaces column in a dataset
      - add new column by multiplying two others:
        >>> df.withColumn("total_value", col("amount") * col("units"))

- datasets vs dataframes
  - dataset represents a collection of data in a broader sense
    - there is also Dataset interface in scala, but there is no such entity in pyspark
  - dataframe is a specific implementation tailored for efficient manipulation and analysis of tabular data within programming languages

- koalas
  - foss library that offers pandas api with spark backend
  - covers more than 60% of pandas api


## schema validation

- you can specify schema using types like StructType and StructField
  ```python
    from pyspark.sql.types import StructType, StructField, StringType, IntegerType
    schema = StructType([
      StructField("Name", StringType(), True),
      StructField("Age", IntegerType(), True)
    ])
    df = spark.createDataFrame([], schema)
  ```

- is relatively weak/buggy out of the box
  - non-nullable column constraints are not always enforced
    - when cloning dataset into a new one with more strict schema
      - schema validation fails only when enumeration reaches a row that violates the schema
      - it will not fail during cloning operation

  - when saving dataframe as delta table, non-null constraints are ignored
    - so when you load it next time, all columns are nullable again

  - columns names are not verified when reading from csv
    - so if csv data changes its columns order, this may not be detected
      - even if there is a header row present in the file
  

- to check data in all columns for missing values
  ```python    
    for col_name in df.columns:
        assert df.filter(df[col_name].isNull()).count() == 0, 'consistency validation failed: missing data was found'
  ```

- to explicitly check specific column for missing values
  ```python
    assert df.select(col('id')).where(isnull(col('amount'))).count() == 1, 'amount column should not contain null values'
  ```

- clone dataframe but with schema where nullable set to False for every column (but can be superslow)
  ```python
    new_fields = []
    for field in df.schema.fields:
        new_field = StructField(field.name, field.dataType, nullable=False)
        new_fields.append(new_field)
    schema_new = StructType(new_fields)
    df_new = spark.createDataFrame(df.rdd, schema_new)
  ```


## types conversion

- to change column type via dataframe api
  ```python
    from pyspark.sql.types import DoubleType
    df = df.withColumn("age", col("age").cast(DoubleType()))
    df = df.withColumn("day", to_date(col("day"), "MM/dd/yyyy"))
  ```


## filesystem tools

```python
  dbutils.fs.rm('dbfs:/myfolder', recurse=True)
  dbutils.fs.mv('dbfs:/src', 'dbfs:/dst', recurse=True)
  files = dbutils.fs.ls('dbfs:/myfolder')
```


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
        - process of identifying, simplifying and evaluating constant expressions within the logical query plan
        - constant expression
          - is one where all the operands are constants
            - meaning they have fixed values that can be determined at compile time
      - loop unrolling

- tungsten
  - execution engine component 
  - focused on improving performance through memory management and code generation
  - key features
    - memory-centric data structures and binary processing for serialized data
      - which reduces memory overhead and improves CPU cache utilization
    - optimizes data serialization and deserialization by using binary formats instead of Java object serialization
    - employs off-heap memory management techniques to minimize garbage collection overhead, improving overall execution efficiency
    - works closely with catalyst by leveraging the optimized query plans generated to execute tasks efficiently


- tips
  - repartition by the same column(s) before groupby operation

  - cache data and preload it into memory before querying by calling count()
    >>> df = df.cache()

  - specifying number of partitions that aligns with total number of executor cores improves performance of the query
    >>> df_opt = df.repartition(spark.sparkContext.defaultParallelism, col('product'))


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
    - udf: user-defined function


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

- key concepts
  - workspace
      - is an environment for accessing all of your Databricks assets
      - organizes objects (notebooks, libraries, dashboards, and experiments) into folders and provides access to data objects and computational resources
    
    - notebook
      - python, sql, scala, r
      - allows running pip commands and importing libraries
      - associated with a cluster
      - schedule and run jobs
    
    - workflows: ui screen containing 'jobs', 'job runs' and 'delta live tables' sections
      - for some reason 'workflows' are often used interchangeably with 'jobs' in official databricks docs
    
    - job (workflow?)
      - contains
        - tasks: 
          - every task is an atomic unit of work
          - can form data processing graph based on a dependency graph
    - job run: instance of a job that has been triggered (manually or automatically)
    
    - unity catalog
      - provides centralized access control, auditing, lineage, and data discovery capabilities across databricks workspaces
      - object model hierarchy
        - metastores
          - catalogs
            - schemas (databases)
              - tables
              - views
              - volumes
              - models
              - functions
        
    - metastore: top level container for metadata
      - metadata about data and ai assets and the permissions that govern access to them.
      - one metastore per region
      - contains catalogs

    - catalog: container for schemas/databases

    - schema/database (used interchangeably)
      - contains: tables, views, volumes, models, functions

    - table
      - types
        - managed
          - are the default way to create tables in unity catalog
          - locally provisioned storage, lifetime managed by databricks
          - always use the 'delta table' format
        - external
          - can map to remote locations
          - can be backed by different file formats: DELTA, CSV, PARQUET JSON, AVRO, ORC, TEXT
    
    - volume: a file that is stored in any format

    - stream: tables that are continuously appended with new data

    - repo
      - a folder whose contents are co-versioned together by syncing them to a remote git repository

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

- autoloader
    - helps automating ingestion part of the pipeline
      - provides stream access to a set of files it watches
    - uses 'cloudfiles reader' to maintain metadata
      - encapsulates
        - blob storage
        - queue (eventgrid?) topic with notifications regarding file modifications for this blob
        - topic subscription that monitors blob changes and loads data for new files 
    - on file change
      - keeps track of changes based on file timestamp
      - it won't process the file again unless you use a specific configuration option
      - databricks generally recommends using autoloader with immutable data files
    - supports 'trigger once' mode, when it processes all the changes and returns
    - supports schema inference and schema tips features
      - allows users to define schema evolution policies to manage schema changes systematically
      - policies specify how to handle schema changes, such as adding new fields, modifying existing fields, or removing fields


- databricks vs snowflake comparison
    
    - both
      - separate storage and compute and allow to scale it independently
      - there are no indexed data (in a classical sense)
        - so system is optimized for efficient full scans
        - z-ordering
          - queries that involve range predicates or equality filters on the Z-ordered columns can benefit from this organization, as it reduces the amount of data that needs to be read from disk
        - data skipping
          - min/max stats are gathered for individual files and used to skip this data during scan
      - support time travel queries

    - snowflake
      - sql engine, works mostly with data stored in s3
      - more suitable for warehouse structured data processing
      - transactions
        - only read-committed isolation layer is supported
        - operations acquire locks on a resource, such as a table, while that resource is being modified
          - locks block other statements from modifying the resource until the lock is released
        - scoped to a single database and can not span multiple databases
          - can involve multiple tables within single database
      - can create, maintain and enforce FKs
      - provides 'stage' abstraction for working with external data sources
        - allows creating structured views over unstructured data (e.g. json)
      - gives access to public datasets from different providers
    
    - databricks
      - spark engine, opensource
        - multiple languages support: python, scala, r, sql
      - deltalake format from variety of sources: s3, hdfs, azure, gcp storage, etc
      - only optimistic concurrency control, no locks
      - pks and fks are supported but not enforced
      - more suitable for processing unstructured data and ml workflows


- delta live tables
  - use autoloader under the hood
    - monitoring folder with weakly structured incoming data (json)
    - infers schema automatically, may handle a schema drift
  - run by pipelines
    - have 'batch' or 'continuous' modes
    - 'batch' allows to release cluster compute between runs, saving costs
    - supports autoscaling of cluster based on current load


## terminology

- py4j: enables python programs running in a python interpreter to dynamically access java objects in a java virtual machine

- difference between transformations and actions in spark
  - transformations accumulate in a lazy manner, actions trigger actual data processing


## useful links

- pyspark examples: https://github.com/spark-examples/pyspark-examples
- timeseries dataframe abstraction: https://databrickslabs.github.io/tempo
  - supports resampling of data



## references

[1]: https://www.youtube.com/watch?v=ChISx0-cMpU&list=PL7_h0bRfL52qWoCcS18nXcT1s-5rSa1yp
[2]: https://www.linkedin.com/pulse/catalyst-tungsten-apache-sparks-speeding-engine-deepak-rajak/