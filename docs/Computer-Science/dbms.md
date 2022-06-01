# DBMS

<h3>Table of Contents</h3>

[TOC]

# Basics

## Transaction
- represents any changes in database
- a unit of work performed in DBMS against a database
- independent of other transactions
- 2 Purposes:
    - provide reliability, can be recovered on failure
    - isolation from other programs accessing DB concurrently to avoid errors

## ACID

A set of properties of _relational_ database __transaction__.

- Atomicity: All or nothing.
- Consistency: One state to another valid state (according to rulesets, constraints defined).
- Isolation: Concurrency control. Execution of multiple concurrent transaction should have the same result as executed sequentially.
- Durability: Changes should persist (permanent is a big word :D).

### Rollback

### Cascade

## Keys
### Primary Key
* A primary is a single column value used to identify a database record uniquely.
* It has following attributes:
    * A primary key cannot be NULL
    * A primary key value must be unique
    * The primary key values cannot be changed
    * The primary key must be given a value when a new record is inserted.

Q. Which is better? Auto-incremental number vs UUID as primary key?

Auto-incremental number

- pros
    - good for internal use
    - small in size (say 8 bytes)
    - fast
    - easy to sort by
- cons
    - could reveal info/confidentiality
        - a user can guess ID of other
    - in long run, (i.e. very huge data, 10s of billions) integer takes more space than string

UUID

- pros
    - good for external use
    - unique not only across table, but accross company, or even world
    - does not reveal any info implicitly
        - hence more secure system
    - easier to merge data in sub-database/sub-table
- cons
    - relatively more space (say 16 bytes)
    - performace disaster for __very large tables__ (say more than 200K)
    - aer very random, so using them as unique/primary key (basically indexing) is inefficient on __very large tables__
    - cannot sort
    - could be adhoc (if we still need a number based unique key as well, say rollno, empid etc)
        - so space for index for uuid as well as for sequence
        - having both is waste

Ref:
- https://stackoverflow.com/questions/33274291/uuid-or-sequence-for-primary-key/33274393#33274393
- https://dba.stackexchange.com/questions/115766/should-i-use-uuid-as-well-as-id/119129
- http://compwron.github.io/2016/06/15/uuids-ids-and-primary-keys.html

#### UUID4
- UUID version 4
- 128 bits
- 122 for data/randomization (i.e. could have 122 random bits)
- 6 bits for identification of UUID version

#### How to generate a custom UUID?
- machine id (MAC?) + timestamp (nano) + process id + thread id + counter
- may keep a lookup cache of 1 second


### Composite Key
* A composite key is a primary key composed of multiple columns used to identify a record uniquely

### Foreign Key
* A key which is referring to a primary key of another table

### Candidate Key
* Candidate for the primary key. Means whichever combination of columns can uniquely identify a record are the candidate keys.

### Super Key
* Superset of all the candidate key. Means a set which contains all the columns from all the candidate keys.

### Dependencies
### Functional Dependency

### Partial Dependency

### Transitive Dependency

## Normalization
* A technique of organizing data in DB
* A systematic approach to decomposing tables to eliminate data redundancy & undesired characteristics like:
    * Insertion Anamolies
    * Update Anamolies
    * Deletion Anamolies
* Multi step process
* Normalization is used for mainly two purposes:
    * Eliminating redundant(useless) data.
    * Ensuring data dependencies make sense i.e data is logically stored.


**Note:** In most practical applications, normalization achieves its **best in 3rd Normal Form.**

### Anamolies
* Insertion Anamoly
    * Suppose for a new admission, we have a Student id, name, and address of a student but if the student has not opted for any subjects yet then we have to insert NULL there, leading to Insertion Anamoly.
* Update Anamoly
    * To update the address of a student who occurs twice or more than twice in a table, we will have to update S_Address column in all the rows, else data will become inconsistent.
* Deletion Anamoly
    * If a student has only one subject and temporarily he drops it. When we delete that row, entire student record will be deleted along with it.

### Types
#### 0 NF: Un Normalized Form
* Multi Valued Cells like Unit Code
<img src="https://s3.amazonaws.com/classmint.img/763744a3-c339-47bf-bb1c-e991287aaa39.gif">

#### 1 NF (E. F. Codd - 1971)
* First normal form enforces these criteria:
    * Eliminate repeating groups in individual tables.
    * Create a separate table for each set of related data.
    * Identify each set of related data with a primary/composite key
* Rules
    * **Atomic**  (i.e. indivisible) / single values in each cell. Means no set of values in a single cell.
    * Values stored in a column should be of the same domain
        * i.e. No repeating group/column/attribute. like Telephone 1, Telephone 2
    * All the columns in a table should have unique names.
    * No repeating rows/records. In other way:
        * For a set of values, create multiple rows/records for each individual values in the set.
        * Or, Identify each row/records by a primary key/composite primary key 
* Disadvantage:
    * Using the First Normal Form, data redundancy increases, as there will be many columns with same data in multiple rows but each row as a whole will be unique.

Table: 1-NF
<img src="https://s3.amazonaws.com/classmint.img/9405e335-04d7-45cf-ac32-5fe9b9a2fb99.gif">

Table: Still  in 1-NF
<img src="https://s3.amazonaws.com/classmint.img/01e58045-b38c-4237-8b8a-2fc93f962392.gif">

* **2 NF**
    * Be in 1 NF
    * There must not be a **Partial Dependency**
Table: 2-NF
<img src="https://s3.amazonaws.com/classmint.img/5e8d99a1-83b1-4834-9114-aca90629e0fc.gif">
* **3 NF**
* **BCNF**

# Index

- are used to quickly locate data without searching every row in the table

## Why 

## Type

## How

## Implementation

## Doubts/FAQs

- why not use hash table instead b-tree?
    - https://stackoverflow.com/questions/7306316/b-tree-vs-hash-table
    - https://www.quora.com/A-B-tree-index-is-better-than-a-hash-index-Why
    - https://dev.mysql.com/doc/refman/8.0/en/index-btree-hash.html
    - read sqlite code/doc as well
    - https://hakibenita.com/postgresql-hash-index
- how a really huge b-tree fits in RAM?
    - https://stackoverflow.com/questions/764221/larger-than-memory-data-structures-and-how-they-are-typically-handled
    - what is paging?
- primary key uses indexing by default?
    - Yes
- when not to use DB index?
    - when table is small
    - on columns on which majority of the values are null
    - on columns which are frequently manipulated
    - on columns which returns a high percentage of rows if use filter condition (like WHERE clause) on those
    - indexing could perform slow on tables which get frequent bulk updates

# SQL

Structured Query Language

(Please stop saying SEQUEL, i.e. Structured English QUEry Language, that was a trademark conflict)

### Stored Procedure & Function

Are schema level subprograms/program unit/commonly used codes, stored in database.


|               Procedure             |              Function                 |
|:------------------------------------|:--------------------------------------|
|Stored Procedures can call functions.|Functions cannot call stored Procedures.|
|Can have select statements as well as DML statements| Cannot use DML statements|
|Can use both table variables as well as temporary table in it.| Cannot use temp tables|
|Procedures cannot be utilized in a select statement| Function can be embedded in a select statement.|
|Procedure can return multiple OUT values(max. 1024)| Function returns 1 value only however it can be collection datatype|

### How to optimize a query? a SP? a Func?
### Cursor?  What? Why? How? When? Type?
### Trigger
### Jobs?
### Dynamic SQL?

### Generally Asked 
* second highest salary, query emp, dept, city
* import excel to table
* Employees with third highest salary @ address Pune? Tables: Employees, Address, Salary?
* delete vs drop vs truncate
