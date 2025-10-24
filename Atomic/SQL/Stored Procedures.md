## Overview

A stored procedure is a saved set of SQL statements.  
You can reuse the code by calling the procedure.  
Stored procedures can accept parameters.  
This allows you to run the same code with different values.

## Syntax

```sql
CREATE PROCEDURE procedure_name
AS
sql_statement
GO;
```

- Use EXEC to run the procedure.

**Example:**  
Create a procedure to select all customers.

```sql
CREATE PROCEDURE SelectAllCustomers
AS
SELECT * FROM Customers
GO;
```

Run the procedure:

```sql
EXEC SelectAllCustomers;
```

## Stored Procedure With Parameters

You can pass parameters to a stored procedure.  
This lets the procedure use different input values.

**Example:**  
Create a procedure with one parameter.

```sql
CREATE PROCEDURE SelectAllCustomers @City nvarchar(30)
AS
SELECT * FROM Customers WHERE City = @City
GO;
```

Run the procedure with a parameter:

```sql
EXEC SelectAllCustomers @City = 'London';
```

**Example:**  
Create a procedure with multiple parameters.

```sql
CREATE PROCEDURE SelectAllCustomers @City nvarchar(30), @PostalCode nvarchar(10)
AS
SELECT * FROM Customers WHERE City = @City AND PostalCode = @PostalCode
GO;
```

Run the procedure with two parameters:

```sql
EXEC SelectAllCustomers @City = 'London', @PostalCode = 'WA1 1DP';
```

## Key Points

- Stored procedures save time and reduce errors.
- You can reuse code by calling the procedure.
- Parameters make procedures flexible.
- This allows you to run complex queries with simple commands.

**Example:**  
Instead of writing the same SELECT statement many times, save it as a procedure and call it when needed.