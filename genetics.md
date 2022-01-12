# notes about genetics and related topics

keywords: biology, bioinformatics, organic-chemistry, gene


## basics

- nucleotide
  - is an organic molecule that is the building block of DNA and RNA
  - also have functions related to cell signaling, metabolism, and enzyme reactions
  - composed of three distinctive chemical sub-units
    - five-carbon sugar molecule
    - nucleobase (the two of which together are called a nucleoside)
    - one phosphate group
  - nitrogen-containing aromatic base attached to a pentose (five-carbon) sugar
    which is in turn attached to a phosphate group

- nucleobase
  - fundamental building blocks of a genome
  - variations
    - adenine   (A)
    - guanine   (G)
    - cytosine  (C)
    - thymine   (T) 
      - dna-only
    - uracil    (U) 
      - rna-only

- nucleoside
  - variations
    - adenosine
    - thymidine
    - cytidine
    - guanosine
    - uridine
  
- nucleic acid
  - sometimes called polynucleotide
  - long chainlike molecules composed of a series of nearly identical building blocks: nucleotides
  - examples: rna, dna

- genetic code
  - rna
    - some ancient bacteria
      - no self-replicators known today
      - hypothetical presnece in ancient life forms
    - some viruses
  - dna
    - most modern cells are dna based
  - functions
    - information storage, replication, transport, catalytic and regulatory

- allele
  - is one of two, or more forms of a given gene variant
    - gene variants are versions of the same gene at the same place on a chromosome


## rna

- is a polymer molecule 
  - essential in various biological roles in coding, decoding, regulation and expression of genes
  - composed of the four nucleotides A, C, G, and U

- functions
  - cellular organisms use messenger RNA (mRNA) to convey genetic information that directs synthesis of specific proteins
  - catalyzing biological reactions
  - controlling gene expression
  - sensing and communicating responses to cellular signals

- limitations
  - unstable, falls apart within hours
  - rna organisms will face major problem: error catastrophe
    - rapid decay of message/information in their genes


## dna

- definition
  - is a polymer of the four nucleotides A, C, G, and T
    which are joined through a backbone of alternating phosphate and deoxyribose sugar residues

- occur in complementary pairs
  - this determined by their ability to form hydrogen bonds between them

- base pair (bp)
  - is a fundamental unit of double-stranded nucleic acids
  - consists of two nucleobases
    - bound to each other by hydrogen bonds
  - size of an individual gene or an organism's entire genome
    - often measured in base pairs
      - because DNA is usually double-stranded
  - A always pairs with T through two hydrogen bonds
  - G always pairs with C through three hydrogen bonds
  - hydrogen-bonded pairs are nearly identical
    - allowing them to bridge the sugar-phosphate chains uniformly
    - this structure, along with the molecule’s chemical stability, makes DNA the ideal genetic material

- codon is a triplet of base pairs 

- gene
  - basic unit of heredity
  - sequence of nucleotides in DNA or RNA that encodes the synthesis of a gene product
    - either RNA or protein
  - each gene is composed by a number of exons and introns
  - each exon is made up of codons

- chromosome
  - long DNA molecule with part or all of the genetic material of an organism
  - each chromosome has several thousand genes
  - contains scaffold or packaging proteins
    - bind to and condense the DNA molecule to maintain its integrity
    - include histones and chaperone proteins
  - histones and chaperanes involved in providing epigenetic function
  - displays a complex three-dimensional structure
    - which plays a significant role in transcriptional regulation
  - each chromosome is duplicated (during an S phase)
    - both copies are joined by a centromere, resulting either in an X-shaped structure
    - centromere – the point where the two chromatids touch
    - joined copies are called sister chromatids
  - humans have a total of 46 chromosomes
    - but there are only 22 pairs of homologous autosomal chromosomes

- homologous chromosomes, homologs, chromosome pair
  - set of one maternal and one paternal chromosome
  - pair up with each other inside a cell during fertilization

- 23 pairs of chromosomes
  - numbered in order of size
  - from 1st the biggest to 22nd the smallest one
  - + 1 with sex pair
    - XX female
    - XY male
      - where Y is the smallest
        - encodes difference between male and female organisms
        - represents almost 2 percent of the total DNA in cells

- transcription process
  - dna -> mrna
    - but what does it?
  - mrna -> aminoacids
    - there is an alphabet of 20 aminoacids
    - transcribed by ribosome machine
  - trna + aminoacids -> protein
    - results in aminoacid chain that folds into a protein
    - proteins play many roles: enzymes 

- reverse transcriptase
  - enzyme used to generate complementary DNA (cDNA) from an RNA template
    - this process is called reverse transcription
  - telomerase reverse transcriptase
    - lengthens telomeres in DNA strands, thereby allowing senescent cells that 
      would otherwise become postmitotic and undergo apoptosis to exceed the 
      Hayflick limit and become potentially immortal, as is often the case with cancerous cells
    - Hayflick limit is the limit on cell replication imposed by the shortening of telomeres 
      with each division. This end stage is known as cellular senescence.


## protein synthesis

- can be divided broadly into two phases
  - transcription
    - happens inside nucleus
    - section of DNA encoding a protein, known as a gene, is converted into a template molecule called messenger RNA (mRNA),
      this conversion is carried out by enzymes, known as RNA polymerases, in the nucleus of the cell
      - in eukaryotes, this mRNA is initially produced in a premature form, pre-mRNA
        - pre-mRNA undergoes post-transcriptional modifications to produce mature mRNA
        - mature mRNA is exported from the cell nucleus via nuclear pores to the cytoplasm of the cell for translation to occur
  - translation
    - happens outside nucleus
    - mRNA is read by ribosomes which use the nucleotide sequence of the mRNA to determine the sequence of amino acids
    - ribosomes catalyze the formation of covalent peptide bonds between the encoded amino acids to form a polypeptide chain

- ribosome
  - cellular particle made of RNA and protein serves as the site for protein synthesis in the cell
  - reads the sequence of the mRNA and, using the genetic code, translates the sequence 
    of RNA bases into a sequence of amino acids


## minimal self-replicators
      
- axenic culture
  - state of a culture in which only a single species, variety, or strain of organism is present
    - and entirely free of all other contaminating organisms
  - typically prepared by subculture of an existing mixed culture

- minimal cell 
  - natural: LUCAs
    - last universal common ancestors
    - there are several of them
      - because of horizontal gene transfer happenning between coexisting replicators
  - synthetic (chassis)
    - 2016 JCVI-Syn3.0, derived from bacterial cell
      - 531,490 bp
        - it has a smaller genome than that of any known organism that can be grown in axenic culture
      - there are only 438 protein-coding genes and 35 RNA-coding genes
      - how hard to prepare such culture?

- see <repo>/notes/comuting.md for info about more generic models


## synthetic biology

- areas of research
  - bioengineering
    - altering dna, making new proteins and protein systems
  - xenobiology
    - describes novel biological systems and biochemistries that differ from the canonical DNA–RNA-20 amino acid system 
    - for example
      - instead of DNA or RNA, XB explores nucleic acid analogues, termed xeno nucleic acid (XNA) as information carriers.
      - it also focuses on an expanded genetic code and the incorporation of non-proteinogenic amino acids into proteins
  - synthetic genomics
    - main goal: artificially create cell genome
    - whole dna is synthesised


## evolutionary models

- fisher's fundamental theorem of natural selection
  - later in 2017 Basener and Sanford showed that [^3]
    - with a more realistic distribution of mutations the population often undergoes perpetual fitness decline
      - this aligns well with observations, where practically all biological populations are finite
    - see simulation at https://people.rit.edu/wfbsma/evolutionary%20dynamics/EvolutionaryModel.html

- modern synthesis
  - early 20th-century synthesis of ideas
  - reconciling Charles Darwin's theory of evolution and Gregor Mendel's ideas on heredity


## python libraries

- http://biopython.org/


## references

[^1]: https://www.britannica.com/science/nucleic-acid
[^2]: https://www.stxnext.com/blog/most-popular-python-scientific-libraries/
[^3]: https://link.springer.com/article/10.1007/s00285-017-1190-x
