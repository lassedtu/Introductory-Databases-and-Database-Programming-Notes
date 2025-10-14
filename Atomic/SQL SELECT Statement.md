The `SELECT` statement is used to select data from a database. The data returned is stored in a result table, called the result-set.

## Basic Syntax
```sql
SELECT column1, column2, ...
FROM table_name;
```

To select all columns from a table:
```sql
SELECT * FROM table_name;
```

## Examples
**Select specific columns:**
```sql
SELECT CustomerName, City, Country 
FROM Customers;
```

**Select all columns:**
```sql
SELECT * FROM Customers;
```

SQL keywords are NOT case sensitive: select is the same as SELECT. However, it's conventional to write SQL keywords in uppercase.

## Related Concepts
- [[SQL SELECT DISTINCT]] - Remove duplicate values
- [[SQL WHERE Clause]] - Filter records with conditions  
- [[SQL ORDER BY]] - Sort the result set
- [[SQL Aggregate Functions]] - Perform calculations on data
- [[SQL Aliases]] - Give temporary names to columns or tables

The SELECT statement forms the foundation of [[SQL Queries]] and is essential for data retrieval in [[SQL (Structured Query Language)]].
