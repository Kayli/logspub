# notes related to formal language design

## basics

- formal language can be defined via
  - automata
  - grammar

- parse tree (concrete syntax tree, cst)
  - is a concrete representation of the input
  - retains all of the information of the input: whitespace, eol and eof characters, etc.

- abstract syntax tree (ast)
  - is an abstract representation of the input
  - only contains all 'useful' elements that will be used for further processing
    - often does not contain parens, control characters and stuff like that

- production rule
  - is a rewrite rule specifying a symbol substitution that can be recursively performed to generate new symbol sequences

- nonterminal: non-terminating character of a sequence being parsed

- context-free grammar
  - production rules can be applied regardless of the context of a nonterminal
  - the single nonterminal on the left hand side can always be replaced by the right hand side no matter which symbols surround it

- leftmost/rightmost derivation
  - the way production rule transforms a sequence

- LL parsers
  - top-down parser for a restricted context-free language
  - left-to-right, leftmost derivation ?
    - parses the input from Left to right, performing leftmost derivation of the sentence
  - LL(k) parser is a deterministic pushdown automaton with the ability to peek on the next k input symbols without reading

- self-hosting: when compiler is written in the same language it compiles


## grammar

- formal grammar
  - describes how to form strings from a language's alphabet that are valid according to the language's syntax
  - does not describe the meaning of the strings or what can be done with them in whatever context
  - is a set of rules for rewriting strings, along with a "start symbol" from which rewriting starts. 
    - can be thought of as a language generator
  - is a 'recognizer'
    - tells whether a given string belongs to the language or is grammatically incorrect
    - to describe such recognizers, formal language theory uses separate formalisms, known as automata theory
  
- grammar standards
    - ebnf (w3c grammar notation, extended backus–naur form)


## parsers

- components
  - lexer: bundles sequence of characters into sequence of lexical tokens
  - parser: converts lexical tokens into ast

- parser generators/combinators
  - antlr
    - industry standard tool to generate parsers
    - antlr is its own grammar standard
    - supports many languages for generated parsers
  - parsec
    - parser combinator in python
    - source code https://github.com/sighingnow/parsec.py/blob/master/src/parsec/__init__.py
    - some examples https://github.com/sighingnow/parsec.py/tree/master/examples
  - treesitter 
    - source code https://github.com/tree-sitter/tree-sitter
    - python bindings https://github.com/tree-sitter/py-tree-sitter
    - finer-grained update of ast based on stream of changes from the source code


## chomsky hierarchy of languages

- regular (most strict)
  - automata: dfa, nfa
  - grammar: right-linear
- context-free
- context-sensitive
- recursive
  - automata: terminating turing machine
- recursively enumerable
  - automata: turing machine


## libraries

- antlr: parser generator for many languages/platforms
- roslyn: open-source implementation of both the c# and vb compilers with an API surface for building code analysis tools
- lark: parsing toolkit for python
- pypeg: your own parser in python


## interesting resources

- chomsky hierarchy visualization https://www.youtube.com/watch?v=9HBF9StGpjg
- lookahead in parsers https://cs.stackexchange.com/questions/130638/what-does-lookahead-refer-to

