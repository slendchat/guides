# CREATE DATABASE + etc.
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


# CREATE TABLE + etc.

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
