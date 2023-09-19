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

- phases
  - training (pre-training and fine-funing sub phases)
  - validation/test
  - application

- dataset types
  - training (60%): used to train the model, learning its parameters
  - validation (20%)
    - tune the model, learning its hyper-parameters 
    - estimate prediction error for model selection
    - is a separate dataset from 'training' one to avoid overfitting
  - test (20%)
    - used to access quality of the model
    - is a separate dataset from 'training' and 'validation' one to have a realistic estimate

- data augmentation in pattern recognition
  - altering input data by introduction of small transformations/disturbances
  - goals
    - make recognition more robust
    - extract invariant representations of detected phenomenon

- ani: artificial narrow intelligence
- agi: artificial general intelligence

- deep learning
  - model has multiple layers of learned representations, which makes it superior to other models
  - dnns are dominating space, but there are some other ways to do it

- transfer learning
  - storing knowledge gained while solving one problem and applying it to a different but related problem

- popular models as of jan 2023
  - GPT-3.5
  - DALL-E 2
  - Codex code generator

- transformer
  - deep learning model
  - adopts the mechanism of self-attention
    - differentially weighting the significance of each part of the input data


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

- as of 2023 
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


## fun

- modern ml models as [^1]
  - stochastic parrots/chameleons
  - analogous to biological mimicry


## references

[^1]: https://www.youtube.com/watch?v=fhn6ZtD6XeE&t=186s