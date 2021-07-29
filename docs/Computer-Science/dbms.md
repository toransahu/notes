# DBMS

<h3>Table of Contents</h3>

[TOC]

# Basics

## ACID
* Atomicity: All or nothing
* Consistency: One state to another valid state (according to rulesets, constraints defined)
* Isolation: concurrency control. multiple transaction should sequentially executed
* Durability: Changes should persist

### Transaction
* a unit of work performed within a database management system
* independent of other transactions
* generally represents any change in a database
* 2 Purposes:
    * 1. provide reliability, can be recovered on failure
    * 2. isolation from other programs accessing DB concurrently to avoid errors

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

### Composite Key
* A composite key is a primary key composed of multiple columns used to identify a record uniquely

### Foreign Key
* A key which is refering to a primary key of another table

### Candidate Key
* Candidate for the primary key. Means Whichever combination of columns can uniquely identify a record are the candidate keys.

### Super Key
* Superset of all the candidate key. Means a set which contains all the columns from all the candidate keys.

### Dependencies
### Functional Dependency:

### Partial Dependency:

### Transitive Dependency:

## Normalization
### Intro
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

$$ Table: 1-NF $$
<img src="https://s3.amazonaws.com/classmint.img/9405e335-04d7-45cf-ac32-5fe9b9a2fb99.gif">

$$ Table: Still  in 1-NF $$
<img src="https://s3.amazonaws.com/classmint.img/01e58045-b38c-4237-8b8a-2fc93f962392.gif">

* **2 NF**
    * Be in 1 NF
    * There must not be a **Partial Dependency**
$$ Table: 2-NF $$
<img src="https://s3.amazonaws.com/classmint.img/5e8d99a1-83b1-4834-9114-aca90629e0fc.gif">
* **3 NF**
* **BCNF**


------------------------------------------

# ORACLE PL/SQL

## Introduction

## DB
* Consist of tablespace and tablespaces consists datafiles 

### Increase DB size?
* Increase size of data file
* Add new data file to existing table space
* Add new table space with atleast one datafile in it
* Datafile with dynamic extension 
```SQL
ALTER DATABASE DATAFILE <DATAFILE1.ORA> AUTOEXTEND ON NEXT 20M MAZSIZE 1000M;
```

### Tablespace & Datafiles??
* Oracle Database stores data logically in tablespaces
* and physically in datafiles associated with the corresponding tablespace.
* Oracle DB consist of at least two logical storage unit
* SYSTEM (Default created, either locally or dictionary managed)
* SYSAUX ( Auxiliary to SYSTEM) 
* TEMP (optional, required when SYSTEM is locally managed)
<img src="https://docs.oracle.com/cd/B28359_01/server.111/b28318/img/cncpt037.gif" >
* src: https://docs.oracle.com/cd/B28359_01/server.111/b28318/physical.htm#CNCPT401

### DB instance?
* db is collection datafiles on server. 
* DB instance is the allocated memory & collection of precesses running on the server when db server starts.
* db instances manages datafiles.
* db instance serves the data in datafiles to db users.

## Schema?
* organization of data as a blueprint of how the database is constructed (divided into database tables, packages, functions, views etc) i.e. schema objects.
* An Oracle database associates a separate schema with each database user
* schema objects includes: tables, views, sequences, synonyms, indexes, clusters, database links, snapshots, procedures, functions, packages
* non-schema objects: users, roles, contexts, directory objects

## Table, Temporary Tables, & View

* **Table:**
    * a preliminary storage for storing data and information in RDBMS
    * a collection of related data entries and it consists of columns and rows
    * Syntax: 
        ```SQL
        CREATE TABLE table_1 AS ( Col1 NUMBER);
        ```

* **View:**
    * It is a saved SELECT query.
    * It is a virtual table, which does not exist as stored data values in db (unless its indexed view)
    * **Advantages:**
        * It can join tables to create some complex statical query to use frequently
        * Does not takes extra space to store values
        * can be used as security mechanism: i.e. only read access, no edit access
    * Types:
        * View
        * Indexed View: 
            * Used to create index on view 
            * Only useful when view is created by joining various tables, otherwise no diff in a indexed view * table
            * Takes space same as tables
    * Syntax:
        ```SQL
        CREATE VIEW view_1 as SELECT statement;
        ```
        
* **Temporary Table:**
    * Oracle can create temp tables to store session specific or transaction specific data
    * data does not persists after session/transaction
    * definition persits? Yes
    * Syntax: ```SQL CREATE GLOBAL TEMPORARY TABLE table_1 (col1 VARCHAR2); ```
    * Clauses:
        * ON COMMIT PRESERVE ROWS: 
    * Used when: 
        * need to hold intermediate data
        * If the amount of data to be processed or utilized from your PL/SQL procedure is too large to fit comfortably in a PL/SQL table
    * Note: A TRUNCATE command issued in transaction/session specific temporary table truncates data in its own session/tranxn. Does not affect other session/trnxn.
    * What can be created on temporary tables:
        * Index
        * View
        * Triggers

## Clauses
* **FROM**
    
* **Where**
    - Optional part of SELECT, DELETE, ALTER, UPDATE
    - Where clause restricts/filters result of a SELECT, DELETE, ALTER, UPDATE queries
* **Having**
    * Having clause restricts/filters result of a "select query with GROUP BY" [1]
    * Applied to each groups of grouped table
    * If there is no GROUP BY clause then HAVING applies to whole table (table is treated as a single group)
    * The SELECT query cannot refer directly to any COLUMN not mentioned in GROUP BY clause, It can however refer to constants, aggregates. [2]
    * Aggregate in HAVING do not need to appear in SELECT
    * Subquery can be used in HAVING [3]
    * e.g. 
    ```SQL
    [1] SELECT emp_no, max(salary) m, min(salary) min_salary FROM salaries group by emp_no having m>70000;
    [2] SELECT emp_no, salary m FROM salaries  having m>70000;
    [3] SELECT emp_no, max(salary) m FROM salaries group by emp_no having m > (SELECT avg(salary) from  salaries);
    ```
* **ORDER BY**
    * To specify the order in which row should appear
    * Optional to use with SELECT, INSERT, CREATE VIEW
    * Meaningless in sub-queries
    * Order: DESC, ASC
    * Uses:
        * Using Correlation Name: 
        ```SQL 
        SELECT first_col AS f from tab_1 ORDER BY f;```
        * Using Column number
        ```SQL 
        SELECT emp_no, salary, addr  from tab_1 ORDER BY 1,2,3;```
        * Using function
        ```SQL 
        SELECT i, len from measure ORDER BY sin(i);```
        * Using NULL order
        ```SQL 
        SELECT i, len from measure ORDER BY NULLS LAST;```
        
* **GROUP BY**
    * Optional part of SELECT
    * The SELECT query cannot refer directly to any COLUMN not mentioned in GROUP BY clause, It can however refer to constants, aggregates.
    * Typically used with AGGREGATE functions
* **FOR UPDATE** 
    * Optional part of SELECT query
    * Syntax: SELECT A, B, C FROM T_1 FOR UPDATE
    * Use: In cursors to make them updatable.
* **WITH**
    * Materialization technique same as View & Temporary tables
    * known as subquery factoring
    * Useful when subqueries are used multiple times
    * e.g. 
    ```PLSQL
    WITH
        sum_sales AS 
          ( select sum(quantity) all_sales from stores ),
        number_stores AS 
          ( select count(*) nbr_stores from stores ),
        sales_by_store AS
          ( select store_name, sum(quantity) store_sales from store natural join sales )
    SELECT
       store_name
    FROM
       store,
       sum_sales,
       number_stores,
       sales_by_store
    where
       store_sales > (all_sales / nbr_stores);
       ```

* **USING**
    * Used in JOIN inplace of ON
    * e.g. 
    
    ```SQL
    SELECT * FROM COUNTRIES JOIN CITIES USING (COUNTRY);
    ```

    where COUNTRY column should exist in both the tables.
* **CONSTRAINT**
    * Optional part of CREATE/ ALTER table.
    * Level: 
        * Column level: Column-level constraints (except for check constraints) refer to only one column
        * Table level: Table constraints allow you to specify more than one column in a PRIMARY KEY, UNIQUE, CHECK, or FOREIGN KEY constraint definition
    * Types: 
        * NOT NULL: Column level, 
        * PRIMARY KEY: Both level, nameable
        * FOREIGN KEY: Both level, nameable 
        * CHECK: Both level, nameable, [DISABLE] keyword to disable
        * UNIQUE: Both level, nameable
    * e.g.:
    ```SQL
    CREATE TABLE suppliers
    (
      supplier_id numeric(4) NOT NULL CONSTRAINT unq_supplier_id UNIQUE,
      supplier_name varchar2(50) NOT NULL,
      CONSTRAINT check_supplier_name
      CHECK (supplier_name = upper(supplier_name)),
      CONSTRAINT pk_supplier_id PRIMARY KEY
    );
    ```
    
## Joins
* Used to combine & then retrieve data from multiple tables or views
* Types:
    * Equijoin: 
        * Joins 2 tables on the basis of equality of 2 columns
        
        ```PLSQL 
        SELECT A.col1, A.col2, B.col1, B.col2 FROM A, B where A.col3 = B.col4;```
    * Self Join
        * Join a table with itself with the help of alias
        
        ```PLSQL 
        SELECT A.col1, A.col2, B.col1, B.col2 FROM Salary AS A JOIN Salary AS B ON A.col3 = B.col4;```
    * Cartesian Product
        * Joins 2 tables without any condition
        
        ```PLSQL 
        SELECT A.col1, A.col2, B.col1, B.col2 FROM A, B;```
    * Inner Join (Join)
        * Simple join
        * Returns all rows that satisfy the join condition
        
        ```PLSQL 
        SELECT A.col1, A.col2, B.col1, B.col2 FROM A JOIN B on ON A.col3 = B.col4;```
    * Left Outer Join (Left Join)
        * Returns all rows that satisfy the join condition and also returns some or all of those rows from left table for which join condition didn't worked
        
        ```PLSQL 
        SELECT A.col1, A.col2, B.col1, B.col2 FROM A LEFT [OUTER] JOIN B ON A.col3 = B.col4;
        SELECT A.col1, A.col2, B.col1, B.col2 FROM A LEFT [OUTER]JOIN B WHERE A.col3(+) = B.col4;```
        
    * Right Outer Join (Right Join)
        * Returns all rows that satisfy the join condition and also returns some or all of those rows from right table for which join condition didn't worked
        
        ```PLSQL 
        SELECT A.col1, A.col2, B.col1, B.col2 FROM A RIGHT [OUTER] JOIN B ON A.col3 = B.col4;
        SELECT A.col1, A.col2, B.col1, B.col2 FROM A, B WHERE A.col3 = B.col4(+);```
        
    * Full Outer Join (Full Join)
        * Returns all rows that satisfy the join condition and also returns some or all of those rows from both the table for which join condition didn't worked 
        
        ```PLSQL 
        SELECT A.col1, A.col2, B.col1, B.col2 FROM A FULL JOIN B on ON A.col3 = B.col4;```
    * Anti Join
        * Returns rows from the table with does not exists in other table
        * Using NOT IN clause
        
        ```PLSQL 
        SELECT * FROM employees 
        WHERE department_id NOT IN 
        (SELECT department_id FROM departments 
           WHERE location_id = 1700)
        ORDER BY last_name;
        ```
        
    * Semi Join
        * Returns rows from table that satisfies EXISTS subquery condition
        
        ```PLSQL
        SELECT * FROM departments 
        WHERE EXISTS 
        (SELECT * FROM employees 
           WHERE departments.department_id = employees.department_id 
           AND employees.salary > 2500)
        ORDER BY department_name;
        ```
        
## Subprograms
* Subprograms are the building blocks of modular, maintainable applications.
* e.g. : Package, Procedure, Function

### Package
* A schema object that groups logically related PL/SQL types, variables, and subprograms
* Packages usually have two parts, 
    * a specification (spec): The specification is the interface to the package. It declares the types/collection types, variables, constants, exceptions, cursors, subprograms, and overloaded subprograms that can be referenced from outside the package.
    * a body: The body defines the queries for the cursors and the code for the subprograms.
    * Advantages:
        * Modularity
        * Easy application Design
        * Information Hiding: Public, Private
        * Better performance: The whole package gets loaded into memory after first call
    * Syntax:
        ```PLSQL
        CREATE PACKAGE emp_bonus AS
            TYPE EmpRecTyp IS RECORD (employees%ROWTYPE);
            PROCEDURE calc_bonus (date_hired employees.hire_date%TYPE);
            CURSOR desc_salary RETURN EmpRecTyp;
            FUNCTION hire_employee (last_name VARCHAR2, first_name VARCHAR2) 
                RETURN NUMBER;
        END emp_bonus;
        /
        
        CREATE PACKAGE BODY emp_bonus AS
            PROCEDURE calc_bonus (date_hired employees.hire_date%TYPE, salary NUMBER) IS
                BEGIN
                    DBMS_OUTPUT.PUT_LINE('Employees hired on ' || date_hired || ' get bonus.');
                    IF salary <= 0 THEN
                        RAISE invalid_salary EXCEPTION;
                    END IF;
                EXCEPTION 
                    WHEN invalid_salary THEN
                        DBMS_OUTPUT.PUT_LINE('Invalid salary input!');
                    WHEN Others THEN
                        RAISE;
                END;
            CURSOR desc_salary RETURN EmpRecTyp IS
                SELECT employee_id, salary FROM employees ORDER BY salary DESC;
                
            FUNCTION hire_employee (last_name VARCHAR2, first_name VARCHAR2) 
                RETURN NUMBER IS
                new_emp_id NUMBER;
                BEGIN
                    NULL;
                    RETURN new_emp_id;
                END hire_employee;
        END emp_bonus;
        /
```

### Stored Procedure & Function

* Schema level subprograms/program unit/ commonly used codes stored in database


|               Procedure             |              Function                 |
|:------------------------------------|:--------------------------------------|
|Stored Procedures can call functions.|Functions cannot call stored Procedures.|
|Can have select statements as well as DML statements| Cannot use DML statements|
|Can use both table variables as well as temporary table in it.| Cannot use temp tables|
|Procedures cannot be utilized in a select statement| Function can be embedded in a select statement.|
|Procedure can return multiple OUT values(max. 1024)| Function returns 1 value only however it can be collection datatype|

* Syntax
    * Procedure 
    
    ```PLSQL
    CREATE OR REPLACE PROCEDURE ADD_EVALUATION
    ( 
        evaluation_id IN NUMBER,
        employee_id IN NUMBER,
        evaluation_date IN DATE,
        job_id IN VARCHAR2,
        manager_id OUT NUMBER,
        department_id OUT NUMBER
    ) 
    AS
    BEGIN
        NULL;
    END ADD_EVALUATION;
    ```

    * Function
    
    ```PLSQL
    CREATE OR REPLACE FUNCTION calculate_score
        ( cat IN VARCHAR2
        , score IN NUMBER
        , weight IN NUMBER
        ) RETURN NUMBER 
    AS
    BEGIN
        RETURN NULL;
    END calculate_score;
    ```
    
### In-Built Functions

### Aggregation Functions
Max, Min, Count, Sum

### Analytical Functions
Top? Last? Rank? 

### Window Function
over()

###  LAG/LEAD Functions


### How to optimize a query? a SP? a Func?
### Index? Why? Type? How/Implementation?
### Cursor?  What? Why? How? When? Type?
### Trigger
### Jobs?
### Dynamic SQL?

### Generally Asked 
* second highest salary, query emp, dept, city
* import excel to table
* Employees with third highest salary @ address Pune? Tables: Employees, Address, Salary?
* delete vs drop vs truncate


# MySQL

## Install

```
sudo apt install mysql-server
```

## Run

```
sudo mysql -u root -p  #default password for root is "password"
```

if you get :

```
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2)
```

then check 

```
service mysql start
```

Default password for root is: **password**

## Help
```
mysql> help;

or

\h
```

### chage root password

```
sudo mysqladmin password <new password>
```

## Database
### Install test_db
- sakila
- employees
- source: https://github.com/toransahu/test_db


### Install `Sakila` db prepared by mysql
```
wget http://downloads.mysql.com/docs/sakila-db.tar.gz
tar -xzf sakila-db.tar.gz
cd sakila-db
mysql -u root -p < sakila-schema.sql
mysql -u root -p < sakila-data.sql
```

### GRANTS

```sql
GRANT ALL PRIVILEGES ON *.* TO 'username'@'localhost' IDENTIFIED BY 'password';
```

### To see databases
```
mysql> show databases;
```

### To create a database
```
mysql> create database <db_name>;

Query OK, 1 row affected (0.00 sec)
```

### To use a database

```
mysql> use <db_name>;
```

## Tables

### To see tables
```
show tables;
```

## Subprograms

### Aggregation Functions


### Analytical Functions
- MySQL doesn't have Analytical Functions
    - while it is in
        - MSSQL
        - Oracle
        - PostgreSQL
        - MariaDB
        
### Window Function
over()

# PostgreSQL

Simple Doc: https://medium.com/coding-blocks/creating-user-database-and-adding-access-on-postgresql-8bfcd2f4a91e

## Introduction
Relational database management systems are a key component of many web sites and applications. They provide a structured way to store, organize, and access information.

PostgreSQL, or Postgres, is a relational database management system that provides an implementation of the SQL querying language. It is a popular choice for many small and large projects and has the advantage of being standards-compliant and having many advanced features like reliable transactions and concurrency without read locks.

In this guide, we will demonstrate how to install Postgres on an Ubuntu 16.04 VPS instance and go over some basic ways to use it.

## Installation
Ubuntu's default repositories contain Postgres packages, so we can install these easily using the apt packaging system.

Since this is our first time using apt in this session, we need to refresh our local package index. We can then install the Postgres package and a -contrib package that adds some additional utilities and functionality:

```
sudo apt-get update
sudo apt-get install postgresql postgresql-contrib
```

Now that our software is installed, we can go over how it works and how it may be different from similar database management systems you may have used.

## Using PostgreSQL Roles and Databases
By default, Postgres uses a concept called "roles" to handle in authentication and authorization. These are, in some ways, similar to regular Unix-style accounts, but Postgres does not distinguish between users and groups and instead prefers the more flexible term "role".

Upon installation Postgres is set up to use ident authentication, which means that it associates Postgres roles with a matching Unix/Linux system account. If a role exists within Postgres, a Unix/Linux username with the same name will be able to sign in as that role.

There are a few ways to utilize this account to access Postgres.

### Switching Over to the postgres Account
The installation procedure created a user account called postgres that is associated with the default Postgres role. In order to use Postgres, we can log into that account.

Switch over to the postgres account on your server by typing:

```
sudo -i -u postgres
```

You can now access a Postgres prompt immediately by typing:

```
psql
```

You will be logged in and able to interact with the database management system right away.

Exit out of the PostgreSQL prompt by typing:

```
\q
```

You should now be back in the postgres Linux command prompt.

### Accessing a Postgres Prompt Without Switching Accounts
You can also run the command you'd like with the postgres account directly with sudo.

For instance, in the last example, we just wanted to get to a Postgres prompt. We could do this in one step by running the single command psql as the postgres user with sudo like this:
```
sudo -u postgres psql
```

This will log you directly into Postgres without the intermediary bash shell in between.

Again, you can exit the interactive Postgres session by typing:

```
\q
```

## Create a New Role
Currently, we just have the postgres role configured within the database. We can create new roles from the command line with the createrole command. The --interactive flag will prompt you for the necessary values.

If you are logged in as the postgres account, you can create a new user by typing:

```
createuser --interactive
```

If, instead, you prefer to use sudo for each command without switching from your normal account, you can type:

sudo -u postgres createuser --interactive
The script will prompt you with some choices and, based on your responses, execute the correct Postgres commands to create a user to your specifications.

Output

```
Enter name of role to add: sammy
Shall the new role be a superuser? (y/n) y
```

You can get more control by passing some additional flags. Check out the options by looking at the man page:

```
man createuser
```

## Create a New Database
By default, another assumption that the Postgres authentication system makes is that there will be an database with the same name as the role being used to login, which the role has access to.

So if in the last section, we created a user called sammy, that role will attempt to connect to a database which is also called sammy by default. You can create the appropriate database with the createdb command.

If you are logged in as the postgres account, you would type something like:

createdb sammy
If, instead, you prefer to use sudo for each command without switching from your normal account, you would type:

sudo -u postgres createdb sammy
Open a Postgres Prompt with the New Role
To log in with ident based authentication, you'll need a Linux user with the same name as your Postgres role and database.

If you don't have a matching Linux user available, you can create one with the adduser command. You will have to do this from an account with sudo privileges (not logged in as the postgres user):

sudo adduser sammy
Once you have the appropriate account available, you can either switch over and connect to the database by typing:

sudo -i -u sammy
psql
Or, you can do this inline:

sudo -u sammy psql
You will be logged in automatically assuming that all of the components have been properly configured.

If you want your user to connect to a different database, you can do so by specifying the database like this:

psql -d postgres
Once logged in, you can get check your current connection information by typing:

\conninfo
Output
You are connected to database "sammy" as user "sammy" via socket in "/var/run/postgresql" at port "5432".
This can be useful if you are connecting to non-default databases or with non-default users.

Create and Delete Tables
Now that you know how to connect to the PostgreSQL database system, we can to go over how to complete some basic tasks.

First, we can create a table to store some data. Let's create a table that describes playground equipment.

The basic syntax for this command is something like this:

CREATE TABLE table_name (
    column_name1 col_type (field_length) column_constraints,
    column_name2 col_type (field_length),
    column_name3 col_type (field_length)
);
As you can see, we give the table a name, and then define the columns that we want, as well as the column type and the max length of the field data. We can also optionally add table constraints for each column.

You can learn more about how to create and manage tables in Postgres here.

For our purposes, we're going to create a simple table like this:

CREATE TABLE playground (
    equip_id serial PRIMARY KEY,
    type varchar (50) NOT NULL,
    color varchar (25) NOT NULL,
    location varchar(25) check (location in ('north', 'south', 'west', 'east', 'northeast', 'southeast', 'southwest', 'northwest')),
    install_date date
);
We have made a playground table that inventories the equipment that we have. This starts with an equipment ID, which is of the serial type. This data type is an auto-incrementing integer. We have given this column the constraint of primary key which means that the values must be unique and not null.

For two of our columns (equip_id and install_date), we have not given a field length. This is because some column types don't require a set length because the length is implied by the type.

We then give columns for the equipment type and color, each of which cannot be empty. We create a location column and create a constraint that requires the value to be one of eight possible values. The last column is a date column that records the date that we installed the equipment.

We can see our new table by typing:

\d
Output
                  List of relations
 Schema |          Name           |   Type   | Owner 
--------+-------------------------+----------+-------
 public | playground              | table    | sammy
 public | playground_equip_id_seq | sequence | sammy
(2 rows)
Our playground table is here, but we also have something called playground_equip_id_seq that is of the type sequence. This is a representation of the serial type we gave our equip_id column. This keeps track of the next number in the sequence and is created automatically for columns of this type.

If you want to see just the table without the sequence, you can type:

\dt
Output
          List of relations
 Schema |    Name    | Type  | Owner 
--------+------------+-------+-------
 public | playground | table | sammy
(1 row)
Add, Query, and Delete Data in a Table
Now that we have a table, we can insert some data into it.

Let's add a slide and a swing. We do this by calling the table we're wanting to add to, naming the columns and then providing data for each column. Our slide and swing could be added like this:

INSERT INTO playground (type, color, location, install_date) VALUES ('slide', 'blue', 'south', '2014-04-28');
INSERT INTO playground (type, color, location, install_date) VALUES ('swing', 'yellow', 'northwest', '2010-08-16');
You should take care when entering the data to avoid a few common hangups. First, keep in mind that the column names should not be quoted, but the column values that you're entering do need quotes.

Another thing to keep in mind is that we do not enter a value for the equip_id column. This is because this is auto-generated whenever a new row in the table is created.

We can then get back the information we've added by typing:

SELECT * FROM playground;
Output
 equip_id | type  | color  | location  | install_date 
----------+-------+--------+-----------+--------------
        1 | slide | blue   | south     | 2014-04-28
        2 | swing | yellow | northwest | 2010-08-16
(2 rows)
Here, you can see that our equip_id has been filled in successfully and that all of our other data has been organized correctly.

If the slide on the playground breaks and we have to remove it, we can also remove the row from our table by typing:

DELETE FROM playground WHERE type = 'slide';
If we query our table again, we will see our slide is no longer a part of the table:

SELECT * FROM playground;
Output
 equip_id | type  | color  | location  | install_date 
----------+-------+--------+-----------+--------------
        2 | swing | yellow | northwest | 2010-08-16
(1 row)
How To Add and Delete Columns from a Table
If we want to modify a table after it has been created to add an additional column, we can do that easily.

We can add a column to show the last maintenance visit for each piece of equipment by typing:

ALTER TABLE playground ADD last_maint date;
If you view your table information again, you will see the new column has been added (but no data has been entered):

SELECT * FROM playground;
Output
 equip_id | type  | color  | location  | install_date | last_maint 
----------+-------+--------+-----------+--------------+------------
        2 | swing | yellow | northwest | 2010-08-16   | 
(1 row)
We can delete a column just as easily. If we find that our work crew uses a separate tool to keep track of maintenance history, we can get rid of the column here by typing:

ALTER TABLE playground DROP last_maint;
How To Update Data in a Table
We know how to add records to a table and how to delete them, but we haven't covered how to modify existing entries yet.

You can update the values of an existing entry by querying for the record you want and setting the column to the value you wish to use. We can query for the "swing" record (this will match every swing in our table) and change its color to "red". This could be useful if we gave the swing set a paint job:

UPDATE playground SET color = 'red' WHERE type = 'swing';
We can verify that the operation was successful by querying our data again:

SELECT * FROM playground;
Output
 equip_id | type  | color | location  | install_date 
----------+-------+-------+-----------+--------------
        2 | swing | red   | northwest | 2010-08-16
(1 row)
As you can see, our slide is now registered as being red.

[Source](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-16-04)



