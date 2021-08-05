# MySQL

<h3>Table of Contents</h3>
[TOC]


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
