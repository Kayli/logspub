# notes related to automated natural language analysis using machine learning

## basics 

- nlp: natural language processing
  - processes free form natural language text and transforms it into a standardized structure

- ner: named entity recognition [1]
  - sometimes referred to as entity chunking, extraction, or identification
  - is the task of identifying and categorizing key information (entities) in text
  - an entity can be any word or series of words that consistently refers to the same thing
  - usually focuses on nouns, numerals
  - frameworks: NLTK, SpaCy, Stanford NER

- nlu: natural language understanding
  - enables machine to 'understand' certain aspect of text being analyzed
  - various ML algorithms are used to identify the sentiment, perform ner, process semantics, etc
  - often operate on text that has already been standardized by text pre-processing steps

- corpus: a body of text

- pos: part of speech

- nlg: natural language generation (language production)

- lexeme
  - simplest unit in a corpus
  - often a word
  - can also be: punctuation, numbers, abbreviations

- n-grams
  - unigram: contains only one lexeme, usually a word
  - bigram: combination of two lexemes fed as single unit to a model
  - weight: probability of n-gram appearing in a random place of a corpus

- lemma: base word and its inflections

- inflectional morphology
  - is the process by which a root form of a word is modified by adding prefixes or suffixes that specify its grammatical function but do not change its part-of-speech
  - lemma (root form) is inflected (modified/combined) with one or more morphological features to create a surface form

- precision: number of correct labels among the labels predicted by ml model
- recall: number of labels that successfully were predicted, among all the real labels

- translation studies
  - ademic interdiscipline 
  - dealing with the systematic study of the theory, description and application of 
    - translation, interpreting, and localization

- internationalization
  - process of designing a software application so that it can be adapted to various 
    languages and regions without engineering changes

- localization
  - process of adapting internationalized software for a specific region or language 
    by translating text and adding locale-specific components

- parallel text [6]
  - is a text placed alongside its translation or translations

- parallel corpora [6]
  - large collections of parallel texts

- cat: computer aided translation

- translation memory
  - specific form of bitext generated and reused in translation (localization) processes
  - file representations: 
    - xml localization interchange file format (xliff)
      - https://docs.oasis-open.org/xliff/xliff-core/xliff-core.html
      - vscode extension https://marketplace.visualstudio.com/items?itemName=rvanbekkum.xliff-sync
    - translation memory exchange (tmx)
      - https://en.wikipedia.org/wiki/Translation_Memory_eXchange

- bitext
  - merged document composed of both source- and target-language versions of a given text
  - have some similarities with translation memories
    - difference is that a translation memory loses the original context, 
      while a bitext retains the original sentence order

- sentence alignment
  - in parallel corpora single sentences in one language can be found translated into several 
    sentences in the other and vice versa
  - long sentences may be broken up, short sentences may be merged

- word alignment
  - natural language processing task of identifying translation relationships among the words 
    (or more rarely multiword units) in a bitext
  - results in a bipartite graph between the two sides of the bitext, 
    with an arc between two words if they are translations of one another

- cat: computer aided translation

- stemming: transforming word to its stem (корень)


## data representations

- word embeddings (word2vec)
  - vectorized representation of word for text analysis
  - encodes the meaning of the word such that the words that are closer in the vector space are expected to be similar in meaning
  - allow to run 'nearest neighbours' algorithm to find closely related words from the trained model
  - types
    - skip-grams (sg)
      - predict context words given a target
    - continuous bag of words (cbow)
      - predict target word from bag-of-words context
  - similarity calculated using dot product of vector representations
  - vector dimensionality ranges from 50 to 300
  - often associated with nlp 
    - due to their effectiveness in capturing semantic relationships between words
    - but found applications in many other domains

- sentence embedding
  - encodes sentence similarity

- distributional hypothesis 
  - the more semantically similar two words are, the more distributionally similar they will be in turn, and thus the more that they will tend to occur in similar linguistic contexts


## nlp/nlu

- tokenization

- lower casing

- stop words removal
  - words which are filtered out because they are insignificant for some specific task
  - example: articles

- stemming/lemmatization
  - reduce inflectional forms and sometimes derivationally related forms of a word to a common base form
  - stemming is cruder approach than lemmatization

- tagging
  - part-of-speech [4]
    - coarse-grained (spacy pos_ attribute)
    - fine-grained (spacy tag_ attribute)
  - dependency tagging

- coreference resolution
  - which noun associated with a given pronoun
  - example: pronoun 'she' will be associated or replaced with name 'alice'
  - spacy module: https://spacy.io/universe/project/crosslingualcoreference

- entities identification (named entity recognition)
  - named entity disambiguation
  - entity linking
    - extracted entities from the text are mapped to corresponding unique ids from a target knowledge base

- information extraction


## natural language generation (nlg)

- software process that produces natural language output

- subfield of artificial intelligence and computational linguistics that is concerned with the
  construction of computer systems than can produce understandable texts in english or other human languages from some underlying non-linguistic representation of information

- language production: term preferred by psycholinguists

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
    - llms: large language models


## preprocessing

- eliminate handles and urls
- tokenize the string into words
- remove stop words like "and, is, a, on, etc."
- stemming: convert every word to its stem. 
  - like dancer, dancing, danced, becomes 'danc'
  - you can use porter stemmer to take care of this
- convert all your words to lower case


## gpt

- generative pre-trained transformer

- gpt2: open-source ai model created by openai in february 2019

- LLaMA (large language model meta ai)
  - open-source, created by meta ai, non-commercial license
  - uses open data for training (commoncrawl, c4)
  - models ranging from 7b to 65b parameters
    - 13b version of a model outperforms gpt3 175b on most benchmarks
    - 7b version can run on a local computer
  - alpaca

- rlhf: reinforcement learning from human feedback
  - fine-funing technique that makes trained language models more predictable/focused

- training separated into two stages
    - pretraining
      - uses data from all internet
      - costly: about 2m USD to train
      - produces 'base model'
    - finetuning
      - 100k domain-specific questions/answers/labeled data
      - produces 'assistant model'


## chatgpt

- openai product, closed source

- temperature hyperparameter
  - if the temperature is low, the probabilities to sample other but the class with the highest log probability will be small, and the model will probably output the most correct text, but rather boring, with small variation
  - if the temperature is high, the model can output, with rather high probability, other words than those with the highest probability. The generated text will be more diverse, but there is a higher possibility of grammar mistakes and generation of nonsense


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
- recursive neural tensor networks
  - fancy name for the model that is often? used for tagging


## popular/interesting libraries

- fasttext
  - source https://github.com/facebookresearch/fastText
  - classification (applies labels to chunks of text)
  - fast training as well as pretrained models
  - uses hierarchical classifier, binary tree of the labels (index)
- spacy
  - source https://github.com/explosion/spaCy
  - see corresponding section below for more details
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
- rebel 
  - source: https://github.com/Babelscape/rebel
  - knowledge extraction, has spacy plugin

- nlg
  - NaturalOWL
    - performs nlg on the semantic web
    - adopts a typical natural language generation pipeline (Reiter and Dale, 2000)
      - produces texts in three stages: document planning, microplanning, and surface realization
    - implemented as a java library and protege plugin https://protege.stanford.edu
    - pretty old project, not supported, with lots of outdated hardcoded owl dependencies (urls) in code

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

- popular training sets in 2023
  - common crawl
  - c4
  - github
  - wikipedia
  - books ???
  - arxiv
  - stackexchange


## optimization techniques

- batch gradient descent (bgd)
- stochastic gradient descent (sgd)


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


## books

- building natural language generation systems (ehud reiter, robert dale)
- evolution of grounded spatial language (michael spranger) https://books.google.ca/books?id=z0VFDAAAQBAJ
  - spatial language as complex adaptive system


## software

- nano gpt by andrew karpathy https://github.com/karpathy/nanoGPT

- dalai  https://github.com/cocktailpeanut/dalai
  - web app to run/query language models (alpaca/llama only?) on local computer

- alpaca https://github.com/tatsu-lab/stanford_alpaca
  - meta's llama model fine-tuned by standford

- LLaMA (large language model meta ai) https://ai.facebook.com/blog/large-language-model-llama-meta-ai/

- ollama.ai
  - simple to install local llm model rest server + cli

- lmstudio https://lmstudio.ai/
  - vscode-based local llm ide

- mALIGNa is a program for aligning documents on the sentence level
  - https://github.com/loomchild/maligna


## educational resources

- online
  - coursera nlp specialization
    - is designed and taught by two experts in NLP, machine learning, and deep learning. 
    - Younes Bensouda Mourri is an Instructor of AI at Stanford University who also helped build the Deep Learning Specialization
    - Łukasz Kaiser is a Staff Research Scientist at Google Brain and the co-author of Tensorflow, the Tensor2Tensor and Trax libraries, and the Transformer paper.
  - classification and vector spaces in nlp https://www.coursera.org/learn/classification-vector-spaces-in-nlp?specialization=natural-language-processing


## terminology

- RAG: retrieval augmented generation
  - using your own data to provide it as part of the prompt with which you query the LLM model


## references

[1]: https://medium.com/mysuperai/what-is-named-entity-recognition-ner-and-how-can-i-use-it-2b68cf6f545d
[2]: https://www.kdnuggets.com/2020/01/guide-natural-language-generation.html
[3]: https://www2.arria.com/wp-content/uploads/2017/09/Technical-Overview-The-Arria-NLG-Engine-ARR3027.pdf
[4]: https://stackabuse.com/python-for-nlp-parts-of-speech-tagging-and-named-entity-recognition/
[5]: https://machinelearningknowledge.ai/tutorial-on-spacy-part-of-speech-pos-tagging/
[6]: https://en.wikipedia.org/wiki/Parallel_text
