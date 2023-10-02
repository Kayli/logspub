# notes about algorithms on graphs

## basics

- graph theory is a major branch of combinatorial mathematics

- composed of
  - nodes (also called vertices)
  - links (also called edges, arrows, arcs)

- network science
  - field of science rooted in graph theory

- in scientific literature the terms network and graph are used interchangeably


## variations

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
  - directed (digraph) or undirected
  - cyclic or acyclic
  - sparse or dense
    - density varies from 0 to 1.0
      - where graphs with density 
        - closer to min are considered 'sparse'
        - closer to max are considered 'dense'
    - complete or clique is the one where each vertice is connected to every other one
  - monopartite, bipartite, n-partite
    - node types and well-defined constraints for connections between them
  - hypergraph
    - edges in such graph are called hyperedges and can connect arbitrarily many vertices
  - planar: one that can be drawn on a plane without any edges crossing
  - euclidian: vertices represent points on a plane

- may form trees


## tree

- asylic connected graph
- types
  - rooted tree: has a special 'root' node and no cycles
  - binary tree: up to 2 child nodes and no cycles
    - full: nodes have either 0 or 2 children
    - complete: filled left to right node by node
    - perfect: all leafs are on the same level
    - 3 ways to visit
      - preorder (node, left, right)
      - inorder (left, node, right)
      - postorder (left, right, node)
  - binary search tree
    - complete binary tree
    - preserves invariant: for every node n
      - left child and its subtree has keys less than the node n
      - right child and its subtree has keys larger than the node n
    - implies inorder traversal of nodes, which gives us a sorted array

  - spanning tree
    - subgraph of all nodes but less relationships and no cycles
  - minimum spanning tree
    - subgraph of all nodes
    - connects all the nodes of a subgraph with least number of hops


## representations

- edges array
  - example graph = [ (C, A, 4), (A, C, 1), (B, C, 6) ]
  - simplest representation, rarely used in practice
  - not as efficient as adjacency list

- adjacency matrix
  - example graph = [ [0, 1, 2],
                      [2, 0, 5],
                      [4, 5, 0] ]
  - space-efficient for dense graph representation
  - time complexity of getting an edge weight is O(1)
  - iterating through the edges takes O(V^2) time
  - space complexity of this data structure is O(V^2)

- adjacency lists
  - example weighted_graph = { 'A' : [('B', 4), ('C', 1)],
                               'B' : [('D', 1)] }
  - space-efficient for sparse graphs
  - iterating over the edges is linear


## algorithms

- depth-first search (dfs)
  - can be recursive
  - can be iterative using explicit stack
  - needs an extra loop for handling disconnected subgraphs

- breath-first search (bfs)
  - replacing stack with a queue in iterative implementation of dfs leads to bfs
  - needs an extra loop for handling disconnected subgraphs

- dijkstra shortest path [3]
  - shortest-path tree from a specified source to all possible goals
  - doesn't work on graphs with negative weights

- bellman-ford
  - similar to dijkstra
  - addresses negative weights problem of dijkstra

- a-star
  - finds the shortest path from a specified source to a specified goal


## libraries 

- c++
  - boost graph library (bgl)

- python [1] [2]
  - graph-tool (bgl-based)
  - NetworkX
  - python-igraph
  - easygraph
  - nographs (implicit graphs: the lazy evaluation way for graph analysis)


## references

[1]: https://stackoverflow.com/questions/606516/python-graph-library
[2]: https://wiki.python.org/moin/PythonGraphLibraries
[3]: https://www.youtube.com/watch?v=pVfj6mxhdMw