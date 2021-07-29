# Algorithms

<h3>Table of Contents</h3>

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

So, we express the Running Time as a mathematican function of the input size i.e. $f(n)$.

## How to compare Algorithms?
Using Running Time.

## What is Rate of Growth?
The rate at which the Running Time increases with the size of the input. aka. the rate at which the value of $f(n)$ increases with the $n$.

Say, $g(n)$ such that $f(n) \propto g(n)$.

Such, $g(n)$ are known as __asymptotic__ in nature to $f(n)$.

## Commonly used Rate of Growths
$1 < log{log n} < \sqrt{log n} < log^2n < 2^{log n} < n < log(n!) < n log n < n^2 < 2^n < 4^n < n! < 2^{2^n}$
<!-- > just to fix the syntax highlighting :P-->

## What is Asymptotic-ness?
For a given function $f(n)$ if, another function $g(n)$ tries to approximate $f(n)$; then $g(n)$ is called _asymptotic curve_ for $f(n)$.

## What is Asymptotic Notation?
Syntax/Symbol/Expression to represent the different Asymptotic nature of a function.

Lets understand this by taking an example of a function $f(n)$ (which may represent Running Time of an algorithm/solution to a problem) in terms of size of input ($n$).

### Big-O 'O' Notation
This notation gives __smallest__ rate of growth $g(n)$ which is __greater than or equal__ to the Running Time $f(n)$ of the given algorithm/solution.

i.e. there exists some positive constants $n_0$ & $c$:

such that $0 \le f(n) \le cg(n)$;  where $n \ge n_0$

This is also called __asymptotically tight upper bound__ of the given function.

$f(n) = O(g(n))$

In this representation/expression $f(n)$ or $O(g(n))$ represents Running Time of an algorithm, $n$ represents the size of the input, $g(n)$ represents the Rate of Growth of the Running Time of the algorithm, and $O$ represents the nature of the asymptoticness of curve $g(n)$ with curve $f(n)$.

### Omega 'Ω' Notation
This notation gives __largest__ rate of growth $g(n)$ which is __less than or equal__ to the Running Time $f(n)$ of the given algorithm/solution.

i.e. there exists some positive constants $n_0$ & $c$:

such that $0 \le cg(n) \le f(n)$;  where $n \ge n_0$

This is also called __asymptotically tight lower bound__ of the given function.

$f(n) = \Omega(g(n))$

### Theta 'Θ' Notation
This notation gives a rate of growth $g(n)$ such that it falls in between the tight lower & upper bound of theRunning Time of the given algorithm.

i.e. there exists some positive constants $c_1$, $c_2$, and $n_0$:

such that $0 \le c_1g(n) \le f(n) \le c_2g(n)$; where $n \ge n_0$

This is also called __asymptotically tight bound__ of the given function.

$f(n) = \Theta(g(n))$

## Type of Analysis

Types of analyzing an algorithm.

### Worst Case
This considers the size of input for which the algorithm may take longest time (or algorithm runs slowest).
Thus it defines the Rate of Growth (the influencing factor in the Running Time) for such input.

We can use any of the asymptotic notation to represent the worst-case Rate of Growth i.e. either $O$ or $\Theta$ or $\Omega$. There is no hard rule to use $O$ to represent the worst-case. Asymptotic notations just tells about the asymptotic nature of the function/curve. It has nothing in specific with the worst/avg/best case analysis.

However, there could be a suitable notation of choice for a type of analysis.
Let's take an example of an algorithm whose Running Time seems to be $f(n) = n^2 + 2n + 1$. 
We can represent the worst-case running time by $\Theta(n^2)$ as for some positive constant $c_1, c_2, n_0$, where $n \ge n_0$ for which the following holds true:

$0 \le c_1g(n) \le f(n) \le c_2g(n)$ i.e. $0 \le c_1*n^2 \le n^2 + 2n + 1 \le c_2*n^2$

Suppose, $n = 1$ & $c_1=4$, $c_2=4$; then $0 \le 4 \le 4 \le 4$. 

Suppose, $n = 1$ & $c_1=3$, $c_2=5$; then $0 \le 3 \le 4 \le 5$.

Also, to be on a safer side we can use $O(n^2)$ to express worst-case running time, like:

For some positive constant $c, n_0$, where $n \ge n_0$ for which the following holds true:

$0 \le f(n) \le cg(n)$ i.e. $0 \le n^2 + 2n + 1 \le c*n^2$

Suppose, $n = 1$ & $c=4$; then $0 \le 4 \le 4$. 
Suppose, $n = 1$ & $c=5$; then $0 \le 4 \le 5$. 

So, we can say $\Theta$ is a __strong__ notion than $O$. And also can say:

1. if $f(n) = \Theta(g(n))$, then $f(n) = O(g(n))$
2. $\Theta(g(n)) \subseteq O(g(n))$

However, using $\Omega$ to denote the worst-case is acceptable but doesn't makes sense. We can say something like: the longest time this algorithm can take will always be more than or equal to 5 minutes. Non sense. Not much of use.

So, the suitable asymptotic notations for this case could be $O$ & $\Theta$.

### Best Case
This considers the size of input for which the algorithm may take lowest time (or algorithm runs fastest).
Thus it defines the Rate of Growth (the influencing factor in the Running Time) for such input.

Suitable asymptotic notations for this case could be $\Omega$ & $\Theta$.

### Average Case
This considers a random size of input tries to define the Rate of Growth (the influencing factor in the Running Time) for such input.

Suitable asymptotic notations for this case could be $\Theta$ & $O$.

## Amortized Analysis

Instead of analysis a data-structure operation and defining the time complexity/cost soley based on that single one, analyse a sequence of data-structure operations and average the cost of all those operations. So that it could be shown that the average cost of an operation is smaller, even though the cost of a single operation within the sequence is expensive.

### How is it different than average-case analyse?
Average case analysis is based on the input to the algorithm, as it assumes that the input provided in this case is a random sized. Thus it relies on a probablistic assumption about the input.

While the amortized analysis does not rely on the input. It applies for all the inputs / any size of input.
Amortized analysis guarantees on the worst-case cost of $N$ operations.

### Techniques
- Aggregate Method
- Accounting Method
- Potential Method

## Recurrence Relation

### Ways to solve recurrence relation
1. Substitution Method (aka Back substitution / Induction)
2. Recursion Tree
3. Master Theorem

Let's understand deriving a recurrence relation and solving it using some examples.

__Example 1: Calculate the time complexity of finding an item in array using Binary Search__?

__Example 2: Calculate the time complexity of finding $n^{th}$ item of the Fibonacci Series__?

A recurrsive solution says that:

$$
F(n) = \left
\{
\begin{array}{lcl} 
0 & if & n=0 \\
1 & if & n=1 \\
F(n-1) + F(n-2) & if & n>1 \\
\end{array}
\right. 
$$

So, the recurrence relation should be: 

$$
T(n) = \left
\{
\begin{array}{lcl} 
1 & if & n \le 1 \\
T(n-1) + T(n-2) & if & n>1 \\
\end{array}
\right. 
$$

Solution using substitution method:

$$
\begin{array}{r, c, l,l}
    T(n) & = & T(n-1) + T(n - 2) & \text{(this will become harder to solve)} \\
    T(n) & \le & T(n-1) + T(n-1)  & \text{(so, approximate} \space T(n-2) \approx T(n-1) \space \text{for upper bound)} \\
    \therefore T(n) & \le & 2 \times T(n-1) & \text{ eq. 1}\\
\end{array}
$$

Let's derive a few other terms using the eq. 1

$$
 \begin{array}{r, c, l,l}
     T(n-1) & \le & 2 \times T(n-2) \\
     T(n-2) & \le & 2 \times T(n-3) \\
     ... \\
     T(1) & = & 1 \\
     T(0) & = & 1 \\
 \end{array}
$$

Now do the substitution

$$
\begin{array}{r, c, l,l}
    T(n) & \le & 2 \times T(n-1) \\
    T(n) & \le & 2 \times [2 \times T(n-2)] \\
    T(n) & \le & 2^3 \times T(n-3) \\
    T(n) & \le & 2^4 \times T(n-4) \\
    ... \\
    T(n) & \le & 2^k \times T(n-k) \\
\end{array}
$$

As we know

$$
\begin{array}{r,c,l}
    T(0) & = & 1 \\
    \therefore T(n-k) & = & 1 \\
    \text{and } n-k & = & 0 \\
    \therefore k & = & n & \text{(for } T(0) = 1 \text{)} \\
\end{array}
$$

Thus

$$
\begin{array}{r,c,l}
    T(n) & \le & 2^n \times T(0) & \text{(for } k=n \text{)} \\
    \therefore T(n) & \le & 2^n \\
    \therefore T(n) & = & O(2^n) & \text{(this is upper bound of the worst case analysis)} \\
\end{array}
$$

However, the tighter bound is $\Theta(\phi^n)$ where $\phi = \frac{1+\sqrt{5}}{2} \approx 1.62 \approx 2$, called as __Golden Ratio__.


__Example 3: Calculate the time complexity of recursive solution of finding the number of ways to reach the top of a stair if allowed steps are 1, 2, and 3__?

## Master Theorem

If the recurrence relation is of the form:

$T(n) = aT(n/b) + \Theta(n^klog^pn)$

TODO

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
- Sorting In Place: Yes (No in a typican implementation)
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
    1. Create a max-heap: Using HEAPIFY (aka `BUILD_<MIN/MAX>_HEAP`. To do so, start from last leaf and make max heap till root node.
    2. EXTRACT (Get and Delete) the Top/Root nodes from the heap one by one to get sorted items
        1. DELETE the top/root node
        1. Fill the empty root position by Swapping the last leaf with root node in max heap
        2. PERCOLATE_DOWN the (newly added) root node (by ignoring nodes added in step #3)
       till the loop covers all the nodes (no need to do anything with the last node in the heap)
    3. While doing step #2, why not add those items/nodes back again to the same array  (start at the end, in right to left direction) so that we can avoid an auxilary space and utilize the same array (to store items in sorted order)
        1. Note: while doing step #2, make sure we're  not considering the nodes added during step #3
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
    - Best value of $m = \sqrt{n}$
- Time Complexity: $O(\sqrt{n})$ i.e. between $O(linear)$ & $O(binary)$
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

# Linkedlist Algorithms

## Remove duplicates
- Remove duplicate nodes from an unsorted linkedlist (w/ auxilary space)
- Remove duplicate nodes from an unsorted linkedlist (w/o auxilary space)

## Reverse the Linkedlist

- Reverse a singly linkedlist
- Reverse a portion of a singly linkedlist
- Reverse a doubly linkedlist
- Reverse a portion of a doubly linkedlist

## Cycle / Loop Detection Algorithms

- Using Hashing/Mapping address of each visited nodes and lookup the map if current node is already mapped there
- By pointing all the visited nodes to A Dummy Node and check if current node already points to the Dummy node
- By adding a flag to each visited nodes and lookup the flag off current node if it is already flagged as visited - applicable only if the nodes are modifiable
- By assigning a special value to each visited nodes and lookup the value of the current node if it is already assigned  that special value - applicable only if the range of the node values are given
- Using Floyd's Cycle Detection Algorithm

## Floyd's Cycle Detection Algorithm

```
        <------------------- S -------------------> <---- X -------
        [a]-->[i]-->[j]-->[k]-->[l]-->[m]-------→ [b] ------→ [d] |
                                                   ↑           |  |
	            	                               |           ↓  |
            	            	                  [e] ←------ [c] ↓
```

A. If a loop is suspected in a linkedlist, then run two pointers - one slow & another fast - starting from the head ($a$). Run the faster pointer double the speed of the slower one. If they meet at some node ($c$), then the loop exists & else not.


B. If a loop has been detected using #A, then idetifying the start of the loop and removing the loop is also possible.


### Axiom A

If in a loop we're at some point $i$, and if we finish $K$ complete (whole number) cycles/rounds of the loop, we'll be back to the same point $i$.  

>  $P_i \cong P_i + K.L$

where:

- $P_i$ is a pointer at some $i^{th}$ node in the __loop__
- $L$ is the length (or number of nodes) of the loop
- $K$ is some non-negative integer

### Lemma A

If pointer $P_s$ and $P_f$ starts from the head ($a$) of the linkedlist. $P_s$ moves 1 node at a time & $P_f$ moves 2 nodes at a time.
Then the __hypothesis__ is _they will meet at some node_ ($c$).

#### Proof

Let's suppose they met $X$ unit far from the start node ($b$) of the loop.

Before they met each other, $P_s$ might have completed $K_1$ whole rounds of the loop and $P_f$ might have completed $K_2$ whole rounds. So,

>
$D_s = S + K_1.L + X$  - where $K_1$ is a whole number  
$D_f = S + K_2.L + X$  - where $K_2$ is a whole number

Also to note that, the speed of the pointer $P_f$ is twice the speed of $P_s$, and they are moving for the same time interval. So, suppose $D_s = D$, then $D_f = 2D$.

Then we can derive the following relation:

$$
\frac{
    \begin{array}{l,c,l}
        +(2D & = & S + K_2.L + X) \\
        -(D & = & S + K_1.L + X)
    \end{array}
}{
    \begin{array}{r,c,l}
        D & = & (K_2 - K_1).L \\
        \therefore D & = & K.L
    \end{array}
}
$$


This equation must holds true for some appropriate values of $D$ & $K$. Thus we can also conclude that our hypothesis that, both slow & fast pointer will meet at some point, is true as well.

#### Corollary / Inference A.1

By Lemma-A, as we know that the speed of the pointer $P_f$ is twice the speed of $P_s$, and they were moving for the same time interval. So,

>
$2.S_s = S_f$  
$\therefore 2.\frac{D_s}{T} = \frac{D_f}{T}$  
$\therefore 2.D_s = D_f$  
$\therefore 2(S + K_1.L + X) = S + K_2.L + X$  
$\therefore 2S + 2K_1.L + 2X = S + K_2.L + X$  
$\therefore S + X = K_2.L - 2K_1.L$  
$\therefore S + X = (K_2 - 2K_1).L$  
$\therefore S = K.L  - X$

By this we can say that the moving $K.L - X$ units from the meeting point $c$, within the loop, is exactly equal to $S$, for some appropriate value of $S, K, X$.

(just remember this relationship)

### Lemma B

If move a pointer from the head $a$ of the linkedlist, and move another pointer from the meeting point $c$, simultaniously, at the same speed, then the __hypothesis__ is both the pointer will meet at the start node $b$ of the loop.

(Note that both the pointers are moving in opposite direction towards each other, thus they are going to meet each other at some node.)

In another word, the __hypothesis__ is, the start node $b$ of the loop could be reached from the meeting point $c$ if we move a pointer $S$ units from the meeting point $c$.

#### Proof

We know that both the pointers (slow an fast) met at node $c$ (meeting point) previously as per Lemma-A.

Now, assume that on moving these two new pointers - one starts from head $a$ & another starts from meeting point $c$ - meets at the start node ($b$) of the loop.

That means $P_s$ reaches the start node $b$ by travelling $D_s$ distance from the head. That is $S$ units.

And, $P_f$ reaches the start node $b$ by travelling $D_f$ distance from the meeting point $c$. That is $L - X$ units.  
But, it is also possible that $P_f$ might have travelled some cycles of the loop before meeting $P_s$. 

Lets assume that $P_f$ might have travelled $J_1$ cycles of the loop. So, $P_f$ reaches the start node $b$ by travelling $J_1.L + (L - X)$ units in total.

i.e. $(J_1 + 1).L - X$

As the speed of both the pointers were same & distance were travelled within the same time interval, we can relate it like:

>
$S_s = S_f$  
$\therefore \frac{D_s}{T} = \frac{D_f}{T}$  
$\therefore D_s = D_f$  
$\therefore S = (J_1 + 1).L - X$  
$\therefore S = J.L - X$  

With the help of Lemma-A & Inference-A.1 we can conclude that this relation $S = J.L - X$ holds true, thus our hypothesis is true as well.

### Applications
- helpful in discovering infinite loop in a computer program
- [more](https://en.wikipedia.org/wiki/Cycle_detection#Applications)

### Pseudo Code

__Input__:= $L$: a singly linkedlist  
__Output__:= `bool`: Loop detected, $L^{'}$: the same linkedlist with loop removed (if any)

1. if $L == \varnothing$; then return ($False, L$)
1. if $L.Head.Next == \varnothing$; then return ($False, L$)
1. if $L.Head.Next == L.Head$; then 
    1. $L.Head.Next = \varnothing$
    1. return ($True, L$)
1. $P_s = L.Head$; $P_f = L.Head$
1. $meetingPoint = \varnothing$
1. __while__ $True$
    1. if $P_s.Next == P_f.Next.Next$; then
        1. $meetingPoint = P_f.Next$
        1. break
    1. if $P_f.Next == \varnothing$ || $P_f.Next.Next == \varnothing$; then
        1. return ($False, L$)
    1. $P_s = P_s.Next$
    1. $P_f = P_f.Next.Next$
1. if $meetingPoint == L.Head$; then
    1. $meetingPoint.Next = \varnothing$
    1. $P_f.Next = \varnothing$
    1. return ($True, L$)
1. $P_s = L.Head; P_f = meetingPoint$
1. __while__ $True$
    1. if $P_s.Next == P_f.Next$; then
        1. break
    1. $P_s = P_s.Next$
    1. $P_f = P_f.Next$
1. $P_f.Next = \varnothing$
1. return ($True, L$)

### Analysis

- Time Complexity: 
    - Worst case: $O(S + K.L + X) + O(S) = O(N)$; when $S >> L$
    - Avg case: $O(S + K.L + X) + O(S) = O(N)$;
    - Best case: $O(S + K.L + X) + O(S) = O(1)$; when $S=0; X=0 L = 1$
- Space Complexity: $O(1)$

---

# Tree Algorithms

## Depth First Search (DFS)
## Breadth First Search (BFS) / Level order traversal

---

# Heap Algorithms

## Heap implemented using (Complete) Binary Tree

- [Basic](https://github.com/toransahu/goutils/blob/master/adt/heap/heap.go#L44-L82)
    - Insert
    - Top
    - Extract Top
    - Replace
- [Internal](https://github.com/toransahu/goutils/blob/master/adt/heap/heap.go#L84-L156)
    - percolate-down
    - percolate-up
    - heapify
- Creation
    - [Build](https://github.com/toransahu/goutils/blob/master/adt/heap/heap.go#L34-L42)


### `heapify()` 

#### Pseudo Code

__input__ = an array $arr$ of numbers  
__output__ = array ordered to follow min-heap properties  
__return__ = none

```python
for i in range(arr.length - 1 to 0):
    percolate_down(arr, i)
```

#### Analysis

##### Asymptotically

$T(n) = n * O(log_2{n})$  
$T(n) = O(nlog_2{n})$  

##### Amortized 

Worst case running time of $heapify()$ =  
percolate down all the nodes at last/leaf ($h$) level to 0 steps/levels  (note: level start from top, i.e. 0 and, $h$ is total height of the heap)  
+ percolate down all the nodes at second last ($h-1$) level to 1 steps/levels  
+ percolate down all the nodes at third last ($h-2$) level to 2 steps/levels  
+ ...  
+ percolate down all the nodes at $h - i$ level to $i$ steps/levels  
+ ...  
+ percolate down all the nodes at zeroth ($0$) level to $h$ steps/levels  


i.e. $T(n) = \sum_{i=1}^{h}$ percolate down all the nodes at level=$h-i$ to $i$ steps/levels  

$\therefore T(n) = \sum_{i=0}^{h}$ (number of nodes at level $h - i$ to percolate down) $\times$ (cost of percolate down a node to $i$ levels)  

$\therefore T(n) = \sum_{i=0}^{h} 2^{h-i} \times O(i)$  $\because$ number of nodes a level $x = 2^{x}$  

$\therefore T(n) = \sum_{i=0}^{\log_2{n}} 2^{h-i} \times i$  $\because$ height $h$ of a heap = $\log_2{n}$  

$\therefore T(n) = \sum_{i=0}^{\log_2{n}} 2^{\log_2{n}-i} \times i$

$\therefore T(n) = \sum_{i=0}^{\log_2{n}} \frac{2^{\log_2{n}}}{2^i} \times i$

$\therefore T(n) = \sum_{i=0}^{\log_2{n}} \frac{n}{2^i} \times i$

$\therefore T(n) = n \times \sum_{i=0}^{\log_2{n}} \frac{i}{2^i}$

$\therefore T(n) \le n \times 2 \because \sum_{i=0}^{\infty} \frac{i}{2^i} = 2$  (upper bound)  

$\therefore T(n) \le O(n)$


### `percolateDown()` 

#### Pseudo Code

__input__ = an array $arr$ of numbers, some index $i$ (index starting at $0$)  
__output__ = item at index $i$ in the array gets repositioned to follow min-heap properties  
__return__ = none

1. if the node at given index $i$ is a leaf node or non-existing node 
    1. __return__
- $leftChildPos := 2*i + 1$
- $rightChildPos := 2*i + 2$
- $minimumNodePos := i$
- if $leftChildPos$ exists and $arr[leftChildPos] \lt arr[i]$:
    1. $minimumNodePos := leftChildPos$
- if $rightChildPos$ exists and $arr[rightChildPos] \lt arr[i]$:
    1. $minimumNodePos := rightChildPos$
- if $i$ and $minimumNodePos$ are not same:
    1. swap item at index $minimumNodePos$ and $i$
    - $percolateDown(arr, minimumNodePos)$

#### Analysis

At worst, a node might have to reposition/move from root to leaf position. Saying that, it might need tree/heap __height__ / __level__ steps i.e. $\log_2{n}$. Where $n$ is number of nodes in the heap.

##### Recurrence relation

$T(n) = T(n/2) + C$ 

i.e. size of the problem is reducing by half (no. of nodes at a left or right sub-tree) each time.

By substitution method:

$$
\frac{
    \begin{array}{l,c,l}
        T(n) = T(n/2) + C \\
        T(n/2) = T(n/2^2) + C \\
        T(n/4) = T(n/2^3) + C \\
        ... \\
        T(1) = 1 \\
        T(0) = 1 \\
    \end{array}
}{
    \begin{array}{r,c,l}
        T(n) = T(n/2^k) + k*C 
    \end{array}
}
$$

Suppose for some $k$, $n/2^k$ becomes 1 so $T(n/2^k) = 1$ i.e. $T(1) = 1$.  

Thus,

$n/2^k =1$  
$n = 2^k$  
$log_2{n} = log_2{2^k}$  
$log_2{n} = k$  
i.e. $k = log_2{n}$  

by putting the value of $k$ in form of $n$  


$T(n) = T(1) + log_2{n}*C$  
$T(n) = 1 + log_2{n}*C$  
$T(n) = O(1) + O(log_2{n})$  
$T(n) = O(log_2{n})$  


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
- [Topologican sort](#topological-sort)
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
1. repeat [4-5] untin we reach a vertex from where we can't move forward  
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

The idea is to randomly select a starting vertex and from there start traversing other vertices such that we visit the adjacent vertices first. Once we visited one level (adjacent vertices at a level), then find adjacent vertices of the previously visited ones, and repeat the step untin we visited all the vertices.

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
1. repeat [3-5] untin the queue is empty
1. we may have some unvisited / disconncted graph (vertices) at this moment
    1. so, iterate through all the unvisited vertices (if any)
    1. repeat [2-6] for them


## Topologican Sort

Topologican sort, is an ordering of vertices of a DAG in which each vertices[1] comes before, all vertices [2], to which[2] it[1] has outgoing edges.

Saying that, [1] will come before [2], if there is an edge from [1] to [2]

Note: There is no solution if the graph is a) Undirected, or b) Directed with cycle(s) - it will cause a deadlock.

### Idea

Topologican sort, arranges the vertices of a DAG in an order of their dependecies in other vertices.
Meaning that, A vertex which is not dependent on (i.e. no edge incidents to it) will be first in the list, and A vertex which is dependent on most of the vertices (or a series of dependecies has to be fullfilled before it) has to be at the end of the sorted list.

### Applications
- To execute some inter-dependent tasks/jobs
    - Run pipeline of computing jobs
    - To implement/evaluate formulae in Speadsheet cells
    - serialization & deserialization
- To detect dead locks
    - To check symbolic link loop (deadlock)

### Properties
- A DAG may have one or more Topologican Order
- If all the consecutive vertices in a topologican order, are connected by edges, then these edges forms Hamiltonian path
    - If the Hamiltonian path exists, then the topologican order is unique; else the DAG can have two or more topologican order

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
   (one to help backtrack, another for topologican order)
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

## Detect Cycle in Graph

- Using DFS by maintaining the immediate call stack (i.e. before any backtrack) a.k.a. detecting back-edge
- Using BFS by maintaining 3 flags/colors/sets
- Using BFS by decreasing In-Degree of the nodes

## Single-Source Shortest Path in Unweighted Graph

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

## Single-Source Shortest Path in Weighted Directed Acyclic Graph (DAG)

### Idea

### Applications

### Properties

### Implementation Using Stack / DFS (Topologican Sort)
- Desc:
- Approach: Topologican Sort
- DS Used:
- Time Complexity:
    - Best:
    - Avg: $\Theta(V + E)$
    - Worst:
- Auxilary Space:
    - Best:
    - Avg:
    - Worst:
- Disadvantage:

#### Pseudo Code

### Optimization

## Dijkstra's Algorithm [Single-Source Shortest Path in Weighted (non-negative) Graph]

Given a _weighted_ graph (directed/undirected) $G = (V, E)$, and a source/distinguished vertex $s$ find the shortest path from $s$ to every other vertices in $G$.

### Idea

If the given graph is undirected, treat it as a directed graph by replacing an undirected edge with two directed edges. And assigning the same given weight to both the edges.

Cycles may exist in the graph.

As the given graph is _weighted_ in nature, simply following BFS and incrementing the distance (or just keep adding the prev. distance + weight) of a vertex may NOT lead us to find an optimal solution.

Why so? Why wouldn't the same method help us here, as it did in the case of unweighted graph?
As we'll start traversing the paths _parallely_ (round-robin), the  calculated  distance (prev. distance + weight) would become the factor of comparision among candidate paths (to the same vertex from $s$). So we cannot rely on the closest/nearest (just based on number of edges inbetween) path because this may lead to an incorrect answer. The path with more edges could be the cheapest/shortest path.

This has become an minimization/optimization problem. 
Which could either be solved by Greedy or Dynamic Programing approach.
Dijkstra chose the Greedy one.

So, this time need to explore all the paths from $s$->$v$, visit the same vertex $v$ multiple times using all the possible (via adjacent vertices, say $u$) paths to that vertex from $s$. And relax(update/overwrite) the existing distance of the vertex $v$ from $s$ when the newly calculated distance is lesser.


Dijkstra says:

Do this initial exercise:

1. Calculate the distance of the immediate reachable (adjacent) vertices first, and set the distance of other vertices as $\infty$
2. Mark all the vertices as `not done`

Then perform this sub task:

1. Now pick the one (say $u$) from __all__ vertices whose distance is minimal & is `not done`
2. Find its adjacent vertices (say $v$) and __Relax__ (recalculate the distance & update) them. __No need to Relax the `done` marked adjacent vertices (not fruitful as per Dijkstra)__.

    Relaxation:
 
    ```
    if d[u] + w(u, v) < d[v]; then
        d[v] = d[u] + w(u, v)
    ```

3. Now, mark that vertex $u$ as `done`. 

Then repeat the sub task untin all the vertices are marked `done`.

### Applications
- finding _cheapest_ way to go from one place to another

### Properties
- approach is Greedy in nature
    - why/how?
        - it's iteratively makes one greedy choice after another
            - mark the distances of nearest vertices first
            - choose the vertex with minimum distance
    - the approach is also dynamic in nature because distances are updated using previously calculated values
- does not relax the edge going (incidenting) to already selected vertex
    - thats why it may give in the cases of a graph with negative edges

### Pseudo Code

1. start
1. create a set/array $S$ to maintain the vertices whose shortest-path has been finalized/determined
1. create a min-priority queue $Q$ (i.e. keyed by distance $u.d$ of the vertex $u$)
1. initialize the distances $u.d$ of all the vertices $u \in G.V$ with $\infty$, but set the distance of source vertex to zero i.e. $s.d = 0$
1. __insert__ (enqueue) all the vertices $u \in G.V$ into the priority queue $Q$
1. create an array $P$ to keep track of the path ($u$-->$v$)
1. __while__ $Q \ne \emptyset$ (min-priority queue is not empty)
    1. $u =$ __extract-min__ (dequeue a vertex $u$) from the priority queue (the one with minimum distance from the source vertex)  
    1. $S = S \cup \{u\}$ (add the current vertex $u$ into the determined set $S$)  
    (as $u$ has already gone through the relaxation & has the minimum distance amongst others)  
    (think about $s$ during the inital step, $s.d == 0$)
    1. explore [BFS] those adjacent vertices $G.adj[u] - S$ (of the current vertex $u$) whose shortest-path are not yet determined
    1. __for__ all adjacent vertices $v \in G.adj[u] - S$
        1. __relax__ (calculate, compare, & __decrease-key__ the distance) $d.v$ for the vertex $v$; where
            1. calculate: the new distance $\delta(s, u) + w(u, v)$
            1. compare: the old distance $\delta(s, u) + w(u, v) < d.v$ <!---->
            1. decrease-key: $v.d = \delta(s, u) + w(u, v)$
        1. if the distance $v.d$ got relaxed due to _current vertex_ $u$; then
            1. store the current vertex $u$ against this vertex $v$ in the path-array $P$  
            (this will help track the shortest path)
1. end

### Implementation Using Adjacency List, Priority Queue, BFS
- Approach: Greedy + BFS
- DS Used: 1 Priority Queue, 1 Array
- Time Complexity:
    - Best: $O(V)$
        - if no edges between the vertices (step-7 will run |V| times)
    - Avg: 
        - $O((V + E) * logV)$
            - if min-heap based priority queue is used
                - DECREASE-KEY: $O(log n)$
                - EXTRACT-MIN: $O(1)$
                - INSERT: $O(log n)$
            - step 5 = insert/enqueue $|V|$ vertices to a priority queue = $O(V * log n)$
            - step 7 * 7.d = loop over $|E|$ times (traverse through each edge exactly once) = $O(E)$
            - step 7.d.i.iii = $O(log n)$
            - step 7 * 7.d * 7.d.i.iii = $O(E * log n)$
            - DOUBT: why the constraint "If the graph is sufficiently sparse — in  particular, $E = O(V^2/log V)$ — we can improve the algorithm by implementing the min-priority queue with a binary min-heap" in CLRS? Why not always use min-heap based PQ?
    - Worst: $O(V + V^2)* logV)$ == $O(E * logV)$ if the graph is a complete graph, where $|E| = |V|*(|V|-1)/2$
- Auxilary Space: $O(V)$
    - Best: --
    - Avg: --
    - Worst: --
- Disadvantage:
    - does a blind search and wastes resources
    - can't guarantee a solution for a negative weighted graph

### Optimization

### Extra
- I personally don't like the way CLRS has mentioned the time complexity $O(V^2 + E)$ = $O(V^2)$ when array/list based priority queue is used. It says `EXTRACT-MIN` would have time complexity $O(n)$, which is a bad implementation IMO. Rather, I'd implement `EXTRACT-MIN` in $O(1)$ & `INSERT` in $O(n)$.
- Why the algorithm may give incorrect answer in the case of a graph with negative edges?
    - because the algorithm does not relax edge pointing (going/incidenting) to the already selected vertex
- Why/how the algorithm is greedy?
    - [see properties section]
- Can Dijkstra's algorithm handle negative edge & result correct answer if we add a positive constant to all the edges?

## Bellman-Ford Algorithm [Single-Source Shortest Path in Weighted (negative) Graph]

Given a _weighted_ graph (directed/undirected) $G = (V, E)$, and a source/distinguished vertex $s$ find the shortest path from $s$ to every other vertices in $G$.

This algorithm can __handle the negative weights__ in the graph which overcomes the drawbacks of Dijkstra's algorithm.

### Idea

If the given graph is undirected, treat is as a directed graph by replacing an undirected edge with two directed edges. And assigning the same given weight to both the edges.

Cycles may exist in the graph. (__But not negative weight cycles__)

As we've seen in previous simple/greedy algorithms that presence of negative weights may trip the approach and lead to incorrect answers. We need to be more careful and try all the possible paths to a vertex $v$ from source $s$. And pick the shortest path (minimum distance) amongst them.

This is again the same minimization/optimization problem, but approach is not Greedy this time.
Bellman-Ford prefers to explore all the possibilies using Dynamic Programing approach - where the target would be to optimize the global solution rather just focusing on the locan optimal solution.

Bellman-Ford says:

1. List down all the edges
1. And start relaxing an edge $u$ -> $v$ for each edge pairs $(u, v)$ in $G.E$
1. Repeat the step-2 $|V| - 1$ times, thus it will perform the relaxation of the each edge $(u, v)$ for $|V| - 1$ times - because the vertex $v$ might be reachable from all the rest of the vertices at max
    1. Why such idea? Because in a worst-case, a simple shortest path from $s$ to $v$ might have maximum $|V|-1$ edges to pass by. Thus, to get a final correct/relaxed distance/answer, all the intermediate edges have to be relaxed as well. Thing to observe in step-2-3 is, each iteration guarantees relaxation/correctness of atleast one edge. (So, in first iteration it calculates the shortest path with atmost one edge in the path, in second iteration it calculates the shortest path with atmost two edges in the path, thus in $i^{th}$ iteration it calculates the shortest path with atmost $i$ edges in the path. So, in each of these repetitions, the number of vertices with correctly calculated distances grows, from which it follows that eventually all vertices will have their correct distances). So, a graph without cycle (assume) expects $|V|-1$ relaxation.
    1. Also, this idea has nothing to do with negative weights (till $|V|-1$ iterations)
    1. [Illustration](https://riptutorial.com/algorithm/example/24029/why-do-we-need-to-relax-all-the-edges-at-most--v-1--times)
1. Repeat the step-2 one more time, and check if further relaxation is possible in $|V|$^{th}$ round; if so, then there exists a Negative Weight Cycle

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
- follows Dynamic Programing approach
    - works in bottom-up manner
- can detect a Negative Weight Cycle

### Pseudo Code

__input__: graph $G(V, E)$, weight function $w$, and source $s$

__output__: a) True, b) distance of all the $v \in V$, c) the shortest path; iff there in no negative weight cycle reachable from source $s$; else a) False

1. __start__
1. create a distance array $d$ & initialize $d[u] \forall u \in V$ with $\infty$
1. create an array $P$ to keep track of the path ($u$-->$v$)
1. set $d[s] = 0$
1. __for__ $|V| -1$ times:
    1. __for__ each edge $(u, v) \in E$:
        1.  __relax__$(u, v, w)$ i.e.
            1. if $d[v] \gt d[u] + w(u, v)$:
                1. $d[v] = d[u] + w(u, v)$
                1. $P[v] = u$
1. __for__ each edge $(u, v) \in E$:
    1. if $d[v] \gt d[u] + w(u, v)$:
        1. return False
1. return True
1. __end__

### Implementation Using Dynamic Programing
- Desc:
- Approach: Dynamic Programing
- DS Used:
- Time Complexity:
    - Best:
    - Avg: $O(V * E)$ (at most $|V|-1$ number of edges might be between vertex $s$ & $v$ `x` # of edges to be relaxed)
    - Worst: $O(V^3)$ if the graph is a complete graph
- Auxilary Space: $O(V)$
    - Best:
    - Avg:
    - Worst:
- Disadvantage:
    - does not work if there is a negative weight cycle
    - does not scale well

### Optimization
- If no more relaxation happens in the Graph; then immediately stop/return.
    - just maintain a flag & check the flag of the

### Extra
- Can Bellman-Ford's algorithm handle negative edge cycle & result correct answer if we add a positive constant to all the edges?
- How negative weight cycle check works?
    - A final scan of all the edges is performed and if any distance is updated, then a path of length $|V|$ edges has been found which can only occur if at least one negative cycle exists in the graph. 

## Floyd-Warshall Algorithm [All-Pair Shortest-Path in Weighted (negative) Graph]

Given a _weighted_ graph (directed/undirected) $G(V, E)$ with vertices $V$ numbered $1$ to $N$, and a weight-function $w_{ij}$ to denote weight of the edge between vertext $i$ & $j$, then find the shortest path from each vertex $i \in V$ to every other vertex $j \in V$ in $G$.

This can be solved using shortest-path single-source algorithm, by running them for $|V|$ times considering each vertex as source each time.

If Floyd-Warshall have chosen Dijkstra's algorithm then it would have cost: $O(V) * O((V + E)* log V)$ (considering it cannot handle negative weights). And $O(V^3 log V)$ in case of a dense graph.

If Floyd-Warshall have chosen Bellman-Ford's algorithm then it would have cost: $O(V) * O(V * E)$, and $O(V^4)$ in case of a dense graph.

However, those two algorithms were based on using Adjacency List, while this algorithm uses Adjacency Matrix. And even with that it solves the problem in $\Theta(V^3)$.

Note:

- If the given graph is undirected, treat it as a directed graph by replacing an undirected edge with two directed edges. And assigning the same given weight to both the edges
- Negative weights may exist in the graph
- Cycles may exist in the graph
- The algorithm assumes that there are no negative cycles
    - if there are negative cycles, the Floyd–Warshall algorithm can be used to detect them
    - How?
        - Its true that the distance between same vertex $i$ should be zero
        - If that distance changes to a negative value, then there is a negative weight cycle

### Idea

It's reasonable to think/assume/say that a shortest-path $p$ from vertex $i$ to $j$ could have (may not have) some intermediate vertices from a set of vertices say $\{1, 2, 3, ..., k \}$.

Also, the shortest-path $p$ may go through vertex $k$ and may not.

If we denote:

1. a shortest-distance (length of a __shortest-path__) from vertex $i$ to $j$ via $k$ as $d_{ij}^k$
1. and, a shortest-distance from vertex $i$ to $j$ - if there is only 1 edge between them  (i.e. no extra vertext between them) as $d_{ij}^0$ (suppose we denote this case by $k=0$)

So, for each pair $i, j \in V$, the observation could be: 

1. if the shortest-path $p$ does NOT even have more than 1 edge.  
   Then we can denote the shortest-distance by $d_{ij}^0 = w_{ij}$ (i.e. whatever weight is initially given in the $G$).
1. if the shortest-path $p$ does NOT go through $k$; i.e. the intermediate vertices falls in set $\{1, 2, 3, ..., k-1\}$ only.  
   Then, we can denote the shortest-distance by $d_{ij}^{k-1}$
1. if the shortest-path $p$ GOES through $k$; then the path could be broken into two parts, say:
    1. $i$ --> $k$ (say path $p_1$)
    1. $k$ --> $j$ (say path $p_2$)

    where both the path using intermediate vertices from set $\{1, 2, 3, ..., k-1\}$.

    And, if the shortest-path $p$ from $i$ to $j$ goes via $k$, then it should definitely be the concatenation of a __shortest-path__ from $i$ to $k$ ($p_1$, using intermediate vertices from set $\{1, 2, 3, ..., k-1\}$), and a __shortest-path__ from $k$ to $j$ ($p_2$, only using intermediate vertices from set $\{1, 2, 3, ..., k-1\}$).  
   Then, we can denote the shortest-distance (of shortest-path $p$) by $d_{ik}^{k-1} + d_{kj}^{k-1}$

Then, from the above observations, we can deduce a relationship between the:

1. shortest-path $p$ (or its distance) from vertex $i$ to $j$
1. some intermediate vertex $k$
1. weight-function $w_{ij}$ given in the graph $G$

Which can be recursively defined as:

$$
d_{ij}^k = \left
\{
\begin{array}{lcl} 
w_{ij} & if & k=0 \\
min( d_{ij}^{k-1}, \space d_{ik}^{k-1} + d_{kj}^{k-1}) & if & k \gt 0 \\
\end{array}
\right. 
$$

### Applications
- find shortest path (from all the vertices) in directed graphs
- detect negative weight cycle in directed graphs
- many more real life applications (see [this](https://en.wikipedia.org/wiki/Floyd%E2%80%93Warshall_algorithm))

### Properties
- follows dynamic programing approach
    - bottom up way (i.e. sub problems are already in indivisible state, so keep combining the results from sub problems till we get the final result)
- can detect negative weight cycle
- utilizes Adjacency Matrix

### Pseudo Code

__input__: graph $G(V, E)$ with weight function $w$ (or just weight matrix $W$)  
__output__: shortest distance between each vertices

> Typically Floyd–Warshall algorithm calculates distances only, and does not reconstruct the shortest path (i.e. does not return predecessor map), also does not tell if a negative weight cycle exists. Though those could be achieved by some additional simple logic/code/steps.

1. $N = |V|$ // number of vertices
1. $D =  (d_{ij})$  // initialize 2-d array of size $N*N$ with $\infty$, to store shortest-distance between vertices
1. __for__ $(i, j) \in G.E$ // for all edges from vertex $i$ to $j$
    1. $d_{ij} = w_{ij}$ // set distance from vertex $i$ to $j$ using $w_{ij}$
1. __for__ $i \in V$
    1. $d_{ii} = 0$ // set distance between same vertex ($i$ to $i$, i.e. self loop) to zero
1. __for__ $k$ = 1 to $N$
    1. __for__ $i \in V$
        1. __for__ $j \in V$
            1. $d_{ij} = min(d_{ij}, \space d_{ik} + d_{kj})$ // relaxation
1. return $D$

### Pseudo Code - detect negative weight cycle

__input__: final distance matrix $D$ from Floyd–Warshall algorithm  
__output__: True if negative weight cycle exists; else False

1. $N = |D|$
1. __for__ $i$ = 1 to $N$
    1. __for__ $j$ = 1 to $N$
        1. if $i == j$ // if diagonal coordinate of the matrix
            1. if $d_{ij} < 0$ <!---->
                1. return True
1. return False

### Pseudo Code - reconstruct shortest-path

TODO

### Implementation using Adjacency Matrix
- Approach: Dynamic Programing
- DS Used: Matrix (2-d array)
- Time Complexity: $\Theta(V^3)$
    - Best: --
    - Avg: --
    - Worst: --
- Auxilary Space: $\Theta(V^2)$ (if weight matrix and/or predecessor matrix has to be created) else $\Theta(1)$
    - Best: --
    - Avg: --
    - Worst: --
- Disadvantage: --

### Optimization

### Extra

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
The each step should find a locan optimal solution, and those locan optimal should lead to global optimal solution.

These algorithms provides a predefined procedure to be followed in each step.

An optimization problem _can_ be solved using greedy approach.

## Elementary cases : Fractional Knapsack Problem, Task Scheduling
## Data Compression using Huffman Trees
## Activity Selection

---

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

### Longest Increasing Monotonican Subsequence

### Rod Cutting

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

# Nomenclature
- use uppercase letters to denote matrices and corresponding subscripted lowercase letters to denote their elements

# References
- [CLRS 3rd Edition](https://edutechlearners.com/download/Introduction_to_algorithms-3rd%20Edition.pdf)
- [Algorithms Unlocked - 2013, by Dr. Thomas Cormen](http://dahlan.unimal.ac.id/files/ebooks/2013%20Algorithms_Unlocked.pdf)
- https://gist.github.com/toransahu/bb1c9f1cd6490ff29c42fa229e827a2a
- https://www.freetechbooks.com/algorithms-and-data-structures-f11.html
- LaTex Math Syntax
    - https://www.caam.rice.edu/~heinken/latex/symbols.pdf
    - https://en.wikibooks.org/wiki/LaTeX/Mathematics
    - https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference
    - https://latex.wikia.org/wiki/Array_(LaTeX_environment)
    - https://tex.stackexchange.com/questions/77589/what-do-the-pieces-of-latex-left-and-right-respectively-mean
