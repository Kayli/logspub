# notes on a topic of algorithms

## basics

- can be specified in english, as a computer program or even a hardware design

- iterative vs recursive
  - recursive is often more elegant but uses stack which may be limiting for large sets

- stable vs unstable sorting algorithms
  - unstable may change order of values with same keys, where stable guarantees initial order
  - starts to matter when you sorting objects

- backtracking
  - class of algorithms, often constraint satisfaction problems
  - algorithm incrementally builds candidates to a solution
  - abandons (backtracks) a candidate as soon as it finds out that it is not a valid one
  - often much faster than brute-force enumeration of all complete candidates, since it can eliminate many candidates with a single test


## data structures

- hashtable
  - synonyms: hashmap, map, dictionary, associative array
  - typical implementation gives access to elements by key in const time
  - implemented as an array containing linked lists
    - keys are mapped to array indexes using hash function
  - load factor: how many items stored comparing to total number of slots available

- binary heap
  - is a binary tree
  - elements can be represented as a binary tree
  - can be stored in array, so that index of element is calculated using formula
    - parent: a[(i-1)/2], left: a[(2*i)+1], right: a[(2*i)+2]
  - types
    - min-heap: parent is less than a child
    - max-heap: child is less than a parent
  - complexity
    - time: linear (search)
    - space: linear

- binary search tree (bst)
  - is a binary tree
  - all elements of a left subtree have less keys comparing to parent
  - all elements of a right subtree have greater keys comparing to parent

- balanced binary tree
  - left and right subtrees of every node differ in height by no more than 1
  - balance is abs(height of the left subtree - height of the right) <=1

- avl tree
  - self-balancing bst
  - has balance theshold (usually 1, but parametrizable)
  - balance is maintained by applying 'rotations' to elements of a tree
  - complexity
    - all operations are logarithmic
    - space is linear

- red–black (rb) trees
  - self-balancing bst
  - may not remain balanced at all times
  - improves insertion/deletion speed
  - may slightly reduce search performance
  - invariants
    - root and null-nodes are always black
    - red nodes always have black parent and children
    - inserted nodes are always red

- splay tree
  - binary tree
  - moves nodes that are frequently searched by a user to the top

- m-way search tree
  - m-1 keys
  - m children max
  - there are only basic rules about how to insert elements, so it can easily become unbalanced

- b-tree
  - is an m-way search tree
  - m/2 children must be there to create ??? 
  - all leafs should be at the same level
  - creation process is bottom-up
  - for every key there is also a pointer stored, which refers to data

- b+ tree
  - only leaf nodes have pointers to data, so every leaf node key has a pointer
  - keys from parent nodes are copied to children
  - leaf nodes are connected, like a linked list


## asymptotic analysis

- notations
  - big-o
    - characterises upper bound for asymptotic behavior of a function
      - function grows no faster than a certain rate
    - non-dominant terms are dropped if they are composed by addition
      - if your algorithm does something that takes log time and then something that takes linear time, complexity will be linear
    - you can't drop terms if they are composed by multiplication
      - if your algorithm does something that takes linear t
    - examples
      - constant     O(1)
      - log:         O(log n)
      - linear:      O(n)
        - fibonacci iterative
      - log-linear:  O(n * log n)
      - quadratic:   O(n^2)
        - fibonacci recursive
      - polynomial:  O(n^const) ???
      - exponential: O(2^n)
      - factorial:   O(n!)

  - omega: characterises lower bound for asymptotic behavior of a function
  - theta: characterises tight bound for asymptotic behavior of a function
    - says that it grows precisely at certain rate
    - based on a highest order term and within a constant factor
  - little-o: upper bound that is not asymptotocally tight
  - little-omega: lower bound that is not asymptotically tight


## search

- linear, sequential
  - complexity
    - time:   linear
    - space:  const

- binary search
  - analogy: phone book
  - operates on a sequence of elements
  - sequence elements
    - need to be sorted
    - need to support comparison operators for equality and ordering
    - need to be indexable
  - complexity
    - time:   worst, average: logarithmic
    - space:  const


## sorting

- naive algorithms
  - bubble
    - complexity
      - time:   worst, average is quadratic
      - memory: constant (inplace)
    - unstable

  - selection
    - complexity
      - time:   worst, average is quadratic
      - memory: constant (inplace)
    - unstable, parallelizable (only inner finding min loop)

  - insertion
    - complexity
      - time:   worst, average is quadratic
      - space:  constant (inplace)
    - stable, not parallelizable (but parallelizable versions of algorithm exist)
    - faster with linked lists
    - can be faster than merge sort for small size sequences
    - algorithm
      - initialize pivot index which divides sorted (left) and unsorted (right) parts
      - increment pivot index
      - enforce sorted requirement for the left part
        - loop through elements of the left part
        - if this is the last element in a left part - do nothing, as element already in a proper place
        - insert element before the one that is greater
          - with an array implementation this will require shifting all elements to the right

- mergesort
  - complexity
    - time:   worst and average are log-linear
    - memory: linear for non-inplace version
  - stable, parallelizable
  - very efficient for sorting linked lists 
  - faster than insertion sort for large-size sequences
  - algorithm
    - split sequence into two equal parts recursively until there is only one element left
    - merge two parts
      - deck of cards analogy is useful
      - take cards from both decks and compare
      - insert smaller one into result array

- quicksort
  - in practice faster than mergesort because of smaller constant factors
  - complexity
    - time:   worst quadratic, average log-linear
    - memory: logarithmic
  - unstable, parallelizable
  - algorithm
    - pivot element needs to be chosen, but can simply take first one
    - split sequence into parts
      - one that less or equal to pivot element
      - another that greater than pivot element
    - recurse sort for each part
    - join parts: lesser + pivot + greater
  - usually combined with insertion sort in practice
    - (sub)arrays below a specific size are not further partitioned, but sorted with insertion sort

- counting sort
  - complexity
    - time:   worst, average: linear
    - memory: linear
  - stable
  - algorithm
    - get bounds of the input data
    - initialize counts array (histogram) based on bounds
    - iterate through input data updating counts array
    - generate sorted array based on counts array (histogram)
    - in jdk is used to sort
      - byte arrays with more than 64 elements
      - short or char arrays with more than 1,750 elements

- radix sort
  - complexity
    - time:   worst, average: linear
    - memory: linear
  - stable, parallelizable
  - best performs when sorting ints
  - algorithm
    - creates ten buckets (radix means base, we're sorting integers, so its base 10)
    - sorts numbers by placing them into buckets based on a single digit
    - numbers are then gathered from buckets in sequential order of the buckets
    - process repeats for every digit, starting from rightmost
    
- heap sort

- bucket sort
  - complexity
    - time: worst quadratic, average linear
    - space: linear
  - elements are distributed among bins
  - elements are sorted within each bin recursively or using other sorting algorithm 
  - size of the bucket: (max - min) / nbuckets


## probablistic algorithms

- examples
  - estimate the value of pi
    - the mathematical constant represents the ratio of the circumference of a circle to its diameter
    - one way to do this is to use the Monte Carlo algorithm: 
      - You could start by drawing a circle on a coordinate plane and inscribing a square around it. Then, you could randomly generate a large number of points within the square and count the number of points that fall within the circle. The ratio of the number of points within the circle to the total number of points is an estimate of the value of pi.


## dynamic programming

- two approaches
  - tabulation: bottom-up approach to essentially caching
    - subproblems are computed first, before proceeding to the top-level one
  - memoization: top-down approach to essentially caching
    - we're starting to solve top problem and then we cache data when needed

- kadane's algorithm
  - finding max subarray tricks: 
    - main 'caching' rule: if the previous sum is positive then take it forward, else not (and reset start index)
    - maintain two max arrays: one for contiguous array another for global max array
    - whenever we find a new global max - save start and end indices

- egg-drop problem
  - given: number of floors and number of eggs
  - goal: find least amount of egg drops to determine a pivotal floor (where egg breaks)


## todo
  
- linear programming
- sudoku solver
- lru-cache


## other stuff

- Monte Carlo algorithm vs Monte Carlo simulation
    - Monte Carlo algorithm is a specific type of algorithm that uses random sampling to solve problems
    - while Monte Carlo simulation is a general term that refers to any simulation that uses random sampling to model the behavior of a system


## references 

[^1]: https://www.interviewkickstart.com/learn
[^2]: https://www.happycoders.eu/algorithms