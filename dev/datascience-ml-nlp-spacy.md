# library: spacy

- tasks: part-of-speech tagging, named entity recognition (ner), and dependency parsing
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