# SQL note

NhanNguyen

some little note by myself to remind what did i learn

---

## Things worth to review:

| No. | Content                                   |
| --- | ----------------------------------------- |
|     |                                           |
| 1   | [SQL, Database - Basic](#sql-database-basic) |
| 1   | [Datatype](#sql-database-basic) |

# SQL, Database - Basic

SQL is a language we use to talk to our database

SQL Server is a database server, this store all of our data, table, stored procedure

MySQL, SSMS is a Database Management System - underthe hood we use SQL language to interact with database

```What is database?```

Database is a collection of data and Database is a method to accessing and manipulating our data

=> When talk about Database we talk about DBMS and Database

```Database is just a bunch of tables```

```
CREATE DATABASE <name>;
show databases;
DROP DATABASE <name>;
SELECT databse();
```

<img src="./img/1.png" width="500">

---
---

```SQL CONVENTION```

..* Uppercase in SQL is not a must
=> It just because people want to separate sql syntax and variable

..* Table name must be in plural

..* Stored procedure should be start with sp not _sp because people want to seperate system procedure with our procedure

..* String in SQL is case insensitive

..* Make sure you select right after delete or update

