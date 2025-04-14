# MySQL Data Types (Version 8.0)

### String Data Types

| Data type                   | Description                                                                                                                                                                                                                                                             |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| CHAR(size)                  | A FIXED length string (can contain letters, numbers, and special characters). The _size_ parameter specifies the column length in characters - can be from 0 to 255. Default is 1                                                                                       |
| VARCHAR(size)               | A VARIABLE length string (can contain letters, numbers, and special characters). The _size_ parameter specifies the maximum string length in characters - can be from 0 to 65535                                                                                        |
| BINARY(size)                | Equal to CHAR(), but stores binary byte strings. The _size_ parameter specifies the column length in bytes. Default is 1                                                                                                                                                |
| VARBINARY(size)             | Equal to VARCHAR(), but stores binary byte strings. The _size_ parameter specifies the maximum column length in bytes.                                                                                                                                                  |
| TINYBLOB                    | For BLOBs (Binary Large Objects). Max length: 255 bytes                                                                                                                                                                                                                 |
| TINYTEXT                    | Holds a string with a maximum length of 255 characters                                                                                                                                                                                                                  |
| TEXT(size)                  | Holds a string with a maximum length of 65,535 bytes                                                                                                                                                                                                                    |
| BLOB(size)                  | For BLOBs (Binary Large Objects). Holds up to 65,535 bytes of data                                                                                                                                                                                                      |
| MEDIUMTEXT                  | Holds a string with a maximum length of 16,777,215 characters                                                                                                                                                                                                           |
| MEDIUMBLOB                  | For BLOBs (Binary Large Objects). Holds up to 16,777,215 bytes of data                                                                                                                                                                                                  |
| LONGTEXT                    | Holds a string with a maximum length of 4,294,967,295 characters                                                                                                                                                                                                        |
| LONGBLOB                    | For BLOBs (Binary Large Objects). Holds up to 4,294,967,295 bytes of data                                                                                                                                                                                               |
| ENUM(val1, val2, val3, ...) | A string object that can have only one value, chosen from a list of possible values. You can list up to 65535 values in an ENUM list. If a value is inserted that is not in the list, a blank value will be inserted. The values are sorted in the order you enter them |
| SET(val1, val2, val3, ...)  | A string object that can have 0 or more values, chosen from a list of possible values. You can list up to 64 values in a SET list                                                                                                                                       |

### Numeric Data Types

|Data type|Description|
|---|---|
|BIT(_size_)|A bit-value type. The number of bits per value is specified in _size_. The _size_ parameter can hold a value from 1 to 64. The default value for _size_ is 1.|
|TINYINT(_size_)|A very small integer. Signed range is from -128 to 127. Unsigned range is from 0 to 255. The _size_ parameter specifies the maximum display width (which is 255)|
|BOOL|Zero is considered as false, nonzero values are considered as true.|
|BOOLEAN|Equal to BOOL|
|SMALLINT(_size_)|A small integer. Signed range is from -32768 to 32767. Unsigned range is from 0 to 65535. The _size_ parameter specifies the maximum display width (which is 255)|
|MEDIUMINT(_size_)|A medium integer. Signed range is from -8388608 to 8388607. Unsigned range is from 0 to 16777215. The _size_ parameter specifies the maximum display width (which is 255)|
|INT(_size_)|A medium integer. Signed range is from -2147483648 to 2147483647. Unsigned range is from 0 to 4294967295. The _size_ parameter specifies the maximum display width (which is 255)|
|INTEGER(_size_)|Equal to INT(size)|
|BIGINT(_size_)|A large integer. Signed range is from -9223372036854775808 to 9223372036854775807. Unsigned range is from 0 to 18446744073709551615. The _size_ parameter specifies the maximum display width (which is 255)|
|FLOAT(_size_, _d_)|A floating point number. The total number of digits is specified in _size_. The number of digits after the decimal point is specified in the _d_ parameter. This syntax is deprecated in MySQL 8.0.17, and it will be removed in future MySQL versions|
|FLOAT(_p_)|A floating point number. MySQL uses the _p_ value to determine whether to use FLOAT or DOUBLE for the resulting data type. If _p_ is from 0 to 24, the data type becomes FLOAT(). If _p_ is from 25 to 53, the data type becomes DOUBLE()|
|DOUBLE(_size_, _d_)|A normal-size floating point number. The total number of digits is specified in _size_. The number of digits after the decimal point is specified in the _d_ parameter|
|DOUBLE PRECISION(_size_, _d_)||
|DECIMAL(_size_, _d_)|An exact fixed-point number. The total number of digits is specified in _size_. The number of digits after the decimal point is specified in the _d_ parameter. The maximum number for _size_ is 65. The maximum number for _d_ is 30. The default value for _size_ is 10. The default value for _d_ is 0.|
|DEC(_size_, _d_)|Equal to DECIMAL(size,d)|

### Date and Time Data Types

| Data type        | Description                                                                                                                                                                                                                                                                                                                                                                                                       |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| DATE             | A date. Format: YYYY-MM-DD. The supported range is from '1000-01-01' to '9999-12-31'                                                                                                                                                                                                                                                                                                                              |
| DATETIME(_fsp_)  | A date and time combination. Format: YYYY-MM-DD hh:mm:ss. The supported range is from '1000-01-01 00:00:00' to '9999-12-31 23:59:59'. Adding DEFAULT and ON UPDATE in the column definition to get automatic initialization and updating to the current date and time                                                                                                                                             |
| TIMESTAMP(_fsp_) | A timestamp. TIMESTAMP values are stored as the number of seconds since the Unix epoch ('1970-01-01 00:00:00' UTC). Format: YYYY-MM-DD hh:mm:ss. The supported range is from '1970-01-01 00:00:01' UTC to '2038-01-09 03:14:07' UTC. Automatic initialization and updating to the current date and time can be specified using DEFAULT CURRENT_TIMESTAMP and ON UPDATE CURRENT_TIMESTAMP in the column definition |
| TIME(_fsp_)      | A time. Format: hh:mm:ss. The supported range is from '-838:59:59' to '838:59:59'                                                                                                                                                                                                                                                                                                                                 |
| YEAR             | A year in four-digit format. Values allowed in four-digit format: 1901 to 2155, and 0000.  <br>MySQL 8.0 does not support year in two-digit format.                                                                                                                                                                                                                                                               |
# SQL Dates

 - **MySQL** comes with the following data types for storing a date or a date/time value in the database:
	`DATE` - format YYYY-MM-DD
	`DATETIME` - format: YYYY-MM-DD HH:MI:SS
	`TIMESTAMP` - format: YYYY-MM-DD HH:MI:SS
	`YEAR` - format YYYY or YY

 - **SQL Server** comes with the following data types for storing a date or a date/time value in the database:
	`DATE` - format YYYY-MM-DD
	`DATETIME` - format: YYYY-MM-DD HH:MI:SS
	`SMALLDATETIME` - format: YYYY-MM-DD HH:MI:SS
	`TIMESTAMP` - format: a unique number

Note: The date types are chosen for a column when you create a new table in your database!