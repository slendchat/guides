# SQL Constraints

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

