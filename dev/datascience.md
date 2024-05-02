# notes on datascience

## basics

- data science
  - is an interdisciplinary academic field
  - uses statistics, scientific computing, scientific methods, processes, algorithms and systems to extract or extrapolate knowledge and insights from noisy, structured, and unstructured data

- data types (non mutually exclusive)
  - structured: relational databases, spreadsheets, and csv files
  - semi-structured: json and xml files, nosql databases
  - unstructured: documents, images, videos, audio files, social media posts, emails
  - multistructured: contains elements of both structured and unstructured data
  - temporal: includes information related to time or timestamps
    - time series
      - data recorded at successive, evenly spaced intervals over time
      - typically represents how a particular variable or set of variables changes over time
  - geospatial: involves information that is tied to specific geographical locations or coordinates
  - graph: represents relationships between entities in a network-like structure
  - streaming: continuously generated and processed in real-time or near real-time

- data analysis
  - is the process of inspecting, cleansing, transforming, and modeling data 
  - the goal is to discover useful information, informing conclusions, supporting decision-making

  - data mining
    - is a particular data analysis technique
    - focuses on statistical modeling and knowledge discovery
    - does so for predictive rather than purely descriptive purposes

  - business intelligence
    - data analysis that relies heavily on aggregation, focusing mainly on business information

- sampling
  - random sampling: generates random subset of your dataset
  - downsampling: reduces the data volume by aggregating over time intervals
  - stratified sampling


## big data

- extremely large and complex sets of data that cannot be easily managed, processed, or analyzed using traditional data processing tools

- key charachteristics
  - velocity
    - big data is generated and collected at high speeds
    - it can flow in rapidly from various sources like sensors, social media, etc.
    - real-time or near-real-time processing is often necessary to extract valuable insights
  - veracity 
    - quality and reliability of the data
    - big data may contain inaccuracies, inconsistencies, or missing information
  - variety
    - encompasses diverse types of data, e.g.
      - structured (e.g., databases)
      - semi-structured (e.g., XML or JSON)
      - unstructured (e.g., text, images, videos)
  - volume
    - involves vast amounts of information
      - often exceeding the capacity of conventional databases and data processing systems
    - can range from terabytes to petabytes or even exabytes of data
  - value
    - benefits and insights that organizations can derive from the analysis and effective utilization of large and complex data sets
    - isn't just profit, as it may have medical or social benefits, as well as customer, employee, or personal satisfaction


## datascience process/methodology

- problem definition
  - clearly define the problem or business question you aim to address using data
  - understand objectives and the context
  - scope: accuracy, time, cost constraints

- data collection
  - where data sourced from and how to receive the data?
    - this can involve structured data (from databases), semi-structured data (e.g., json or xml files), and unstructured data (text, images, etc.)
    - consider batch processing as well as streaming techniques
  - talk to domain experts
  - where are we going to store all the data we're planning to collect?
  - how data will be stored?

- preparation
  - data preprocessing
    - clean and prepare the data for analysis. this step involves handling missing values, outliers, data normalization, and transforming data into a suitable format for analysis.
  
  - exploratory data analysis (eda)
    - perform exploratory data analysis to understand the data's characteristics and identify patterns, trends, or anomalies. this often involves visualizations, statistical summaries, and data profiling
  
  - feature engineering
    - create new features or transform existing ones to extract more meaningful information from the data. this can improve the performance of machine learning models.

- modelling
  - focuses on developing models that either descriptive or predictive
  - model development
    - build/select appropriate machine learning or statistical models based on the problem's nature (e.g., classification, regression, clustering)
    - split data into training and testing sets
  - model training
    - train the selected models using the training data. hyperparameter tuning and cross-validation may be applied to optimize model performance.

- model evaluation
  - evaluate model performance using various metrics (e.g., accuracy, precision, recall, f1-score, rmse) on the testing dataset. make adjustments and refinements if necessary.

- model deployment
  - deploy the model into a production environment, where it can make predictions or generate insights for the organization. this may involve integrating the model into a software application or system.

- interpretability and explanation
  - for transparency and trustworthiness, interpret the model's predictions or decisions, especially when working with stakeholders or end-users who may need to understand the rationale behind the results


## approaches

- data warehouse: classic approach
  - pros
    - relatively simple, homogeneous tech stack
    - clean, well-structured relational data

  - painpoints
    - no native support/optimization for ml applications
    - not well suited to work with unstructured data
      - unconventional data formats are not supported
    - proprietary storage formats
      - don't allow outside vendors to easily access their data
    - don't scale that well comparing to alternatives

- data lake
  - data storage and compute are not coupled
  - centralized, infinite scaling
  - data stored in open formats

- data mesh: distributed, fast, realtime

- data lakehouse
  - transaction support
  - schema enforcement and governence
  - data governence: privacy regulation and data use metrics
  - b.i. support
  - open storage formats, eg apache parquet
  - support for diverse datatypes
  - end-to-end streaming ?? enables realtime analytics


## apache spark and databricks

- see datascience-spark.md for details


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

- spark or presto are often used as a replacement for map-reduce and hive components of hadoop stack


## interesting ideas

- medallion architecture
  - helps to logically organize data in a lakehouse
  - goal: incrementally and progressively improving the structure and quality of data as it flows through each layer of the architecture
  - flow: bronze ⇒ silver ⇒ gold
  - layers
    - bronze
      - raw unstructured data in a state as it just gets ingested
      - examples: json, csv files
    - silver
      - filtered, clean, normalized, augmented data
      - ready for use by analysts and ml
      - represents a single source of truth
    - gold
      - provides aggregates to query for a specific business case
      - example: weekly reports
      


## terminology

- etl: extract, transform, load
- elt: extract, load, transform


## useful links

- spark and ml basics video tutorial and jupiter notebook
  - https://www.youtube.com/watch?v=crtBiZvcUOE
  - https://colab.research.google.com/github/JohnSnowLabs/spark-nlp-workshop/blob/master/tutorials/Certification_Trainings/Public/6.Playground_DataFrames.ipynb

- spark full course: https://www.youtube.com/watch?v=S2MUhGA3lEw

