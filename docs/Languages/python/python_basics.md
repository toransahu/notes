<h1>Python Basics</h1>

[TOC]

# Introduction


## The Zen of Python (PEP 20)

- Beautiful is better than ugly.
- Explicit is better than implicit.
- Simple is better than complex.
- Complex is better than complicated.
- Flat is better than nested.
- Sparse is better than dense.
- Readability counts.
- Special cases aren't special enough to break the rules.
- Although practicality beats purity.
- Errors should never pass silently.
- Unless explicitly silenced.
- In the face of ambiguity, refuse the temptation to guess.
- There should be one-- and preferably only one --obvious way to do it.
- Although that way may not be obvious at first unless you're Dutch.
- Now is better than never.
- Although never is often better than *right* now.
- If the implementation is hard to explain, it's a bad idea.
- If the implementation is easy to explain, it may be a good idea.
- Namespaces are one honking great idea -- let's do more of those!

### Easter Egg
- In computer software and media, an Easter egg is an intentional inside joke, hidden message or image, or secret feature of a work

The Zen of python can be listed by importing `this`

```python
>>> import this
```


## Implementations
- CPython (Default)
- Jython
- IronPython
- RPython (PyPy)

## Internal
- Runs on a single process by forking
- Each process have seperate  GIL
- Python can run only one thread at once
- [Context Manager ](https://jeffknupp.com/blog/2016/03/07/python-with-context-managers/)

## PEP 8 - Style Guide for Python Code

* Package: lowercase, '_' is discouraged, use hyphen '-' instead
* Module: lowercase + '_'
* Class: Initial Capital, Camal Case
* Function: lowercase, Valid word, '_'
* Method: self, lowercase, Valid word, '_'
* Variable: Same as functions
    * Local:
    * Global: 
    * Static:
    * Constant: Generally Module Level, All CAPS + '_'
* Private Attribute: To avoid name clashes with subclasses, Leading dunder 
* Protected Attribute:  For non-public methods and instance variables, Leading underscore '_'
* Exception Name: Same as class   

NOTE: Never use the characters 'l' (lowercase letter el), 'O' (uppercase letter oh), or 'I' (uppercase letter eye) as single character variable names.    

## Features of Python are:

* Unique
    * Interpreted Language
    * Dynamic type system but strongly typed (changing data type need explicit conversion)
    * emphasizes on code readability - lesser line of code/syntax
    * Supports multiple programming paradigms, including object-oriented, imperative, functional and procedural
    * Has community based developement model
    * Dynamic name resolution/ late binding: unlike compiled languages, the name of method, variable is lookedup by name at runtime
    * Data types are strongly and dynamically typed. Mixing incompatible types (e.g. attempting to add a string and a number) causes an exception to be raised, so errors are caught sooner.
    * Python contains advanced programming features such as generators and list comprehensions.
    * Lambda functions
    * Multiple inheritance
* Common
    * A variety of basic data types are available: numbers (floating point, complex, and unlimited-length long integers), strings (both ASCII and Unicode), lists, and dictionaries.
    * Python supports object-oriented programming with classes and multiple inheritance.
    * Code can be grouped into modules and packages.
    * The language supports raising and catching exceptions, resulting in cleaner error handling.
    * Python's automatic memory management frees you from having to manually allocate and free memory in your code.


#### Compilers
A type of translator.

Compiler analyze the whole source code at once and translate it to another language. i.e. machine code

#### Interpreters

An interpreter is also a program that translates a high-level language into a low-level one (but not directly into machine code), and it does it at the moment the program is run. 

It takes the program, one line at a time, and translates each line before running it: It translates the first line and runs it, then translates the second line and runs it etc.

##### Compiler characteristics:

* spends a lot of time analyzing and processing the program
* the resulting executable is some form of machine- specific binary code
* the computer hardware interprets (executes) the resulting code
* program execution is fast

##### Interpreter characteristics:

* relatively little time is spent analyzing and processing the program
* the resulting code is some sort of intermediate code
* the resulting code is interpreted by another program
* program execution is relatively slow


## Python interpreted/compiled?

#### Compiled Language
A compiled language turn human-readable code into machine code (a string of binary numbers), which are directly executed by OS & CPU.

#### Interpreted Language
A language which is in non-machine code form just before its execution.

In general an interpreted prog. language turn human-readable code into non-machine code (byte-code), which are then line by line executed by virtual machine.


Interpreted/Compiled is not property of language, its property of implementation.

Its byte-code INTERPRETED, because .py is first COMPILED/translated to .pyc (a byte-code language, a non-machine language, executed by python virtual machine, not by OS / CPU).

## How python works?
* run module i.e. .py file
* .py loaded into memory
* parsing in order
* .py compiled to bytecode .pyc file (which is not binary machinecode)
    * compilation is translation step
    * .pyc (.i.e. bytecode) is low-level **platform -independent** version of source-code
    * require more work than CPU instructions
* if .pyc of source code is present, compilation step will be skipped by checking time-stamp of .py & .pyc
* if python cannot create .pyc, then bytecode will be created in-memory
* then routed/shipped to python virtual machine PVM for execution
    * pre-installed / inbuilt
    * it is runtime engine of python
* .pyc is also way of shipping python code without source-code

#### Note
* no initial/explicit compilation phase
* compiles at runtime only and then executes in single step
* able to produce executable, frozen binaries using
    * py2exe
    * PyInstaller
    * freeze

## What is .pyc file?
Low-level Platform-independent Bytecode

## What is .pyo file?
in addition to .pyc, .pyo removes all the comments & docs(i guess)

## Memory Management 
* Basics:
    * Python's memory allocation and deallocation method is automatic.
    * involves a private heap
    * the heap contains all the objects & data structures
    * managed by python "memory manager MM"
    * interpreter manages this all
    * no user control
    * heap space allocation for objects & buffers are performed **on-demand** by MM
    * c memory management libs works in-behind: malloc(), calloc(), realloc(), free()
    * at low level, raw memory allocator allocates enough memory for all the data
    * on top of low-level, object-specific allocators allocates memory as per object's policies
    * e.g. for integer: speed tradeoff

* Memory De-allocation Strategies:
    * Reference Counting
        * Was only option Prior Python 2.0
        * When an object gets created and referenced, it counts the number of times the object is referenced **by some other objects**
        * When reference is removed, the reference count for the object is decremented
        * When the reference count becomes zero, the object is deallocated.
        * Extremely efficient but
        * Have limitations like:
            * Cannot handle **reference cycle**
            * Reference Cycle: When there is no way to reach an object but its reference count is still greater than zero
            * e.g.
                ```python
                list1 = []
                list1.append(list1)
                ```
        - Examples, where the reference count increases:
            - assignment operator
            - argument passing
            - appending an object to a list (object's reference count will be increased).
            
        ```python
        foo = []

        # 2 references, 1 from the foo var and 1 from getrefcount
        print(sys.getrefcount(foo))

        def bar(a):
            # 4 references
            # from the foo var, function argument, getrefcount and Python's function stack
            print(sys.getrefcount(a))

        bar(foo)
        # 2 references, the function scope is destroyed
        print(sys.getrefcount(foo))
        ```        
             
    * Garbage Collection
        * Introduced after Python 2.0
        - it contains reference counting as well as garbage collector
        * Automatic / Scheduled: The "Reference Counting" mechanism was not able to deallocate objects in few cases like: Reference Cycle
        - How reference counting is solved by garbage collection
            - it is a scheduled task based on a threshold
                - threshold  = allocations - de-allocations
                
            - The GC classifies container objects into three generations. Every new object starts in the first generation. If an object survives a garbage collection round, it moves to the older (higher) generation. Lower generations are collected more often than higher. Because most of the newly created objects die young, it improves GC performance and reduces the GC pause time.
            - Source :
                - read Pro Python for better understanding
                - https://rushter.com/blog/python-garbage-collector/
            - whenever threshold is reached, garbage collector starts identifying memory spaces which are garbage
                - garbage?
                    - the memory spaces which are un-reachable to python objects  
                        - e.g.
                        
                        ```python
                        import gc
    
                        gc.disable()
                        obj1 = {"val":1}
                        obj2 = {"val":2}
                        obj1["obj2"] = obj2
                        obj2["obj1"] = obj1
                        del obj1, obj2
                        
                        ```
                    - it is most important to identify a memory space whether it is a garbage or not
                        - otherwise it will lead to `memory leak`
                            - `memory leak` means, automatically data loss
                    
        * Note: Automatic garbage collection will not run if your Python device is running out of memory
        * Manual / Explicitly 
        ```python
            import gc
            
            # get_count() returns a tuple of (threshold, no. of objects allocated, no. of objects de-allocated)
            print(gc.get_count())
            # With no arguments, run a full collection
            gc.collect()
        ```


* https://docs.python.org/3/c-api/memory.html
* pass by value
* pass by reference
* change reference
* change value
* behaviour of mutable and immutable

## Data types in python?
data type: set of data with predefined values.

* primitive:
    * integers
    * floating 
    * char
    * string
* user-defined
    

## Data structure in python?
Data Structure: are special format/structures to store & organize data.
#### 4 Built in
* Sequence data types:
    * Ordered Sequence:
        * List 
        * Tuple
    * Set
* Dictionary

**We consider string more as a data type.**

#### Collection & heapq modules
* provides additional data structure
* collections:
    * dequeue
    * ordereddict
* heapq:
    * priority queue
    * heap

#### Abstract data type we can create are
* linear:
    * linked list
    * stack
    * queue
    * hash table
* non-linear:
    * tree
    * graph

# Data Types

## Strings

### String formatting

```python
i = 1
v = 'a'
print("Value at index {0} is {1}".format(i,v))
print("Value at index {} is {}".format(i,v))
print("Value at index %d is %s" % (i,v))

# my favorite way before Python 3.6.4
emp = {'name':'toran', 'age':26, 'mobile':'8602431733'}
print("My name is {name} and I'm {age} years old. You can contact me at {mobile}".format(**emp))

# in Python 3.6.4
print(f'The value of i is {i} and value of v is {v}')
```


### What is doc string?
* way of associating document with modules, functions, class, methods
* describes what it does instead how
* first line should heading (start with capital, end with dot), then gap of one-line, then desc

### byte string vs unicode string

#### Intro
- there are a lot of encodings available world-wide
- e.g. ASCII, CP-1252 (windows), Mac-greek.. etc
- computer only understands bit, bytes
- e.g. in ASCII: 65 is -a, 97 is A
- HOW TO REPRESENT ALL LANGUAGEs IN SAME FILE?

#### 3 things
- `str` python object
- byte string, computer native array of bytes
- unicode, some encoded text

#### unicode
- one encoding, all chars
- represent a char as 4-byte number: 4*8 = 32; UTF-32
    - a lot memory freak
- similarly, 2*8 = 16; UTF-16
- **UTF-8**
    - a variable-length encoding system for Unicode
    - till 128, ASCII & UTF-8 is same, uses 1 byte
    - uses 2 bytes for latin
    
read more at [1](http://timothybramlett.com/Strings_Bytes_and_Unicode_in_Python_2_and_3.html), [2](http://www.diveintopython3.net/strings.html)

## List

### Intro
* A data structure/type to store objects/data/items
* Ordered collection: stores in ordered way i.e. using index from 0
* Variable length: dynamic sized
* Mutable: can change any existing element in run-time
* Preferred for homogenious collection, but can store heterogenious data types inside.
* many attribute/member methods:

### Why? When?
* when dynamic data structure is benificial like: appending, removing, altering
* use when implementing buffer, stack, queues

### Features

#### List Generator
* generates iterable items on demand
* build up in memory
* xrange in Python 2.x i.e. range() in Python 3.x is example of generator
* Advantages:
    * No need to wait until all the elements have been generated before we use them
    * in python 2.x, range returns a list while xrange returns a generator
* e.g.

```python
def first_n(n):
    num = 0
    while(num < n):
        yield num
        num += 1

for i in first_n(5):
    print(i)

```        

#### List comprehension

``` python
l = [i for i in range(0,10)]
print(l)
```
``` 
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

#### List Flattening

```python
l = [[1,2,3], [4,5,6], [7,8,9] ]
flat_list = [item for sublist in l for item in sublist]
```

which is equivalent to 

```python
flat_list = []

for sublist in l:
    for item in sublist:
        flat_list.append(item)
```



#### Randomize items of list in place
Code:
```python
from random import shuffle
l = [1,2,3,4]
shuffle(l)
print(l)
shuffle(l)
print(l)
```
Out:
``` 
[3, 2, 1, 4]
[4, 1, 2, 3]
```

#### How to insert an element in between a list?
Code:
``` python
l = [1,2,3,5,6,7]
l.insert(3,4)
l
```
Out:
```
[1, 2, 3, 4, 5, 6, 7]
```

#### Diif  between append and extend method in list?
* append - appends object at the end
* extend - extends list by appending elements from iterables

Code:
``` python
l = [1,2,3]
a = [4,5]
e = [6,7,8]

l.append(a)
l.extend(e)

print(l)
```
Out:
```
[1, 2, 3, [4, 5], 6, 7, 8]
```

#### enumerate()
``` python

for i,v in enumerate(['f','s','t']):
    print("Value at index %d is %s" % (i,v))
    print("Value at index {0} is {1}" % (i,v))
    print("Value at index {} is {}".format(i,v))
```    

## Tuple
* A fixed data structure/type to store objects/data/items
* Ordered collection: stores in ordered way i.e. using index from 0
* Fixed length: cannot change length of a tuple, cannot append, pop an element
* Immutable: cannot change any existing element in run-time
* Preferred for heterogenious collection, but can store homoge data types inside.

### Why? When? 
* when a collection of values will not change i.e. in case of functions args.
* use when fixed structure is benificial like: heavy memory intensive work, api, server
* can be used as key in dictionary due to its fixed structure
* use when need to store a db table data and want to maintain column structure

### Properties
``` python
l = [1,2, (3,'a'), 'b', [4,5]]
t =(1,2,[3,'a'], 'b', (4,5) )

#Lets try to make changes in l & t

# l[2][0] = 1 #does not work
# l[2] = 3 #works

# t[2] = 3 #does not work
# t[2][0] = 1 #works
```

### Expanding Tuple
- used to pass tuple elements as function parameter

```python
t = (1,2,3,4,5)

# simple
def bar(a,b,c,d,e):
    print(a,b,c,d,e)

bar(*t)    

# in general
def foo(*args):
    for arg in args:
        print(arg)
        
foo(*t)
```

## Dictionary
- Is map type of data structure which holds a key value pair.
- Unordered collection: does not maintain order

### When to use dict & set?
* When data is labelled
* Use a dictionary when you have a **set of unique keys** that map to values.
* Use a set to store an **unordered unique** set of items.

### dict vs list lookup performance?
* dict - O(1) due to hashing 
* list - O(n)

### dict comprehension
Code:

``` python
d = {i:i*i for i in range(0,10)}

print(d)
```

Out:
```
{0: 0, 1: 1, 2: 4, 3: 9, 4: 16, 5: 25, 6: 36, 7: 49, 8: 64, 9: 81}
```

### dict with order
- maintains the order of elements in which they were inserted

``` python
from collections import OrderedDict
d = OrderedDict({ 2:'second', 1:'first'})
d.items()
```

# Variables


## Global vs Local vs Non-Local Variable
* src: https://www.python-course.eu/python3_global_vs_local_variables.php
* not same as other languages (by default global)
* by default all are local (if you need, declare global)

```python
def f():
    s = "I'm local"
    print(s)

s = "I'm global"
f()
print(s)
```
Out:
```
I'm local
I'm global
```

## Global Variable
How to access global variable inside a function:

```python
def f():
    # print(s) #error : cannot access a global variable directly
    global s # keyword global will give access to outer s
    s = "I'm local" # value of global s has been changed
    print(s)

s = "I'm global"
f()
print(s)
```
Out:
```
I'm local
I'm local
```

### Global Variables in Nested Functions
* keyword global inside inner function will not access the upper function level variable
* instead, it will create a variable in __main __ scope
* to make it possible there is one more keyword : nonlocal

```python
def f():
    x = 42
    def g():
        global x
        x = 43
    print("Before calling g: " + str(x))
    print("Calling g now:")
    g()
    print("After calling g: " + str(x))
    
f()
print("x in main: " + str(x))
```
Out:
```
Before calling g: 42
Calling g now:
After calling g: 42
x in main: 43
```

## Local Variable
* variable defined inside a function are local to that function

## Non-Local Variable
* introduced in Python 3
* different than global
* can only be used inside of nested functions
* has to be defined in the enclosing/upper function scope

```python
def f():
    y = 42
    def g():
        nonlocal y
        y = 43
    print("Before calling g: " + str(y))
    print("Calling g now:")
    g()
    print("After calling g: " + str(y))
    
f()
print("y in main: " + str(y)) # this will create error
```

Out:

```bash
Before calling g: 42
Calling g now:
After calling g: 43
NameError: name 'y' is not defined
```

# Operators

## `in`
- Searching
- Time Complexity: (Depends on type of operand)
    - List 
        - Avg: O(n)
    - Dict/Set 
        - Avg: O(1)
        - Worst: O(n)
- magic/member method: `__contains__(<element>)`         
    

## `and`

## `or`

## `xor`

## `is`

## `not`




# Generators

## xrange vs range?
** python3: **
* xrange  is renamed to range.

** python2:**
* same result but xrange is more memory efficient
* range creates iterable  list (in python2)
* while xrange creates xrange object and generate list of demand


# Statements

## assert
* A statement
* Used to check an expectation
* Works on logical condition
* If true, return nothing, if false raise AssertionError exception

## yield
* A statement
* Does not end a function
* Returns value to its caller
    * suspends the function and then return value to its caller then resume the function
* Continues with next line of statement
* uses: in `generators` like `range`

## return
* A statement
* Ends function
* Returns value to caller


## Compound Statements
* Compound statements contain (groups of) other statements
* they affect or control the execution of those other statements in some way
- contains multi line code block
- e.g. `if`, `while`,  `for`, `def`, `class`, `with`

### with
- The `with` statement is used to wrap the execution of a block with methods defined by a context manager
- `with` statement allows the execution of initialization and finalization code around a block of code  
- i.e. `try`/`finally` + `context manager` having methods `__enter__()` & `__exit__()`
- [read more](https://www.python.org/dev/peps/pep-0343/)

#### Example #1 : file handling
```python

    # automatically acquring `csv.txt` file and does not allows others to acquire it
    with open('csv.txt', 'r', encoding='utf-8') as f:
        # do some operations on f
        # do some operations more on f
        # if any exception occur, closes the file before exception is caught and shown by interpreter

    # automatically closed/released `csv.txt` file for others
```

- `with` statement opens a file or acquires a resource then do some block of codes 
- then closes the file or releases the resource
- if any exception occur, during operations closes the file before exception is caught and shown by interpreter
- thats how we are better than `try, except, finally`
- I/O operation : GIL free

#### Example #2: 
```python
with A() as a, B() as b:
    suite
```
is equivalent to
```python
with A() as a:
    with B() as b:
        suite

```
- thats how, it does not need help of GIL

# Expressions

## [lambda](#Lambda)


# Operators

## Ternary Operator
[on-true] if [expression] else [on-flase]

Code:
``` python
x,y = 23,50
big = x if x>y else y
print(big)
```
Out:
```
50
```

## [Operator Overloading Using Magic Methods]
- Read in Python-OOPs notebook

# Functions
- Source
    - https://docs.python.org/3/library/functions.html

## `eval()`
- Source:
    - https://www.programiz.com/python-programming/methods/built-in/eval
- a built-in function to evaluate the python expression writter in string form

```python
str = "lambda x: x**2"
square = eval(str)
square(2)  # returns 4

str_list = "[1,2,3]"
eval(str_list)  # returns a list

str_dict = "{'a':1, 'b':[2,3]}"
eval(str_dict)  # returns a dict
```
- eval takes 3 parameters
    - expression: string
    - globals: dict (used for namespace)
    - locals: any mapping object
   

## `partial()`
- a closure or a nested function
- used to fulfill the cases
    - when we need to provide some/few fixed parameters to any functions
- need to import `from functools import partial`    
- `partial` always takes functions as first parameter
- e.g.

```python
from functools import partial

def foo(a,b,c=10):
    print(f"I'm foo with {a}, {b}, and {c}")
    
foo_partial = partial(foo, 1, 2)

foo_partial()
```

## `lambda`
* format: lambda arg1, arg2, ...argN : expression using arguments
* anonymous function
* single-line <s>statement</s> expression
* in-place function definition
* can be stored in a variable
* syntax: 
```python
lambda x: return x*x
```
Scopes:
    * to make Jump Tables
    * nested lambda
    * loop in lambda using map()


## map()
* signature: map(aFunction, aSequence)
* applies a passed-in function to each item in an iterable object
* __python2__:returns a list containing all the function call results
* __python3__:returns an iterator of type map object
* Syntax
```python
sqrs = list(map(lambda x: x*x, range(0,10)))
print(sqrs)
```
Out:
```
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

## filter()
* signature: filter(aFunction, aSequence)
* applies a passed-in function to each item in an iterable object
* __python2__:returns a list of items for whose ** function call returns True**
* __python3__:returns an iterator of type map object for the items whose ** function call returns True**
* Syntax
```python
evens = list(filter(lambda x: x%2 == 0, range(0,10)))
print(evens)
```
Out:
```
[0, 2, 4, 6, 8]
```

## reduce()
(Dropped out in Python 3.x)
* signature: filter(aFunction, aSequence)
* applies a passed-in function to each item in an iterable object
* __python2__:returns a single value
* __python3__: dropped out

<img src="https://www.python-course.eu/images/reduce.png">

## zip() 

```python
list1 = ['A',
'B','C'] and list2 = [10,20,30].
zip(list1, list2) # results in a list of tuples say [('A',10),('B',20),('C',30)]
```


### Inverse a Matrix (list/tuple)

```python
m = [[1,2,3,4],
     [5,6,7,8],
     [9,10,11,12]
    ]

m_inverse = list(zip(*m))   # here *m is expanding of list/tuple, mostly used in passing tuple as func parameters
```


## Decorators
- are a thin wrapper arround any function or any class
    - there are also decorators for classes (read in Python-OOPs)
        - benifits: do not need to decorate each method manually
- when we apply a decorator to any function
    - a few lines code in before start (if any) of the fuction call will get executed
    - and/or a few lines code in after end (if any) of the fuction call will get executed

- types of function decorator
    - made out of a nested functions
    - made out of a class
    - decorator with param
    - decorator over decorator 
        - order of decorators
    - Using `wraps` from functools
        - The way we have defined decorators so far hasn't taken into account that the attributes
        
        ```python
            __name__ (name of the function),
            __doc__ (the docstring) and
            __module__ (The module in which the function is defined) 
        ``` 
           
        of the original functions will be lost after the decoration. 

- simplest form of e.g. to create a custom decorator is:

```python
def exec_time(some_func):
	print('this is start time')
	some_func()
	print('this is end time')


@exec_time
def foo():
	print('running foo')	
```    
- gist: https://gist.github.com/toransahu/7ac4c7f139e78d15b74ca0ce6e17cf85

## Nested function
```python
def outer_func():
  x = 5
  def inner_func(y = 3):
    return (x + y)
  return inner_func
a = outer_func()
 
print(a())	# 8
```

### Closures
- is a concept - not a function
    - a few may refer it as a nested function
- The local function is able to reference the outer scope through closures. 
- Closures maintain references to objects from the earlier scope.

#### As per JavaScript
A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

## Function Factory 
- these are functions that return other functions
- the returned functions are specialized
- Function Factory takes in argument(s), creates local function that creates its own argument(s) and also uses the argument(s) passed to the function factory
- this is possible with closures

```python
def multiply_by(num):
  def multiply_by_num(k):
    return num * k
  return multiply_by_num
  
five = multiply_by(5)
print(five(2))	# 10
print(five(4))	# 20
 
decimal = multiply_by(10)
print(decimal(20))	# 200
print(decimal(3))	# 30
```

## Parameter passing in python
### Passed As
* by default, all the parameters (arguments) are passed âby referenceâ to the functions
* numbers, strings, tuples (i.e. immutables) are passed by value

### Default Parameters
- Non-default parameters comes before default parameters
- following will give `SyntaxError`
```python
def add(a, b=3, c):
    return a+b+c
```
```
SyntaxError: non-default argument follows default argument
```

### Variable Number of Parameters
- `*args`
- `**kwarg`


# Exception Handling
* Syntax:
```python
try:
    # do something 
except IOError as e:
    # handle
except ValueError:
    # handle
except:
    # handle
finally:
    # do final work
```
* can also put an else block after all the except block (will be executed if no exception occurs)

### Inbuilt Exceptions
- All the buil-in exceptions are subclass of `BaseException`


#### AssertionError
- raised when `assert` statement fails

#### AttributeError

#### EOFError
- raised when the `input()` function hits an end-of-file condition without reading any data

#### ImportError
- raised when there is some trouble loading mudules

#### IndentationError
- wrong indentation

#### IndexError
- raised when a sequence is out of range

#### KeyError
- when key not found in Dict

#### NameError
- when a local or global name is not found

#### NotImplementedError
- when a abstract/interface method lacks real implementation in sub-class

#### OSError
- when there is some OS level failure like, `file not found`, `disk full`

#### RecursionError
- when intrepreter detects maximum recursion depth

#### SyntaxError
- when parser encounters some syntax error
    ```python
    print 1
    ```
    ```
    SyntaxError: Missing parentheses in call to 'print'
    ```
    
#### TypeError
- when an operation or function is applied to an inappropriate object
- e.g.
    - when index is not an int
    - addition of int + str
    ```python
    a = 1 + 'abc'
    ```
    ```
    TypeError: unsupported operand type(s) for +: 'int' and 'str'
    ```
    
#### UnicodeError
- when a unicode related encoding/decoding error occurs

#### ValueError
- when a built-in operations or function receives an argument that has the right type but an inappropriate value.
    ```python
    int('abc')
    ```
    ```
    ValueError: invalid literal for int() with base 10: 'abc'
    ```
   
#### ZeroDivisionError
- when 2nd arg in division or modulo operation is zero

### User-defined Exception
* make a class 
* inherit the `Exception` class
* syntax:

```python
# define Python user-defined exceptions
class Error(Exception):
   """Base class for other exceptions"""
   pass

class ValueTooSmallError(Error):
   """Raised when the input value is too small"""
   pass

class ValueTooLargeError(Error):
   """Raised when the input value is too large"""
   pass
```   

# Performance
- https://wiki.python.org/moin/TimeComplexity



# Misc


## `is` vs `==` operator
- `==` compares for values
- i.e. checks that 2 arguments have the same value

```python
l1 = [1,2,3]
l2 = l1
l3 = [1,2,3]

l1 == l2  # returns True
l1 == l3  # returns True
l3 == l2  # returns True
```

- `is` checks if `operand1` is exact copy of `operand2`
- i.e. checks that 2 arguments refer to the same object

```python
l1 = [1,2,3]
l2 = l1
l3 = [1,2,3]

l1 is l2  # returns True
l1 is l3  # returns False
l3 is l2  # returns False
```

## Pickling Unpickling
### Pickling 
- python object hierarchy is converted into byte stream
- aka serialization, marshal, flattening
- can say 'binary serialization format'
- module: `pickle`

### Unpickling 
- `byte-like objects` or `binary files` are converted back into objects hierarchy
- opposite of pickling

### Comparision with JSON
- JSON is a text serialization format
- it outputs unicode text, and most of the time it is then encoded to 'utf-8'
- JSON text is human readable which `pickle` is not
- widely used outside the python, while pickle is python-specific

## Monkey Patching
* an evil hack ;)
* It's simply the dynamic replacement of attributes of a class/module at runtime.
* its possible because classes are mutable & methods are just attributes
* Also, we can replace classes and functions in a module

### Uses
* for testing purpose, replace a function which calls a heavy API with a dummy one

Code:
```python
class MyClass:
    def f(self):
        print("f()")
        
def monkey_f(self):
    print("monkey_f()")

MyClass.f = monkey_f
obj = MyClass()
obj.f() # here, definition of f has been replace with def of monkey_f
#obj.monkey_f()        
```
Out:
```
monkey_f()
```



## Duck Typing
* EAFP: Easier to Ask Forgiveness than Permission
* Tag line definition: If an object can quack & fly, then its a duck.
* Do not worry about, if this object has this attribute or not, just try it inside try: block. If work then great, else handle the error.
* Opposite is LBYL: Look Before You Leap. (Check if it is possible or not, then try)
* e.g. https://gist.github.com/toransahu/337c287f8ead0d663c13b96d4b8fb7d2

# Copy


## Regular Reference (Hard Copy)
* Copies reference of original only not value.
* Changes in copy will also reflect in original. i.e. id of both would be same

**
The difference between shallow and deep copying is only relevant for compound objects (objects that contain other objects, like lists or class instances)
**


## Shallow copy
* A shallow copy constructs a new compound object and then (to the extent possible) inserts references into it to the objects found in the original.
* Copies top level data & references other level objects into new
* Changes in top level not reflect in orignal
* Changes in other level objects reflect in orignal

Means ids of nested/child objects will remain same in both the copies

* doesn't slow downs programs
* refer example

## Deep copy
* A deep copy constructs a new compound object and then, recursively, inserts copies into it of the objects found in the deforiginal.
* slow downs programs

```python
print("Regular reference Example\n")
print("Ops on mutable")
l1 = [1,2,3]
l2 = l1 # l2 have reference of l1

# changes in regular reference affects original data
l2.append(4)
print("l1 =", l1)
print("l2 =", l2)
print("id(l1) =", id(l1))
print("id(l2) =", id(l2))

print("Ops on Immutable")
s1 = "abcd"
s2 = s1
print(id(s1))
print(id(s2))
print(s1)
print(s2)
s1 = "efgh"
print(id(s1))
print(id(s2))
print(s1,s2)
```

Out:
```
Regular reference Example

Ops on mutable
l1 = [1, 2, 3, 4]
l2 = [1, 2, 3, 4]
id(l1) = 140486838971464
id(l2) = 140486838971464
Ops on Immutable
140486838172392
140486838172392
abcd
abcd
140486838172784
140486838172392
efgh abcd
```

```python
print("\nShallow Copy Example - Manual\n")

l0= [1,2,3]
l3 = [1,l0]
l4 = list(l3)

print("l3 = ",l3)
print("l4 = ", l4)
print("id(l3) =",id(l3))
print("id(l4) = ", id(l4))

print("l3 == l4",l3 == l4) #checks value-wise
print("l3 is l4",l3 is l4) #checks object identity-wise

print("id(l3[1]) =",id(l3[1]))
print("id(l4[1]) = ",id(l4[1]))

print("l3[1] == l4[1]", l3[1] == l4[1])
print("l3[1] is l4[1]", l3[1] is l4[1])

print("Size of l3 = ",sys.getsizeof(l3))
print("Size of l4 = ",sys.getsizeof(l4))

print("Size of l3[1] = ",sys.getsizeof(l3[1]))
print("Size of l4[1] = ",sys.getsizeof(l4[1]))
```

Out:
```

Shallow Copy Example - Manual

l3 =  [1, [1, 2, 3]]
l4 =  [1, [1, 2, 3]]
id(l3) = 140486838605384
id(l4) =  140486838202312
l3 == l4 True
l3 is l4 False
id(l3[1]) = 140486839016584
id(l4[1]) =  140486839016584
l3[1] == l4[1] True
l3[1] is l4[1] True

---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-14-607e640db462> in <module>()
     19 print("l3[1] is l4[1]", l3[1] is l4[1])
     20 
---> 21 print("Size of l3 = ",sys.getsizeof(l3))
     22 print("Size of l4 = ",sys.getsizeof(l4))
     23 

NameError: name 'sys' is not defined

```

Here,
* values of l3 and l4 are same
* but ids of l3 and l4 are different
* nested/child object of l3 is not directly copied to l4 instead the reference of that child is provided. 
* the id of l3[1] & l4[1] are same, means changes in l4[0] will affect l3[0].
* sizes of l3 & l4 are different
* sizes of l3[1] & l4[1] are different

```python
print("\nShallow Copy Example - copy.copy()")
import copy
import sys

l3 = [1,l0]
l4 = copy.copy(l3) 
# some value of l3 are copied to l4 and reference of some are passed to l4

print("l3 = ",l3)
print("l4 = ", l4)
print("id(l3) =",id(l3))
print("id(l4) = ", id(l4))

print("l3 == l4",l3 == l4) #checks value-wise
print("l3 is l4",l3 is l4) #checks object identity-wise

print("id(l3[1]) =",id(l3[1]))
print("id(l4[1]) = ",id(l4[1]))

print("l3[1] == l4[1]", l3[1] == l4[1])
print("l3[1] is l4[1]", l3[1] is l4[1])

print("Size of l3 = ",sys.getsizeof(l3))
print("Size of l4 = ",sys.getsizeof(l4))

print("Size of l3[1] = ",sys.getsizeof(l3[1]))
print("Size of l4[1] = ",sys.getsizeof(l4[1]))

```

Out:
```

Shallow Copy Example - copy.copy()
l3 =  [1, [1, 2, 3]]
l4 =  [1, [1, 2, 3]]
id(l3) = 140486838153032
id(l4) =  140486838151368
l3 == l4 True
l3 is l4 False
id(l3[1]) = 140486839016584
id(l4[1]) =  140486839016584
l3[1] == l4[1] True
l3[1] is l4[1] True
Size of l3 =  80
Size of l4 =  104
Size of l3[1] =  88
Size of l4[1] =  88
```
Here,
* Results are same as Manual shallow copy.

Except,
* sizes of l3 & l4 are different
* sizes of l3[1] & l4[1] are same


```python
print("\nDeep Copy Example - Manual")
import copy
import sys

l5 = [1,l0]
l6 = [1, list(l0)]
# all value of l5 are copied to l6

print("l5 = ",l5)
print("l6 = ", l6)
print("id(l5) =",id(l5))
print("id(l6) = ", id(l6))

print("l5 == l6",l5 == l6) #checks value-wise
print("l5 is l6",l5 is l6) #checks object identity-wise

print("id(l5[1]) =",id(l5[1]))
print("id(l6[1]) = ",id(l6[1]))

print("l5[1] == l6[1]", l5[1] == l6[1])
print("l5[1] is l6[1]", l5[1] is l6[1])

print("Size of l5 = ",sys.getsizeof(l5))
print("Size of l6 = ",sys.getsizeof(l6))

print("Size of l5[1] = ",sys.getsizeof(l5[1]))
print("Size of l6[1] = ",sys.getsizeof(l6[1]))

```

Out:
```
Deep Copy Example - Manual
l5 =  [1, [1, 2, 3]]
l6 =  [1, [1, 2, 3]]
id(l5) = 140486838605384
id(l6) =  140486838226760
l5 == l6 True
l5 is l6 False
id(l5[1]) = 140486839016584
id(l6[1]) =  140486838253000
l5[1] == l6[1] True
l5[1] is l6[1] False
Size of l5 =  80
Size of l6 =  80
Size of l5[1] =  88
Size of l6[1] =  112
```

Here,
* values of l5 and l6 are same
* but ids of l5 and l6 are different
* nested/child object of l5 is directly copied to l6 instead of passing the reference
* the id of l5[1] & l6[1] are different, means changes in l6[0] will not affect l5[0]
* sizes of l5 & l6 are same
* sizes of l5[1] & l6[1] are different

```python
print("\nDeep Copy Example - copy.deepcopy()")
import copy
import sys

l5 = [1,l0]
l6 = copy.deepcopy(l5)
# all value of l5 are copied to l6

print("l5 = ",l5)
print("l6 = ", l6)
print("id(l5) =",id(l5))
print("id(l6) = ", id(l6))

print("l5 == l6",l5 == l6) #checks value-wise
print("l5 is l6",l5 is l6) #checks object identity-wise

print("id(l5[1]) =",id(l5[1]))
print("id(l6[1]) = ",id(l6[1]))

print("l5[1] == l6[1]", l5[1] == l6[1])
print("l5[1] is l6[1]", l5[1] is l6[1])

print("Size of l5 = ",sys.getsizeof(l5))
print("Size of l6 = ",sys.getsizeof(l6))

print("Size of l5[1] = ",sys.getsizeof(l5[1]))
print("Size of l6[1] = ",sys.getsizeof(l6[1]))

```

Out:

```
Deep Copy Example - copy.deepcopy()
l5 =  [1, [1, 2, 3]]
l6 =  [1, [1, 2, 3]]
id(l5) = 140486838138056
id(l6) =  140486838211656
l5 == l6 True
l5 is l6 False
id(l5[1]) = 140486839016584
id(l6[1]) =  140486838168328
l5[1] == l6[1] True
l5[1] is l6[1] False
Size of l5 =  80
Size of l6 =  96
Size of l5[1] =  88
Size of l6[1] =  96
```

Here, 
* Results are same as Manual Deep copy. 

Except,
* <span style="color:red">sizes of l5 & l6 are different</span>
* <span style="color:red">sizes of l5[1] & l6[1] are different</span>

** Two problems often exist with deep copy operations that don’t exist with shallow copy operations: **

* Recursive objects (compound objects that, directly or indirectly, contain a reference to themselves) may cause a recursive loop.
* Because deep copy copies everything it may copy too much, such as data which is intended to be shared between copies.


