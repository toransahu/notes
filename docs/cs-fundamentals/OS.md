[TOC]

# Operating Systems

#### Semaphore Vs Mutex
* Are kernel resources and provides synchronization service
* Also known as synchronization primitives
* both are semaphores
    * Semaphore/Binary Semaphore (are generalized mutext)
    * Mutual Exclusive (Mutex) Semaphore
    * Recursive mutex
* But are different and work differently:
    * Mutex: 
        * Locking Mechanism
        * Ownership involved: The thread/process which have mutex and accessing data can only release mutex 
    * Semaphore: 
        * Signalling Mechanism: An
        * 
* Why 2 different synchronization premitives?

#### Producer-Consumer Problem
#### Critical Section
In con-current programming
* A group of instructions/statements or region of code
* that region to be executed atomically (i.e. all or nothing)

A simple solution to critical section
```python
acquireLock()
executeCriticalSection()
releaseLock()
```


### Inter Process Communication
