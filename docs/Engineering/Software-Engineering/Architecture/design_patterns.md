# Design Patterns

### Table of Contents
[TOC]


# What
- a model solution to common design problems
	- which we encouter often, occurs over-and-over
- describes the problem, and a genereal approach to solve them


# How we discovered?

# Why
- to ensure our work is
	- consistent
	- reliable
	- understandable
- we dont want to re-invent the wheel, just check if for current problem there is design solution

# When

# Classification

- Creational (helps create objects in oops world)
	- Builder
	- Factory
	- Abstract factory
	- Singleton
	- Prototype
	- Object Pool
- Structural (helps design relationship between the objects)
	- Adaptor
	- Facade
	- Composite
- Behavioral (helps design object interaction and responsibilites; control the operation of some objects)
	- Strategy / Policy
	- Observer / Dependant / PubSub
	- Command / Action / Transaction
- Concurrency
- No Pattern (python only?)
- Mono-State Pattern (python only?)
- Visitor Pattern



# Builder Pattern
## What
- helps separate the construction of a complex object
	- e.g. a custom/assembled computer
- encapsulates the construction of the object
	- ie. follows this: "encapsulate what varies" - hence single responsibility principle
- allows multistep construction process (main property)

## Why
- separates the "how" from "what"
- assembly separates from components
- encapsulates what varies - the parts
- permits diff. representations
- can leverage `Director` concept, e.g. to manage order of building attributes
- builder adds parts to the products

## How

## When

# Factory Pattern
## What
- define interface for creating an object
- lets subclasses decide which object to create
	- it achieves it through `factory()` method
- makes subclasses responsible for instantiation / defer instantiation to subclasses
- also known as `Virtual Constructor`

## Why
- when we want to build/instantiate and return at runtime based on some params

## How

## When

## Thoughts
- i think dependency-inversion could not be solved 

# Abstract Factory
## What
- whereas `Factory` creates from one product class, `AbstractFactory` can produce from family of product class
- enforces dependencies between concrete class
- defer instantiation to subclasses
- also knows as `Kit` pattern 

## Why

## How

## When

## Thoughts
- i think dependency-inversion could not be solved 

# Singleton Pattern

## What
- ensures to create a single object/instance of a class
	- .e.g. Web/DB connection pool, device access, buffer pools
	- sometimes based on implementation - objects (its memory loc) could be diff. but there state would remain same  (see monostate e.g.)
- responsible for creating that instance
- provides a global point of access 
- can also facilitate "lazy instantiation", if instantiation is costly

## Why
- read _What_
- disallowing creation on new instance
- reduces the global namespace, as it self it global
- subsclassible for extended purposes
- variable number of instances - as all of them are same only
	- e.g. base class + meta class variants
- more flexible than a static class, since we can have multiple instances
	- (in python, static class is one with no instances)
- monostate variant can share all/full state

## How

## When

## Cons
- violates single-responsibilty principle
	- how? it does it own task + creates and stores itw own instance as well
- non-standard class access / design (who knows there is .instance() `static method`)
- harder to test ?? why??
- carry a global state 
- hard to sub-class ?? why - just mandatoryily override the `.instance()` ?? else don't follow `.instance()` design
- singletons are considered harmful by experts
	- and are called `antipattern`

# Prototype
## What
## Why
## How
## When
## Cons

# Object Pool
## What
## Why
## How
## When
## Cons

- structural (helps design relationship between the objects)
	- adaptor
		- what
		- why
		- how
		- when
	- facade
		- what
		- why
		- how
		- when
	- composite
		- what
		- why
		- how
		- when
- behavioral (helps design object interaction and responsibilites; control the operation of some objects)
	- strategy / policy
		- what
			- 
		- why
		- how
		- when
	- observer / dependant / pubsub
		- what
			- defines one-to-many relationship between a set of objects
				- so that when the state of one changes, all its dependents are notified
			- e.g. Lets say there is a `News` class to which many `Reader` can subscribe to
				- here `News` is a Subject class and `Reader` is an Observer class
				- many Observers can subscribe to the Subject
				- the Subject should have facility to `attach`, `detach`, and `notify` the Observers
			- we can implement a `Push` model using this pattern
		- why
			- separates the concerns subject, object, and main program
			- acheives SOLID
				- single-responsibilty
					- individual classes for each
				- interface-segregation
					- by creating abstract classes for `Subject` and `Object`
				- open-closed
					- `Subject` and `Observer` are open for extension but closed for modification
				- dependency-inversion
					- `Subject` and `Observer` are programmed towards abstraction and not implementation
		- note
			- its a good idea to handle automatic `detach` of observers once they finish
				- this will avoid memory leak and help automatic garbage collector
					- by removing dangling references
	- command / action / transaction
		- usage
			- CLI, GUI
		- why
			- encapsulate behaviors
			- seperate command logic from client
			- easiliy provide/provision additional capabilities
				- validate
				- undo
		- how
			- encapsulate a request as an object
				- and facilitates to parameterize an object for diff. requests
			- supports queues and logs
				- queues for:
					- updating a DB
					- executing a list of commands
			- can bake support for undoable operations and macros
				- macros (sequences of commands)

- concurrency
	- what
	- why
	- how
	- when
- no pattern (python only?)
	- what
	- why
		- in python helps avoid check for `none`
	- how
	- when	
- mono-state pattern (python only?)
	- what
		- every instance of the class should have the same `state` (say if state is a dict, then all objects will have same dict)
	- why
		- one ans. is to achieve singleton
	- how
		- create a class dict `state`; update that dict with `instance` inside `__new__`; add `state` to `instance.__dict__`
		- this way, first, second, .. last every instance will have same `state`
	- when	
		- singleton
		- many other use cases
- visitor pattern
