# SQL note

NhanNguyen

some little note by myself to remind what did i learn

---

## Things worth to review:

| No. | Content                                   |
| --- | ----------------------------------------- |
|     |                                           |
| 1   | [Basic](#basic) |
| 2   | [Datatype](#```SQL```-```Database```-basic) |
| 3   | [String Function](#string-function) |
| 4   | [Selection](#selection) |
| 5   | [Where clause and Logical operator](#logical-perator) |
| 6   | [Relationship and join](#Relationship-and-join) |
| 7   | [Stored Procedure](#stored-procedure) |

# SQL, Database - Basic

```SQL``` is a language we use to talk to our ```Database```

```SQL``` Server is a ```Database``` server, this store all of our data, ```Table```, stored procedure

My```SQL```, SSMS is a ```Database``` Management System - underthe hood we use ```SQL``` language to interact with ```Database```

```What is Database?```

```Database``` is a collection of data and ```Database``` is a method to accessing and manipulating our data

=> When talk about ```Database``` we talk about DBMS and ```Database```

=> ```Database``` is just a bunch of ```Table```s

```
CREATE Database <name>;
show Databases;
DROP Database <name>;
SELECT databse();
```

<img src="./img/1.png" width="500">

## SQL CONVENTION

* Uppercase in ```SQL``` is not a must
=> It just because people want to separate ```SQL``` syntax and variable

* ```Table``` name must be in plural

* ```Stored procedure``` should be start with sp not _sp because people want to seperate system procedure with our user defined procedure

* String in ```SQL``` is case insensitive

* Make sure you select right after delete or update

## Namespace of a database

```
Use [name of Database]
Go
```

=> It will do the query based on this Database, and change our environment to this namespace

## Creating and Altering Database/```Table```

Creat Database/```Table``` <Database/```Table``` Name>: To Create

Alter Database/```Table``` <Database/```Table``` Name>: To Modify

Drop Database/```Table``` <Database/```Table``` Name>: To Drop

> It is important to note that we cant delete/drop databse is currently in use, because other developer is quering to this database. It will th```row``` to us an error

> If we really want to drop a database we must set Database to single user with rollback immediate -> It mean disconnect the database with other user and only accessalbe with one user only

<img src="./img/7.PNG" width="500">

## Table

We have to change the namespace of database where we want to create ```Table```, unless our ```Table``` will create some where not we want

### Foreign key and Primary key constraint

We have to specifty this constraint to restrict foreign key in one ```Table``` is not match primary key in another ```Table``` => Establist the relationship between two ```Table```

To add a foreign key reference using a query

    Alter ```Table``` tblPerson 
    add constraint tblPerson_GenderId_FK FOREIGN KEY (GenderId) references tblGender(ID)


The general formula is here

    Alter ```Table``` ForeignKey```Table``` add constraint ForeignKey```Table```_ForiegnKeyColumn_FK 
    FOREIGN KEY (ForiegnKeyColumn) references PrimaryKey```Table``` (PrimaryKeyColumn)

### Default constraint - Default value for column

Altering an existing column to add a default constraint:

    ALTER Table { Table_NAME }
    ADD CONSTRAINT { CONSTRAINT_NAME }
    DEFAULT { DEFAULT_VALUE } FOR { EXISTING_COLUMN_NAME }


Adding a new column, with default value, to an existing ```Table```:

    ALTER Table { Table_NAME } 
    ADD { COLUMN_NAME } { DATA_TYPE } { NULL | NOT NULL } 
    CONSTRAINT { CONSTRAINT_NAME } DEFAULT { DEFAULT_VALUE }


The following command will add a default constraint, DF_tblPerson_GenderId.

    ALTER Table tblPerson
    ADD CONSTRAINT DF_tblPerson_GenderId
    DEFAULT 1 FOR GenderId

<img src="./img/8.PNG" width="500">

[Cascading referential integrity constraint](https://www.youtube.com/watch?v=ETepOVi7Xk8&list=PL08903FB7ACA1C2FB&index=6)

### Check Constraint

To check a columns before it was insert into our database

The following check constraint, limits the age between ZERO and 150.

    ALTER TABLE tblPerson
    ADD CONSTRAINT CK_tblPerson_Age CHECK (Age > 0 AND Age < 150)


The general formula for adding check constraint in SQL Server:

    ALTER TABLE { TABLE_NAME }
    ADD CONSTRAINT { CONSTRAINT_NAME } CHECK ( BOOLEAN_EXPRESSION )

* ```CK_```: is a convention to prefix of constraint

If the BOOLEAN_EXPRESSION returns true, then the CHECK constraint allows the value, otherwise it doesn't. Since, AGE is a nullable column, it's possible to pass null for this column, when inserting a row. When you pass NULL for the AGE column, the boolean expression evaluates to UNKNOWN, and allows the value.


To drop the CHECK constraint:

    ALTER TABLE tblPerson
    DROP CONSTRAINT CK_tblPerson_Age

# Datatype

Column (header) in ```Table``` must be consisten type (```SQL``` force you to do it) because only if these have the same type - you can use ```SQL``` language to query them 

1. Storing text

    * Char: fixed length - if it longer -> automatically reduce (it will auto fill if it not enough charactor

    * Varchar: not fill automatically

2. Decimal number

    * Decimal: Decimal(n,d) -> very precis

    * Float, Double: store gain number -> not percise

    * => Better using Decimal

3. Others

    * Date - CURDATE(): only date YYYY-MM-DD

    * Time - CURTIME(): only ti#me HH:MM:SS

    * DateTime - NOW(): YYYY-MM-DD HH:MM:SS

4. Formatting Date

    * DAY(DateTime) - get day

    * DAYNAME(DateTime) - get day name (mon, tues…)

    * DAYOFWEEK(DateTime)  - get number of day in week

    * DAYOFYEAR(DateTime) - get number of day in year

5. Date Math

    * DATEDIFF(NOW(), date)

6. TiMESTAMP

    * TimeStamp is a term refer to the time user insert some thing or the time of the ```row``` be created

    * It take up less space than DateTime

# String function

* CONCAT
* SUBSTRING
* REPLACE
* REVERSE
* CHARLENGTH
* UPPER 
* LOWER


# Selection

* Select all: *
* DISTINCT + STRING FUNCTION
* ORDER BY - ORDER BY <number> - ORDER BY DESC - ORDER BY author_lname, author_fname - ORDER BY + TOP 
* LIMIT - LIMIT + ORDER BY 
* TOP - TOP + ORDER BY
    - SELECT * FROM books ORDER BY stock_quantity DESC OFFSET 0 ```row```S FETCH NEXT 10 ```row```S ONLY;
* LIKE - better searching data

# Logical Operator

WHERE + LOGICAL OPERATOR

* ````Equal: ````=
* ````Not Equal:```` !=
* ````Greater than:```` >
* ````Smaller than:```` <
* ````Between: ```` <column> BETWEEN … IN
* ````Not between:```` <column> NOT BETWEEN … IN
* ````IN: ````<column> IN (value1, value2,… valueN)
* ````NOT IN:```` <column> NOT IN (value1, value2,… valueN)
* ````CASE - ````WHEN - THEN - ELSE - END : Case staments
* ````IFNULL: ````IFNULL(<checkedValue>, relacedValue)

=> When use logical operator with datetime => It is best CAST(value AS DATETIME)  to convert to the same type

=> Cast('2021-10-28' as DATETIME)

<img src="./img/2.png" width="500">


# Relationship and join

## Basic

* One to one

* One to many

* Many to many

Why we need a relationship between two ```Table```?

=> It make easier to work with single ```Table``` for single purpose

=> It reduce null value in many column

<img src="./img/3.png" width="600">

=> Best idea to seperate to many ```Table``` and make relationship between them

## Primary key and Foreign Key

1. Primary key: is the unique ID of one ```Table```, it guarantee this ```record``` /this ```row``` to be unique
	
    * The MS ```SQL``` Server uses the IDENTITY keyword to perform an auto-increment feature.
		
    * In the example above, the starting value for IDENTITY is 1, and it will increment by 1 for each new ```record```.

    * Tip: To specify that the "Personid" column should start at value 10 and increment by 5, change it to IDENTITY(10,5).
		
    * From <https://stackoverflow.com/questions/10991894/auto-increment-primary-key-in-```SQL```-server-management-studio-2012> 
		
2. Foreign key: is the key reference to other ```Table```. Foreign key not require to be unique
	
## ```Database``` schema

The ```Database``` schema is its structure described in a formal language supported by the ```Database``` management system (DBMS). The term "schema" refers to the organization of data as a blueprint of how the ```Database``` is constructed (divided into ```Database``` ```Table```s in the case of relational ```Database```s). 

- From <https://en.wikipedia.org/wiki/```Database```_schema> 

A ```Database``` schema is an abstract design that represents the storage of your data in a ```Database```. It describes both the organization of data and the relationships between ```Table```s in a given ```Database```. Developers plan a ```Database``` schema in advance so they know what components are necessary and how they will connect to each other.

- From <https://www.educative.io/blog/what-are-```Database```-schemas-examples> 

## One to many

Config: 

		CREATE ```Table``` customers (
			id INT IDENTITY(1,1) PRIMARY KEY,
			first_name VARCHAR(100),
			last_name VARCHAR(100),
			email VARCHAR(100),
		)
		
		CREATE ```Table``` orders (
			id INT IDENTITY(1,1) PRIMARY KEY,
			order_date DATE,
			amount DECIMAL(8,2),
			customer_id INT,
			FOREIGN KEY (customer_id) REFERENCES customers(id)
		)

<img src="./img/4.png" width="600">

## Inner Join


=> Join two ```Table``` and take ```record``` from that ```Table``` where condition is met

> https://dataschool.com/how-to-teach-people-```SQL```/inner-join-animated/

<img src="./img/5.png" width="600">

## Left Join 

=> Take right ```Table``` and join with the left ```Table``` where the condition is met

> https://dataschool.com/how-to-teach-people-```SQL```/left-right-join-animated/

<img src="./img/6.png" width="600">

# Stored Procedure

- This is a way to store/wrap a query code, help you avoid to write the same query again and again.
	
- This ```stored procedure``` is already compiled and it will run the query logic inside ```stored procedure``` when we excecute this ```stored procedure```.

- ```Stored Procedure``` is stored in our ```Database``` and it already excecuted

- Benefit:
    - Security
    - Network traffic

> on nocount 

=> Mean we specify we dont want to count how many ```row``` is effected

