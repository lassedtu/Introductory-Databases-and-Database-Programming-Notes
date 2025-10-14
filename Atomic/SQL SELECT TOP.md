The `SELECT TOP` clause is used to specify the number of records to return from the beginning of a result set. This is useful when working with large tables and you only want to return a limited number of records.

## Syntax

**SQL Server / MS Access:**
```sql
SELECT TOP number column_name(s)
FROM table_name
WHERE condition;
```

**MySQL:**
```sql
SELECT column_name(s)
FROM table_name
WHERE condition
LIMIT number;
```

**Oracle:**
```sql
SELECT column_name(s)
FROM table_name
WHERE condition
AND ROWNUM <= number;
```

## Examples

**Get first 3 customers:**
```sql
-- SQL Server/MS Access
SELECT TOP 3 * FROM Customers;

-- MySQL
SELECT * FROM Customers LIMIT 3;

-- Oracle  
SELECT * FROM Customers WHERE ROWNUM <= 3;
```

**Get top 50 percent of records:**
```sql
SELECT TOP 50 PERCENT * FROM Customers;
```

## Related Concepts
- [[SQL SELECT Statement]] - Foundation for data retrieval
- [[SQL WHERE Clause]] - Filter records before limiting
- [[SQL ORDER BY]] - Sort before limiting to get meaningful results
- [[SQL LIMIT]] - MySQL equivalent to TOP

Essential for performance optimization in [[SQL Queries]] and [[SQL (Structured Query Language)]].
