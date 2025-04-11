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



## Comments
comments starts with `--`





