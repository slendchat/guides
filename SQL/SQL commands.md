# Basic commands
- `SELECT` - **extracts** data from a database
- `UPDATE` - **updates** data in a database
  Syntax:
```
	UPDATE table_name
	SET column1 = value1, column2 = value2, ...
	WHERE condition;
```

- `DELETE` - **deletes** data from a database
  Syntax:
```
DELETE FROM table_name WHERE condition;
```

- `INSERT INTO` - **inserts** new data into a database
 Syntax:
```
	INSERT INTO table_name
	VALUES (value1, value2, value3, ...);
```
 
- `CREATE DATABASE` - **creates** a new database
- `ALTER DATABASE` - **modifies** a database
- `CREATE TABLE` - **creates** a new table
- `ALTER TABLE` - **modifies** a table
- `DROP TABLE` - **deletes** a table
- `CREATE INDEX` - **creates** an index (search key)
- `DROP INDEX` - **deletes** an index
- `SELECT DISTINCT` statement is used to return only distinct (different) values.
- `WHERE` clause is used to filter records. (WHERE Country='Mexico';)
- `ORDER BY` keyword is used to sort the result-set in ascending or descending order.
  Syntax:
```
	SELECT _column1_, _column2, ...
	FROM table_name   
	ORDER BY _column1, column2, ... ASC|DESC;
```
 
 - The `WHERE` clause can contain one or many `AND` operators.
 - The `WHERE` clause can contain one or more `OR` operators.
 - The `NOT` operator is used in combination with other operators to give the opposite result, also called the negative result.
   Syntax:
```
	SELECT _column1_, _column2, ...
	FROM table_name   
	WHERE NOT condition;
```

 -  The `IS NULL` and `IS NOT NULL` operators
   Syntax:
```
	SELECT column_names
	FROM table_name
	WHERE column_name IS NULL;
```

 - The `SELECT TOP` clause is used to specify the number of records to return.
   Syntax:
```
	SELECT TOP 3 * FROM Customers;
```

The most commonly used SQL aggregate functions are:
- `MIN()` - returns the smallest value within the selected column
- `MAX()` - returns the largest value within the selected column
- `COUNT()` - returns the number of rows in a set
- `SUM()` - returns the total sum of a numerical column
- `AVG()` - returns the average value of a numerical column
Syntax:
```
	SELECT MAX(Price)
	FROM Products;
```

The `LIKE` operator is used in a `WHERE` clause to search for a specified pattern in a column.
There are two wildcards often used in conjunction with the `LIKE` operator:
-  The percent sign `%` represents zero, one, or multiple characters
-  The underscore sign `_` represents one, single character

| Symbol | Description                                                  |
| ------ | ------------------------------------------------------------ |
| %      | Represents zero or more characters                           |
| _      | Represents a single character                                |
| []     | Represents any single character within the brackets *        |
| ^      | Represents any character not in the brackets *               |
| -      | Represents any single character within the specified range * |
| {}     | Represents any escaped character **                          |

 - * Not supported in PostgreSQL and MySQL databases.
 - ** Supported only in Oracle databases.

Syntax:
```
	SELECT _column1, column2, ..._  
	FROM _table_name_  
	WHERE _columnN_ LIKE _pattern_;
```

 - The `IN` operator allows you to specify multiple values in a `WHERE` clause.
   The `IN` operator is a shorthand for multiple `OR` conditions.
   Syntax:
```
	SELECT _column_name(s)_  
	FROM _table_name_  
	WHERE _column_name_ IN (_value1_, _value2_, ...);
```

 - The `BETWEEN` operator selects values within a given range. The values can be numbers, text, or dates. The `BETWEEN` operator is inclusive: begin and end values are included.
   Example:
```
	SELECT * FROM Products
	WHERE Price BETWEEN 10 AND 20;
```


# SQL Aliases
SQL aliases are used to give a table, or a column in a table, a temporary name.
An alias is created with the `AS` keyword.
Example:
```
SELECT CustomerID AS ID  
FROM Customers;
```

Actually, in most database languages, you can skip the AS keyword and get the same result:
```
SELECT CustomerID ID  
FROM Customers;
```


# SQL Joins
A `JOIN` clause is used to combine rows from two or more tables, based on a related column between them.
## Different Types of SQL JOINs
- `(INNER) JOIN`: Returns records that have matching values in both tables
- `LEFT (OUTER) JOIN`: Returns all records from the left table, and the matched records from the right table 
- `RIGHT (OUTER) JOIN`: Returns all records from the right table, and the matched records from the left table
- `FULL (OUTER) JOIN`: Returns all records when there is a match in either left or right table
  
Example:
```
SELECT ProductID, ProductName, CategoryName  
FROM Products  
INNER JOIN Categories ON Products.CategoryID = Categories.CategoryID;
```

| ![[Pasted image 20250411102553.png]] | ![[Pasted image 20250411102603.png]] | ![[Pasted image 20250411102605.png]] | ![[Pasted image 20250411102609.png]] |
| ------------------------------------ | ------------------------------------ | ------------------------------------ | ------------------------------------ |

## The SQL UNION, GROUP BY, HAVING, EXISTS Operator

The `UNION` operator is used to combine the result-set of two or more `SELECT` statements.
- Every `SELECT` statement within `UNION` must have the same number of columns
- The columns must also have similar data types
- The columns in every `SELECT` statement must also be in the same order
Example: (returns the cities from both the "Customers" and the "Suppliers" table)
```
SELECT City FROM Customers  
UNION  
SELECT City FROM Suppliers  
ORDER BY City;
```

The `GROUP BY` statement groups rows that have the same values into summary rows, like "find the number of customers in each country".
Example: (lists the number of customers in each country)
```
SELECT COUNT(CustomerID), Country  
FROM Customers  
GROUP BY Country;
```

The `HAVING` clause was added to SQL because the `WHERE` keyword cannot be used with aggregate functions.
Syntax:
```
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
HAVING condition
ORDER BY column_name(s);
```

The `EXISTS` operator is used to test for the existence of any record in a subquery.
The `EXISTS` operator returns TRUE if the subquery returns one or more records.
Syntax:
```
SELECT column_name(s)
FROM table_name
WHERE EXISTS
(SELECT column_name FROM table_name WHERE condition);
```

# SQL ANY and ALL Operators
The `ANY` and `ALL` operators allow you to perform a comparison between a single column value and a range of other values.
The `ANY` operator:
- returns a boolean value as a result
- returns TRUE if ANY of the subquery values meet the condition
!`ANY` means that the condition will be true if the operation is true for any of the values in the range.!
AT LEAST ONE OF THEM
Example: (if ANY records in the OrderDetails table has Quantity equal to 10) 
```
SELECT ProductName  
FROM Products  
WHERE ProductID = ANY  
  (SELECT ProductID  
  FROM OrderDetails  
  WHERE Quantity = 10);
```

The `ALL` operator:
- returns a boolean value as a result
- returns TRUE if ALL of the subquery values meet the condition
- is used with `SELECT`, `WHERE` and `HAVING` statements

`ALL` means that the condition will be true only if the operation is true for all values in the range.
Example: (lists ALL the product names)
```
SELECT ALL ProductName  
FROM Products  
WHERE TRUE;
```

Example: (lists the ProductName if ALL the records in the OrderDetails has Quantity equal to 10.)
```
SELECT ProductName  
FROM Products  
WHERE ProductID = ALL  
  (SELECT ProductID  
  FROM OrderDetails  
  WHERE Quantity = 10);
```

The `SELECT INTO` statement copies data from one table into a new table.
Syntax:
Copy all columns into a new table:
```
SELECT *
INTO newtable [IN externaldb]
FROM oldtable
WHERE condition;
```

Copy only some columns into a new table:
```
SELECT column1, column2, column3, ...
INTO newtable [IN externaldb]
FROM oldtable
WHERE condition;
```


The `INSERT INTO SELECT` statement copies data from one table and inserts it into another table.
The `INSERT INTO SELECT` statement requires that the data types in source and target tables match.
Syntax:
Copy all columns from one table to another table:
```
INSERT INTO table2
SELECT * FROM table1
WHERE condition;
```

Copy only some columns from one table into another table:
```
INSERT INTO table2 (column1, column2, column3, ...)
SELECT column1, column2, column3, ...
FROM table1
WHERE condition;
```


The `CASE` expression goes through conditions and returns a value when the first condition is met (like an if-then-else statement). So, once a condition is true, it will stop reading and return the result. If no conditions are true, it returns the value in the `ELSE` clause.
If there is no `ELSE` part and no conditions are true, it returns NULL.
Syntax:
```
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    WHEN conditionN THEN resultN
    ELSE result
END;
```
Example:
```
SELECT OrderID, Quantity,
CASE
    WHEN Quantity > 30 THEN 'The quantity is greater than 30'
    WHEN Quantity = 30 THEN 'The quantity is 30'
    ELSE 'The quantity is under 30'
END AS QuantityText
FROM OrderDetails;
```

# SQL Stored Procedures for SQL Server

### Stored Procedure Syntax
```
CREATE PROCEDURE procedure_name
AS
sql_statement
GO;
```
### Execute a Stored Procedure
```
EXEC procedure_name;
```

Example:
```
CREATE PROCEDURE SelectAllCustomers @City nvarchar(30)
AS
SELECT * FROM Customers WHERE City = @City
GO;
```
Parameters are given with @parameter,  `nvarchar(30)` stands for data type.

## Comments
comments starts with `--`

# CREATE DATABASE Statement
The `CREATE DATABASE` statement is used to create a new SQL database.
Syntax:
```
CREATE DATABASE databasename;
```

`DROP DATABASE` statement is used to drop an existing SQL database.
```
DROP DATABASE databasename;
```

**Tip:** Make sure you have admin privilege before dropping any database. Once a database is dropped, you can check it in the list of databases with the following SQL command: 
`SHOW DATABASES;`

The `BACKUP DATABASE` statement is used in SQL Server to create a full back up of an existing SQL database.
Syntax:
```
BACKUP DATABASE databasename  
TO DISK = 'filepath';
```
OPTIMIZATION
A differential back up only backs up the parts of the database that have changed since the last full database backup.
```
BACKUP DATABASE databasename
TO DISK = 'filepath'
WITH DIFFERENTIAL;
```


The `CREATE TABLE` statement is used to create a new table in a database.
Syntax:
```
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
   ....
);
```

Create Table Using Another Table
A copy of an existing table can also be created using `CREATE TABLE`.

The new table gets the same column definitions. All columns or specific columns can be selected.
If you create a new table using an existing table, the new table will be filled with the existing values from the old table.
Syntax:
```
CREATE TABLE new_table_name AS
    SELECT column1, column2,...
    FROM existing_table_name
    WHERE ....;
```


The following SQL creates a new table called "TestTable" (which is a copy of the "Customers" table): 
Example:
```
CREATE TABLE TestTable AS  
SELECT customername, contactname  
FROM customers;
```

The `DROP TABLE` statement is used to drop an existing table in a database.
```
DROP TABLE table_name;
```

The `TRUNCATE TABLE` statement is used to delete the data inside a table, but not the table itself.
```
TRUNCATE TABLE table_name;
```


The `ALTER TABLE` statement is used to add, delete, or modify columns in an existing table.
The `ALTER TABLE` statement is also used to add and drop various constraints on an existing table.
To add a column in a table, use the following syntax:
```
ALTER TABLE _table_name_  
ADD _column_name datatype_;
```

DROP
```
ALTER TABLE table_name
DROP COLUMN column_name;
```

RENAME
```
ALTER TABLE table_name
RENAME COLUMN old_name to new_name;
```

change data type
 - SQL Server / MS Access:
```
ALTER TABLE table_name
ALTER COLUMN column_name datatype;
```
 
 - My SQL / Oracle (prior version 10G):
```
ALTER TABLE table_name
MODIFY COLUMN column_name datatype;
```

 - Oracle 10G and later:
```
ALTER TABLE table_name
MODIFY column_name datatype;
```

## SQL Constraints

Constraints are used to limit the type of data that can go into a table. This ensures the accuracy and reliability of the data in the table. If there is any violation between the constraint and the data action, the action is aborted.

Constraints can be column level or table level. Column level constraints apply to a column, and table level constraints apply to the whole table.

The following constraints are commonly used in SQL:

- `[NOT NULL]` - Ensures that a column cannot have a NULL value
- `[UNIQUE]` - Ensures that all values in a column are different
- `[PRIMARY KEY]` - A combination of a `NOT NULL` and `UNIQUE`. Uniquely identifies each row in a table
- `[FOREIGN KEY]` - Prevents actions that would destroy links between tables
- `[CHECK]` - Ensures that the values in a column satisfies a specific condition
- `[DEFAULT]` - Sets a default value for a column if no value is specified
- `[CREATE INDEX]` - Used to create and retrieve data from the database very quickly

The following SQL creates a `PRIMARY KEY` on the "ID" column when the "Persons" table is created:
 - MySQL:
```
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    PRIMARY KEY (ID)
);
```

 - SQL Server / Oracle / MS Access:
```
CREATE TABLE Persons (
    ID int NOT NULL PRIMARY KEY,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int
);
```


The `FOREIGN KEY` constraint is used to prevent actions that would destroy links between tables.
A `FOREIGN KEY` is a field (or collection of fields) in one table, that refers to the `[PRIMARY KEY]` in another table.

The following SQL creates a `FOREIGN KEY` on the "PersonID" column when the "Orders" table is created:
 - MySQL:
```
CREATE TABLE Orders (
    OrderID int NOT NULL,
    OrderNumber int NOT NULL,
    PersonID int,
    PRIMARY KEY (OrderID),
    FOREIGN KEY (PersonID) REFERENCES Persons(PersonID)
);
```

 - SQL Server / Oracle / MS Access:
```
CREATE TABLE Orders (
    OrderID int NOT NULL PRIMARY KEY,
    OrderNumber int NOT NULL,
    PersonID int FOREIGN KEY REFERENCES Persons(PersonID)
);
```

