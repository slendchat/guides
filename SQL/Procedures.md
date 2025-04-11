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