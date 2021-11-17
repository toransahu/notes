# System Design

<h3>Table of Contents</h3>
[TOC]

# Application Architecture Types

## Monolithic / N-Tier / Layered
- monolithic aka n-Tier app
- separates/segregates concerns and decompose code base into functional components/layers
    - e.g. Data Access Layer, Presentation Layer, Business Logic Layer
    - or, MVC (Model, View, Controller) Framework
    - IDEA: to work with any component of the architecture independent of the other

### Cons
- long term maintainability (cumbersome codebase)
- decoupling issue
- code change --> whole code base change
- deployment --> whole application deplyment
- difficulty adopting new technologies
- less agile (tight coupled features/code/team) -> takes more time
- scalling --> scale whole application --> more cost
- ...

### Pros
- simple/fast development (in initial days)
- performant/fast (as no network calls)
- fewer intercommunication pains

PS: Not outdated yet.

## SOA (hybrid?)

Service-based architectur

- was the evolution to the limitation of the Monolithic architecture
- decouples the application in smaller modules
- all the smaller modeules/services then work with an aggregation layer/bus/message queue etc.
- involves 2 main roles
    - service provider
    - service consumer
- idea/concept
    - reusable modules
    - easily integrateable modules

### Cons
- complex management
    - communication between each services
- scalling/mgnt of the communication bus/message queue
    - e.g. Kafka?
- cost
    - more human resource
    - tech
    - development
- decreased response time
    - network calls
    - more running codes
        - more request/response validation

### Pros
- better resuablity
- better maintainability
- better testability/debugability
    - better reliability
- agile
    - parallel development
- separates internal & external elements


PS: better for complex systems, where decomposition is not quite feasible/suitable.

## Microservice

- a kind of SOA
- are the evolution to some limitation of the SOA architecture
- idea/concept
    - encouraging autonomus services/components
    - to gain agility to priorities business
    - to gain more capabilities in many terms
    - reduce duplication
    - increase cohesion
    - reduce tight-coupling
        - thus easier to understand, maintain, scale system
- need experience to get it right
    - too granular or too broad can destroy the architecture
- could be defined by
    - business case
    - hierchy
    - domain separation
- inter-service communication is through some light weight protocol
    - REST over HTTP? really?
    - an organized way of doing that is through API Proxy (by configuring service communication)
    - or, by service mesh (like Istio)

### Frameworks
- Sidecar
- Ambassador
- Adapter

### Cons
- complex overall system
    - overhead of inter-service communication
    - automation to manage multiple small services
- careful planning, 
- skilled & experience human resource
- harder to achieve data consistency & transaction management
    - network calls
        - latency
            - can affect other service
    - individual DBs
- more security concerns
    - coz of more small public service/APIs
- multiple programing lang
    - double-edged sword

### Pros
- easy to develop, test, deploy
    - autonomous/independent
- increased agility
- ability to scale hosrizontally
- a way towards cloud-native model/approach

PS: Good but not required always.

## Serverless
- application running on a server managed by a 3rd party/cloud vendor etc
- are event-driven
- idea
    - deligate the server maintainance to 3rd party
        - reduce devops cost
        - server, db management/maintainance
        - application scalability
    - focus on feature dev/business logic only
- methods
    - FaaS
        - function as a service
        - a piece of code / fuctions runs on the vendor-managed server
    - BaaS
        - backend as a service
        - backend (db, storage, user authn service) managed by the vendor
        - only need to consume those in some app/code
    - MBaaS
        - Mobile-Backend as a service
        - functions for mobile applications
- vendors
    - AWS Lambda
    - Google Cloud Functions
    - Azure Functions
    - IBM OpenWhisk
    - Oracle Fn Project
    - Kubeless
    - ...

### Cons
- vendor lock-in
    - all things are stored there only
    - migration from one vendor to another could be challenging
- not for long-term tasks

### Pros
- easy to deploy
- lower cost
    - optimized infra cost by 3rd party
- enhanced scalability
    - automatic & seamless scaling managed by 3rd party
- better for client-heavy apps
- better for apps which need exponential/limitless scaling
    - really growing fast


## Cloud Native
- for applications planning to deploy in cloud
- applies to SOA & Microservices (and to monolithic & serverless as well)
- an approach to
    - deploy on public clouds (aws, gcp, azure, some one else's data center etc)
    - make services ready to be containerized
        - i.e. orchestration
    - thus ready for CI/CD
- services are usually stateless
- services communicates through HTTP or messaging queue
- envolves 
    - multiple node of the service
        - thus a centralized DB/session state/config server
    - CI/CD
    - API gateway
    - container registry
    - message-oriented middleware (MOM: publish/subscribe)
    - service mesh (like Istio)
    - orchestration (kubernetes/mesos)
- containerization
    - brings container orchestration
        - brings mesos, kubernetes

### Cons
- complexity
- experience

### Pros
- agility
- flexible
- resilient

## Cloud Based
- somewhere in between Cloud Enabled & Cloud Native
- running on cloud, vendor is auto scaling server/db, managing backups/log etc

## Cloud Enabled
- legacy monolithic apps, migrated to cloud
- depends on local services
- can't take advantage of shared services blah blah

# Microservices

A detailed view on this hot/major topic.

## Principles (https://dzone.com/articles/design-patterns-for-microservices)
A few principle microservice architecture follows are:

- Scalability
    - Availability
    - Resiliency/Fault-tolerant/Reliability
    - Consistency
- Maintainability
    - Independent, autonomous
    - Decentralized governance
    - Auto-Provisioning
    - Continuous delivery through DevOps
- Serviceability
    - Failure isolation
        - Failure detection
        - Recovery

## Patterns/Architecture (https://microservices.io/patterns/microservices.html)
- Domain-driven-design
- CQRS (command-query responsibity segragation)
- Event-driven
- Database per service
- Decomposition patterns
    - Decompose by business capability
    - Decompose by subdomain
- The Database per Service pattern describes how each service has its own database in order to ensure loose coupling.
- The API Gateway pattern defines how clients access the services in a microservice architecture.
- The Client-side Discovery and Server-side Discovery patterns are used to route requests for a client to an available service instance in a microservice architecture.
- The Messaging and Remote Procedure Invocation patterns are two different ways that services can communicate.
- The Single Service per Host and Multiple Services per Host patterns are two different deployment strategies.
- Cross-cutting concerns patterns: Microservice chassis pattern and Externalized configuration
- Testing patterns: Service Component Test and Service Integration Contract Test
- Circuit Breaker
- Access Token


## A few common properties of a service/software
### High Performance
### Low Latency
### High Throughput

# Trades-Off
## Scalability vs Performance

A detailed view on this hot/major topic.


Performance: 

1. about speed
1. capability of a service w.r.t its response time (how fast)
1. serving # of unit work over a period of time
1. how fast the service is if there is only 1 user (1 traffic only)

Scalability: 

1. about handling large load/traffic or doing large unit of work
1. capability of a service to perform directly proportional to the hardwares/resources added
1. increament in performance of the service when added more resources
1. service is fast for 1 user, but how fast the service is under heavy load (high traffic)

- scale up aka vertical scaling
    - increase server's power (cpu. ram, disk, network speed)
- scale out aka horizontal scaling
    - increase # of servers/instances

scalability gives
- availability
- resiliency/fault-tolerance/reliability
- performance/responsiveness
    - low latency
    - high throughput

## Latency vs Throughput
strive for high throughput with acceptable latency

## Availability vs Consistency
### CAP Theorem
In a distributed system (where there is a network partition) either of the only 2 choice is available.
- consistency
- or, availability

e.g. what NoSQL's BASE principle says: "basically available, soft state, eventually consistent"

# Scalability
## Availability
### Fail Over
A fall back mechanism

### Redundancy/Replication
kind
- active (push)
- passive (pull)

- Master Slave
- Master Master
- Tree Replication
- Buddy Replication

## Resiliency/Fault-tolerant/Reliability
## Consistency

## Other Patterns

# Maintainability
## Independent, autonomous
## Decentralized governance
## Auto-Provisioning
## Continuous delivery through DevOps

# Serviceability
## Failure isolation


There are various techniques/methods/patterns to achieve so:

## Load Balancing
- scalability
- availability

## Stateless application
- scalability
- consistency

## Loose coupling
## Asynchrony
## Lazy loading
## Caching
## Parallelism
## Partitioning / Sharding
## Routing
## Master Slave??



# Observability
## Log aggregation
## Application metrics
## Audit logging
## Distributed tracing
## Exception tracking
## Health check API
## Log deployments and changes


# Pratice Problems
- [Designing a URL Shortening service like TinyURL](https://www.educative.io/courses/grokking-the-system-design-interview/m2ygV4E81AR?affiliate_id=5073518643380224)
- [How do you design an Elevator of the Lift system?](https://dzone.com/articles/21-object-oriented-and-system-design-problems-to-p)
- [How do you design the Vending Machine in Java?](http://javarevisited.blogspot.sg/2016/06/design-vending-machine-in-java.html#axzz4sZVwtCgs)
- How to design an ATM machine?
- [Design a LRU Cache System](http://blog.gainlo.co/index.php/2016/05/17/design-a-cache-system/)
    - https://www.geeksforgeeks.org/lru-cache-implementation/
- Design & implement LFU cache
- Design phone book: search by name, phone number and print 10 most dialled numbers.
- Design a TODO list cloud application, multiple client support, millions of users, synchronize updates across multiple clients.
- Design an Authorization Service.
- [How would you design a Parking Lot system?](https://www.youtube.com/watch?v=eV5Xh6jNfmU&feature=emb_imp_woyt)
- How do you design a traffic control system?
- How do you design a website like Pastebin?
- How do you design an API Rate Limiter?
- How do you design a Search Engine?
- What is required to design a garbage collection system?
- [Design of Review Systems](https://medium.com/@pranavVersed/15-minute-product-design-challenge-1-rating-review-system-for-ecommerce-342293362efe)
- How do you design a recommendation system?
- How do you design a web crawler, and when should it be used?
- [How do you design a chat application like WhatsApp or Facebook Messenger?](https://click.linksynergy.com/deeplink?id=JVFxdTr9V80&mid=39197&murl=https%3A%2F%2Fwww.udemy.com%2Fcourse%2Fpreparing-for-system-design-interviews%2F)
- [How to design a global video streaming service like YouTube or NetFlix?](https://www.java67.com/2019/09/top-5-courses-to-learn-system-design.html)
- [How do you design global file sharing and storage apps like Google Drive or Dropbox?](https://www.youtube.com/watch?v=U0xTu6E2CT8&feature=emb_imp_woyt)
- how would you evaluate a software?
    - must fulfill basic requirements
    - cost
    - vendor / license / open-source
    - adoptability in team
        - brainstorm within team
    - maintainability
        - ease of use / document / customer-community support
        - modifiability as per special need
    - scalability
    - installation / setup

- system design
	- type
		- hld
			- high level problem solve 
		- lld
			- ludo
				- class design 
				- no other things

	- expectations
		- not expected to complete uber or whatsapp
		- hld: how many use cases you could think of
		- lld: build fault tolerant, scalable

	- by example
		- whatsapp
			- features
				- chat
				- call
				- group chat
				- group call
			- try define requirements at your own/ come up with requirement
				- I'll solve this things
				- confirm requirements first
				- then try start solving the problem
		- uber
			- come up with requirements

	- Q: 
		- how much time to define the requirements? -> 5 to 10 minutes
		- expected to code the same system design? -> No, very rare
		- approach to solve uber?
			- define req.
			- user should be able to see drivers
			- send request.
			- asked to include toll in the prices
		- SOLID principles? Most imp.
		- Design Patterns? Most imp.
		- how much to talk about lld vs hld? whatsapp? protocol? if you it--> it is a +ve point
		- 2-3yrs exp -> good lld, no system design; >=4 yrs -> both (some time they skip lld) hld->partitioning, sharding, replication, load-balancing, rolling upgrade, rolling logs, high scalability, high intensive system, horizontal vs vertical scaling
		- resources for preparation?
			- hld
				- start with core concept
		- how can play safe? 
			- you can lead the interview 
				- start with req.
				- if you know something, make interviewer ask those question
					- always start with high level components
					- same very wage, high level thing-> like say DB, don't say sql/nosql
				- practice many problems
				- prepare basic concepts
		- 3 imp point of sys design
			- partitioning
			- availability
			- sql/nosql; load balance
		- top 3 design patterns
			- interface segregation
			- compositions
			- SOLID
		- freshers?
			- only coding, os, dbms; no lld/hld-
		- discuss tech stack?
			- not imp, no brand name req.
			- only basic concept like quue, cache (not redis vs mem; kafka vs rabitmq)
		- how to handle opinion mis-match
			- say sql vs no-sql
				- back your decision
					- 1 million data, need horizontal partitioning etc.
				- use decision approach
				- don't be rigid with your decision
					- try to seek interviews feedback and try to mold your solution, try to incorporate
		- req.? who tells?
			- 75% we need to define and confirm
		- other skills to deveope? leadership, mgmnt? imp for higher position
		- how knowing big data helps sys-d interviews?
			- helps how to setup queue, high vol. db etc
		- when async, batch vs real-time?
		- learn paritionning in nosql
		- take examples of problems (to learn)
	- CP & DP
		- start writting recursive solution
			- then memoize it, but first need to be confortable in recurr
		- C++ STL, Java, Python
		- For working profs: Facebook hacker, Google Code Jam, Codechef lo.. etc.
		- 1 year, 2 prob each day is enough to be a good CP/DP
		- DS, Algo, OS, N/W, DBMS
		- Microsoft, Google, Amazon - CP, DS, Algo
		- Explain from Zero
		- Don't go blank in interview
		- 1st & 2nd year of college - CP

	- Ref:
		The course for LLD (Object Oriented Design & Design Patterns):
		https://practice.geeksforgeeks.org/co...

		The course for System Design:
		https://practice.geeksforgeeks.org/co...

		Our courses : 
		https://practice.geeksforgeeks.org/co...

		LinkedIn Profiles of the people in the video:

		Shashi Bhushan Kumar
		https://www.linkedin.com/in/shashi-bh...

		Udit Agarwal
		https://www.linkedin.com/in/anomaly2104/

		You can follow Udit's YouTube Channel for System Design videos:
		https://www.youtube.com/c/UditAgarwal21  


# Must Read
- [How to design a system to scale to first 100 million users](https://levelup.gitconnected.com/how-to-design-a-system-to-scale-to-your-first-100-million-users-4450a2f9703d)
- [System Design Primer](https://github.com/donnemartin/system-design-primer/blob/master/README.md)
- https://www.freecodecamp.org/news/systems-design-for-interviews/
