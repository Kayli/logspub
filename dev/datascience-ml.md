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

- loss vs accuracy for ml models evaluation
  - accuracy metric is only applicable to classification tasks
    - is usually determined after the model parameters are learned and fixed and no learning is taking place
    - accuracy is not differentiable and therefore you can't backprop on it
  - loss metric is for regression tasks
    - loss is calculated on training and validation and its interperation is how well the model is doing for these two sets


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




## data representations

- one-hot vector, localist ([00000000100000] vector)
  - pros: simple, intuitive representation
  - cons
    - huge size
    - does not encode relations between words
    - for high-cardinality variables — those with many unique categories — the dimensionality of the transformed vector becomes unmanageable
    - doesn't work well for cosine-distance similarity comparison algorithm
      - similarity is 0 for every comparison between entities
      - this is because encoding does not place similar entities closer to one another in vector space

- embeddings [4]
  - learned low-dimensional representations of discrete data as continuous vectors
  - overcome limitations of one-hot encoding
  - can be extracted from model and reused to speed-up training in some situations
  - training and testing sets can be joined for the purpose of training embeddings [gpt]


## aritificial neural networks (anns)

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

- universal approximation theorem
  - states that feedforward neural network with a single hidden layer containing a finite number of neurons (units) can approximate any continuous function to arbitrary accuracy, given a sufficiently large number of neurons in the hidden layer


- adam: (adaptive moment estimation) 
  - optimization algorithm used for training artificial neural networks
  - extension of the stochastic gradient descent (sgd) optimization algorithm and is designed to address some of its limitations
  - combines ideas from two other optimization methods: rmsprop (root mean square propagation) and momentum

- most common mathematical operations
  - sum and multiplication: dot product
  - exponentiation: softmax normalization layer

- ann model sizes as of 2023 
  - number of parameters: tens of billions 
  - dimensions: thousands
  - n heads: tens
  - n layers: tens
  - learning rate: 10^-4 (e.g. 3.0e-4)
  - batch size: 4m
  - n tokens: 1-1.4 trillion

- march 2024
  - number of parameters: 10^12
    - estimate of gpt4, 8 models in mixture of experts (moe) mode


## popular techniques

- attention
  - used primarily for training dnns?
  - network should devote more focus to the small, but important, parts of the data

- self-attention

- cosine similarity
  - dot product of the vectors (e.g. embeddings) divided by the product of their magnitudes
  - results in a value between -1 and 1 where
    (1) means vectors are identical
    (0) means vectors are orthogonal
    (-1) means vectors are diametrically opposed


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
  - final state machine (fsm)

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
  - top
    - mlflow model serving (foss)
    - seldon core (foss)
    - tensorflow serving (google)
    - torchserve (aws)
    - triton inference server, also tensorrt (nvidia)
  - there are bunch of others
    - BentoML, Cortex, KFServing, Multi Model Server, ForestFlow, DeepDetect, DeepSparse, OpenVINO Model Server, KServe

- hosting
  - https://dagshub.com/pricing (mlflow hosting but no inference server)


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

- squaring vs abs
  - terminology
    - L2 norm: square of a quantity, also 'squared loss', 'l2 loss'
    - L1 norm: absolute value
    - L1 and L2 regularization: using squares vs abs
  - pros of squaring
    - squaring a term makes the function differentiable everywhere
      - while the absolute value function is not differentiable at zero
      - derivative changes smoothly when squaring, and abruptly with abs
    - penalizing larger errors
  - cons
    - squaring tends to amplify the influence of outliers because large errors contribute disproportionately to the overall loss. Absolute values are less sensitive to outliers in this regard
  - examples
    - some algorithms, like LASSO (L1 regularization), promote sparsity and are useful for feature selection, while others, like Ridge regression (L2 regularization), penalize the magnitude of weights and can help prevent overfitting

- for educational purposes 
  - it might help to use 'finite difference' method for approximating derivative 
    - to start with something simple
    
- its impossible to model xor gate with a single neuron
  - but combination of 'or', 'nand', 'and' will do: (x|y) & ~(x&y)


## terminology

- ani: artificial narrow intelligence
- agi: artificial general intelligence

- features: variables (columns) that are used as input to a machine learning model
- labels: target or output variables (columns) in a supervised learning problem
- example: is a particular instance of data
  - labeled example: used to train the model
  - unlabeled example: used for making predictions on new data
- model: maps examples to predicted labels
  - defined by internal parameters, which are learned
- training: creating or learning the model
- inference: applying the trained model to unlabeled examples to make useful predictions
- batch: is the set of examples you use to calculate the gradient in a single training iteration

- regression vs. classification
  - regression model predicts continuous values
  - classification model predicts discrete values

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

- ann
  - artificial neural network
  - approximate nearest neighbor, a variant of 'nearest neighbor' search

- orthogonal relationship: two things are independent or unrelated to each other
- diametrically opposed: as opposed as they can be, related to line outlining diameter of a circle

- epoch: pass through all the input data in learning phase

- LR: learning rate
  - neural network adjusts its weights based on the error between its predictions and the actual target values. The learning rate influences the size of these weight updates.

- mse: (mean square error) is the average squared loss per example over the whole dataset.

- новые перспективные области исследования
  - neuro-inspired computing: вдохновленные нейроным вычислением
  - neuromorphic engineering: нейроморфная инженерия


## tensorflow

- tf.keras: high-level api, easy to use


## useful links

- foundational ml courses from google with executable collab notebooks
  - https://developers.google.com/machine-learning/foundational-courses

- stable diffusion: https://deforum.art

- music generator https://suno.com/

- writing assistaints [5]
  - jenni https://jenni.ai/
  - grammarly https://www.grammarly.com/
  - writesonic https://writesonic.com/
  - jasper https://www.jasper.ai/

- research [5]
  - quivr: chat with your documents https://www.quivr.com/
  - ai search engine for research https://consensus.app/
  - research papers reading assistaint https://www.explainpaper.com/
  - semantic scholar https://www.semanticscholar.org/

- tools for teachers and instructors [5]
  - magic school, eduaide, teachmateai

- memory [6]
  - spaced-repetition flashcard https://www.idorecall.com/
  - quizlet, kahoot!, anki


## references

[1]: https://www.youtube.com/watch?v=fhn6ZtD6XeE&t=186s
[2]: https://www.amazon.ca/gp/product/B0BXQTTJ3N (scaling machine learning with spark by adi polak)
[3]: https://www.amazon.ca/Building-Machine-Learning-Pipelines-Automating-ebook/dp/B08CXDBWTX/
[4]: https://towardsdatascience.com/neural-network-embeddings-explained-4d028e6f0526
[5]: https://www.coursera.org/learn/learning-chatgpt/lecture/tYhuv/10-mapping-the-landscape-of-large-language-models-and-genai-learning
[6]: https://www.coursera.org/learn/learning-chatgpt/lecture/3Ybkc/11-ai-driven-learning-maximizing-retrieval-practice