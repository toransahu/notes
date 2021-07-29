# System Design

[TOC]

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
		- why want to change the job?
			- location
			- e-commerce
			- what is left in your current job?
				- not getting good project in LAST 1 YEAR
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
