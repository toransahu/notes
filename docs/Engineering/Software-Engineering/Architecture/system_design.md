# System Design

<h3>Table of Contents</h3>
[TOC]

# Pratice Problems
- [Designing a URL Shortening service like TinyURL](https://www.educative.io/courses/grokking-the-system-design-interview/m2ygV4E81AR?affiliate_id=5073518643380224)
- [How do you design an Elevator of the Lift system?](https://dzone.com/articles/21-object-oriented-and-system-design-problems-to-p)
- [How do you design the Vending Machine in Java?](http://javarevisited.blogspot.sg/2016/06/design-vending-machine-in-java.html#axzz4sZVwtCgs)
- How to design an ATM machine?
- [Design a LRU Cache System](http://blog.gainlo.co/index.php/2016/05/17/design-a-cache-system/)
    - https://www.geeksforgeeks.org/lru-cache-implementation/
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