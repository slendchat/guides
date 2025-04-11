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

Example: (lists the ProductName if ALL the records in the OrderDetails table has Quantity equal to 10.)
```
SELECT ProductName  
FROM Products  
WHERE ProductID = ALL  
  (SELECT ProductID  
  FROM OrderDetails  
  WHERE Quantity = 10);
```