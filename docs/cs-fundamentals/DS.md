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
    - Simple Queue
    - Circular Queue
    - [Priority Queue](#priority-queue)
    - Dequeue / Double Ended Queue
- [Hash](#hash)
- Matrix

### Non Linear Data Structure
Every data item is attached to several other data items with a relationships.

The data items are not arranged in a sequential structure.

- [Tree](#tree)
    - [Binary Tree](#binary-tree)
        - [Full Binary Tree](#full-binary-tree)
        - [Complete Binary Tree](#complete-binary-tree)
            - Binary Heap
                - Max Heap
                - Min Heap
        - [Perfect Binary Tree](#perfect-binary-tree)
        - [Degenerated / Pathological Tree](#degenerated-pathological-tree)
    - [Binary Search Tree - BST](#binary-search-tree-bst)
        - Self Balancing / Balanced / Height Balanced BST
            - AVL Tree
            - Red-Black Tree
            - Splay Tree
            - Treap
    - K-ary Tree
    - B Tree
        - B+ tree
    - Heap
        - Max Heap
        - Min Heap
        - Binary Heap
        - Bionomial Heap
        - Fibbonacci Heap
    - Trie
    - Misc
        - Indexing with Trees
        - Segment Tree
        - Fenwick Tree
        - Binary Indexed Tree (BIT)
        - Binomial Queues
        - Fibonacci Heaps
        - Leftist Heaps
        - Skew Heaps
        - Open Hash Tables (Closed Addressing)
        - Closed Hash Tables (Open Addressing)
        - Closed Hash Tables, using buckets
- [Graph](#graph)
    - Undirected
    - Directed
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
        - Null Graph
        - Complete Graph
        - Pseudo Graph
        - Regular Graph
        - Bipartite Graph
        - Labelled Graph
        - Connected & Disconnected Graph
        - Cyclic Graph
        - Vertex Labelled Graph
        - Digraph
        - Subgraph

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

## Priority Queue
### Desc
### Properties
### Operations
### Implementation
- Array
- Binary Heap
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
- Root: The top node in a tree.
- Child: A node directly connected to another node when moving away from the Root.
- Parent: The converse notion of a child.
- Siblings: A group of nodes with the same parent.
- Descendant: A node reachable by repeated proceeding from parent to child.
- Ancestor: A node reachable by repeated proceeding from child to parent.
- Leaf: (less commonly called External node) A node with no children.
- Branch: Internal node, A node with at least one child.
- Degree: The number of subtrees of a node.
- Edge: The connection between one node and another.
- Path: A sequence of nodes and edges connecting a node with a descendant.
- **Level**: The level of a node is defined by 1 + (the number of connections between the node and the root).
- **Height of node**: The height of a node is the number of edges on the longest path between that node and a leaf.
- Height of tree: The height of a tree is the height of its root node.
- Depth: The depth of a node is the number of edges from the tree's root node to the node.
- Forest: A forest is a set of n â¥ 0 disjoint trees.

## Why
- need to store in hierchical way, e.g. computer filesystem
- provides quicker insertion/deletion than array but slower than unordered linked list
- No upper limit on number of nodes (like linkedlist & unlike array)

## Application
- Easy to search (using traversal)
- Router Algorithm
- decision making

## Hand Shaking Lemma
In an undirected graph, Number of vertex of odd degree are alway even.
Vertex of odd degree = Vertex connected to 3 edges.

## Binary Tree

### Desc
- tree whose each node have at most 2 children
- children typically known as left and right child.

### Representation
- a node consist of data, pointer to left child, pointer to right child

### Properties
- Level(Root) = 1, but height = 0 (don't get confuse)
- Maximum number of nodes at level $ i = 2^{i-1}$ 
- Level of a Node = Height of the Node + 1
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


## Full Binary Tree
Every node has 0 or 2 children

## Complete Binary Tree
All level are completely filled, except possibly last level and last level has all keys as left as possible.  
Practical e.g.: Binary Heap


                                                  18
                                               /       \  
                                             15         30  
                                            /  \        /  \
                                          40    50    100   40


                                                   18
                                               /       \  
                                             15         30  
                                            /  \        /  \ 
                                          40    50    100   40
                                         /  \   /
                                        8   7  9 



## Perfect Binary Tree
All internal nodes have 2 children and all leaves are at same level.

## Degenerated / Pathological Tree
Every internal node has one child. Performance-wise same as linked list.

## Binary Search Tree (BST)
### Desc
### Operations
- SEARCH, MINIMUM, MAXIMUM, PREDECESSOR, SUCCESSOR, INSERT, DELETE

## Self Balancing Binary Tree

## B-Tree
### Desc
- Generalization of BST i.e. a node can have more than 2 children
### Application
- Indexing in Databases
- Filesystem


## Heap

## Min Heap

## Max Heap

## Trie

# Graph

## Undirected Graph

## Directed Graph

## Directed Acyclic Graph (DAG)

## Directed Cyclic Graph (DCG)

## Weighted Graph

---

# References
- https://gist.github.com/toransahu/bb1c9f1cd6490ff29c42fa229e827a2a
