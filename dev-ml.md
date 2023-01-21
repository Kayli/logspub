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
  - training
  - validation/test
  - application

- dataset types
  - training (60%): used to train the model, learning its parameters
  - validation (20%)
    - used to tune the model, learning its hyper-parameters 
    - is used to estimate prediction error for model selection
    - uses separate dataset to avoid overfitting??
  - test (20%): used to access quality of the model

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


## popular libraries

- tensorflow
  - keras: acts as an interface to a tensorflow library
- pytorch
- onnx (pronounced like onyx)
- sklearn
  - built on NumPy, SciPy, and matplotlib
- nextflow
  - dockerized pipeline for scientific data processing tasks


## books to consider

- python machine learning (raschka, 2019) https://www.amazon.ca/dp/1789955750


## reinforcement learning

- reading reinforcement learning textbook from RL online course 
  - pdf link https://www.coursera.org/learn/fundamentals-of-reinforcement-learning/supplement/07PG7/reinforcement-learning-textbook


- reading materials for the coursera "fundamentals of reinforcement learning" [course](https://www.coursera.org/learn/fundamentals-of-reinforcement-learning)
  - main challenges: exploration vs exploitation tradeoff


## useful commands

- to get amount of vram on linux
  > sudo apt install mesa-utils
  > glxinfo | egrep -i 'device|memory|video'

- watch gpu resources consumption
  > watch -n0.1 nvidia-smi


## linear algebra

- matrix/tensor multiplication operator
  > m1 @ m2   # matrix multiplication (__matmul__ method)

- dot product 
  - algebraically, it is the sum of the products of the corresponding entries of the two sequences of numbers


## speech to text

- asr: automated speech recognition
- stt: speech-to-text

- as GPUs can only process small chunks of audio, we need to split input audio into chunks dynamically
  - it is not a trivial task, as chunks should contain whole phrases, without cutting any of them in the middle
  - see here for more https://huggingface.co/blog/asr-chunking

- whisper transformer https://github.com/openai/whisper.git
  - had to install the following packages to make examples from huggingface work
    > sudo apt install ffmpeg
    > poetry add python numpy whisper transformers torch datasets soundfile librosa torchaudio
  
  - simple way to transcribe long audio https://gist.github.com/darinkist/71f27e248938d3f4b511acbfba5f0372
    > import whisper
    > model = whisper.load_model("base")
    > result = model.transcribe("opto_sessions_ep_69_excerpt.wav")
    > print(result["text"])


## software

- https://midjourney.gitbook.io/docs/
  - offers a discord midjourney bot, which you can use to generate images
  - there is a free plan as well as paid subscription
