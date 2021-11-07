# Operating Systems

<h3>Table of Contents</h3>

[TOC]

# Process Scheduling

## Preemptive Scheduling
- is a kind of process scheduling
- which have facility to interrupt an on going process to proceed with other high priority process (and the resource, mainly CPU, is allocated to the new process)
- in such case, the running process moves to the ready state & the process in ready state moves to the running state

## Non-Preemptive Scheduling

# Process Synchronization
The shared resources can be used by all the processes but the processes should make sure that at a particular time, only one (or, a finite number of) process should be using that shared resource. This is called process synchronization.

## Methods used for Process Synchronization
- Semaphore
- Mutex (Mutual Exclusive object)

### Semaphore AND Mutex
* Are kernel resources and provides synchronization service
* Also known as synchronization primitives
* both serves the same purpose but the mechanism, implementation, and use-cases are different

### Semaphore
* is a Signalling Mechanism

#### Types
- Binary Semaphore
- Counting Semaphore

### Mutex
- an object
* is a Locking Mechanism
* Ownership involved: The thread/process which have mutex and accessing data can only release mutex 

#### Types
- Recursive mutex

#### Pros

#### Cons

### Mutex VS Semaphore

- Mutex uses a locking mechanism i.e. if a process wants to use a resource then it locks the resource, uses it and then release it. But on the other hand, semaphore uses a signalling mechanism where wait() and signal() methods are used to show if a process is releasing a resource or taking a resource.
- A mutex is an object but semaphore is an integer variable.
- In semaphore, we have wait() and signal() functions. But in mutex, there is no such function.
- A mutex object allows multiple process threads to access a single shared resource but only one at a time. On the other hand, semaphore allows multiple process threads to access the finite instance of the resource until available.
- In mutex, the lock can be acquired and released by the same process at a time. But the value of the semaphore variable can be modified by any process that needs some resource but only one process can change the value at a time.

### Why 2 different synchronization premitives?

#### Producer-Consumer Problem

#### Critical Section

In conncurrent programming
* A group of instructions/statements or region of code
* that region to be executed atomically (i.e. all or nothing)

A simple solution to critical section
```python
acquireLock()
executeCriticalSection()
releaseLock()
```

#### Preemption

### Inter Process Communication

# Concurrency vs Parallelism



# IO bound, Memory bound, Cache bound, CPU bound operations

speed of IO bound $\lt$ Memory bound $\lt$ Cache bound $\lt$ CPU bound operations

# Memory Management

## Virtual Memory

- Virtual memory is a memory manage scheme
    - as per which the secondary memory could act as a part of the primary memory
- implemented using __demand paging__ or __demand segmentation__
- other insights
    - a program does not refers to actual physical (primary) or machine (secondary) memory address
    - rather it refers to the logical addresses
    - logical addresses are translated into physical addresses during execution of the programs
    - thus a process could be stored & executed in non-contiguos chunks

## Paging

## Demand Paging


## Page Fault

## Swapping

- Swapping a process out: marking its all pages as free/unloaded from memory
- Swapping a process in: bringing in all the pages of a process from secondary memory to primary memory

## Thrasing
- When a process is busy swapping pages in and out then it is called thrasing

