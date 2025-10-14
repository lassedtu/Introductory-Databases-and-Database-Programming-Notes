The `UPDATE` statement is used to modify the existing records in a table.

## Syntax
```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

**⚠️ WARNING:** Always use a WHERE clause! Without it, ALL records will be updated.

## Examples

**Update a single record:**
```sql
UPDATE Customers
SET ContactName = 'Alfred Schmidt', City = 'Frankfurt'
WHERE CustomerID = 1;
```

**Update multiple records:**
```sql
UPDATE Customers
SET ContactName = 'Juan'
WHERE Country = 'Mexico';
```

**Update with calculation:**
```sql
UPDATE Products
SET Price = Price * 1.1
WHERE CategoryID = 1;  -- Increase prices by 10%
```

## Update Multiple Columns
```sql
UPDATE Customers
SET ContactName = 'Alfred Schmidt',
    City = 'Frankfurt',
    Country = 'Germany'
WHERE CustomerID = 1;
```

## Update with Subquery
```sql
UPDATE Products
SET Price = (SELECT AVG(Price) FROM Products WHERE CategoryID = 1)
WHERE ProductID = 10;
```

## Common Mistakes

**Missing WHERE clause (updates all rows):**
```sql
-- DANGEROUS - Updates ALL customers
UPDATE Customers
SET City = 'Oslo';

-- CORRECT - Updates specific customers  
UPDATE Customers
SET City = 'Oslo'
WHERE Country = 'Norway';
```

## Related Concepts
- [[SQL INSERT INTO Statement]] - Add new records
- [[SQL DELETE Statement]] - Remove records  
- [[SQL WHERE Clause]] - Essential for targeted updates
- [[SQL Subqueries]] - Use queries in SET or WHERE
- [[Data Manipulation Language (DML)]] - Category of SQL commands

Part of [[Data Manipulation Language (DML)]] in [[SQL (Structured Query Language)]] for modifying existing data.
