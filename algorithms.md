# notes on a topic of algorithms


## graphs

- network science
  - field of science rooted in graph theory

- in scientific literature the terms network and graph are used interchangeably

- may differ by number of relationships
  - simple graph
    - nodes can have only one relationship (edge) between them
  - multigraph
    - nodes can have multiple relationships between each other
  - graph or pseudograph
    - same as multigraph but nodes can loop back to themselves

- may vary by nesting depth
  - random network
    - all nodes have the same probability attaching to other nodes
      - average distribution of connections
      - as a result, there are no hierarchies
  - small-world network
    - nodes usually associate with a small group of other nodes (friends)
      - at the same time you're not many hops away from everyone else
    - sometimes referred as 'hub-and-spoke pattern'
  - scale-free network
    - deeply nested hierarchies
    - hub-and-spoke pattern is noticeable independent of scale

- may also be
  - connected or disconnected
  - weighted or unweighted
  - directed or undirected
  - cyclic or acyclic
  - sparse or dense
    - density varies from 0 to 1.0
      - where graphs with density 
        - closer to min are considered 'sparse'
        - closer to max are considered 'dense'
    - complete or clique is the one where each vertice is connected to every other one
  - monopartite, bipartite or n-partite (hypergraph)
    - node types and well-defined constraints for connections between them

  
- may form trees
  - which is asylic undirected graph
  - types
    - rooted tree: root node and no cycles
    - binary tree: up to 2 child nodes and no cycles
    - spanning tree
      - subgraph of all nodes but less relationships and no cycles
    - minimum spanning tree
      - subgraph of all nodes
      - connects all the nodes of a subgraph with least number of hops
    - 
    


