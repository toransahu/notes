[TOC]

# Dynamic Programing

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
* **Pre-requisites:** Sorted array of numbers (integers/floats)
* **Method**: Divide and search (conquer)
* Equation: T(n) = T(n/2) + O(1)
* **Time Complexity:** $ O(log n) $
* Implementaion:
    * Recursive
        * Auxilary Space: $ O(log n) $  recursion call stack space
    * Iterative
        * Auxilary Space: $ O(1) $


### 3. Jump
* **Pre-requisites:** Sorted array of numbers
* **Desc:**
    * Enhancement over linear search.
    * Jumps a step (of m) **by index** and search, if it was searching value 52 and found 55 then will jump a step back and start linear search from that index.
    * Similar to linear search.
* Recurrence Equation: 
    * Total number of comparision in worst case: (n/m) + (m-1) i.e. (total number of jumps + linear search within one step)
    * Best value of $m = \sqrt(n)$
* Time Complexity: $ O(\sqrt(n))$ i.e. between O(linear) & O(binary)
* Auxiliary Space : O(1)


### 4. Interpolation
* **Pre-requisites:** Sorted array
* **Desc:**
    * Enhancement over Binary search.
    * Enhancement:
        * Pivot is calculated based on interpolation, i.e.
        * Pivot = $ left + \frac{(right - left)} { (arr[right] - arr[left])  (e - arr[left])} $
* Time Complexity: 
    * $ O(log log n) $ (if elements are uniformaly distributed)
    * Worst case: O(n)
* Auxilary space:
    $ O(1) $  
        

### 5. Exponential 
* **Pre-requisites:** Sorted array
* **Desc:**
    * Enhancement over binary search.
    * Enhancement: 
        * Find a range where element is present, and then do binary search found range.
        * Range: 
            * Start with subarray of size 1 and chech if last element of subarray is greater than 'e'.
            * If not, then increment size by two times
* Equation:
* Time Complexity: O(log n)
* Auxilary Space: O(1) (if used iterative binary search)
* Advantage: Better to use if array is infinite (Unbounded Searches/ Unbounded Binary Search)
    

### 6.  Ternary
* **Pre-requisites:** Sorted array
* **Desc:**
    * Divide and Conquer + Linear search
    * Same as binary search.
    * When searching space gets shorter, use linear search according to precision = right-left
* Time Complexity: O(log<sub>3</sub>n)
* Auxilary Space:
    * Iterative = O(1)
    * Recursive = O(log<sub>3</sub>n) recursive stack space
* Application:
    * Unimodel Functions
    
---    

# Sorting Algorithms


## Types

### 1. Bubble Sort:
* **Description:**
    * Swapping adjacent elements if there are in wrong orders.
* Time Complexity: Always O(n <sup>2 </sup>) (even for sorted arrays)
* Can be optimized for sorted array  

### 2. Selection Sort:
* **Description:**
    * Pulls a minimum element from unsorted-subarray and appends infront of the array (as a sorted sub-array)
* Time Complexity: O(n<sup>2</sup>) (all cases)
* Auxilary Space: O(1)  
    
### 3. Insertion Sort:
* **Description:**
    Keep first element on left side, start one by one from 2nd element (lets say ith element). Compare the picked element (ith) with all the elements in left sub-array (i.e. with i-1<sup>th</sup> to 0<sup>th</sup>).
    If LHS sub-array element is greater than i element, then shift that element right by one index.
    Repeat for all LHS elements.
    Fill the empty cell with picked element.
* **Time Complexity:** 
    * Best Case: O(n); if array is as small as n=1 or array is already sorted
    * Avg Case: Theta(n<sup>2</sup>))
    * Worst Case: O(n<sup>2</sup>)
* **Auxilary Space:** O(1)  

### 4. Merge Sort
* Description:
    1. Split the array in Binary fashion, till you get minimum/single entity
    2. Start merging 2 single entities --> you'll get 2 sorted sub-array --> merge both
    3. Continue merging till end
* Merge Function:
    1. Merges two sorted sub-arrays by using an extra space of O(n).
    2. Begin from 0th index of both sub-array (using pointers like i,j), do comparision in temporary (un-touched) array
    3. Make changes in original array till both i & j reaches the end of the sub-array
* Time Complexity: 
    * Merge: O(n)
    * Merge Sort:
        * Best Case: O(nlogn)
        * Avg Case: O(nlogn)
        * Worst Case: O(nlogn)
* Auxiliary Space: 
    * Merge: O(n)
    * Merge Sort: O(n) + O(1)
* Algorithmic Paradigm: Divide and Conquer
* Implementations: Recursive only
* Sorting In Place: Yes (No in a typical implementation)
* Applications:
    * Sorting linkedlist in O(nlogn)
    * Inversion Count Problem (i.e. in an array Ei>Ej>Ek where i<j<k)
    * In External Sorting  
        
### 5. Quick Sort Recursive(arr,left,right):
* Description:
    1. Partition the array about a pivot: re-arrange smaller elements in LHS & greater elements in RHS of pivot
    2. Return partitioned index (i.e. index of pivot after re-arrangement)
    3. Re-call quicksort for sub-array smaller than pivot
    4. Re-call quicksort for sub-array greater than pivot
* Partition Function(arr,left,right):
    * Desc:
        * Pick pivot is any preferable fashion:
            1. First element
            2. Last element
            3. Mean
            4. Randon
        * Find index of pivot element in array by counting number of elements smaller than it + re-arranges elements smaller than pivot to left (and greater to right) in original Array.
        * Swap pivot element with element at that index 
        * return the pivot/partioning index
    * Returns: Partitioning Index (Re-calculated index of pivot)
    * Time Complexity: O(n)
    * Auxilary Space: O(1)
* Time Complexity:
    1. Best Case: O(nlogn) (Occurs when pivot element is middle element value-wise)
    2. Avg Case: O(nlogn) 
    3. Worst Case: O(n2) (Occurs when pivot element is either smaller or larger element)
* Auxilary Space: O(1)
* Algorithm Paradigm: Divide and Conquer
* Implementation: Recursive (Generally) and Iterative
* In-Place: Yes (because auxilary space O(n))
* Recurrence Relation:
    * Best Case: T(n) = O(n) + 2*T(n/2) == O(nlogn) 
    * Avg Case: T(n) = O(n) + 2*T(n/2) == O(nlogn)
    * Worst Case: T(n) =  O(n) + T(n-1) == O(n<sup>2</sup>) 
* Applications:
    1. In case of memory limitation this algo is used
* Advantages: 
    1. One of the fastest algo for avg case
    2. Does not need additional memory, i.e. In-place processing/sorting
* Disadvantages:
    1. Worst case complexity O(n2)
    2. speed is not guaranteed

### 5.1 Quick Sort Iterative:
* Description:
    * Use tha same Partition technique
    * Instead of re-calling the quick_sort function, use stack to keep track of left and right indexes of the sub-arrays (LHS & RHS of partition_idx) found after partition. Keep doing this while stack is not empty.
    * At the end partition() will arrange all the elements at their perfect index.

### 6. Heap Sort    
* **Desc:**
    * Make max heap using heapify(). To do so, start from last leaf and make max heap till root node.
    * Loop from last leaf to second node.
        * Swap last leaf with root node in max heap
        * Heapify the sub-tree (by ignoring last leaf) at root node till the loop covers all the nodes except the root node
* **Pre-requisites:** 
* **Useful:**
    * When there is time (Quick's problem) and space (Merge's problem) bound
* **Advantage:**
    * Worst case upper bound is O(nlogn) with only O(1) auxilary space
* **Applications:**
    * Sort a nearly sorted (or K sorted) array
    * k largest(or smallest) elements in an array
* **Time Complexity:** O(heapify) * O(n) = O(nlogn)
* **Auxilary Space:** O(1)
* **In-Place:** Yes
* **Implementation:** Recursive (Heapify)
* **Algorithm Paradigm:** Comparision Based
* **Data Structure:** Array + Complete Binary Tree
* **Stable:** Not in general
* **Note:** Quick & Merge are better in practice.

### 7. Bucket Sort
* **Pre-requisites:** 
    * Standard: A uniform distributed input array in a range of [0,1). CLRS. 
    * Generalized: A uniform distributed input array in a range of non negative integers + floats. [0, k).
    * Efficient Hash Function (specially in case of "Generalized" implementation.
* **Desc:**
    * Hashing:
        * hash_table_size or number of buckets:
            * = size of input array; Standard
            * OR = int(sqrt(size)); Generalized
        * hash_func() = (element/MAX)* (hash_table_size)
    * Condition: if i < k then hash(i) < hash(k)
    * Partion inp array on the basis of hash function, store then in right bucket/array
    * Sort each array using Insertionsort 
    * Merge all sorted arrays into one.
* **Useful:** When input is uniformly distributed over a positive range
* **Advantage:** 
    * Sorting in O(n)
* **Applications:**
    * When input is uniformly distributed over a positive range
* **Recurrence Equation:** $\theta(n) + n.O(2 - 1/n)$
* **Time Complexity:** 
    * Best: Omega(n) == $\Omega(n)$
    * Avg: Theta(n)
    * Worst: Theta(n2); When all the elements fall under single bucket
* **Auxilary Space:**  $O(bucket size) == O(n)$
* **In-Place:** No
* **Implementation:**  Iterative
* **Algorithm Paradigm:** Hashing, Partion
* **Data Structure:** Hashtable, Array
* **Stable:** Yes
* **Note:** If input is not uniformally distributed, but also bucketsort may still run in linear time. CLRS.
* **Why Insertion sort is used here? How overall time complexity of bucketsort is still O(n) then?**
    Following Standard way: As, input is uniformly distributed, On avg each bucket/array will have 1 elements (k/k=1), some may have zero and some may have multiple with same value. And as insertionsort's best case is O(n) (if array size is 1). Hence overall its O(n)
    
### 8. Counting Sort

* **Pre-requisites (Standard):**
    1. Elements should be Non Negative Integers
    2. Over a range of 0 to k where k < size of array to maintain O(n)    
* **Desc:**
    For each element X in the input array find the number of elements smaller than X.
Steps:
    1. Store counts of each element in a counting array
    2. Add previous count to current count, to find index of last occurence of that element
    3. Reverse Iterate over input array & pick index of the element from counting array
    4. Put the element in output array and decrement the count by 1
* **Useful:** same as pre-requisites
* **Advantage:**
    1. Sorting in O(n + k)
* **Applications:**
    1. Same as pre-requisites
    2. As a subroutine in Radix Sort
* **Time Complexity:**
    Best: Omega(n + k)
    Avg: Theta(n + k)
    Worst: O(n + k)
* **Auxilary Space:** O(counting + output array) == O(n + k)
* **In-Place:** No
* **Implementation:** Iterative
* **Algorithm Paradigm:** Partial Hashing
* **Data Structure:** Hashtable, Array
* **Stable:** Yes (order of elements with same value in input array maintains same order in output)
* **Comparion Sort:** No
* **Note:** Can be extended to sort negative integers also    

### 9. Radix Sort.

* **Pre-requisites (Standard):**
    * input array have non negative integers
    * range should be 0 to n**c where c is some constant & numbers are represented in base n
    * or each number takes only log2(n) bits
* **Desc:**
    * for 1 to d: where d is most significant digit position of MAX element in inp array
    * do counting sort on array (considering current digit of each iteration)
* **Useful:** same as prerequisites
* **Advantage:** Better worst case performance than bucket sort's Worst case
* **Applications:** Card sorting machine
* **Recurrence Equation:** n*O(n + k) == O(n + k)
* **Time Complexity:**
    * Best Case: Omega(n + k)
    * Avg Case: theta(n + k)
    * Worst Case: O(n + k)
* **Auxilary Space:** d*O(counting array + output array) = d*O(n + k)
* **In-Place:** No
* **Implementation:** Iterative
* **Algorithm Paradigm:** Partial Hashing
* **Data Structure:** Hashtable, array
* **Stable:** Yes
* **Comparion Sort:** No
* **Note:**

### 10. Tim sort

    
#### Quick Sort Vs Merge Sort
* Merge sort is preferred over Quick sort when:
    * Sorting a linkedlist: 
* Quick sort is preferred over Merge sort when:
    * There is memory limitation


---

# Greedy Algorithms

## Types

###  Elementary cases : Fractional Knapsack Problem, Task Scheduling
###  Data Compression using Huffman Trees
###  Activity Selection

---

# Graph/Search Algorithms


## Types

###  Depth First Search (DFS)
###  Breadth First Search (BFS) / Level order traversal
###  Iterative Deepening Depth First Search (Depth Limited Search)
###  A* Search
###  Ternary Search
###  Meet in the middle
###  Strongly Connected Components (SCC)
###  Bipartite Matching
###  Kruskal Minimum Cost Spanning Tree Algorithm
###  Prim's Minumum Cost Spanning Tree
###  Dijkstra's Algorithm for Shortest Paths
###  Floyd-Warshall Algorithm for Shortest Paths
###  Bellman-Ford Algorithm
###  Edmonds-Karp Algorithm
###  Hungarian Algorithm
###  Sweep Line Algorithm
###  Graham scan
###  Tarjan's Algorithm
###  Knuth-Morris-Pratt Algorithm
###  Z algorithm
###  Hill Climbing
### Topological Sort


# Number Theory

## Types

###  Modular Arithmetic
###  Fermat’s Theorem
###  Chinese Remainder Theorem(CRT)
###  Euclidian Method for GCD
###  Logarithmic Exponentiation
###  Sieve of Eratosthenes
###  Euler’s Totient Function


# Geometric Algorithms

## Types

###  2D Rotation and Scale Matrices
###  2D Rotation and Translation Matrices
###  2D Changing Coordinate Systems
###  3D Rotation and Scale Matrices
###  3D Changing Coordinate Systems

# Misc

##  Recursion
##  Huffman Coding
##  Regex Algorithm (Pattern Matching and Parsing)
##  Hashing- Hash Functions
##  Monotone Chains Algorithm
##  Coordinate Compression
##  Ford-Fulkerson Method
##  Preflow-Push Algorithm
##  Dinic's Algorithm
##  Monte Carlo method or Metropolis Algorithm
##  Krylov Subspace Iteration Method
##  Householder Matrix Decomposition
##  QR Algorithm
##  Fast Fourier Transform
##  Integer Relation Detection Algorithm
##  Fast Multipole algorithm
##  MinMax Algorithm
##  Divide and Conquer Algorithm
-----------------------------------

# References
- https://gist.github.com/toransahu/bb1c9f1cd6490ff29c42fa229e827a2a
