## Overview

Comments in SQL explain code or prevent execution of code.  
Comments are ignored by the SQL engine.  
Microsoft Access does not support comments.

## Single Line Comments

- Start with -- (two dashes).
- Everything after -- on the line is ignored.

**Example:**  
Add a comment before a statement.

```sql
-- Select all:
SELECT * FROM Customers;
```

**Example:**  
Ignore part of a line.

```sql
SELECT * FROM Customers -- WHERE City='Berlin';
```

**Example:**  
Ignore a whole statement.

```sql
-- SELECT * FROM Customers;
SELECT * FROM Products;
```

## Multi-line Comments

- Start with /* and end with */.
- Everything between /* and */ is ignored.

**Example:**  
Add a multi-line explanation.

```sql
/*Select all the columns
of all the records
in the Customers table:*/
SELECT * FROM Customers;
```

**Example:**  
Ignore multiple statements.

```sql
/*SELECT * FROM Customers;
SELECT * FROM Products;
SELECT * FROM Orders;
SELECT * FROM Categories;*/
SELECT * FROM Suppliers;
```

**Example:**  
Ignore part of a statement.

```sql
SELECT CustomerName, /*City,*/ Country FROM Customers;
```

**Example:**  
Ignore part of a WHERE clause.

```sql
SELECT * FROM Customers WHERE (CustomerName LIKE 'L%'
OR CustomerName LIKE 'R%' /*OR CustomerName LIKE 'S%'
OR CustomerName LIKE 'T%'*/ OR CustomerName LIKE 'W%')
AND Country='USA'
ORDER BY CustomerName;
```

## Key Points

- Use -- for single line comments.
- Use /* */ for multi-line or inline comments.
- Comments help explain code or disable parts of code.
- Comments are not supported in MS Access.

**Example:**  
Use comments to document your SQL code or to test changes by disabling lines.