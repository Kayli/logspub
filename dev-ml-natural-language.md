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
    - similarity calculated using dot product of vector representations

- sentence embedding
  - encodes sentence similarity


## nlp/nlu

- tbd


## natural language generation (nlg)

- software process that produces natural language output

- subfield of artificial intelligence and computational linguistics that is concerned with the
  construction of computer systems than can produce understandable texts in english or other human languages from some underlying non-linguistic representation of information

- language production: term preferred by psycholonguists


- practical applications
  - analysis summary (reporting) for business intelligence dashboards
  - individual client financial portfolio summaries and updates
  - personalized customer communications

- research applications
  - understanding the human language production facility
  - planning extended monologic discourses
  - psycholinguistic modeling
  - composing target language texts in machine translation systems

- abstract document specification
  - is the model from which text output gets generated

- popular approaches [2]
  - gap-filling
    - template with several gaps which are filled
    - not a real nlg
  - scripts or rules-producing text
    - often implemented via web templating languages
  - word-level grammatical functions
    - similar to previous but with a twist: adding word-level grammatical functions to deal with morphology, morphophonology, and orthography as well as to handle possible exceptions
  - dynamic sentence generation
    - creates sentences from representations of the meaning to be conveyed by the sentence or its desired linguistic structure
    - referred as 'micro-writing'
  - dynamic document creation
    - produces a document which is relevant and useful to its readers, and also well-structured as a narrative
      - how it is done depends on the goal of the text
    - example: a piece of persuasive writing may be based on models of argumentation and behavior change to mimic human rhetoric; and a text that summarizes data for business intelligence may be based on an analysis of key factors that influence the decision
    - referred as 'macro-writing'  


- document planning [3]
  - takes the messages derived from the data and works out how to best structure the information they contain into a narrative
  - purpose of the document planning stage is to use the messages available in the knowledge pool to tell a story about the data. The genre of the reports to be generated will dictate what information should be conveyed and in what order it should be presented, or at least place constraints on acceptable orderings
  - provides overall organisation for the text, supporting the ordering of presentation and the clustering of messages into paragraph-sized chunks. Messages are essentially language-independent; so, although a message may contain symbols that are reminiscent of English words, this is just a convenience for the software developer. They are best understood as concepts, and so the particular words to be used in expressing these concepts still have to be selected. Also, although each message could at this point be expressed as a simple sentence, typically this would result in a low-quality, unsophisticated text.
  - we need to select the subset of the messages in the knowledge pool that should be reported in the text to be generated. In some cases, all the messages in the knowledge pool may need to be reported, but this is not always appropriate. Once we have determined what content needs to be expressed in the document, we have to provide an overall organisation for that content in text; this is achieved by a document structuring process.
  - the result is a tree-structured object that we refer to as a document plan. The leaves of the tree are messages, and the intermediate nodes indicate how the subordinate nodes are related to each other.

- microplanning
  - works out how to package the information into sentences to maximise fluency and coherence
  - stages
    - lexicalization
    - aggregation
    - referring expression generation
  - result: a document plan that provides various types of information about the text to be produced
    - We know the overall structuring and ordering of the material to be conveyed.
    - We know what rhetorical relations hold between the constituent parts of the document plan.
    - We know how the messages are combined together into sentences.
    - We know what words and phrases are to be used to refer to entities and concepts in the messages.

- surface realization
  - ensures that the meanings expressed in the sentences are conveyed using correct grammar, word choice, morphology and punctuation
  - realisation process provides a way of mapping from the message structures into natural language structures
  - makes use of a grammar which specifies the valid syntactic structures in the language, and provides a way of mapping from the message structures into natural language structures. The realisation process also carries out morphological processing, ensuring that the correct inflections are used on words (so that, for example, plurals are properly formed and verb tenses are used correctly); and it also carries out orthographic processing, whereby punctuation marks are inserted, the first words of sentences are capitalised, and so on.

- ml models used
  - markov chains: is a simplest method to implement nlg
  - recurrent neural network (rnn)
  - long short-term memory (lstm) 
  - transformer and self-attention (gpt-2)



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


## popular/interesting libraries

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
  
- nlg
  - NaturalOWL
    - performs nlg on the semantic web
    - adopts a typical natural language generation pipeline (Reiter and Dale, 2000)
      - produces texts in three stages: document planning, microplanning, and surface realization
    - implemented as a java library and protege plugin https://protege.stanford.edu

  - simplenlg https://github.com/simplenlg/simplenlg 
    - surface realization for a simple grammar

  - list of NLG applications and techniques
    - https://github.com/accelerated-text/awesome-nlg
    - realizers https://github.com/accelerated-text/awesome-nlg#realizers


## datasets

- kaggle https://www.kaggle.com/datasets
- iris dataset https://archive.ics.uci.edu/ml/datasets/Iris
  - beginner friendly: flowers, petals and stuff
- mnist dataset
  - images of handwritten digits


## optimization techniques

- batch gradient descent (bgd)
- stochastic gradient descent (sgd)


## books

- building natural language generation systems by Ehud Reiter, Robert Dale


## references

[1]: https://medium.com/mysuperai/what-is-named-entity-recognition-ner-and-how-can-i-use-it-2b68cf6f545d
[2]: https://www.kdnuggets.com/2020/01/guide-natural-language-generation.html
[3]: https://www2.arria.com/wp-content/uploads/2017/09/Technical-Overview-The-Arria-NLG-Engine-ARR3027.pdf