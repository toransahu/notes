# Design Principles

# SOLID

- Single Responsibilty
- Open/Closed
- Liskov Substitution
- Interface Segregation
- Dependency Inversion

Most popular sets of design principle in OOPs software engineering.

Promoter: Robert C. Martin (Uncle Bob), 2000

## Single Responsibilty Principle

> A class should have one, and only one, reason to change.
>
> _- Robert C. Martin, 2000_

### What
- a class should have a single responsibilty
- can be applied to other software components as well - function, method, module, package, microservice

### Issue
- in todays world, requirements changes quite fast, thus the responsibilities of classes
- the more responsibilities a class have, more frequent it need to be refactored
- more refactoring --> more side effects in multiple components, at least in unit tests for that class

### Benefit
- easy to maintain
- minimal side effect
- easy to explain a class/component
- improved testability
- makes developers/maintainers life easy

### Notes
- don't overly simplify the class
    - this would result in injecting a lot of dependencies to the dependent/consumer classes
- use commonsense

## Open-Closed Principle

> A class is closed, since it may be compiled, stored in a library, baselined, and used by client classes. But it is also open, since any new class may use it as parent, adding new features. When a descendant class is defined, there is no need to change the original or to disturb its clients.
>
> _- Bertrand Mayer, 1988_

- open: a class should open for extension usually by inheritence
- closed: but the class should be closed for modification

_"As we learned over years that, Inheritance introduces tight coupling if the subclasses depend on implementation details of their parent class."_

Thus uncle Bob and others redefined the principle to __Polymorphic__ Open-Closed principle:

> Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification.
>
> _- Robert C. Martin, 2000_

- it uses interfaces instead of supe/parent classes
- closed: the interface should be closed for modification
- open: a class should open for extension usually by implementing the interface
- define very much required properties/methods in the interface
- if two are more implementations have some code in common, then there could be a chance of inheritence or composition

### Issue
- if interface/class kept open for modification, then more refactoring & more side-effect 

### Benefit
- no changes to existing code (class/interface), thus no side-effect
    - easy to maintain, test, understand
- interface provides additional level of abstraction
- interface enables loose coupling between classes

## Liskov Substitution

This principle extends the Open/Closed principle by focusing on the behavior of a superclass and its subclasses.

> Let Φ(x) be a property provable about objects x of type T. Then Φ(y) should be true for objects y of type S where S is a subtype of T.
>
>_- Barbara Liskov, 1987_

- objects of a superclass shall be replaceable with objects of its subclasses without breaking the application
    - that requires the objects of its subclasses to behave in same way as the objects of the superclass
- i.e., sub-classes should stand for their parents without breaking anything


- don't implement any stricter validation rules on input parameters than implemented by the parent class
- apply at least the same rules to all the return/output parameters as applied by the parent class

## Interface Segregation 

> Clients should not be forced to depend upon interfaces they do not use.
>
> _- Robert C. Martin, 2000_

### What 
- many specific interfaces are better than one do-it-all interfaces
- in python we use abstract base class with multiple inheritence to achieve this

### Issue
- if multiple clients depends on a huge do-it-all interface, then change in requirements could lead to multiple modification, then more refactoring & more side-effect 

### Benefit
- no changes to existing code (class/interface), thus no side-effect
    - easy to maintain, test, understand
- avoids bloated interface that define multiple responsibilities

### How
- split the software into multiple, independent parts
- split a huge do-it-all interface into some heirchical parts, say IBase, IKindA extends IBase, IKindB extends IBase 
- if a class really behaves as do-it-all, then it can implement all the small interfaces - like mixins

## Dependency Inversion

It is based on the Open/Closed principle and Liskov Substitution principle.

> 1. High-level modules should not depend on low-level modules. Both should depend on abstractions.  
> 2. Abstractions should not depend on details. Details should depend on abstractions.  
>
> _- Robert C. Martin, 2000_

### What

- we should program towards abstractions, not towards implementations
	- implementations can vary, abstraction should not
- what does above point say?
	- the higher class (container class) should not dependent on the lower classes (class being stored/used in higher class) instead depend upon the abstraction of the lower classes
	- e.g. say Manager class should have a list of Empoyees class obj, instead of maintaing individual list of Developer, Designer, Tester class objs
- so text-book term
	- a Context class uses-a Strategy Interface, whereas many ConcreteStrategy class implements the Strategy Interface
	- Encapsulate algorithms and separate them as ConcreteStrategy
- in Python Strategy could be function, lambda as well
- applying the Open/Closed and the Liskov Substitution principles, makes the code also comply with the Dependency Inversion Principle

## Ref
- books
	- Design Patterns, Elements of Resusable Pbject-Oriented Software
- pluralsight - https://app.pluralsight.com/course-player?clipId=a880a2a0-4d79-4b5f-a9da-c40411ebb11f

# DRY

# KISS

# YAGNI
