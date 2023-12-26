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

- embeddings
  - vectorized representation of a word or a phrase in nlp
  - often associated with nlp due to their effectiveness in capturing semantic relationships between words
    - but found applications in many other domains
  


## data representations

- word embeddings (word2vec)
  - representation of words for text analysis, typically in the form of a real-valued vector that encodes the meaning of the word such that the words that are closer in the vector space are expected to be similar in meaning
  - you can get 'nearest neighbours' to find closely related words from the trained model
  - types
    - skip-grams (sg)
      - predict context words given a target
    - continuous bag of words (cbow)
      - predict target word from bag-of-words context
  - similarity calculated using dot product of vector representations
  - word embeddings have dimensions ranging from 50 to 300

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


## library: spacy

- tasks: part-of-speech tagging, named entity recognition, and dependency parsing
- encodes all strings to hash values to reduce memory usage and improve efficiency
- pipeline
  - does not support stream processing of data
  - whole text is converted into a document object
  - document object passed from one step of pipeline to the other


- data extraction articles
  - https://www.kaggle.com/code/pavansanagapati/knowledge-graph-nlp-tutorial-bert-spacy-nltk
    - see 'relations extraction' and 'build knowledge graph' sections

- split text into sentences
  >>> from spacy.lang.en import English
  >>> nlp = English()
  >>> nlp.add_pipe('sentencizer')
  >>> doc = nlp(text)
  >>> print(doc.sents)

- part of speech coarse grained tags
  POS	  DESCRIPTION	              EXAMPLES
  ADJ	  adjective	                big, old, green, incomprehensible, first
  ADP	  adposition	              in, to, during
  ADV	  adverb	                  very, tomorrow, down, where, there
  AUX	  auxiliary	                is, has (done), will (do), should (do)
  CONJ	conjunction	              and, or, but
  CCONJ	coordinating conjunction	and, or, but
  DET	  determiner	              a, an, the
  INTJ	interjection	            psst, ouch, bravo, hello
  NOUN	noun	                    girl, cat, tree, air, beauty
  NUM	  numeral	                  1, 2017, one, seventy-seven, IV, MMXIV
  PART	particle	                ’s, not
  PRON	pronoun	                  I, you, he, she, myself, themselves, somebody
  PROPN	proper noun	              Mary, John, London, NATO, HBO
  PUNCT	punctuation	              ., (, ), ?
  SCONJ	subordinating conjunction	if, while, that
  SYM	  symbol	                  $, %, §, ©, +, −, ×, ÷, =, :), 😝
  VERB	verb	                    run, runs, running, eat, ate, eating
  X	    other	                    sfpksdpsxmsa
  SPACE	space

- part of speech fine grained tags
  POS	POS_Description	Fine-grained Tag	Description	Morphology	EXAMPLE
  - adjective (ADJ)
    TAG   Description	            Morphology	                EXAMPLE
    AFX	  affix	                  Hyph=yes	                  The Flintstones were a **pre**-historic family.
    AFX	  affix	                  Hyph=yes	                  The Flintstones were a **pre**-historic family.
    JJ	  adjective	              Degree=pos	                This is a **good** sentence.
    JJR	  adjective, comparative	Degree=comp	                This is a **better** sentence.
    JJS	  adjective, superlative	Degree=sup	                This is the **best** sentence.
    PDT	  predeterminer	          AdjType=pdt PronType=prn	  Waking up is **half** the battle.
    PRP$	pronoun, possessive	    PronType=prs Poss=yes	      **His** arm hurts.
    WDT	  wh-determiner	          PronType=int rel	          It’s blue, **which** is odd.
    WP$	  wh-pronoun, possessive	Poss=yes PronType=int rel	  We don’t know **whose** it is.
  
  ADP	adposition	IN	conjunction, subordinating or preposition		It arrived **in** a box.
  ADV	adverb	EX	existential there	AdvType=ex	**There** is cake.
  ADV	adverb	RB	adverb	Degree=pos	He ran **quickly**.
  ADV	adverb	RBR	adverb, comparative	Degree=comp	He ran **quicker**.
  ADV	adverb	RBS	adverb, superlative	Degree=sup	He ran **fastest**.
  ADV	adverb	WRB	wh-adverb	PronType=int rel	**When** was that?
  CONJ	conjunction	CC	conjunction, coordinating	ConjType=coor	The balloon popped **and** everyone jumped.
  DET	determiner	DT	determiner		**This** is **a** sentence.
  INTJ	interjection	UH	interjection		**Um**, I don’t know.
  NOUN	noun	NN	noun, singular or mass	Number=sing	This is a **sentence**.
  NOUN	noun	NNS	noun, plural	Number=plur	These are **words**.
  NOUN	noun	WP	wh-pronoun, personal	PronType=int rel	**Who** was that?
  NUM	numeral	CD	cardinal number	NumType=card	I want **three** things.
  PART	particle	POS	possessive ending	Poss=yes	Fred**’s** name is short.
  PART	particle	RP	adverb, particle		Put it **back**!
  PART	particle	TO	infinitival to	PartType=inf VerbForm=inf	I want **to** go.
  PRON	pronoun	PRP	pronoun, personal	PronType=prs	**I** want **you** to go.
  PROPN	proper noun	NNP	noun, proper singular	NounType=prop Number=sign	**Kilroy** was here.
  PROPN	proper noun	NNPS	noun, proper plural	NounType=prop Number=plur	The **Flintstones** were a pre-historic family.
  PUNCT	punctuation	-LRB-	left round bracket	PunctType=brck PunctSide=ini	rounded brackets **(**also called parentheses)
  PUNCT	punctuation	-RRB-	right round bracket	PunctType=brck PunctSide=fin	rounded brackets (also called parentheses**)**
  PUNCT	punctuation	,	punctuation mark, comma	PunctType=comm	I**,**me and myself.
  PUNCT	punctuation	:	punctuation mark, colon or ellipsis		colon **:** is a punctuation mark
  PUNCT	punctuation	.	punctuation mark, sentence closer	PunctType=peri	Punctuation at the end of sentence**.**
  PUNCT	punctuation	”	closing quotation mark	PunctType=quot PunctSide=fin	“machine learning**”**
  PUNCT	punctuation	“”	closing quotation mark	PunctType=quot PunctSide=fin	**””**
  PUNCT	punctuation	“	opening quotation mark	PunctType=quot PunctSide=ini	**”**machine learning”
  PUNCT	punctuation	HYPH	punctuation mark, hyphen	PunctType=dash	ML site **-** machinelearningknowledge.ai
  PUNCT	punctuation	LS	list item marker	NumType=ord	
  PUNCT	punctuation	NFP	superfluous punctuation		
  SYM	symbol	#	symbol, number sign	SymType=numbersign	This is hash**#** symbol.
  SYM	symbol	$	symbol, currency	SymType=currency	Dollar **$** is the name of more than 20 curre…
  SYM	symbol	SYM	symbol		this is a symbol **$**
  VERB	verb	BES	auxiliary “be”		Let it **be**.
  VERB	verb	HVS	forms of “have”		I**’ve** seen the Queen
  VERB	verb	MD	verb, modal auxiliary	VerbType=mod	This **could** work.
  VERB	verb	VB	verb, base form	VerbForm=inf	I want to **go**.
  VERB	verb	VBD	verb, past tense	VerbForm=fin Tense=past	This **was** a sentence.
  VERB	verb	VBG	verb, gerund or present participle	VerbForm=part Tense=pres Aspect=prog	I am **going**.
  VERB	verb	VBN	verb, past participle	VerbForm=part Tense=past Aspect=perf	The treasure was **lost**.
  VERB	verb	VBP	verb, non-3rd person singular present	VerbForm=fin Tense=pres	I **want** to go.
  VERB	verb	VBZ	verb, 3rd person singular present	VerbForm=fin Tense=pres Number=sing Person=3	He **wants** to go.
  X	other	ADD	email		example@gmail.com
  X	other	FW	foreign word	Foreign=yes	Hello in spanish is **Hola**
  X	other	GW	additional word in multi-word expression		
  X	other	XX	unknown		
  SPACE	space	_SP	space		
  NIL	missing tag

- dependency tags
	Tag	      Description
  ROOT      root word of a sentence
  det	      determiner
  compound	compound
  nsubj	    nominal subject
  amod	    adjectival modifier
  cc	      coordinating conjunction
  conj	    conjunct
  dobj	    direct object
  relcl	    relative clause modifier
  punct	    punctuation
  ccomp	    clausal complement
  prep	    prepositional modifier
  pobj	    object of preposition
  pcomp	    complement of preposition
  advmod	  adverbial modifier
  aux	      auxiliary
  mark	    marker
  nsubjpass	nominal subject (passive)
  auxpass	  auxiliary (passive)
  advcl	    adverbial clause modifier
  appos	    appositional modifier
  dative	  dative
  acomp	    adjectival complement
  nummod	  numeric modifier
  attr	    attribute
  dep	      unclassified dependent
  agent	    agent
  expl	    expletive
  acl	      clausal modifier of noun (adjectival clause)
  npadvmod	noun phrase as an adverbial modifier
  neg	      negation modifier
  xcomp	    open clausal complement
  intj	    interjection


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


## references

[1]: https://medium.com/mysuperai/what-is-named-entity-recognition-ner-and-how-can-i-use-it-2b68cf6f545d
[2]: https://www.kdnuggets.com/2020/01/guide-natural-language-generation.html
[3]: https://www2.arria.com/wp-content/uploads/2017/09/Technical-Overview-The-Arria-NLG-Engine-ARR3027.pdf
[4]: https://stackabuse.com/python-for-nlp-parts-of-speech-tagging-and-named-entity-recognition/
[5]: https://machinelearningknowledge.ai/tutorial-on-spacy-part-of-speech-pos-tagging/