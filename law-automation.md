# ideas for automation in a law domain (jurisprudence)


## terms

- document automation
  - syn: document assembly, document management
  - refers to design of systems and workflows that assist in the creation of electronic documents
  - this process is increasingly used within certain industries to assemble legal documents, contracts and letters


## interesting ideas

- document automation can be subdivided into 2 relatively independent modules
  - document lifecycle
    - may be implemented reusing existing tools like git
      and wrapping it with additional layer that enforces specific flows/set of invariants
  - document structure analysis
    - adapting existing
      - popular general-purpose languages
        - easily manageable ast model of a program
      - template engines
      - modern nlp frameworks
        - to provide assistance in raw documents parsing, like detecting/normalizing morphological invariants

- provisions [4]
  - parametrized fragments of a regulation
  - can be described according to a metadata scheme which consists of provision types and their arguments
  - provision metadata elements can be grounded into some standard ontology framework

- identified provisions can be represented in a form of a graph and stored in some industry standard graph database


## likely candidates

- software licenses
  - relatively easy to formalize and integrate into ecosystem
  - biggest impact for end users with relatively low effort


## formalised semantics

- problem statement/motivation
  - lack of automation around digital contracts and their validation is concerning
  - i've implicitly and explicitly signed/agreed thousands of contracts while using all kinds of products and services
    - i have no clear track record of this
  - digital services
    - digital agreements are 
      - not easily readable
      - are changing from time to time, so i have to spend time reevaulating them
  - automatic validation/evaluation/reevaluation of contracts does not exist
    - becoming unmanagable pretty quickly
    - results in situation when 
      - people not reading digital contracts
      - blindly clicking 'accept' button
        - just to start using service and hope its gonna be fine
  - system is not making steps to make sure users understand what they are signing up for

- ideal situation from user's perspective
  - for software products and digital services
    - user creates default terms and conditions profile on his machine that defines how it and its data has to be treated
      - examples 
        - can system collect and resell data to third parties?
        - is author of the software legally responsible for software failures?
      - so that user answers typical questions and gives consent to typical actions only once
        - so that user has to compile its profile and understand responsibility of parties only once
    - user terms and conditions profile gets automatically applied whenever its needed by software products and services
      - search engine won't display sites that don't comply with user's terms and conditions profile
      - when you try running app or use service that needs more permissions than your profile defines
        - you asked to review/agree/accept only those few new permissions
          - not the whole terms and conditions document
  - for regular contracts
    - formalized, automatically verifiable semantics should allow user to
      - bring transparency to agreements without need of an expensive lawyer
      - avoid situation when service provider tries to 'muddy the waters' with overcomplicated wording/formulation
  - before using profile
    - system should be able to verify user's understanding of terms
      - user needs to 'pass' some kind of test based on the profile preferences
      - test should likely be in a form of a government certification program
  

- trying to find information about legal documents with formalised semantics
  - https://github.com/mkoniari/LegalParser
  - http://www.akomantoso.org/ OFFICIAL SCHEMA APPROVED AS OASIS STANDARD ON 29 August 2018
  - https://docparser.com/solutions/legal-documets
  - https://hal.archives-ouvertes.fr/hal-01572443/document 
    - problem stated well but proposed solution is far form being satisfactory
  - formal verification https://en.wikipedia.org/wiki/Formal_verification
 
    

## projects and products

- foss
  - https://github.com/accordproject
    - template engine + several templates using esotheric languages
    - attempts parsing of legal documents to match a predefined template, kinda overengineered 
  - https://vernrwalker.github.io/LegalSemanticAnalysis/
    - just bla bla website hosted on a github pages
    - claims to work on some semantic analysis
    - most likely related to government grant geared towards helping veterans or something
  - joinup licensing assistaint
    https://joinup.ec.europa.eu/collection/eupl/solution/joinup-licensing-assistant/jla-find-and-compare-software-licenses

- commercial
  - contract express, exari, hotdocs, avvoka, clarilis, contract mill, legito, precisely, prose, springcm


## ridiculous

- cookies accept/reject shit that regulatory institutions force businesses to put everywhere now is a fucking scam/joke
  - does not solve problem of tracking
    - at best, it makes it slightly harder computationally for some businesses
  - bullshits end users into a false safety mindset


## useful pieces

- [4] The legal system usually suffers from scarce transparency which is caused by a non-systematic organization of the legal order ...
  ... hence the inability to obtain an analytical/systematic vision of a legal order itself, allowing to query
  a legal information system according to the content of each norm ... difficulties in norm accessing by both citizens and legal expert 


## references

- https://en.wikipedia.org/wiki/Document_automation
- https://blog.clause.io/from-document-assembly-to-computable-documents/
- https://accordproject.org/
[4]: https://www.researchgate.net/publication/221539373_Automatic_semantics_extraction_in_law_documents
