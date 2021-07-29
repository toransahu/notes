# Data Structure

<h3>Table of Contents</h3>

[TOC]

# Introduction
- Data structure (is a way) or (are the special format/structures in computer memory) to store & organize the data. 
- To suit a specific purpose.
- So, that we can perform some operations on them like search, add, delete, insert

## Data Structure Vs Data Type

### Data Type
- It is class of objects sharing certain properties.
- It is a premitive element of a particular language like C, C++, Java, Python, Go
- Have predefined characteristics according to the language
- Contains data/information without any semantic
- Can't be reduced anymore
- e.g. integer, float, character, string, boolean


### Data Structure
- It is an abstract description of organization of data & operations on them
- It uses data types
- Can be decomposed to smaller
- DS are data type as well, but not a premitive type

### Abstract Data Type (ADT)
- Its visualization, thought, logical description, or a picture of a new data type which we are going to create
- while DS is a real & concrete thing, we can directly use them

__DS is a super set and Data type is sub set or building block for DS__

---

## Types

### Linear Data Structure
Traverses the data elements sequentially.

Only one data element can directly be reached.

- [Array](#array)
- [Linked List](#linked-list)
    - Singly Linked List
    - Circular Linked List
    - Doubly Linked List
- [Stack](#stack)
- [Queue](#queue)
    - [Simple Queue](#simple-queue)
    - [Circular Queue](#cicular-queue)
    - [Priority Queue](#priority-queue)
    - [Dequeue / Double Ended Queue](#dequeue)
- [Hash](#hash)
- Matrix

### Non Linear Data Structure
Every data item is attached to several other data items with a relationships.

The data items are not arranged in a sequential structure.

- [Tree](#tree)
    - [Binary Tree](#binary-tree)
        - [Full Binary Tree](#full-binary-tree)
        - [Complete Binary Tree](#complete-binary-tree)
            - [Heap](#heap)
        - [Perfect Binary Tree](#perfect-binary-tree)
        - [Binary Search Tree - BST](#binary-search-tree-bst)
        - [Degenerated / Pathological Tree](#degenerated-pathological-tree)
        - Skew Binary Tree
            - Left Skew Tree
            - Right Skew Tree
    - [Binary Search Tree - BST](#binary-search-tree-bst)
        - [Self Balancing / Balanced / Height Balanced BST](#self-balancing-binary-tree)
            - [AVL Tree](#avl-tree)
            - [B-tree](#b-tree)
            - [Red-Black Tree](#red-black-tree)
            - [B+ tree](#b-tree_1)
            - Splay Tree
            - Treap
    - K-ary Tree
    - [Heap](#heap)
        - [Binary Heap](#binary-heap)
            - [Max Heap](#max-heap)
            - [Min Heap](#min-heap)
        - Bionomial Heap
        - Fibbonacci Heap
        - Leftist Heap
        - Skew Heap
    - Trie
    - Misc
        - Indexing with Trees
        - Segment Tree
        - Fenwick Tree
        - Binary Indexed Tree (BIT)
        - Binomial Queues
        - Open Hash Tables (Closed Addressing)
        - Closed Hash Tables (Open Addressing)
        - Closed Hash Tables, using buckets
- [Graph](#graph)
    - Undirected Graph
    - Directed Graph (Digraph)
        - Directed Acyclic Graph (DAG)
        - Directed Cyclic Graph [having cycle(s)] (DCG)
    - Weighted
        - Weighted Undirected Graph
        - Weighted Directed Graph (WITHOUT negative weights)
            - Weighted DAG
            - Weighted DCG
        - Weighted Directed Graph (WITH negative weights)
            - Weighted DAG
            - Weighted DCG
                - WITH Negative Weight Cycle
                - WITHOUT Negative Weight Cycle
    - Misc
        - Finite Graph
        - Infinite Graph
        - Trivial Graph
        - Simple Graph
        - Multi Graph
        - Null Graph (Empty Graph)
        - Complete Graph
        - Pseudo Graph
        - Regular Graph
        - Bipartite Graph
        - Labelled Graph
        - Connected & Disconnected Graph
        - Cyclic Graph
        - Vertex Labelled Graph
        - Subgraph
        - Rooted Graph
        - Mixed Graph
        - Path Graph
        - Planar Graph
        - Cycle Graph
        - Petersen Graph
        - Perfect Graph
        - Cograph
        - Chordal Graph
- Misc
    - Disjoint-set Data Structures
    - Suffix Arrays

---

### Language Specific
1. Python
    - list
    - tuple
    - set
    - dict
        - built-in dict
        - collections.OrderedDict
            - remember insertion order of keys
        - collections.defaultdict
            - return default values for missing keys
        - collections.ChainMap
            - search multiple dicts as a single mapping
        - types.MappingProxyType
            - A wrapper for making read-only dictionaries
1. Java
1. C#
1. Go

---

# Array

# Linked List

## Doubly Linked List

## Circular Linked List

# Stack
LIFO

# Queue
FIFO

## Simple Queue

## Circular Queue

## Dequeue

(aka Doubly eneded queue)

## Priority Queue
### Desc
### Application
- job scheduling
- event-driven simulation
### Properties
### Operations
- INSERT
- MAXIMUM
- EXTRACT-MAX
- REPLACE
### Implementation
- Array/Set/List(LinkedList)
- [Binary Heap](#binary-heap)
- Fibbonacci Heap

# Hash
## Desc
- Linear data structure (ADT) to make lookup fast
- uses a hashing functions, a slot list and, a data list
- time complexity (lookup): 
    - best: O(1)
    - worst: O(n)
## Terminologies
- hash function
    - folding method
    - mid-squared method
- perfect hash functions
- slot/bucket
- load factor
- collision
    - resolution techniques (rehashing)
        - open addressing
            - linear probing
            - quadratic probing
            - disadvantages
                - clustered data 
        - chaining
## Why
- to optimize the look-up speed after binary search and other varients


## Dictionary
- a general concept/data structure that maps keys to values
- many ways to implement dictionary
    - hashtable; O(1) - O(N)
    - red-black tree; always O(longN)

## Hash Table
- synchronized
- thread safe
- can be shared with many threads
- doesn't allows any null key or values

## Hash Map
- non synchronized
- non-thread safe
- can't be shared between many threads without proper synchronization code
- allows one null key and multiple null values
- preferred over hash-table

---

# Tree

## Desc
- Are hierchical data structure
- made up of nodes or vertices and edges without having any cycle
- The tree with no nodes is called the null or empty tree

## Terminologies
- Root: The top node in a tree
- Child: A node directly connected to another node when moving away from the Root
- Parent: The converse notion of a child
- Siblings: A group of nodes with the same parent
- Descendant: A node reachable by repeated proceeding from parent to child
- Ancestor: A node reachable by repeated proceeding from child to parent
- Leaf: (less commonly called External node) A node with no children
- Branch: Internal node, A node with at least one child
- Degree: The number of subtrees of a node
- Edge: The connection between one node and another
- Path: A sequence of nodes and edges connecting a node with a descendant
- __Depth of node__: The depth of a node is the number of edges from the tree's root node to the node
- __Level of node__: All nodes of depth $d$ are at level $d$
- __Height of node__: The height of a node is the number of edges on the longest path between that node and a leaf
- __Depth & Level__ of __root__ node is zero (some may say 1 as well - no problem)
- __Depth & Level__ are measured from top (root) to bottom (leaf)
- __Height__ is measured from bottom (leaf) to top (root)
- __Height__ of the __leaf in last level__ is zero
- __Depth of tree__: The number of edges between root & deepest leaf + 1
- __Level of tree__: The number of levels in the tree (i.e. number of edges between root & deepest leaf + 1; i.e. _same as Depth of tree_)
- __Height of tree__: The height of a tree is the height of its root node using longest path
- Forest: A forest is a set of $n \ge 0$ disjoint trees

## Why
- need to store in hierchical way, e.g. computer filesystem
- provides quicker insertion/deletion than array but slower than unordered linked list
- No upper limit on number of nodes (like linkedlist & unlike array)

## Application
- Easy to search (using traversal)
- Router Algorithm
- decision making

## Hand Shaking Lemma
In an undirected graph, Number of vertex of odd degree are always even

e.g. Vertex of odd degree = Vertex connected to 3 edges.

## Binary Tree

### Desc
- tree whose each node have at most 2 children
- children typically known as left and right child

### Representation
- a node consist of data, pointer to left child, pointer to right child

#### Array Representation
- Root at index $0$
- Left child at index $2 \times i$
- Right child at index $2 \times i + 1$
- Parent at index $i / 2$

Note: 
- The array should be filled with `nil` value for non-existing child nodes
- i.e. if traverse level-by-level, then if there are any missing nodes, then the index of those nodes should be filled with `nil` values

### Properties
- Level(Root) = 0
- Height of tree with only root node = 0
- Maximum number of nodes __possible at level__ $i$ is $2^{i}$ 
- Maximum number of nodes __possible in a binary tree__ of height $h$ is $2^{h+1}-1$ 
- no. of Levels in a Tree = Height of the Tree + 1
- Minimum Possible Height of a tree having N nodes: $h = \lfloor \log_2{(N+1)} \rfloor$
- A binary tree with L leaves is of at least height $h = \lceil \log_2{L} \rceil$
- Number of leaves = Number of internal nodes having 2 children + 1

### Operations
#### [Depth First Traversal](../Algo/#depth-first-search-dfs)
- Types:
    - In Order: left, root, right
    - Pre Order: root, left, right
    - Post Order: left, right, root
- Ways:
    1. Standard (Recursive)
        1. Desc:
        1. Approach: Recursive
        1. DS Used:
    1. Using Stack (Iterative, Which is same as Recursive one)
        1. Desc:
        1. Apprach: Iterative
        1. DS Used: Stack
    1. Without Recursion, Without Stack: Morris Traversal: Based on Threaded Binary Tree
        1. Desc:
        1. Apprach:
        1. DS Used:
- Time Complexity: O(n)
- Auxilary Space:
    - Avg: O(h) due to Recursive call stack; where h is max height of the tree
    - Worst: When tree is skewed tree, i.e. h at last level = $O(\log_2{n})$
- Dis-Advantage:
    - Recursive solution
    - Traversal starts from Leaf, unlike BFS.

#### Breadth First Traversal (Level Order Traversal)
- Way:
    - Using Level By Level Looping:
        - Desc: 
            1. Find out total level of the tree : Traverse each sub-tree + Compare level of left & right
            2. Loop from first level to last
            3. For each level print all the nodes:
                1. If root is empty, return; If level reached 1, print the data
                2. Make Recursive  call for each child by decreasing level by 1
        - Approach: Recursive
        - DS Used: None
    - Using Queue
        - Desc:
            1. If given node is not none, visit & print given node, 
            2. Then enqueue left & right child in the queue (if they are not none).
            3. Dequeue one node from the queue & make recursive call for that node.
        - Approach: Recursive
        - DS Used: Queue
- Time Complexity:  $\theta{(n)}$
- Auxilary Space: 
    - Avg: O(w), where w is max width of the tree
    - Worst: When tree is Perfect tree, i.e. w at last level = $O(\lceil {n/2} \rceil)$
- Advantage:
    - Non recursive solution
    - Traversal starts from root, unlike DFS. So, better if our finding is closer to root.

#### Vertical Order Traversal

When nodes are traversed in vertical lines.

```
          1
        /   \
       2     3
      / \   / \
     4   5 6   7
              /  \
             8    9

Vertical Order should be:

4
2
1 5 6
3 8
7
9
```

TODO

## Views

### Top View of a binary tree
Top view of a binary tree is the set of nodes visible when the tree is viewed from the __top__.

Imagine a real X-mas tree, and view it from sky.

Note: Order of nodes doesn't matter.

```
       1
    /     \
   2       3
  /  \    / \
 4    5  6   7
Top view:
4 2 1 3 7

        1
      /   \
    2       3
      \
        4
          \
            5
             \
               6
Top view:
2 1 3 6
```


### Bottom View of a binary tree
Bottom view of a binary tree is the set of nodes visible when the tree is viewed from the __bottom__.

__Horizontal distance of node__: The distance of a node from root, when measured horizontally (say in x-axis).
And suppose root node lies on y-axis (i.e. x=0).

So, another definition of bottom view: 

Set of bottommost nodes at their horizontal distance, i.e. For each horizontal distance unit, pick the bottom most node.

Note: If there are two bottom most nodes at same horizontal distance, then pick the last/right one.

```
                      20
                    /    \
                  8       22
                /   \      \
              5      3      25
                    / \
                  10    14

        Bottom view: 5, 10, 3, 14, 25
        Horizontal Distance: -2, -1, 0, 1, 2

                      20
                    /    \
                  8       22
                /   \    /   \
              5      3 4     25
                    / \      
                  10    14

              5, 10, 4, 14, 25
```            

### Left View of a binary tree
Left view of a binary tree is the set of nodes visible when the tree is viewed from the __left-side__.

### Right View of a binary tree
Right view of a binary tree is the set of nodes visible when the tree is viewed from the __right-side__.

## Full Binary Tree
Every node __at a particular level__ has 0 or 2 children

## Complete Binary Tree
All level are completely filled, except possibly last level and last level has all keys as left as possible.  
Practical e.g.: Binary Heap


                                                 18
                                               /    \  
                                             15      30  
                                            /  \     / \
                                          40    50  100 40


                                                  18
                                                /    \
                                               /      \  
                                             15        30  
                                            /  \       /  \ 
                                          40    50   100   40
                                         /  \   /
                                        8   7  9 


### Properties
1. height of a complete binary tree (having N nodes) = $\log_2{N}$

## Perfect Binary Tree
All internal nodes have 2 children and all leaves are at same level.

## Degenerated / Pathological Tree
Every internal node has one child. Performance-wise same as linked list.

## Skew (Binary) Tree
A tree with every node having one child only

## Left Skew (Binary) Tree
A tree with every node having one Left child only

## Right Skew (Binary) Tree
A tree with every node having one Right child only

## Binary Search Tree (BST)
### Desc
### Operations
- SEARCH, MINIMUM, MAXIMUM, PREDECESSOR, SUCCESSOR, INSERT, DELETE

## Self Balancing Binary Tree

(aka Balanced / Height Balanced BST)

To over come the downside of the skewed BST, (when its search performance degrades to linear time), various self-balancing BST were proposed around 1962 - 1973.

- AVL Tree [1962]
- B-tree [1970]
- Red-Black Tree [1972]
- B+ tree [1972-73]
- Splay Tree
- Treap

## AVL Tree

First self-balancing BST to overcome the limitations of BST when its skewed.

Invented|By
--------|--
1962|Georgy Adelson-Velsky & Evgenii Landis

Idea: While creating/updating a BST, if the __heights of the two child subtree of a node__ differs by more than 1, then rebalance that node.

Rebalancing is done by performing single or double-step rotation.

Note: Try to rebalance the BST as soon as possible.

### Rotations

#### LL (left-left) Rotation

           5
          /
         4
        / 
       3

Here, the __balance factor__ of the:

- node 3 
    - = height of left subtree - height of right tree
    - = 0 - 0
    - = 0
- node 4 
    - = height of left subtree - height of right tree
    - = 1 - 0
    - = 1
- node 5
    - = height of left subtree - height of right tree
    - = 2 - 0
    - = 2

The balance factor of 5 is not in -1,0,1 (i.e. imbalanced by more than 1).
Thus node 5 is imbalanced due to recent addition of node 3, to which we can reach by following "Left-->Left" i.e. LL.

Thus node 5 is said to be LL imbalanced.

To fix that, rotate the tree around 5 such that, 4 becomes parent of 3 & 5.

(Assume putting a nail under node 5 and pulling 5 1-step towards right)

i.e.

         4
        / \
       3   5

Thus, it is called LL-rotation.


#### RR (right-right) Rotation

        5
         \
          7
           \
            9

Similarly this is called RR imbalance.

If we rotate the tree around node 5, such that node 7 become the parent of the 5 & 9. i.e.

        7
       / \
      5   9
Then, this is called RR rotation.


#### LR (left-right) Rotation

        7
       /
      5
       \
        6

Here, the __balance factor__ of the:

- node 6 
    - = height of left subtree - height of right tree
    - = 0 - 0
    - = 0
- node 5 
    - = height of left subtree - height of right tree
    - = 0 - 1
    - = -1
- node 7
    - = height of left subtree - height of right tree
    - = 2 - 0
    - = 2

The balance factor of 7 is not in -1,0,1 (i.e. imbalanced by more than 1).
Thus node 7 is imbalanced due to recent addition of node 6, to which we can reach by following "Left-->Right" i.e. LR.

Thus node 7 is said to be LR imbalanced.

To fix that, follow a 2-step rotation:

1. swap the node 5 & 6 (doing so, we achieved LL imbalanced state; Note: we changed the side as well)

            7
           /
          6
         /
        5

2. now follow the LL rotation (i.e. rotate the tree around 7 such that, 6 becomes parent of 5 & 7. i.e.

            6
           / \
          5   7

#### RL (right-left) Rotation

        5
         \
          7
         /
        6  

Similarly this is called RL imbalance.

If we:

1. swap the node 7 and 6

        5
         \
          6
           \
            7

1. rotate the tree around node 5, such that node 6 become the parent of the 5 & 7. i.e.

          6
         / \
        5   7

Then, this is called RL rotation.

The shorthand for this 2-step rotation could be:

Replace Parent (node 5) with node L (node 6) and make the Parent (node 5) L child of node 6.


#### Exercises

Q1. 


            7
           / \
          6   St1  
         / \
        5   St2

A.

            6
           / \
          5   7
             / \
            St1 St2

Q2.

        5
       / \
      St1 7
         / \
        6   St2

A.

        6
       / \
      5   7
     /     \
    St1    St2

Q3. 

             7
           /   \
          6     St1
         / \     \
        3   St2   St3
       / \
      1   5
         /
        4 (added 4)

A.

Addition of 4 causes LLRL (no just call it LL) imbalance of node 7.

Now, just focus on node 3, 6, and 7 (as we do in LL rotation).

              6
           /    \
          3       7
         /  \    /  \
        1    5 St1 St2
            /  /
           4  St3

### Complexities

Of|Avg|Worst
--|---|-----
Space|$\Theta(n)$|$O(n)$
Search|$\Theta(log_2{n})$|$O(log_2{n})$
Insert|$\Theta(log_2{n})$|$O(log_2{n})$
Delete|$\Theta(log_2{n})$|$O(log_2{n})$

## B-Tree

(aka Balanced/Bayer/Boeing/Broad/Bushy Tree)

First self-balancing [m-way Search Tree (ST)](#m-way-search-tree) to overcome the limitations of m-way ST when its skewed.

Invented|By
--------|--
1970|Rudolf Bayer & Edward M. McCreight while working at Boeing Research Labs

Idea: While creating/updating a BST, if the __heights of the two child subtree of a node__ differs by more than 1, then rebalance that node.


I see it as: 
- generalization of the AVL tree
- self balanced version of m-way search tree

### Application
- Indexing in Databases
- Filesystem

## Red-Black Tree

## B+ Tree

# K-ary Tree

# M-way Search Tree

# Heap

- Heap are nothing but a speacial form of tree
- The special condition is:
    - the value of a node MUST be $\ge$ (or $\le$ ) value of its children (heap property)
        - notice its different than BST
- Another good to have condition is (not mandatory, but good for performance)
    - all the levels should be fullfilled, except the possible last
    - i.e. all the leaves should be in the level $l$ or $l-1$ (suppose $l$ is height of the tree/root, for $l \gt 0$)
    - i.e. the heap should be a complete binary tree
    - __reason__:
        - it will guarantee $O(log_{2} N)$ to __build__ operation
        - it will guarantee $O(log_{2} N)$ to __insert__ operation
        - because both depends on the height of the heap
            - and $height = log_{2} N$, where $N$ is size of the heap

# Binary Heap
A heap with atmost 2 children

## Applications
- Heap Sort: Heap Sort uses Binary Heap to sort an array in O(nLogn) time.
- Priority Queue: Priority queues can be efficiently implemented using Binary Heap because it supports insert(), delete() and extractmax(), decreaseKey() operations in O(logn) time. Binomoial Heap and Fibonacci Heap are variations of Binary Heap. These variations perform union also efficiently.
- Graph Algorithms: The priority queues are especially used in Graph Algorithms like Dijkstra’s Shortest Path and Prim’s Minimum Spanning Tree.
- Many problems likes
    - K’th Largest Element in an array.
    - Sort an almost sorted array/
    - Merge K Sorted Arrays.

# Min Heap
A __binary__ heap in which the value of a node MUST be $\le$ value of its children

## Operations
- Insertion
- Top/Min
- Delete-Top / Extract-Min (Get & Delete) Top
- Replace


# Max Heap
A __binary__ heap in which the value of a node MUST be $\ge$ value of its children

## Operations
- Insertion
- Top/Max
- Delete-Top / Extract-Max (Get & Delete) Top
- Replace

## Implementations
|Implementation|Insert|Delete-Max|Extract-Min|
|--------------|------|----------|-----------|
|Unordered Array|1|n|n|
|Unordered List|1|n|n|
|Ordered Array|n|1|1|
|Ordered List|n|1|1|
|Binary Search Tree|$log n$|$log n$|$log n$|
|Balanced Binary Search Tree|$log n$|$log n$|$log n$|
|Binary Heaps|$log n$|$log n$|1|



## Operations

# Trie

# Graph

`G = (V, E)`

## Desc
- a data structure describing pairwise relations between objects
- made up of nodes/vertices and edges; with or without having any cycle
- sometimes called undirected graph for distinguishing from a directed graph, or simple graph for distinguishing from a multigraph

## Terminologies
- Vertex (Node/Point): fundamental unit of the graph; 
- Edge (Link/Line/Arc): The connection between one vertex and another
- Degree (of a Vertex): `𝛿(v)` in a graph is the number of edges incident to it
- In Degree: `𝛿 -(v)` number of incoming edges
- Out Degree: `𝛿 +(v)` number of outgoing edges 
- Adjacent Vertex: vertices directly connected to the given vertex
- Adjacency Matrix: `Size: VxV` a matrix denoting (ordered/unordered) relations/edge between all the vertices
- Adjacency List: a map of size `V` of list/linkedlist denoting vertices connected to a particular vertex
- Isolated Vertex: is a vertex with degree zero
- Leaf Vertex (Pendant Vertex): is a vertex with degree one
- Source vertex: is a vertex with indegree zero
- Sink vertex: is a vertex with outdegree zero
- Simplicial vertex: is one whose neighbors form a clique: every two neighbors are adjacent
- Universal vertex: is a vertex that is adjacent to every other vertex in the graph
- Cut vertex: is a vertex the removal of which would disconnect the remaining graph
- Tree: A graph with no cycle; aka Acyclic Connected Graph
- Forest: is a disjoint set (non-overlapping elements in each set) iof trees
- Spanning Tree: A subset of a graph, such that it covers all the vertices of the graph but with minimal edges.
    - Thus, it does NOT have any cycle
    - It is NOT disconncted
    - Can say, every connected & undirected graphs have atleast 1 spanning tree

    ![spanning-tree](https://www.tutorialspoint.com/data_structures_algorithms/images/spanning_trees.jpg)

- Connected components: A connected component or simply component of an undirected graph is a subgraph in which each pair of nodes is connected with each other via a path
- Strongly connected components (SCC): In a directed graph if every vertex is reachable from every other vertex
<!-- - Level -->
<!-- - Height -->
<!-- - Depth -->

## Why
- need to store network of objects / relations between objects
    - e.g. 
        - a map of cities
        - social n/w
    - to describe such complicated thing in less space

## Application
- transport networks
- computer networks
- database relationships
- relationships between electronic components

## Representation

### Adjacency Matrix

A matrix (2-d array) denoting if there is an edge (directed/undirected) between 2 vertices or not.

```
  | 0 1 2 3
--|--------
0 | 0 1 1 1
1 | 0 0 1 0
2 | 1 0 0 1
3 | 0 0 0 0 
```

- Size: V*V
- Advantages
    - Some operations are efficient and easy
- Disadvantages
    - More space
        - could be wastage if the graph is sparse (not dense)

### Adjacency List

A array of list (or a map of list) denoting adjacent vetices of a particular vertex.

```
[0]: [1]-->[2]--[3]
[1]: [2]
[2]: [0]-->[3]
[3]:
```

- Size: E + V
- Advantages
    - less space than adjacency matrix
        - especially when the graph is not dense
- Disadvantages
    - some operations are not efficient using adjacency list
        - where lookup (whether there is an edge between 2 vertices or not) is required
    - deleting a vertex
    - deleting an edge 

### Adjacency Set

TODO

## Operations
- Addition
    - Add Node
    - Add Edge
- Removal
    - Remove Node
    - Remove Edge
- Search
    - Contains - check if the graph contains a given value
    - HasEdge - check if there is an edge between 2 given vertices
- Traversal - traverse the graph & its nodes/edges in various fashion

## Undirected Graph

## Directed Graph

## Directed Acyclic Graph (DAG)

## Directed Cyclic Graph (DCG)

## Weighted Graph

## Subgraph
A graph whose edge & veritices are subset of the other graph.

## Bipartite Graph

A graph whose vertices could be divided/partitioned into 2 sets. Such that vertices of one set incidents an edge to verices on the other set.

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e8/Simple-bipartite-graph.svg/800px-Simple-bipartite-graph.svg.png" style="width:200px"/>

## Complete Graph
A graph whose all the vertices are connected to each other. aka A graph whose all the edges are present.

```
|E| = |V|(|V|-1)/2
```

## Sparse Graph
A graph with relatively less edges.

```
E < |V| * log|V|
```

## Dense Graph
A graph with relatively less edges are missing.

---

# References
- https://gist.github.com/toransahu/bb1c9f1cd6490ff29c42fa229e827a2a
