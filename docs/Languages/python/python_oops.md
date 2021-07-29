# Python OOPs

[TOC]

TODO:

- stack queue class
- design class
- custom metaclass creation



# OOPs Basics
## UML 2.x (Unified Modeling Language)
- UML can be used for many diagrams other then ERD
    - sequence diagram
    - state diagram
    - more for the funcionality of the application (what user can do, who does it, when he does it, before what step, what table he use to do it) other then the tables description.
    - many more (http://agilemodeling.com/essays/umlDiagrams.htm)
- read more: 
    - https://www.omg.org/spec/UML
    - https://en.wikipedia.org/wiki/Unified_Modeling_Language#UML_2    
    
## ERD (Entity Relation Diagram)
- Gives image of how the tables should connect
- what fields are going to be on each table
- the tables connection, if many-to-many, one-to-many.




# OOPs Features

* Inheritance
* Polymorphism
* Encapsulation
* Abstraction

## Abstraction
(Implementation hiding)
* Core concept in all of computer science. 
* Without abstraction, we would still be programming in machine code or worse not have computers
* Give names to things, so that the name captures the core of what a function or a whole program does.
* Used to hide internal details and show only functionalities. 
* e.g : Any Verb

### Ex
1. Imagine a graphics library "nicepic" that contains pre-defined functions for: rectangles, squares, triangles, house, village.
```python
import nicepic 
draw_house()
```
2. Suppose an ATM. You simply insert your card and click some buttons and get the money. You dont know what is happening internally on press of these buttons.


## Encapsulation
(Information hiding)
* Is a characteristic to bind data members and functions in single unit.
* Is packing of data and functions operating on that data into a single component and restricting the access to some of the objects components.
* Is a mechanism which represent the essential features without including implementation details.
* e.g : Any Noun



### Ex.
1. **A class is an example of encapsulation as it encapsulates all the data that is member functions,variables etc.**
2. Suppose there is a tree. Tree can have root, stem, branches, leaves, flowers and fruits. But in a single unit we call it a tree.

### Difference between Abstraction and Encapsulation:
* Abstraction:Implementation hiding.
* Encapsulation:Information hiding.

### Implementation in Class using <u>Access Modifiers</u>
Python has no privacy model, there are no access modifiers like in C++, C# or Java. There are no truly 'protected' or 'private' attributes. 

* Public:

* Protected members:
    * Accessible outside the class and from its subclasses. 
    * By prefixing the name of your member with a single underscore
    * Accessing using: obj._protected_mem
    * Just a convention to show, the variable is protected

``` python
    class Person:
      def __init__(self): 
        self.name = 'Toran'
        self._lastname = 'Sahu' # protected
        self.__gender = 'Male'
        

      def PrintName(self):
        return self.name +' ' + self._lastname
    
    #Outside of class
    p = Person()

    print(p.name) # Out - Toran
    print(p.PrintName()) # Out - Toran Sahu
    # print(p._lastname) # Out - Sahu
```

* Private members:
    * Add ____ (double underscore ) in front of the variable and function name
    * Accessing private member : Using name mangling : obj._classname__private_mem
    
    ```python
    # print(p.__gender) # AttributeError - no attribute '__gender'
    print(p._Person__gender) # name-mangling : Out - Male
    ```

## Polymorphism

In general: The ability to appear in many forms.
Specifically: The ability to redefine methods for derived classes.

### Static Polymorphism (Method-Overloading)
* Multiple times method with same name does not support in Python (its always takes the last definition)
* We can achieve this in python in Single method itself
* By passing default parameters or by using ```*arg```, ```**kwargs```

### Runtime Polymorphism (Method-Overriding)
* Supports using Inheritance

## Inheritance
- keyword: is-a
- sign: ![sign](https://javapapers.com/wp-content/uploads/2010/06/generalization.jpg)

### Types
* Single 
* Multilevel
* Multiple
* Hierchical

### Diamond Problem 
* resolved in python using order-preference (Method Resolution Order" MRO) in multiplle inheritance
* preference order 
    - Search Path using Depth first search with linear search (old style python 2 classes)
    - Search Path with optimization using Depth first search & linear search (new style python3 classes + python2 classes whicj inherits `object`)

```python
class A:
    def m(self):
        print("m of A called")

class B(A):
    pass
    
class C(A):
    def m(self):
        print("m of C called")

class D(B,C):
    pass

d = D()
d.m()
```
Out:
```
m of C called
```

### Need of super()
- lets avoid referring to the base class explicitly (i.e. just one class above)
- e.g.
    - python 3.x: ` super().__init__()`
    - python 2.x: `super(<ChildClassName>, self.__init__())`
- 2 Basic Uses
    - In class hierarchy with single inheritance
        - used to refer to parent classes without naming them explicitly
        - thus making code more maintainable
        - similar in other languages
    - Support cooperative multiple inheritance in dynamic execution environment
        - unique to python only
        - implements diamond diagram
            - Magic happens like: `m of A called` printed once instead twice
        - e.g. 
            - **as shown below**
            - https://stackoverflow.com/questions/5033903/python-super-method-and-calling-alternatives
- applications
    - useful for accessing inherited methods that have been overridden in a child class
- Note:
    - uses MRO, in case of multiple inheritance, e.g. of class D

- Facts:
    - if super().m() is used in a member functions of a sub-class D to call its parent's member function, where class  D inherits class B and C
        - then super().m() will instantiate both the parent class B and C and will call method m() in both
            - also, if B and C 's method m() calls its super().m(), where B & C inherits class A
                - then only one time m() of A will be called (the smartest decision)

```python
class A:
    def m(self):
        print("m of A called")

class B(A):
    def m(self):
        print("m of B called")
        # A.m(self) 
        super().m()

class C(A):
    def m(self):
        print("m of C called")
        # A.m(self) 
        super().m()

class D(B,C):
    def m(self):
        print("m of D called")
        # B.m(self) 
        # C.m(self) 
        super().m()

d = D()
d.m()
```
Out:
```
m of D called
m of B called
m of C called
m of A called
```

### Other relationships
- src: https://javapapers.com/oops/association-aggregation-composition-abstraction-generalization-realization-dependency/
- These relationships are totally implementation based
    - how you want to function relationship between two or more classes & their instances

- Association
    - Aggregation
        - Composition
- Generalization
- Specialization
- Dependency

- Note:
    - uses-a
        - has-a / uses-a
            - part-of (contains-a, consists-a) / has-a / uses-a
    - i.e. a part-of relation can always use words like has-a, uses-a
    - so, to find out a perfect relationship, try to approach in a top-to-down manner, to make the relationship more specific


![set](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/Associatn.png)

## Association
- keyword: uses-a
- sign: single line with arrow
    - unidirectional
        - if class A uses instance of class B
            - arrow will point towards class B
    - bidirectional
![bi-association](https://javapapers.com/wp-content/uploads/2010/06/association.jpg)
- explanation
    - defines the multiplicity (cardianality) between objects
        - one-to-one, one-to-many, many-to-one, many-to-many
    - all classes/instances have their own life cycle (in general cases)
    - no body have ownership over another (in general cases)
- e.g.
    - house uses-an internet provider


### Weak Association (Aggregation)
- explanation:
    - Lets say we have class A & B
    - class A has-an (or uses-an) instance class B
        - means class A's any method uses instance of class B as a parameter or returns the instance
        - or if an instance of class A calls a member function (an operation) of an instance of the class B
            - or class A holds instance of class B but instance of class B doesn't get destroyed
                - when instance of class B is created & passed to constructor of class A
        
### Strong Association (Composition)
- explanation:
    - Lets say we have class A & B
    - class A has-an instance of class B / class B is part-of class A / class A consists of class B
        - means class A holds instance of class B & the instance gets destroyed with destruction of instance of class A
            - i.e. instance of class B is created & gets destroyed inside class A
        
        
## Aggregation 
- aka
    - Shared Association
    - Weak Association
- keyword: has-a (uses-a)
- sign: a line with hollow diamond
    - "whole" end have a hollow diamond shaped arrow-head 
    ![aggregation](https://javapapers.com/wp-content/uploads/2010/06/aggregation.jpg)
- cardianality: one-to-one, one-to-many, many-to-many
- explanation
    - Classes Within Classes
    - When an object ‘has-a’ another object
        - when one object is an attribute of another
    - whole/part relationship (i.e. part of relationship)
    - special form of Association
- e.g.
    - a library has-a student
        - a student can exist without a library
    - a Text-editor has-a file opened
        - if text editor is closed, file still exists

- conditional e.g.
    - if parts of a car are reusable
        - car uses-a/has-a engine
            - if car is scrapped, engine still exists

- note:
    - It’s always safe to call a relationship an association,but if class A contains objects of class B , and is organizationally superior to class B , it’s a good candidate for aggregation.

### Association vs Aggregation 

- The association link can replace aggregation link in every situation


## Composition (Not-Shared Association)
- keyword: has-a (part-of, consists-of, composed-of)
- sign: a line with solid diamond
    - unidirectional only
    - "whole" end have a solid diamond shaped arrow-head 
![Composition](https://javapapers.com/wp-content/uploads/2010/06/composition.jpg)
- cardianality: one-to-many, many-to-many
- explanation:
    - When an object contains the other object (The part may belong to only one whole)
        - if the contained object cannot exist without the existence of container object
        - i.e. The lifetime of the part is the same as the lifetime of the whole.
    - special form of Aggregation
        - Stronger/restricted aggregation
    - ownership relation
    
- e.g
    - a house has-a room
        - if house is destroyed, room also gets
    - a class has (contains) students
        - students cannot exist without a class
    - a text editor has a buffer
        - if text editor is closed, buffer also gets destroyed
        
- conditional e.g.
    - if parts of a car are NOT reusable 
        - a car has-a wheel
            - if a car is destroyed,  wheel also gets destroyed 

    


## Realization

![Realization](https://javapapers.com/wp-content/uploads/2010/06/realization.jpg)

## Dependency
![Dependency](https://javapapers.com/wp-content/uploads/2010/06/dependency.jpg)


# Implementations of OOPs


## `class`
- in python everything is object of some class
    - classes are `first-class` objects
        - they can be created at runtime, passed as parameters and returned from functions, and assigned to variables
- even `class` is object of something
    - this something by default is `type` class
    - we can create a class which is an object of `type` class
        - read metaclass for deep knowledge
    
    ```python
    cls_a = type('A', (object,), dict({'foo':2, 'bar':3})) # type(class_name_str, base_classes_tuple, body_dict)
    ```

    - this way we can create a class at runtime

### `type`
- `type` is the class of python classes

```python
class Example:
    pass

e = Example()
e.__class__  # prints: <class __main__.Example>
Example.__class__  # prints: <type 'type'>
```

- so in above code, e is object of class Example and Example is object of class `type`
- in python3 we can use `type` and `class` interchangabely
    - which was not used in python2
- so, whenever we write keyword `class` while defining a class, an object of class `type` gets created    

### `metaclass`
- source: 
    - https://eli.thegreenplace.net/2011/08/14/python-metaclasses-by-example/
    - https://realpython.com/python-metaclasses/#defining-a-class-dynamically
-  a `metaclass` is defined as `the class of a class`
- Any class whose instances are themselves classes, is a metaclass
- so, `type` is also a kind of metaclass (which is by default for all python classes and mostly used), but not always
    - we can define a `metaclass` for a `class`
    
    ```python
    class Example(metaclass=SomeMetaclass):
        # in python2 define metaclass here like
        # __metaclass__ = SomeMetaclass
        pass
    ```

- Since a metaclass is the class of a class
    - it is used to construct classes (just as a class is used to construct objects)    
    - as we have already seen, `class` keyword invokes `type` function to create a class
        - it was because, `type` is default `metaclass`
    - in reality `class` keyword do followings
        - when python encounters `class` definiton, it collects all the attributes in a `dict`
        - when collection is over, python determines `metaclass` of the class, lets say `SomeMetaclass`
            - using `SomeClass.__metaclass__`
        - then python calls `Metaclass(class_name, (base_classes, ), body_dict)`, where
            - `class_name` is the name of the class (string )
            - `(base_clasees, )` is the tuple of base classes, if it was empty in class definition, then by dafault it is `object`
            - `body_dict` is a python dict contaning all the class attribute names
            
- metaclass defines structure/metadata of the class

Methods of metaclass to create & initialize a class are:

#### `__new__()`
- used to perform some basic stuff like memory allocation
- called on creation of an object of the class

#### `__init__()`
- works as contructor in python
- used to perform initialization of data
- called on creation of an object of the class
- it is called after above methods `__new__()`
- so in case of creation of class (suppose `A`), it is called when we call `type()`

#### `__call__()`
- it is called after above two methods
- in case of creation of class, it is called when an object (suppose `a = A()`)  of the class (created from above two steps) is created.


### `instance` 
TODO:
    - confusion in magic method call orders
- how a `class` instance are created
    - as a class is object of a metaclass
    
    ```python
    #here class A
    A = type('A', (object,), {"a":1})
    ```
    
    - whenever we call any object/instance of any class, it calls the `__call__` of that class
    
    ```python
    a = A()
    
    #here A() will call the __call__ of metaclass type
    ```
    
    - so, a is created by A(), where A() means calling `__call__` of `type` metaclass
    - if we provide A() parameters, like A(1,2), then `__call__(self, *args, **kwargs)__` handles those parameters
    - then inside metaclass's `__call__` , `__init__` of the class is called by passing all the parameters passed to `__call__`
    
- so, whenever we create an object/instance of a class, following things happens:
    - metaclass's ` __new__` is called; creates memory (object) for class
    - metaclass's `__init__` is called; intializes class with its name and body
    - when class, lets say `Example` is called Example(), then metaclass's `__call__` is called
    - to initialize the object of Example class, `Example.__init__` is called
    


### Old vs New Style
- in python realm, there are two varities of classes
    - Old-Style
        - object of a class is always a <type 'instance'>
        - in python 2.x , classes are old-style by deafult due to compatibility issues
        - in python 2.x, New-Style classes are created by inheriting other New-style classes or `top-level type` `object`
            - here `object` is a keyword which is instance of class `type`, and we know that `type` is a metaclass
                - and `metaclass` is `a class of class`
                - hence instance of a metaclass is always a `class`
                - hence `object` keyword is a kind of class, which is created already in python just to implement a New-Style class
        - syntax are like 
        
        ```python
        class A(object):
            pass
        ```
        
    - New-Style
        - object of a class is always a <type '__main__.ClasssName'>
        - in python 3.x has new-style classes only
            - hence no need to inherit `object` in class
            
            ```python
            class Example :
                pass
            ```
            
        - introduced in python2.2 to unify the concepts of `class` and `type`
            - in new-style `type(x)` and `x.__class__` are always same 
            - a new-style class is simply a user-defined type
- more differences at https://stackoverflow.com/questions/4015417/python-class-inherits-object
    - TODO:
        

### `object` keyword    
- `object` is a keyword which is instance of class `type`, and we know that `type` is a metaclass
    - and `metaclass` is `a class of class`
    - hence instance of a metaclass is always a `class`
    - hence `object` keyword is a kind of class, which is created already in python just to implement a New-Style class

### MRO 
(Method Resolution Order)
- source:
    - https://makina-corpus.com/blog/metier/2014/python-tutorial-understanding-python-mro-class-search-path
- `class.__mro__` is only available in New-Style class

Script: 1 

```python
class A:
    def m(self):
        print("m of A called")

class B(A):
    def m(self):
        print("m of B called")


class C(A):
    #def m(self):
    #   print("m of C called")
     pass

class D(B,C):
    #def m(self):
    #    print("m of D called")
    pass

d = D()
d.m()        
```

Script: 2

```python
class A1():
#      def who_am_i(self):
#          print("I am a A1")
    pass

class A2():
     def who_am_i(self):
         print("I am a A2")


class B(A1, A2):
#     def who_am_i(self):
#         print("I am a B")
    pass

class C(A2):
    def who_am_i(self):
        print("I am a C")

class D(B,C):
#     def who_am_i(self):
#         print("I am a D")
    pass

d1 = D()
d1.who_am_i()
```

#### DLR (Old) MRO Algorithm (Based on Old-Style Class)
- depth first left to right
- uses `depth-first` search followed by `linear` search (left to right)
    - we call this order `search path`
- in script 1
    - Looking in D
    - If not found, looking in B
    - If not found, looking un B first parent A
    - If not found, going back in B others parents (none)
    - If not found, looking in D others parents : C
    
- in script 2
    - search path will be  D, B, A1, A2, C, A2


#### C3 New MRO Algorithm (Based on New-Style Class)
- default in python3
- works in python2 with classes who inherits `object`
- Algo
    - defines search path same as old algorithm
    - then simplifies the search path like this
        - iterate through the original search path
        - put pointer on current class
        - check if any classes after the pointer are child of current class (in other words, check if any classes after the pointer inherits the current class) 
            - if yes, then remove the current class from search path
            - if no, then move the pointer to next class in the right
            - do the same till end of search path list

- in script 1
    - original search path will be  D, B, A, C, A
    - then simplified search path will be  D, B, C, A
    
- in script 2
    - search path will be  D, B, A1, A2, C, A2
    - then simplified search path should be  D, B, A1, C, A2

#### Impossible Method Resolution
<img src="https://makina-corpus.com/blog/metier/2014/python-mro-conflict" >

Script:

```python
class X():
    def who_am_i(self):
        print("I am a X")
    
class Y():
    def who_am_i(self):
        print("I am a Y")
    
class A(X, Y):
    def who_am_i(self):
        print("I am a A")
    
class B(Y, X):
     def who_am_i(self):
         print("I am a B")

class F (A, B):
    def who_am_i(self):
        print("I am a F")
```

- In Old MRO algo, search path is F, A, X, Y, B, Y, X
- In New MRO algo, simplified search path is F, A, B, Y, X  but New MRO algo fails to give `__mro__`
    - and throws following exception
    
    ```
    TypeError: Cannot create a consistent method resolution
    ```




### Abstract Base Class (Abstract Class)
* Classes that contains one or more abstract methods as well as concrete methods. A normal class cannot have abstract methods.
* Cannot instantiate an abstract class that has abstract methods
* Subclass which implements all the abstract method can be instantiated

Python Implementation:
``` python
    # Python 3.4+
    from abc import ABC, abstractmethod
    class Abstract(ABC):
        @abstractmethod
        def foo(self):
            pass

    # Python 3.0+
    from abc import ABCMeta, abstractmethod
    class Abstract(metaclass=ABCMeta):
        @abstractmethod
        def foo(self):
            pass

    # Python 2
    from abc import ABCMeta, abstractmethod
    class Abstract:
        __metaclass__ = ABCMeta

        @abstractmethod
        def foo(self):
            pass    

```

### Bottom Line
- in python3:
    - base class of classes are: `object`
    - metaclass of classes are: `type`
    - type of classes are: `type`
    - classes are instance of class: `type`

## Class Decorators
- e.g. https://github.com/toransahu/py-misc/blob/master/class_based_class_decorator_with_pre_post.py
TODO:

### Class Decorators versus __metaclass__
- source:
    - https://jfine-python-classes.readthedocs.io/en/latest/decorators-versus-metaclass.html

- nothing different other than implementation style

## Interface
* Doesn't need in Python (bcoz, it was need in other lang. to full-fill the Multiple inheritance)

Concept:
* A class with **all the methods abstract**
* Contains Methods signature
* Do not contain definition/method body
* **Constant variables (which must be Static + Final in other langs.)**
    - in python there is no `final` or `const` keyword
* **Cannot instantiated**
* Behaviour/methods which **must** be implemented by classes
* Class which implement interface should **implement all the methods** OR **be an abstract class**

Python Implementation:
``` python
    class Engine():
        """ Engine Interface"""
        
        def ignition(self):
            raise NotImplementedError( "Ingnition should have implemented." )
        def fuel(self):
            raise NotImplementedError( "Fuel should have implemented." )

```


## Variables

### Instance Variable
* variable defined inside class methods
* different for different objects
* every object have its own copy

### Static or Class Variable
* defined in class level
* shared by all the objects
* can be accessed by Class name as well as objects
* **with the same name, there can be one class level variable and one instance level variable, see in e.g.**
    * in this case, Class.variable will definitely access the static var
    * but instance.variable will access the instance variable
* accessing inside methods
    - it can be accessed using Class.var & self.var
    - if there is instance variable with the same name then self.var will access the instance variable

```python
class A:
    variable = 'Static/class Variable'  # static/class variable
    var = 'Static/class Var'  # static/class variable

    def __init__(self):
        self.variable = 'Instance Variable'

    def foo(self):
        print(A.variable, self.variable, self.var)


print(A.variable)

a = A()
a.foo()
```

Out:
```
Static/class Variable
Instance Variable
Static/class Var
Static/class Variable Instance Variable
```

### Instance vs Class/Static attribute lookup order
> instance/object > static/class > base class

which is:
> a.__dict__['x'] > type(a).__dict__['x'] > type(a) 

## Methods

### Abstract Method
* a method without definition (only declared)
* only signature
* In python: a method decorated with @abstractmethod


### Method vs Function

* Method works exactly same as a simple function. 
* But a method's first argument always receives the instance object:

Code:
``` python
def outside_foo():
    pass

def outside_foo(self,):
    pass
```

### Static Method
#### What    
- an organization/stylistic feature
- functionality-wise same as normal module level functions
    - except, module level func can access an instance and hence instance variables, but static method cannot
- designed to work on class attributes
- can be called using class as well as instance
- A static method has no self argument 
- Never receive an automatic self argument, whether called through a class or an instance. 
- can access/modify class or static variables using `class_name.var`

#### How
* two way of declaration
    - using decorator @staticmethod 
    - [fn_name] = staticmethod([fn_name])

#### Why
- to restrict access of instance attributes (unlike a normal method have access)
- to fix the access of static variable of a that particular class only
    - because it is hardcoded like A.static_variable


* src: http://radek.io/2011/07/21/static-variables-and-methods-in-python/

#### Code
``` python
class A:
    static_variable = 'Static/class Variable of class A'  # static/class variable

    def __init__(self):
        self.instance_variable = 'Instance Variable'

    @staticmethod
    def static_method():
        print('Inside static_method()', A.static_variable)  # works
        # print('Inside static_method()', A.instance_variable)  # error, static method can't access instance attributes

    # static method
    def way2():
        pass

    # making way2() a static method
    way2 = staticmethod(way2)


class B(A):
    static_variable = 'Static/class Variable of class B'  # static/class variable


# but a module level func can access an instance attribute
def module_level_func():
    a1 = A()
    print(a1.instance_variable)


a2 = A()

a2.static_method()
A.static_method()
B.static_method()  # still accessing static_variable from class A
```

Out:
```
Inside static_method() Static/class Variable of class A
Inside static_method() Static/class Variable of class A
Inside static_method() Static/class Variable of class A
```

### Class Method
#### What
- an organization/stylistic feature
* not different from static method, only signature diff
* it receives one mandatory arguement: a class name it was called from
- apart from this first parameter, there is no any functionality diff between class & static method
- designed to work on class attributes
- can be called using class as well as instance
- can access/modify class or static variables using `cls.var` where cls is first parameter provided to a classmethod

#### How
* implemented using 
    - decorator @classmethod
    - assigning to function i.e., method_name = classmethod(method_name)

#### Why
- to restrict access of instance attributes (unlike a normal method have access)
- to make code more maintanable than static methods

#### Code
``` python
class A:
    static_variable = 'Static/class Variable of class A'  # static/class variable

    def __init__(self):
        self.instance_variable = 'Instance Variable'

    @classmethod
    def class_method(cls):
        print('Inside class_method()', cls.static_variable)  # works
        # print('Inside class_method()', cls.instance_variable)  # error, class method can't access instance attributes

    # static method
    def way2(cls):
        pass

    # making way2() a static method
    way2 = classmethod(way2)


class B(A):
    static_variable = 'Static/class Variable of class B'  # static/class variable


# but a module level func can access an instance attribute
def module_level_func():
    a1 = A()
    print(a1.instance_variable)


a2 = A()

a2.class_method()
A.class_method()
B.class_method()  # now it will access static variable of class B
```

Out:
```
Inside class_method() Static/class Variable of class A
Inside class_method() Static/class Variable of class A
Inside class_method() Static/class Variable of class B
```


### Magic Method
TODO:

- Source:
    - https://www.python-course.eu/python3_magic_methods.php
    - https://rszalski.github.io/magicmethods/
* Methods with dunders
* (+) : `__add()__`
* (-) : `__sub()__`

- Can be used for operator overloading, as

```python

class Calc(int):
    def __init__(self, x):
        self.x = x
    def __add__(self, other):
        return self.x + other.x + 1

a = Calc(1)    
b = Calc(1)
a + b
```

Out:

```
3
```

### Class Internal Methods
TODO:

- Source:
    - http://www.diveintopython3.net/special-method-names.html
    - https://rszalski.github.io/magicmethods/

Some famous magic methods / internal methods of a class


#### `__new__`
- allocates memory to class instance

#### `__init__`
- initializes instance with some values

#### `__call__`
- called upon calling an instance (e.g. a = A(); a())

#### `__get__`
- get descriptor method

#### `__set__`
- set descriptor method

#### `__del__`
- del descriptor method

#### `__slots__`
- allows us to explicitly declare data members (like properties) and deny the creation of `__dict__` & `__weakref__` (unless explicitly declared in `__slots__`)

#### `__getattribute__`
- called when accessing any attribute via class instance 

```python
c = C()
c.name
```

#### `__getattr__`
- same as `__getattribute__` but gets called only when attribiute is not found via `__getattribute__` 

#### `__getattr__` vs  `__getattribute__`
- Source:
    - http://www.diveintopython3.net/special-method-names.html
    
#### `__enter__`    

#### `__exit__`

#### `__repr__`
#### `__str__`
#### `__format__`
#### `__iter__`
#### `__next__`
#### `__reversed__`
#### `__dir__`
#### `__setattr__`
#### `__delattr__`
#### `__len__`
#### `__contains__`
#### `__getitem__`




### Properties

- Source:
    - https://www.journaldev.com/14893/python-property-decorator
    - https://docs.python.org/3/howto/descriptor.html#properties
    - https://medium.com/shecodeafrica/managing-class-attributes-in-python-c42d501c5ee0

- Why
    - to manage access to an attribute to outer world
        - can only allow get
        - can only allow set
        - can only allow del
        - can perform something more while doing above operations
        
    - to solve problem like this (dependent attribute value issue)
        
        - e.g.

        ```python
        class Example:
            def __init__(self,ap, bp):
                self._a = ap
                self._b = bp
                self.c = self._a + self._b

            def get_c(self):
                return self.c

        e = Example(1,2)        
        print(e._a)
        print(e._b)
        print(e.c)
        print(e.get_c())
        e._a = 5
        print(e._a)
        print(e.c)
        print(e.get_c())
        ```

        - solution e.g.

```python

        class Example:
            def __init__(self,ap, bp):
                self._a = ap
                self._b = bp

            @property
            def c(self):
                return self._a + self._b


        e = Example(1,2)        
        print(e._a)
        print(e._b)
        print(e.c)
        e._a = 5
        print(e._a)
        print(e.c)
```
    
- What
    - property are built -in python decorators
    - provides 3 methods
        - get
        - set
        - del

- How
    - property in python are implemented using `Descriptors`

- uses : pattern 1

```python
class Example:
    def __init__(self,ap):
        self._a = ap

    
    @property
    def a(self):
        return self._a

    @a.setter
    def a(self, value):
        self._a = value

    @a.deleter
    def a(self):
        del self._a


e = Example(1)        
print(e.a)
e.a = 5
print(e.a)
del(e.a)
print(e.a)  #AttributeError: 'Example' object has no attribute '_a'
```

- uses : pattern 2

```python
class Example:
    def __init__(self,ap):
        self._a = ap

    def get_a(self):
        return self._a

    def set_a(self, value):
        self._a = value

    def del_a(self):
        del self._a

        
    # will give only get access
    a = property(fget=get_a)
    
    # will give only set access
    a = property(fset=set_a)
    
    # will give only del access
    a = property(fdel=del_a)
    
    #will give all access of var `a`
    a = property(get_a, set_a, del_a)  #property(fget=None, fset=None, fdel=None, doc=None)

e = Example(1)        
print(e.a)
e.a = 5
print(e.a)
del(e.a)
print(e.a) # AttributeError: 'Example' object has no attribute '_a'
```

### Descriptors
TODO:

- Source:
    - https://docs.python.org/3/howto/descriptor.html

- descriptor is an object attribute with “binding behavior”, one whose attribute access has been overridden by methods in the descriptor protocol
- Those methods are __get__(), __set__(), and __delete__()
- Basic
	- default behavior for attribute access is to get, set, or delete
	- For instance, a.x has a lookup chain starting with a.__dict__['x'], then type(a).__dict__['x'], and continuing through the base classes of type(a) excluding metaclasses
	- If there is descriptor `x` defined, then descriptor will override the lookup order and will become number one
- Use Cases
	- They are the mechanism behind properties, methods, static methods, class methods, and super()
	- They are used throughout Python itself to implement the new style classes introduced in version 2.2

#### Protocol
```python
descr.__get__(self, obj, type=None) --> value

descr.__set__(self, obj, value) --> None

descr.__delete__(self, obj) --> None
```

- define any of the above in any class, and object will considered as descriptor
    - and descriptor will override the default attribute lookup behavior (in class dictionary lookup)
- if object defines both `__get__` and `__set__`; then its `data descriptor`     
    - if instance have attribute (means entry in instance dict) with same name as descriptor, then here lookup order will become `data descriptor > instance dict`
- if object defines only `__get__`; then its `non-data descriptor`
    - in this case if instance have attribute with same name as descriptor, then here lookup order will become `instance dict > data descriptor`


#### Simple Implemetation

TODO
    - Issue with `__del__`; not explained in python doc

```python
class ExampleDescriptor:
    def __init__(self, val):
        self.val = val

    def __get__(self, obj, objtype=None):
        print("getting")
        return self.val

    def __set__(self, obj, val):
        print("setting")
        self.val = val


class Example:
    name = ExampleDescriptor("toran")


if __name__ == "__main__":
    e = Example()
    print(e.name)
    e.name = "sahu"
    print(e.name) 
```    

#### Property implementation
```python
class Property(object):
    "Emulate PyProperty_Type() in Objects/descrobject.c"

    def __init__(self, fget=None, fset=None, fdel=None, doc=None):
        self.fget = fget
        self.fset = fset
        self.fdel = fdel
        if doc is None and fget is not None:
            doc = fget.__doc__
        self.__doc__ = doc

    def __get__(self, obj, objtype=None):
        if obj is None:
            return self
        if self.fget is None:
            raise AttributeError("unreadable attribute")
        return self.fget(obj)

    def __set__(self, obj, value):
        if self.fset is None:
            raise AttributeError("can't set attribute")
        self.fset(obj, value)

    def __delete__(self, obj):
        if self.fdel is None:
            raise AttributeError("can't delete attribute")
        self.fdel(obj)

    def getter(self, fget):
        return type(self)(fget, self.fset, self.fdel, self.__doc__)

    def setter(self, fset):
        return type(self)(self.fget, fset, self.fdel, self.__doc__)

    def deleter(self, fdel):
        return type(self)(self.fget, self.fset, fdel, self.__doc__)
```



# Misc

## Ways to call a class member function
- 
    ```python
    a = A()
    a.foo(args)
    ```
- 
    ```python
    a = A()
    A.foo(a,args)
    ```

## `__slots__` : reduce RAM usage
- source http://book.pythontips.com/en/latest/__slots__magic.html

### Unbound vs Bound Method

#### Unbound Method (Simple Function in Python 3.x)
* Unbound means not bound to any instance
* i.e. callable using class name 

#### Bound Method
* Bound methods are bound to some instance 
* Need an instance to call it.

**Note: In Python 3.x, the notion of Unbound Method has been dropped and we treat it as Simple Function.**


### Closure
* A combination of code and scope.
* It's about nested function and the scope of the function

Code:
``` python
def startAt(start):
    def incrementBy(inc):
        return start + inc
    return incrementBy

f = startAt(10)
g = startAt(100)
print(f(1), g(2))

# Using lamba
def startAt(start):
    return lambda inc : start + inc

f = startAt(10)
g = startAt(100)
print(f(1), g(2))
```

Out:
```
11 102
11 102
```
