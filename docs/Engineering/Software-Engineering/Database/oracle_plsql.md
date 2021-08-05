# Oracle DB (PL/SQL)

<h3>Table of Contents</h3>
[TOC]

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
    * Syntax:
        ```sql
        CREATE GLOBAL TEMPORARY TABLE table_1 (col1 VARCHAR2);
        ```
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
            SELECT first_col AS f from tab_1 ORDER BY f;
            ```
        * Using Column number
            ```SQL
            SELECT emp_no, salary, addr  from tab_1 ORDER BY 1,2,3;
            ```
        * Using function
            ```SQL
            SELECT i, len from measure ORDER BY sin(i);
            ```
        * Using NULL order
            ```SQL
            SELECT i, len from measure ORDER BY NULLS LAST;
            ```
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
        ```SQL
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
            ```SQL
            SELECT A.col1, A.col2, B.col1, B.col2 FROM A, B where A.col3 = B.col4;
            ```
    * Self Join
        * Join a table with itself with the help of alias
            ```SQL
            SELECT A.col1, A.col2, B.col1, B.col2 FROM Salary AS A JOIN Salary AS B ON A.col3 = B.col4;
            ```
    * Cartesian Product
        * Joins 2 tables without any condition
            ```SQL
            SELECT A.col1, A.col2, B.col1, B.col2 FROM A, B;
            ```
    * Inner Join (Join)
        * Simple join
        * Returns all rows that satisfy the join condition
            ```SQL
            SELECT A.col1, A.col2, B.col1, B.col2 FROM A JOIN B on ON A.col3 = B.col4;
            ```
    * Left Outer Join (Left Join)
        * Returns all rows that satisfy the join condition and also returns some or all of those rows from left table for which join condition didn't worked
            ```SQL
            SELECT A.col1, A.col2, B.col1, B.col2 FROM A LEFT [OUTER] JOIN B ON A.col3 = B.col4;
            SELECT A.col1, A.col2, B.col1, B.col2 FROM A LEFT [OUTER]JOIN B WHERE A.col3(+) = B.col4;
            ```
    * Right Outer Join (Right Join)
        * Returns all rows that satisfy the join condition and also returns some or all of those rows from right table for which join condition didn't worked
        ```SQL
        SELECT A.col1, A.col2, B.col1, B.col2 FROM A RIGHT [OUTER] JOIN B ON A.col3 = B.col4;
        SELECT A.col1, A.col2, B.col1, B.col2 FROM A, B WHERE A.col3 = B.col4(+);
        ```
    * Full Outer Join (Full Join)
        * Returns all rows that satisfy the join condition and also returns some or all of those rows from both the table for which join condition didn't worked
        ```SQL
        SELECT A.col1, A.col2, B.col1, B.col2 FROM A FULL JOIN B on ON A.col3 = B.col4;
        ```
    * Anti Join
        * Returns rows from the table with does not exists in other table
        * Using NOT IN clause
        ```SQL
        SELECT * FROM employees
        WHERE department_id NOT IN
        (SELECT department_id FROM departments
           WHERE location_id = 1700)
        ORDER BY last_name;
        ```
    * Semi Join
        * Returns rows from table that satisfies EXISTS subquery condition
        ```SQL
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
        ```SQL
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
    ```SQL
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
    ```SQL
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

### LAG/LEAD Functions
