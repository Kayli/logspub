# notes on datascience



## datascience process

- analysis
  - use case
    - what goal do we want to achieve?
    - what problem to solve?
    - scope: accuracy, time, cost constraints
  - what kind of data is required? 
    - talk to a domain expert

- data engineering
  - data collection
  - data preparation
  - exploratory data analysis
  - feature engineering
    - ml technique
    - transform available datasets into sets of figures essential for a specific task

- machine learning
  - model training and evaluation
  - model deployment
  - post deployment: monitor model performance against real-life data


## approaches

- data warehouse: classic approach, for relational structured data
- data lake: centralized, infinite scaling
- data mesh: distributed, fast, realtime
- data lakehouse
  - transaction support
  - schema enforcement and governence
  - data governence: privacy regulation and data use metrics
  - b.i. support
  - open storage formats, eg apache parquet
  - support for diverse datatypes
  - end-to-end streaming ?? enables realtime analytics


## apache spark [1]

- is an open-source unified analytics engine for large-scale data processing
- the most popular opensource platform for data science
- written in scala, has scala shell for interacting with data
- sparksql: lets you query structured data inside Spark programs, using either SQL or a DataFrame API
- graphx: used to query network/graph data
- pyspark
  - bindings/adapters for spark
  - heavily influenced by pandas

- spark cluster architecture
  - driver program: provides context for user operation
  - cluster manager: coordination of worker nodes based on user request
    - default spark cluster manager
    - on hadoop via yarn
    - in aws using elastic mapreduce
  - worker nodes
  - data sources
    - hdfs, sql, nosql, etc.
    - azure datalake gen1 gen2: emulate hdfs, but implement it more efficiently for the azure cloud

- spark components
  - spark core: provides shared functionality for all other components
  - spark streaming: realtime data
  - spark sql: treat your data like in a data warehouse
  - mllib: ml algorithms, like pearson correlation
  - graphx: network theory algorithms

- localhost deployment using kind and kubernetes
  - spark operator, argocd and argo workflows to create a spark application workflow solution on kubernetes and uses gitops to propagate the changes
  - is cloud-agnostic
  - see article for more details: https://medium.com/empathyco/running-apache-spark-on-kubernetes-2e64c73d0bb2
  - spark k8s operator on gcp https://github.com/GoogleCloudPlatform/spark-on-k8s-operator

- supports 'schema on read'
  - allows to derive schema by sampling only small fraction of data

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

  - analogous to iqueryable in dotnet in some ways
    

- spark full course: https://www.youtube.com/watch?v=S2MUhGA3lEw


## databricks

- commercial product
- was created by developers of apache spark and uses apache spark under the hood
- complete development environment designed to get up and running quickly
- designed for large size team collaboration
- can't run on-premise, designed to run in the cloud

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


## apache hadoop

- a set of big-data analytics applications, quite diverse
- key components
  - hive
    - allows to use sql to run scale-out queries using map-reduce over hdfs underneath
    - converts queries to hadoop map-reduce jobs
  - map-reduce
  - yarn (yet another resource manager)
  - hdfs (distributed filesystem)

- hdfs (hadoop distributed file system)
  - distributed file-system that stores data on commodity machines
  - provides very high aggregate bandwidth across the cluster
  - written in java
  - stores large files (typically in the range of gigabytes to terabytes) across multiple machines
  - achieves reliability by replicating the data across multiple hosts
    - with the default replication factor 3 data is stored on three nodes
      - two on the same rack, and one on a different rack
  - designed for mostly immutable files 
    - may not be suitable for systems requiring concurrent write operations
  - supports cloud storages
    - amazon s3
    - windows azure storage blobs (wasb) file system

- spark or presto are often used as a replacement for map-reduce amd hive components of hadoop stack


## references

[1]: https://www.youtube.com/watch?v=ChISx0-cMpU&list=PL7_h0bRfL52qWoCcS18nXcT1s-5rSa1yp
