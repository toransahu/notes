[TOC]

# Introduction

## What is Algorithm?
Step by step instructions to solve a problem.

## Why Analysis of Algorithms?
To determine efficient amongst multiple solution in terms of Time & Space consumed.

## Goal of Analysis of Algorithms?
To compare solutions/algorithms mainly in terms of _running time_, but also in other factors like _memory_, developers effort, readability, simplicity etc.

## What is Running Time Analysis?
Determining how processing time increases with the size of the input (or problem).

## What is Running Time?
_Execution time_ taken by a program in a particular machine? __NO__.

This metric should be independent of other factors like: programing language, execution enviroment i.e. computer, CPU, RAM etc.

So, we express the Running Time as a mathematical function of the input size i.e. $f(n)$.

## How to compare Algorithms?
Using Running Time.

## What is Rate of Growth?
The rate at which the Running Time increases with the size of the input. aka. the rate at which the value of $f(n)$ increases with the $n$.

Say, $g(n)$ such that $f(n) \propto g(n)$.

## Commonly used Rate of Growths
$1 < log{log n} < \sqrt{log n} < log^2n < 2^{log n} < n < log(n!) < n log n < n^2 < 2^n < 4^n < n! < 2^{2^n}$
<!-- > just to fix the syntax highlighting :P-->

## Type of Analysis

Types of analyzing an algorithm.

### Worst Case
This considers the size of input for which the algorithm may take longest time (or algorithm runs slowest).
Thus it defines the Rate of Growth (the influencing factor in the Running Time) for such input.

The asymptotic notation for the same is: $f(n) ~= O(g(n))$

### Best Case
This considers the size of input for which the algorithm may take lowest time (or algorithm runs fastest).
Thus it defines the Rate of Growth (the influencing factor in the Running Time) for such input.

The asymptotic notation for the same is: $f(n) ~= \Omega(g(n))$

### Average Case
This considers a random size of input tries to define the Rate of Growth (the influencing factor in the Running Time) for such input.

The asymptotic notation for the same is: $f(n) ~= \Theta(g(n))$

## What is Asymptotic Notation?
Syntax/Symbol/Expression to represent the different Asymptotic nature of a function.

Lets understand this by taking an example of a function $f(n)$ (which may represent Running Time of an algorithm/solution to a problem) in terms of size of input ($n$).

### Big-O $O$ Notation
This notation gives __smallest__ rate of growth $g(n)$ which is __greater than or equal__ to the Running Time $f(n)$ of the given algorithm/solution.

i.e. there exists some positive constants $n_0$ & $c$:

such that $0 \le f(n) \le cg(n)$;  where $n \ge n_0$

This is also called __tight upper bound__ of the given function.

$f(n) = O(g(n))$

### Omega $\Omega$ Notation
This notation gives __largest__ rate of growth $g(n)$ which is __less than or equal__ to the Running Time $f(n)$ of the given algorithm/solution.

i.e. there exists some positive constants $n_0$ & $c$:

such that $0 \le cg(n) \le f(n)$;  where $n \ge n_0$

This is also called __tight lower bound__ of the given function.

$f(n) = \Omega(g(n))$

### Theta $\Theta$ Notation
This notation defines a rate of growth $g(n)$ such that it falls in between the tight lower & upper bound of the function.

i.e. there exists some positive constants $c_1$, $c_2$, and $n_0$:

such that $0 \le c_1g(n) \le f(n) \le c_2g(n)$; where $n \ge n_0$

This is also called asymptotic __tight bound__ of the given function.

$f(n) = \Theta(g(n))$

## What is Asymptotic-ness?
For a given function $f(n)$ if, another function $g(n)$ tries to approximate $f(n)$; then $g(n)$ is called _asymptotic curve_ for $f(n)$.

## Recurrence Relation

## Master Theorem

If the recurrence relation is of the form:

$T(n) = aT(n/b) + \Theta(n^klog^pn)$


# Dynamic Programing

Dynamic programing is an approach to solve a problem which requires an optimal solutions amongst various other possible solutions.

So, the goal is to get a global optimal solution.

To do so, we analyze the problem and identify a repeated subtask (step) in that. Then we make decision at each step considering current problem and solution to previously solved sub problem to calculate optimal solution.

## Intro

### Memoization
Top - Down approach in a subproblem tree

- Intro
    - divides a big problem into subproblems
    - starts solving smallest problem  first; approaching root of problem
    - memoize/cache the solved subproblems
    - for repeated/same subproblems, utilizes the cache/memoization table
    - uses recursion
- Pros
    - easy implementation
- Cons
    - recusrsion stach could be deeper and that might create stack-overflow/memory issue
- Extra
    - memo table fills up in bottom to top order

### Tabulation
Bottom - Up approach in a subproblem tree

- Intro
    - Understands a root problem and finds subproblems to that
    - starts solving subproblems (in a particular order which approaches the root problem, like smallest to bigger, 1 to 100 etc.) in iterative way
    - store the answer to those subproblems in a table
- Pros
    - avoids recursion stack issue
    - suitable for extremly complicated problems
    - suitable where optimization is concern
        - because it gives flexibility of command over coding style
- Cons
    - need more rigid thinking ahead of time to find the ordering of subproblems so that we do not need to backtrack and solve a smaller problem in order to solve a larger problem

- Extra
    - table fills up in top to bottom order

## Examples    

### Edit Distance

### Knapsack problem

#### 0/1 Knapsack Problem

#### 0/1 Knapsack Problem (with repetition of items)

#### Knapsack Problem (with fractional items)

### Matrix Chain Multiplication

### Longest Common Substring

### Longest Common Subsequence

### Longest Increasing Monotonical Subsequence

### Rod Cutting

---

# Searching Algorithms

## Types

### 1. Linear


### 2. Binary
- **Pre-requisites:** Sorted array of numbers (integers/floats)
- **Method**: Divide and search (conquer)
- Equation: $T(n) = T(n/2) + O(1)$
- **Time Complexity:** $O(log n)$
- Implementation:
    - Recursive
        - Auxilary Space: $O(log n)$  recursion call stack space
    - Iterative
        - Auxilary Space: $O(1)$


### 3. Jump
- **Pre-requisites:** Sorted array of numbers
- **Desc:**
    - Enhancement over linear search.
    - Jumps a step (of $m$) --by index-- and search, if it was searching value 52 and found 55 then will jump a step back and start linear search from that index.
    - Similar to linear search.
- Recurrence Equation: 
    - Total number of comparision in worst case: $(n/m) + (m-1)$ i.e. (total number of jumps + linear search within one step)
    - Best value of $m = \sqrt(n)$
- Time Complexity: $O(\sqrt(n))$ i.e. between $O(linear)$ & $O(binary)$
- Auxiliary Space : $O(1)$


### 4. Interpolation
- **Pre-requisites:** Sorted array
- **Desc:**
    - Enhancement over Binary search.
    - Enhancement:
        - Pivot is calculated based on interpolation, i.e.
        - $Pivot = left + \frac{(right - left)} { (arr[right] - arr[left])  (e - arr[left])}$
- Time Complexity: 
    - $O(log log n)$ (if elements are uniformaly distributed)
    - Worst case: $O(n)$
- Auxilary space: $O(1)$

### 5. Exponential 
- **Pre-requisites:** Sorted array
- **Desc:**
    - Enhancement over binary search.
    - Enhancement: 
        - Find a range where element is present, and then do binary search found range.
        - Range: 
            - Start with subarray of size 1 and chech if last element of subarray is greater than 'e'.
            - If not, then increment size by two times
- Equation:
- Time Complexity: $O(log n)$
- Auxilary Space: $O(1)$ (if used iterative binary search)
- Advantage: Better to use if array is infinite (Unbounded Searches/ Unbounded Binary Search)

### 6.  Ternary
- **Pre-requisites:** Sorted array
- **Desc:**
    - Divide and Conquer + Linear search
    - Same as binary search.
    - When searching space gets shorter, use linear search according to precision = right-left
- Time Complexity: $O(log_3 n)$
- Auxilary Space:
    - Iterative = $O(1)$
    - Recursive = $O(log_3 n)$ recursive stack space
- Application:
    - Unimodel Functions

---    

# Sorting Algorithms


## Types

### 1. Bubble Sort:
- **Description:**
    - Swapping adjacent elements if there are in wrong orders.
- Time Complexity: Always $O(n^2)$ (even for sorted arrays)
- Can be optimized for sorted array 

### 2. Selection Sort:
- **Description:**
    - Pulls a minimum element from unsorted-subarray and appends infront of the array (as a sorted sub-array)
- Time Complexity: $O(n^2)$ (all cases)
- Auxilary Space: $O(1)$

### 3. Insertion Sort:
- **Description:**
    Keep first element on left side, start one by one from $2^{nd}$ element (lets say ith element). Compare the picked element ($i^{th}$) with all the elements in left sub-array (i.e. with $i-1^{th}$ to $0^{th}$).
    If LHS sub-array element is greater than i element, then shift that element right by one index.
    Repeat for all LHS elements.
    Fill the empty cell with picked element.
- **Time Complexity:** 
    - Best Case: $O(n)$; if array is as small as n=1 or array is already sorted
    - Avg Case: $\Theta(n^2)$
    - Worst Case: $O(n^2)$
- **Auxilary Space:** $O(1)$

### 4. Merge Sort
- Description:
    1. Split the array in Binary fashion, till you get minimum/single entity
    2. Start merging 2 single entities --> you'll get 2 sorted sub-array --> merge both
    3. Continue merging till end
- Merge Function:
    1. Merges two sorted sub-arrays by using an extra space of O(n).
    2. Begin from 0th index of both sub-array (using pointers like i,j), do comparision in temporary (un-touched) array
    3. Make changes in original array till both $i$ & $j$ reaches the end of the sub-array
- Time Complexity: 
    - Merge: $O(n)$
    - Merge Sort:
        - Best Case: $O(nlogn)$
        - Avg Case: $O(nlogn)$
        - Worst Case: $O(nlogn)$
- Auxiliary Space: 
    - Merge: $O(n)$
    - Merge Sort: $O(n) + O(1)$
- Algorithmic Paradigm: Divide and Conquer
- Implementations: Recursive only
- Sorting In Place: Yes (No in a typical implementation)
- Applications:
    - Sorting linkedlist in $O(nlogn)$
    - Inversion Count Problem (i.e. in an array $E_i>E_j>E_k$ where $i<j<k$) <!--just to fix syntax hl-->
    - In External Sorting

### 5. Quick Sort Recursive(arr, left, right):
- Description:
    1. Partition the array about a pivot: re-arrange smaller elements in LHS & greater elements in RHS of pivot
    2. Return partitioned index (i.e. index of pivot after re-arrangement)
    3. Re-call quicksort for sub-array smaller than pivot
    4. Re-call quicksort for sub-array greater than pivot
- Partition Function(arr, left, right):
    - Desc:
        - Pick pivot is any preferable fashion:
            1. First element
            2. Last element
            3. Mean
            4. Randon
        - Find index of pivot element in array by counting number of elements smaller than it + re-arranges elements smaller than pivot to left (and greater to right) in original Array.
        - Swap pivot element with element at that index 
        - return the pivot/partioning index
    - Returns: Partitioning Index (Re-calculated index of pivot)
    - Time Complexity: $O(n)$
    - Auxilary Space: $O(1)$
- Time Complexity:
    1. Best Case: $O(nlogn)$ (Occurs when pivot element is middle element value-wise)
    2. Avg Case: $O(nlogn)$ 
    3. Worst Case: $O(n^2)$ (Occurs when pivot element is either smaller or larger element)
- Auxilary Space: $O(1)$
- Algorithm Paradigm: Divide and Conquer
- Implementation: Recursive (Generally) and Iterative
- In-Place: Yes (because auxilary space $O(n)$)
- Recurrence Relation:
    - Best Case: $T(n) = O(n) + 2*T(n/2) == O(nlogn)$
    - Avg Case: $T(n) = O(n) + 2*T(n/2) == O(nlogn)$
    - Worst Case: $T(n) =  O(n) + T(n-1) == O(n^2)$ 
- Applications:
    1. In case of memory limitation this algo is used
- Advantages: 
    1. One of the fastest algo for avg case
    2. Does not need additional memory, i.e. In-place processing/sorting
- Disadvantages:
    1. Worst case complexity $O(n^2)$
    2. speed is not guaranteed

### 5.1 Quick Sort Iterative:
- Description:
    - Use tha same Partition technique
    - Instead of re-calling the quick_sort function, use stack to keep track of left and right indexes of the sub-arrays (LHS & RHS of partition_idx) found after partition. Keep doing this while stack is not empty.
    - At the end partition() will arrange all the elements at their perfect index.

### 6. Heap Sort    
- **Desc:**
    - Make max heap using heapify(). To do so, start from last leaf and make max heap till root node.
    - Loop from last leaf to second node.
        - Swap last leaf with root node in max heap
        - Heapify the sub-tree (by ignoring last leaf) at root node till the loop covers all the nodes except the root node
- **Pre-requisites:** 
- **Useful:**
    - When there is time (Quick's problem) and space (Merge's problem) bound
- **Advantage:**
    - Worst case upper bound is O(nlogn) with only O(1) auxilary space
- **Applications:**
    - Sort a nearly sorted (or K sorted) array
    - k largest(or smallest) elements in an array
- **Time Complexity:** $O(heapify) * O(n) = O(nlogn)$
- **Auxilary Space:** $O(1)$
- **In-Place:** Yes
- **Implementation:** Recursive (Heapify)
- **Algorithm Paradigm:** Comparision Based
- **Data Structure:** Array + Complete Binary Tree
- **Stable:** Not in general
- **Note:** Quick & Merge are better in practice.

### 7. Bucket Sort
- **Pre-requisites:** 
    - Standard: A uniform distributed input array in a range of $[0,1)$. CLRS. 
    - Generalized: A uniform distributed input array in a range of non negative integers + floats. $[0, k)$.
    - Efficient Hash Function (specially in case of "Generalized" implementation.
- **Desc:**
    - Hashing:
        - hash_table_size or number of buckets:
            - = size of input array; Standard
            - OR = $int(sqrt(size))$; Generalized
        - `hash_func() = (element/MAX)* (hash_table_size)`
    - Condition: if $i < k$ then $hash(i) < hash(k)$ <!---->
    - Partion inp array on the basis of hash function, store then in right bucket/array
    - Sort each array using Insertionsort 
    - Merge all sorted arrays into one.
- __Useful:__ When input is uniformly distributed over a positive range
- __Advantage:__ 
    - Sorting in $O(n)$
- __Applications:__
    - When input is uniformly distributed over a positive range
- __Recurrence Equation:__ $\Theta(n) + nO(2 - 1/n)$
- __Time Complexity:__ 
    - Best: $\Omega(n)$
    - Avg: $\Theta(n)$
    - Worst: $\Theta(n^2)$; When all the elements fall under single bucket
- __Auxilary Space:__  $O(bucket size) == O(n)$
- __In-Place:__ No
- __Implementation:__  Iterative
- __Algorithm Paradigm:__ Hashing, Partion
- __Data Structure:__ Hashtable, Array
- __Stable:__ Yes
- __Note:__ If input is not uniformally distributed, but also bucketsort may still run in linear time. CLRS.
- __Why Insertion sort is used here? How overall time complexity of bucketsort is still O(n) then?__
    Following Standard way: As, input is uniformly distributed, On avg each bucket/array will have 1 elements $(k/k=1)$, some may have zero and some may have multiple with same value. And as insertionsort's best case is $O(n)$ (if array size is 1). Hence overall its $O(n)$

### 8. Counting Sort

- __Pre-requisites (Standard):__
    1. Elements should be Non Negative Integers
    2. Over a range of 0 to k where `k < size` of array to maintain $O(n)$
- __Desc:__
    For each element $X$ in the input array find the number of elements smaller than $X$.

- Steps:
    1. Store counts of each element in a counting array
    2. Add previous count to current count, to find index of last occurence of that element
    3. Reverse Iterate over input array & pick index of the element from counting array
    4. Put the element in output array and decrement the count by 1
- __Useful:__ same as pre-requisites
- __Advantage:__
    1. Sorting in $O(n + k)$
- __Applications:__
    1. Same as pre-requisites
    2. As a subroutine in Radix Sort
- __Time Complexity:__
    - Best: $\Omega(n + k)$
    - Avg: $\Theta(n + k)$
    - Worst: $O(n + k)$
- __Auxilary Space:__ $O(counting + output array) == O(n + k)$
- __In-Place:__ No
- __Implementation:__ Iterative
- __Algorithm Paradigm:__ Partial Hashing
- __Data Structure:__ Hashtable, Array
- __Stable:__ Yes (order of elements with same value in input array maintains same order in output)
- __Comparion Sort:__ No
- __Note:__ Can be extended to sort negative integers also

### 9. Radix Sort.

- __Pre-requisites (Standard):__
    - input array have non negative integers
    - range should be $0$ to $n^c$ where $c$ is some constant & numbers are represented in base $n$
    - or each number takes only $log_2n$ bits
- __Desc:__
    - for $1$ to $d$: where d is most significant digit position of MAX element in inp array
    - do counting sort on array (considering current digit of each iteration)
- __Useful:__ same as prerequisites
- __Advantage:__ Better worst case performance than bucket sort's Worst case
- __Applications:__ Card sorting machine
- __Recurrence Equation:__ $n*O(n + k) == O(n + k)$
- __Time Complexity:__
    - Best Case: $\Omega(n + k)$
    - Avg Case: $\Theta(n + k)$
    - Worst Case: $O(n + k)$
- __Auxilary Space:__ $d*O(counting array + output array) = d*O(n + k)$
- __In-Place:__ No
- __Implementation:__ Iterative
- __Algorithm Paradigm:__ Partial Hashing
- __Data Structure:__ Hashtable, array
- __Stable:__ Yes
- __Comparion Sort:__ No
- __Note:__

### 10. Tim sort

#### Quick Sort Vs Merge Sort
- Merge sort is preferred over Quick sort when:
    - Sorting a linkedlist: 
- Quick sort is preferred over Merge sort when:
    - There is memory limitation

---

# Tree Algorithms

## Depth First Search (DFS)
## Breadth First Search (BFS) / Level order traversal

---

# Graph Algorithms

## Depth First Search (DFS)

DFS works in similar manner as pre-order travesal of a tree.

### Idea

The idea is to randomly select a starting vertex and from there start traversing other vertices such that we go through a path at a time till its end depth and start printing the vertices from there while back tracking. Do the same for the rest of the untraversed/unvisited/unprinted paths/vertices.

Imagine a person trying to figure out escape a maze. Trying to explore a path at once till its end (depth).

### Applications
- Finding the path
- To check if the graph is bipartite
- To detect cycles in the graph
- [Topological sort](#topological-sort)
- Solving puzzles as maze
- Finding connected components
- Finding strongly connected components
- Finding "cut vertices"

### Implementation - Standard (Recursive)
- Desc: TODO
- Approach: Recursive
- DS Used: (Internally Stack - for recursive function calls)
- Time Complexity:
    - Best: O(V + E) if used adjacency list; O(V x V) if used adjacency matrix
    - Avg: same
    - Worst: same 
- Auxilary Space:
    - Best: O(V) (to track the visited/unvisited vertices)
    - Avg: same
    - Worst: same
- Disadvantage:
    - TODO

### Properties
TODO

#### Pseudo Code

1. pick/choose a vertex as starting point - randomly
1. find it adjacent vertices
1. mark the the choosen vertex as visited & print it
1. pick one of the adjacent vertices - randomly
1. repeat [2-4] for this node as well; return
1. repeat [4-5] for rest of the unvisited adjacent vertices


### Implementation Using Stack (Iterative, Which is same as Recursive one)
- Desc: TODO
- Approach: Iterative
- DS Used: Stack
- Time Complexity:
    - Best: O(V + E) if used adjacency list; O(V x V) if used adjacency matrix
    - Avg: same
    - Worst: same
- Auxilary Space:
    - Best: O(V) (to track the visited/unvisited vertices + size of Stack)
    - Avg: same
    - Worst: same
- Disadvantage:
    - TODO

#### Pseudo Code

1. mark all the vertices as unvisited
1. pick/choose a vertex as starting point - randomly
1. put that into a stack; mark that as visited; print the vertex
1. find any _one_ of its (the vertex we printed recently) unvisited adjacent vertices
1. put that into the stack; mark that as visited; print the vertex
1. repeat [4-5] until we reach a vertex from where we can't move forward  
   (i.e. it has no adjacent vertices or has no unvisited adjacent vertices)
1. now start back tracking (using the stack) from current vertex
    1. pop the top element from the stack
    1. go back to that vertex
    1. repeat [4-6] for that vertex
1. we may have some unvisited / disconncted graph (vertices) at this moment
    1. so, iterate through all the unvisited vertices (if any)
    2. repeat [2-6] for them


### DFS Tree
TODO

## Breadth First Search (BFS) / Level order traversal

BFS works in similar manner as level-order travesal of a tree.

### Idea

The idea is to randomly select a starting vertex and from there start traversing other vertices such that we visit the adjacent vertices first. Once we visited one level (adjacent vertices at a level), then find adjacent vertices of the previously visited ones, and repeat the step until we visited all the vertices.

### Applications
- Finding the path
- To check if the graph is bipartite
- To find the shortest path between two vetices
- Finding connected components

### Properties
TODO


### Implementation Using Queue (Iterative)

- Desc: TODO
- Approach: Iterative
- DS Used: Queue
- Time Complexity:
    - Best: O(V + E) if used adjacency list; O(V x V) if used adjacency matrix
    - Avg: same
    - Worst: same
- Auxilary Space:
    - Best: O(V) (to track the visited/unvisited vertices + size of Queue)
    - Avg: same
    - Worst: same
- Disadvantage:
    - TODO

#### Pseudo Code

1. mark all the vertices as unvisited
1. pick/choose a vertex as starting point - randomly
    1. put it into a queue 
    1. mark this as visited
1. dequeue and get the item from the queue
1. print the vertex
1. find/explore its unvisited adjacent vertices
    1. mark all of them as visited
    1. put them into the queue
1. repeat [3-5] until the queue is empty
1. we may have some unvisited / disconncted graph (vertices) at this moment
    1. so, iterate through all the unvisited vertices (if any)
    1. repeat [2-6] for them


## Topological Sort

Topological sort, is an ordering of vertices of a DAG in which each vertices[1] comes before, all vertices [2], to which[2] it[1] has outgoing edges.

Saying that, [1] will come before [2], if there is an edge from [1] to [2]

Note: There is no solution if the graph is a) Undirected, or b) Directed with cycle(s) - it will cause a deadlock.

### Idea

Topological sort, arranges the vertices of a DAG in an order of their dependecies in other vertices.
Meaning that, A vertex which is not dependent on (i.e. no edge incidents to it) will be first in the least, and A vertex which is dependent on most of the vertices (or a series of dependecies has to be fullfilled before it) has to at the end of the sorted list.

### Applications
- To execute some inter-dependent tasks/jobs
    - Run pipeline of computing jobs
    - To implement/evaluate formulae in Speadsheet cells
- To detect dead locks
    - To check symbolic link loop (deadlock)

### Properties
- A DAG may have one or more Topological Order
- If all the consecutive vertices in a topological order, are connected by edges, then these edges forms Hamiltonian path
    - If the Hamiltonian path exists, then the topological order is unique; else the DAG can have two or more topological order

### Implementation Using Stack / DFS
- Desc: TODO
- Approach: Iterative+Recursive
- DS Used: Stack
- Time Complexity:
    - Best: O(V + E) if used adjacency list; O(V x V) if used adjacency matrix
    - Avg: same
    - Worst: same
- Auxilary Space:
    - Best: O(V) (to track the visited/unvisited vertices + size of Stack)
    - Avg: same
    - Worst: same
- Disadvantage:
    - TODO

#### Pseudo Code

1. start [perform a tweaked version of DFS of the graph]
1. mark all the vertices unvisited
1. create two stacks (backtrack-stack & topo-stack) to hold |V| number of vertices in each  
   (one to help backtrack, another for topological order)
1. arbitrarily choose a vertex as root to start DFS
1. push that vertex into the backtrack-stack
1. mark that vertex as visited
1. find _one_ of the unvisited adjacent vertices
1. put that unvisted adjacent vertex into the backtrack-stack
1. mark that vertex as visited
1. repeat [7-9] for the current vertex
1. if there is no way further (i.e. no unvisited adjacent vertices); then pop the top element from the backtrack-stack
1. push that popped vertex to the topo-stack
1. go to that popped vertex
1. while backtrack-stack is not empty; repeat [7-14]
1. we may have some unvisited / disconncted graph (vertices) at this moment
    1. so, iterate through all the unvisited vertices (if any)
    1. repeat [4-15] for them
1. while topo-stack is not empty; pop the top element from the stack and print them
1. end

### Implementation Using Queue / In-degree
- Desc: TODO
- Approach: Iterative
- DS Used: Queue
- Time Complexity:
    - Best: O(V + E) if used adjacency list; O(V x V) if used adjacency matrix
    - Avg: same
    - Worst: same
- Auxilary Space:
    - Best: O(V) (to track the visited/unvisited vertices + size of Queue)
    - Avg: same
    - Worst: same
- Disadvantage:
    - TODO

#### Pseudo Code

1. start
1. traverse the graph (adjacency matrix/list) & calculate the in-degree of every vertices
    1. maintain an array to store in-degree of each vertices
    1. traverse the adjacency matrix/list
    1. increment the in-degree value corresponding to vertex if a new edge is known to incident on that
1. if there are vertices with in-degree zero then goto step [4]; else goto step [10]
1. create a queue & enqueue all those vertices with in-degree = 0
1. dequeue an element from the queue
1. print that vertex
1. find all the adjacent vertices of that vertex and decrement their in-degree
1. if the in-degree of any of those adjacent vertices becomes zero, enqueue them
1. while the queue is not empty; repeat [5-8]
1. end

## Shortest Path in Unweighted Graph

Given a _unweighted_ graph (directed/undirected) `G = (V, E)`, and a source/distinguished vertex `S` find the shortest path from `S` to every other vertices in `G`.

### Idea

If the given graph is undirected, treat is as a directed graph by replacing an undirected edge with two directed edges.

Cycles may exist in the graph.

As the graph is unweighted, we can consider the cost of a path between 2 adjacent vertices are either zero or equal (suppose 1) - apply the same for all the `V` in the `G`.

Start traversing the graph starting from `S` in level-order (BFS fashion), meaning explore all the adjacent vertices of the given vertex, then explore the adjacent vertices of them - while doing so, increment the distance of the adjacent vertices (from its parents) by 1.

Interestingly -  we'll be calculating the distance of each vertices only once (keep track of visited vertices), thus we'll not encounter such condition where we'll be updating/overwriting the existing distance, and we also don't need to bother about checking if the newly calculated distance is lesser than the existing one.

Why so? Why the calculated distance/path will be the shortest?
Think we started traversing from `S` parallely (round-robin?) . And a Queue & BFS helped us to achieve so.
This is possible because of the fact that - the distance got calculated by traversing a path - which was shortest among others (think level order traversing) thats why _this_ path brought us to that vertext first (among others) and we calculated the distance. There could be multiple shortest path as well.

At the end, all the vertices will have shortest distance calculated from the vertex `S`.

### Applications
- finding _fastest_ way to go from one place to another

### Properties

### Implementation Using Queue / BFS
- Desc:
- Approach: Iterative / Recursive
- DS Used: 1 Queue, 2 Arrays
- Time Complexity: O(V+E) if adjacency list is used; O(VxV) if adjacency matrix is used
    - Best: --
    - Avg: --
    - Worst: --
- Auxilary Space: O(V)
    - Best: --
    - Avg: --
    - Worst: --
- Disadvantage:
    - can't be applied on a weighted graph

#### Pseudo Code

1. start
1. create a queue
1. create an array to store distances of the vertices from source `S` vertex
1. initialize the distance array `d` with `-1` (or `INF` infinite)
1. mark all the vertices unvisited
1. set the distance from `S` to `S` zero
1. enqueue the source vertex `S`
1. mark that vertex as visited
1. dequeue an element
1. explore the adjacent vertices of that vertex (`u` - dequeued vertex)
1. set the distance of the adjacent vertices to: d(`u`) + 1
1. enqueue them
1. mark them as visited
1. while queue is not empty; repeat [9-13]
1. end

## Dijkstra's Algorithm [Shortest Path, Single Source, Weighted Graph]

Given a _weighted_ graph (directed/undirected) `G = (V, E)`, and a source/distinguished vertex `S` find the shortest path from `S` to every other vertices in `G`.

### Idea

If the given graph is undirected, treat is as a directed graph by replacing an undirected edge with two directed edges. And assigning the same given weight to both the edges.

Cycles may exist in the graph.

As the given graph is _weighted_ in nature, simply following BFS and incrementing the distance (or just keep adding the prev. distance + weight) of a vertex may NOT lead us to find an optimal solution.

Why so? Why wouldn't the same method help us here, as it did in the case of unweighted graph?
As we'll start traversing the paths _parallely_, the  calculated  distance (prev. distance + weight) would become the factor of comparision among candidate paths (to the same vertex from `S`). And blindly following a single/first/nearest (just based on number of edges inbetween) path may lead to an incorrect answer.

This has become an minimization/optimization problem. Greedy approach might have solution for that.

So, this time need to explore all the paths from `S-->v`, visit the same vertex `v` multiple times using all the possible paths to that vertex from `S`. And update/overwrite the existing distance of the vertex `v` from `S` when the newly calculated distance is lesser.

Again, doing this would definitely 

Dijkstra says:

Do this initial exercise:

1. Calculate the distance of the immediate reachable (adjacent) vertices first, and set the distance of other vertices as `INF` (infinite)
2. Mark all the vertices as `not done`

Then perform this sub task:

1. Now pick the one (say `u`) from __all__ vertices whose distance is minimal & is `not done`
2. Find its adjacent vertices (say `v`) and __Relax__ (recalculate the distance & update) them. No need to Relax the `done` marked adjacent vertices (not fruitful).

    Relaxation:
    
    ```
    if d[u] + w(u, v) < d[v]; then
        d[v] = d[u] + w(u, v)
    ```

3. Now, mark that vertex `u` as `done`. 

Then repeat the sub task until all the vertices are marked `done`.

### Properties
- A minimization problem --> an optimization problem --> Greedy method
- May work for negative weights, may not

### Applications
- finding _cheapest_ way to go from one place to another

### Implementation Using Priority Queue + BFS
- Desc:
- Approach: Greedy + BFS
- DS Used: 1 Priority Queue, 1 Array
- Time Complexity:
    - Best: O(V) if no edges between the vertices
    - Avg: 
        - O((V + E) x logV) [# of updates `X` time complexity of insert/enqueue to a priority queue (for V items)] - if adjacency list is used
        - O((V x V) + (E x logV)) [to traverse all the edges (and weigths) `+` # of updates `X` time complexity of insert/enqueue to a priority queue (for V items)] - if adjacency list is used
    - Worst: O(E x logV) if the graph is a complete graph, where |E| ~ |V| x |V|
- Auxilary Space: O(V)
    - Best: --
    - Avg: --
    - Worst: --
- Disadvantage:
    - does a blind search and wastes resources
    - can't guarantee a solution for a negative weighted graph

#### Pseudo Code

1. start
1. create a priority queue
1. create an array to mark vertices as `done`
1. create an array to keep track of the distance (d[v]: S-->v)
1. initialize the distance array to `INF`, but set the distance of source vertex to zero
1. create an array to keep track of the path (u-->v)
1. explore [BFS] the adjacent vertices of the source vertext `S`
1. calculate the distance to those immediate adjacent vertices from `S`
1. update the distance array for those adjacent vertices
1. enqueue them into the priority queue
1. dequeue a vertex from the priority queue (the one with minimum distance from the source vertex)
1. explore [BFS] the adjacent vertices of the current vertex which are `not done`
1. __relax__ (calculate & update) the distance to those adjacent vertices from `S` 
1. if the distances got relaxed due to `current vertex` then:
    1. update the distance array for those adjacent vertices
    1. store the current vertex against these vertices in the path-array  
    (this will help track the shortest path)
1. enqueue them into the priority queue
1. mark the current vertex as `done`
1. while priority queue is not empty; repeat [11-16]
1. end

## Bellman-Ford Algorithm

Given a _weighted_ graph (directed/undirected) `G = (V, E)`, and a source/distinguished vertex `S` find the shortest path from `S` to every other vertices in `G`.

This algorithm can handle the negative weights in the graph which overcomes the drawbacks of Dijkstra's algorithm.

### Idea

If the given graph is undirected, treat is as a directed graph by replacing an undirected edge with two directed edges. And assigning the same given weight to both the edges.

Cycles may exist in the graph. (But not negative weight cycles)

As we've seen in previous simple/greedy algorithms that presence of negative weights may trip the approach and lead to incorrect answers. We need to be more careful and try all the possible paths to a vertex `v` from source `S`. And pick the shortest path (minimum distance) amongst them.

This is again the same minimization/optimization problem, but approach would be Dynamic Programing - where the target would be to optimize the global solution rather just focusing on the local optimal solution.

Bellman-Ford says:

1. List down all the edges
2. And start relaxing a vertex `v` in an edge `u -> v` for all the edges
3. Perform the relaxation of the vertex `v` for `|V| - 1` times (because it might be connected to all the rest of the vertices) - i.e. repeat step 2 `|V| - 1` times
4. If no more relaxation happens/is possible in step 3; then stop

Relaxation:

```
if d[u] + w(u, v) < d[v]; then
    d[v] = d[u] + w(u, v)
```

### Applications
- Negative weights are found in various applications of graphs. For example, instead of paying cost for a path, we may get some advantage if we follow the path.
- in networks, in routing information protocol (RIP)
- finding _cheapest_ way to go (or send something) from one place to another

### Properties
- A minimization problem --> an optimization problem --> Dynamic Programing
    - works in bottom-up manner
- Negative Weight Cycle
- Does not work if there is a negative weight cycle

### Implementation Using Dynamic Programing
- Desc:
- Approach: Dynamic Programing, Recursive
- DS Used:
- Time Complexity:
    - Best:
    - Avg: O(V x E) (# of vertices to be relaxed `x` # of paths/adjacents to be considered while relaxing each vertex)
    - Worst: O(V x V x V) if the graph is a complete graph
- Auxilary Space:
    - Best:
    - Avg:
    - Worst:
- Disadvantage:
    - Does not work if there is a negative weight cycle
    - does not scale well

#### Pseudo Code

## Floyd-Warshall Algorithm for Shortest Paths

### Idea

### Applications

### Properties

### Implementation Using Stack / DFS
- Desc:
- Approach:
- DS Used:
- Time Complexity:
    - Best:
    - Avg:
    - Worst:
- Auxilary Space:
    - Best:
    - Avg:
    - Worst:
- Disadvantage:

#### Pseudo Code

## Kruskal Minimum Cost Spanning Tree Algorithm

### Idea

### Applications

### Properties

### Implementation Using Stack / DFS
- Desc:
- Approach:
- DS Used:
- Time Complexity:
    - Best:
    - Avg:
    - Worst:
- Auxilary Space:
    - Best:
    - Avg:
    - Worst:
- Disadvantage:

#### Pseudo Code

## Prim's Minumum Cost Spanning Tree
## Knuth-Morris-Pratt Algorithm
## Bipartite Matching
## Iterative Deepening Depth First Search (Depth Limited Search)
## A* Search
## Ternary Search
## Meet in the middle
## Strongly Connected Components (SCC)
## Edmonds-Karp Algorithm
## Hungarian Algorithm
## Sweep Line Algorithm
## Graham scan
## Tarjan's Algorithm
## Z algorithm
## Hill Climbing

---

# Number Theory

## Modular Arithmetic
## Fermat’s Theorem
## Chinese Remainder Theorem(CRT)
## Euclidian Method for GCD
## Logarithmic Exponentiation
## Sieve of Eratosthenes
## Euler’s Totient Function

---

# Geometric Algorithms

## 2D Rotation and Scale Matrices
## 2D Rotation and Translation Matrices
## 2D Changing Coordinate Systems
## 3D Rotation and Scale Matrices
## 3D Changing Coordinate Systems

---

# Greedy Algorithms

The problem should be solved in stages, by consider one step a time and one input at a time.
The each step should find a local optimal solution, and those local optimal should lead to global optimal solution.

These algorithms provides a predefined procedure to be followed in each step.

An optimization problem _can_ be solved using greedy approach.

## Elementary cases : Fractional Knapsack Problem, Task Scheduling
## Data Compression using Huffman Trees
## Activity Selection

---

# Misc

## Recursion
## Huffman Coding
## Regex Algorithm (Pattern Matching and Parsing)
## Hashing- Hash Functions
## Monotone Chains Algorithm
## Coordinate Compression
## Ford-Fulkerson Method
## Preflow-Push Algorithm
## Dinic's Algorithm
## Monte Carlo method or Metropolis Algorithm
## Krylov Subspace Iteration Method
## Householder Matrix Decomposition
## QR Algorithm
## Fast Fourier Transform
## Integer Relation Detection Algorithm
## Fast Multipole algorithm
## MinMax Algorithm
## Divide and Conquer Algorithm

---

# References
- https://gist.github.com/toransahu/bb1c9f1cd6490ff29c42fa229e827a2a
