# notes related to a topic of machine learning

## basics

- major types of ML
  - supervised learning
    - it is most common ML method, but is defferent from RL
    - deals with labeled data and training sets
  - unsupervised learning
    - uncovering hidden structures in unlabeled data
    - likely clustering algorithms
  - reinforcement learning
    - agent interacting over time with its environment to achieve a goal
    - tasks that RL focuses on: sensation, action, goal
    - state: is a formalism that represents the state of the world, i.e. what the agent's idea of the world is
    - policy: maps states to actions, where action is what action it should take in that state

- key components to manage
  - execution environments
  - models
  - data
  - code

- popular models as of jan 2023
  - gpt-3.5
  - dall-e 2
  - codex code generator


## stages of ml worklflow [2]

- collect and load/ingest data

- explore and validate data (exploratory data analysis, eda)
  - evaluate its quality, perform statistical testing, assess distribution and variety

- clean/preprocess data
  - remove or fill-in missing data
  - determine which features are useful and which are redundant
    - analyse correlations

- extract features (feature engineering)
  - writing code to produce new features
  - enrich existing data from other sources

- split data into different dataset types
  - training (60%): used to train the model, learning its parameters
  - validation (20%)
    - tune the model, learning its hyper-parameters 
    - estimate prediction error for model selection
    - is a separate dataset from 'training' one to avoid overfitting
  - test (20%)
    - used to access quality of the model
    - is a separate dataset from 'training' and 'validation' one to have a realistic estimate

- train and tune the model
  - pick appropriate ml technique/algorithm
  - train model using ml algorithm and training dataset
  - tune model hyperparameters using validation dataset
  - outcome of this stage is the model
    - popular formats: tensorflow savedmodel, pmml, pfa or onnx

- evaluate model with test data
  - measure model performance on previously unseen data: test dataset
  - here you may have to go back and retrain the model if results are not satisfactory

- model governance/compliance checks (optional)
  - set of policies, procedures, and controls put in place to ensure that ML models and systems are developed, deployed, and used responsibly, ethically, and in compliance with regulations

- deploy the model
  - consider its all dependencies
  - model server is often used which allows serving model via https or grpc

- monitor the model
  - must be constantly monitored for drift using fresh data
    - the decay of models' predictive power as a result of the changes in real world environments

...


## standard terminology for anns

- parameter: value that is learned by the network during the training process
  - types
    - weights: determine the strength of the connections between neurons
    - biases: represent the minimum activation level required for a neuron to fire and produce an output

- token: one sample/record of data

- batch size
  - number of samples of training data loaded into memory at once
  - more precisely, processed in one forward and backward pass of the network during training

- dimensions: number of neurons in a typical layer of ann

- heads
  - output layers that are added to the network for specific tasks such as classification or regression
  - example: in a typical image classification task, the "head" of the network is a softmax layer that predicts the probability of each class based on the features extracted by the previous layers of the network


## model sizes

- anns as of 2023 
  - number of parameters: tens of billions
  - dimensions: thousands
  - n heads: tens
  - n layers: tens
  - learning rate: 10^-4 (e.g. 3.0e-4)
  - batch size: 4m
  - n tokens: 1-1.4 trillion


## popular techniques

- attention
  - used primarily for training dnns?
  - network should devote more focus to the small, but important, parts of the data

- self-attention


## reinforcement learning

- reading reinforcement learning textbook from RL online course 
  - pdf link https://www.coursera.org/learn/fundamentals-of-reinforcement-learning/supplement/07PG7/reinforcement-learning-textbook


- reading materials for the coursera "fundamentals of reinforcement learning" [course](https://www.coursera.org/learn/fundamentals-of-reinforcement-learning)
  - main challenges: exploration vs exploitation tradeoff


## linear algebra

- dot product 
  - algebraically, it is the sum of the products of the corresponding entries of the two sequences of numbers

- matrix/tensor multiplication operator in python
  > m1 @ m2   # matrix multiplication (__matmul__ method)


## cognitive architectures

- digital model of a brain
- key components: inputs, processing, output
  - similarities with definition of a function in math, but just for ai domain

- simplest ones
  - final state machine (fsm): used in computer games and some devices

- notable examples
  - connectionist: neural networks
  - gpt


## books to consider

- scaling machine learning with spark by adi polak https://www.amazon.ca/gp/product/B0BXQTTJ3N
- python machine learning (raschka, 2019) https://www.amazon.ca/dp/1789955750


## software

- https://midjourney.gitbook.io/docs/
  - offers a discord midjourney bot, which you can use to generate images
  - there is a free plan as well as paid subscription

- https://github.com/DeepGenX/CodeGenX
  - free vscode plugin for intelligent coding assistaint


## popular libraries

- tensorflow
  - foss, founded by google
  - keras: acts as an interface to a tensorflow library
- pytorch
  - foss, founded by meta
- onnx (pronounced like onyx)
- sklearn
  - built on NumPy, SciPy, and matplotlib
- nextflow
  - dockerized pipeline for scientific data processing tasks


## useful nix commands

- to get amount of vram on linux
  > sudo apt install mesa-utils
  > glxinfo | egrep -i 'device|memory|video'

- watch gpu resources consumption
  > watch -n0.1 nvidia-smi


## automated ml pipelines [3]

- benfits
  - ability to focus on new models, not maintaining old ones
  - prevention of bugs
    - a common source of bugs is a change in the preprocessing step after a model was trained
      - leads to deploying a model with different set of instructions than the model was trained with
  - audit trail
  - standardization
  - simpler processes to update existing models
    - as soon as model has users, it will require continuous updates and fine-tuning
  - less time to reproduce models

- typical steps
  - data ingestion and versioning
  - data validation
  - data preprocessing
  - model training and tuning
  - model analysis (manual)
  - model versioning
  - model deployment
  - feedback (can be manual)

- tools
  - apache beam
  - apache airflow
  - kubeflow pipelines
  - mlflow

- model servers
  - also called 'inference servers'
  - there are bunch of them: BentoML, Cortex, TensorFlow Serving, TorchServe, KFServing, Multi Model Server, Triton Inference Server, ForestFlow, DeepDetect, Seldon Core, DeepSparse, OpenVINO Model Server, KServe


## mlflow

- open source platform for the machine learning lifecycle
- key features
  - tracking
    - api and ui for logging parameters, code versions, metrics, and output files 
    - available when running your machine learning code and for later visualizing the results
    - lets you log and query experiments using 
      - python, rest, r api, and java api apis
      - spark datasource
  - projects: format for packaging data science code in a reusable and reproducible way
  - models: standard format for packaging machine learning models
    - supported by mlserver
  - model registry: store, annotate, discover, and manage models in a central repository


## interesting ideas

- modern ml models as [1]
  - stochastic parrots/chameleons
  - analogous to biological mimicry

- data augmentation in pattern recognition
  - altering input data by introduction of small transformations/disturbances
  - goals
    - make recognition more robust
    - extract invariant representations of detected phenomenon


## terminology

- ani: artificial narrow intelligence
- agi: artificial general intelligence

- features: variables (columns) that are used as input to a machine learning model
- labels: target or output variables (columns) in a supervised learning problem

- deep learning
  - model has multiple layers of learned representations, which makes it superior to other models
  - dnns are dominating space, but there are some other ways to do it

- transfer learning
  - storing knowledge gained while solving one problem and applying it to a different but related problem

- transformer
  - deep learning model
  - adopts the mechanism of self-attention
    - differentially weighting the significance of each part of the input data

- champion/challenger models
  - champion is the model that was elected to be deployed in production
  - challengers are potential candidates for a champion

- structured/unstructured data
  - structured data comes with a pattern that is clearly identifiable and searchable by computers
  - while unstructured data, despite having an internal structure humans can understand, lacks those patterns

- ibb: image bounding boxes, used for object detection and annotation
- rag: retrieval augmented generation
- completion: llm output based on input prompt
- vector database: type of database that indexes and stores vector embeddings for fast retrieval and similarity search, with capabilities like CRUD operations, metadata filtering, and horizontal scaling
- embeddings: vectorized representation of a word or a phrase in nlp

- ann
  - artificial neural network
  - approximate nearest neighbor, a variant of 'nearest neighbor' search


## references

[1]: https://www.youtube.com/watch?v=fhn6ZtD6XeE&t=186s
[2]: https://www.amazon.ca/gp/product/B0BXQTTJ3N (scaling machine learning with spark by adi polak)
[3]: https://www.amazon.ca/Building-Machine-Learning-Pipelines-Automating-ebook/dp/B08CXDBWTX/