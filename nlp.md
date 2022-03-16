# natural language processing

## basics [^1]

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

- parallel text
  - is a text placed alongside its translation or translations

- parallel corpora
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


## software projects

- mALIGNa is a program for aligning documents on the sentence level
  - https://github.com/loomchild/maligna


## references

[^1]: https://en.wikipedia.org/wiki/Parallel_text
