The `DELETE` statement is used to delete existing records in a table.

## Syntax
```sql
DELETE FROM table_name 
WHERE condition;
```

**WARNING:** Always use a WHERE clause! Without it, ALL records will be deleted.

## Examples

**Delete a specific record:**
```sql
DELETE FROM Customers 
WHERE CustomerName = 'Alfreds Futterkiste';
```

**Delete multiple records:**
```sql
DELETE FROM Customers 
WHERE Country = 'Norway';
```

**Delete with complex conditions:**
```sql
DELETE FROM Orders 
WHERE OrderDate < '2023-01-01' AND CustomerID IN (1, 2, 3);
```

## Delete All Records
```sql
-- Deletes all records but keeps table structure
DELETE FROM table_name;

-- Alternative: TRUNCATE (faster, cannot be rolled back)
TRUNCATE TABLE table_name;
```

## Delete vs DROP vs TRUNCATE

| Command | Effect |
|---------|---------|
| `DELETE` | Removes specific rows, keeps table structure |
| `TRUNCATE` | Removes all rows, keeps table structure, faster |
| `DROP TABLE` | Removes entire table and structure |

## Delete with Subquery
```sql
DELETE FROM Customers
WHERE CustomerID IN (
    SELECT CustomerID 
    FROM Orders 
    WHERE OrderDate < '2020-01-01'
);
```

## Common Mistakes

**Missing WHERE clause (deletes all rows):**
```sql
-- DANGEROUS - Deletes ALL customers
DELETE FROM Customers;

-- CORRECT - Deletes specific customers
DELETE FROM Customers
WHERE Country = 'Germany';
```

## Related Concepts
- [[SQL INSERT INTO Statement]] - Add new records
- [[SQL UPDATE Statement]] - Modify records
- [[SQL WHERE Clause]] - Essential for targeted deletion
- [[SQL DROP TABLE]] - Remove entire table
- [[SQL TRUNCATE]] - Fast delete all rows
- [[Data Manipulation Language (DML)]] - Category of SQL commands

Part of [[Data Manipulation Language (DML)]] in [[SQL (Structured Query Language)]] for removing data.
