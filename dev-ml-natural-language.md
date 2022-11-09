# notes related to automated natural language analysis using machine learning

## basics [1]

- nlp: natural language processing
  - processes free form natural language text and transforms it into a standardized structure

- ner: named entity recognition
  - sometimes referred to as entity chunking, extraction, or identification
  - is the task of identifying and categorizing key information (entities) in text
  - an entity can be any word or series of words that consistently refers to the same thing
  - usually focuses on nouns, numerals
  - frameworks: NLTK, SpaCy, Stanford NER

- nlu: natural language understanding
  - enables machine to 'understand' certain aspect of text being analyzed
  - various ML algorithms are used to identify the sentiment, perform ner, process semantics, etc
  - often operate on text that has already been standardized by text pre-processing steps

- stop word removal
  - words which are filtered out because they are insignificant
  - example: articles, pronouns (местоимения)

- pos: part of speech
- pos tagging
  - recursive neural tensor networks
    - fancy name for the model that is often? used for tagging

- nlg: natural language generation (language production)

- word representations
  - one-hot, localist ([00000000100000] vector)
    - huge size
    - does not encode relations between words
  - word embeddings (word2vec)
    - representation of words for text analysis, typically in the form of a real-valued vector that encodes the meaning of the word such that the words that are closer in the vector space are expected to be similar in meaning
    - you can get 'nearest neighbours' to find closely related words from the trained model
    - types
      - skip-grams (sg)
        - predict context words given a target
      - continuous bag of words (cbow)
        - predict target word from bag-of-words context

- sentence embedding
  - encodes sentence similarity


## nlp/nlu

- tbd


## natural language generation (nlg)

- software process that produces natural language output

- subfield of artificial intelligence and computational linguistics that is concerned with the
  construction of computer systems than can produce understandable texts in english or other human languages from some underlying non-linguistic representation of information

- language production: term preferred by psycholonguists


## processing pipeline examples

- expert system processing pipeline
  - stage 1
    - extract pos-tree from corpus of texts
    - perform pattern matching on a tree in order to
      - augment it with additional semantic/pragmatic metainformation
    - construct semantic web representing extracted knowledge
      - also known as knowledge graph
  - stage 2
    - get structured domain-specific request from user
    - query knowledge graph for subgraph with information relevant to user
    - construct and generate response based on subgraph


## popular algorithms

- word2vec
- glove


## popular libraries

- fasttext
  - source https://github.com/facebookresearch/fastText
  - classification (applies labels to chunks of text)
  - fast training as well as pretrained models
  - uses hierarchical classifier, binary tree of the labels (index)
- spacy (word2vec)
  - source https://github.com/explosion/spaCy
- starspace
  - source https://github.com/facebookresearch/StarSpace
  - learning word, sentence or document level embeddings
  - embedding graphs
- nltk
  - libs for classification, tokenization, stemming, tagging, parsing, and semantic reasoning
  - wordnet corpus reader
    - taxonomy
      - synonyms (synsets)
      - hypernyms: super-subordinate relation, also called hyperonymy, hyponymy or ISA relation


## datasets

- kaggle https://www.kaggle.com/datasets
- iris dataset https://archive.ics.uci.edu/ml/datasets/Iris
  - beginner friendly: flowers, petals and stuff
- mnist dataset
  - images of handwritten digits


## optimization techniques

- batch gradient descent (bgd)
- stochastic gradient descent (sgd)


## references

[1]: https://medium.com/mysuperai/what-is-named-entity-recognition-ner-and-how-can-i-use-it-2b68cf6f545d