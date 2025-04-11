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
