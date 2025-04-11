
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

