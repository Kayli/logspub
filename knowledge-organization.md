# knowledge graphs, ontologies, standards, frameworks and related stuff

- lexicon
  - collection of words, terms, and phrases associated with a knowledge domain
  - there is no other context provided in a lexicon
  - no definitions, no explanations of how terms are related, no prioritization of significance

- gloss
  - a fancy linguistic term for a definition
  - domain-specific single definition
  - glossary is like a lexicon but with glosses added

- taxonomy
  - expressed by
    - hypernymy (vehicle is a hypernym of motorcycle)
      - also called the "is-a" relationship
    - hyponym (motorcycle is a hyponym of vehicle)
  - most of the time, attributes possessed by a concept higher in a taxonomy are also held by its sub-concepts
    - exceptions: emergent attributes and behaviours
  - example: biological tree of life - organized by kingdom, phylum, class, order family, genus, and species

- folksonomy
  - shares features of both a lexicon and a taxonomy, but it is not as deeply structured as a taxonomy
  - example: word cloud (graphical representation of the frequency a term appears in some collection of text. The more frequent the term, the larger the term appears in the graphic)

- ontologies
  - model for knowledge storage and representation
  - desired characteristics: memory, dynamism, polysemy, and automation
  - entails relationships like hypernymy
    - may have hypernymy relationships from multiple overlapping taxonomies
  - include additional types of relationships that are usually binary
    - describe a relationship between exactly two concepts or entities
    - commonly written as either xry (bear is a mammal) or in predicate form (is a mammal: bear)
    - examples: part-whole, property, value
  - semantic triple: binary relation and the two entities x and y connected by it

- knowledge graphs
  - encode structured information of entities and their relations 
  - represented as a directed graph G = (C,R)
    - where 𝐶 is the set of vertices representing concepts
    - and 𝑅 is the set of edges that symbolizes a relationship between two concepts in a graph
  - more dynamic

- semantic network
  - similar concept to a knowledge graph


## knowledge bases

- 2007
  - dbpedia
  - freebase
- 2012
  - knowledge graph (google)
    - building on DBpedia and Freebase among other sources
    - incorporated RDFa, Microdata, JSON-LD content extracted from indexed web pages
      including the CIA World Factbook, Wikidata, and Wikipedia
      
  - wikidata (wikimedia foundation)
    - uses sparql as a query language 
      - rdf query language, semantic query language for databases
    - after glimpsing through articles for about an hour it was hard to understand
      list of main components and how they are related to each other
      - components often referred as 'wikimedia extensions'
        - essentially wikimedia cms plugin thing

- yago https://yago-knowledge.org

- foundational ontologies library (wfol)
  - dolce
  - ochre
  - bfo 

- wordnet (not officially/strictly an ontology, but can be used as one)


## standards

- rdf: resource description framework
- owl: web ontology language


## references

- https://en.wikipedia.org/wiki/Knowledge_graph
- https://en.wikipedia.org/wiki/Google_Knowledge_Graph
