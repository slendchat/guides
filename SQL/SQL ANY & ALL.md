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
