<h1>Design Patterns</h1>

[TOC]

## what?
- a model solution to common design problems
	- which we encouter often, occurs over-and-over
- describes the problem, and a genereal approach to solve them


## how we discovered?

## why?
- to ensure our work is
	- consistent
	- reliable
	- understandable
- we dont want to re-invent the wheel, just check if for current problem there is design solution

## when?

## classification
- creational (helps create objects in oops world)
	- builder
		- what
			- helps separate the construction of a complex object
				- e.g. a custom/assembled computer
			- encapsulates the construction of the object
				- ie. follows this: "encapsulate what varies" - hence single responsibility principle
			- allows multistep construction process (main property)
		- why
			- separates the "how" from "what"
			- assembly separates from components
			- encapsulates what varies - the parts
			- permits diff. representations
			- can leverage `Director` concept, e.g. to manage order of building attributes
			- builder adds parts to the products
		- how
		- when
	- factory
		- what
			- define interface for creating an object
			- lets subclasses decide which object to create
				- it achieves it through `factory()` method
			- makes subclasses responsible for instantiation / defer instantiation to subclasses
			- also known as `Virtual Constructor`
		- why
			- when we want to build/instantiate and return at runtime based on some params
		- how
		- when
		- thoughts
			- i think dependency-inversion could not be solved 
	- abstract factory
		- what
			- whereas `Factory` creates from one product class, `AbstractFactory` can produce from family of product class
			- enforces dependencies between concrete class
			- defer instantiation to subclasses
			- also knows as `Kit` pattern 
		- why
		- how
		- when
		- thoughts
			- i think dependency-inversion could not be solved 
	- singleton
		- what
			- ensures to create a single object/instance of a class
				- .e.g. Web/DB connection pool, device access, buffer pools
				- sometimes based on implementation - objects (its memory loc) could be diff. but there state would remain same  (see monostate e.g.)
			- responsible for creating that instance
			- provides a global point of access 
			- can also facilitate "lazy instantiation", if instantiation is costly
		- why
			- + what
			- disallowing creation on new instance
			- reduces the global namespace, as it self it global
			- subsclassible for extended purposes
			- variable number of instances - as all of them are same only
				- e.g. base class + meta class variants
			- more flexible than a static class, since we can have multiple instances
				- (in python, static class is one with no instances)
			- monostate variant can share all/full state
		- how
		- when
		- cons
			- violates single-responsibilty principle
				- how? it does it own task + creates and stores itw own instance as well
			- non-standard class access / design (who knows there is .instance() `static method`)
			- harder to test ?? why??
			- carry a global state 
			- hard to sub-class ?? why - just mandatoryily override the `.instance()` ?? else don't follow `.instance()` design
			- singletons are considered harmful by experts
				- and are called `antipattern`
	- Prototype
		- what
		- why
		- how
		- when
		- cons
	- Object Pool
		- what
		- why
		- how
		- when
		- cons

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

## Object oriented design principles

### 5 principles - SOLID
- single responsibilty 
	- a class should have a single responsibilty
- open-closed
	- open: a class should open for extension usually by inheritence
	- closed: but the class should be closed for modification
- Liskov substitution
	- sub-classes should stand for their parents without breaking anything
- interface segregation 
	- many specific interfaces are better than one do-it-all interfaces
	- in python we use abstract base class with multiple inheritence to achieve this
- dependency inversion
	- we should program towards abstractions, not towards implementations
		- implementations can vary, abstraction should not
	- what does above point say?
		- the higher class (container class) should not dependent on the lower classes (class being stored/used in higher class) instead depend upon the abstraction of the lower classes
		- e.g. say Manager class should have a list of Empoyees class obj, instead of maintaing individual list of Developer, Designer, Tester class objs
	- so text-book term
		- a Context class uses-a Strategy Interface, whereas many ConcreteStrategy class implements the Strategy Interface
		- Encapsulate algorithms and seprate them as ConcreteStrategy
	- in Python Strategy could be function, lambda as well


## Ref
- books
	- Design Patterns, Elements of Resusable Pbject-Oriented Software
- pluralsight - https://app.pluralsight.com/course-player?clipId=a880a2a0-4d79-4b5f-a9da-c40411ebb11f


## Mist
- papi
	- redis caching
		- singleton pattern?
	- coon. to internal microservices
		- singleton pattern?
	- CRUD api method
		- repository pattern?
- papi-internal
	- bot
		- command pattern
	- config
		- factory pattern?
- papi-ws
	- observer pattern
- papi-portal
- papi-bolt