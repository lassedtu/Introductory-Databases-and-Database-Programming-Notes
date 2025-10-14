The `SELECT DISTINCT` statement is used to return only distinct (different) values. It removes duplicate rows from the result set.

## Syntax
```sql
SELECT DISTINCT column1, column2, ...
FROM table_name;
```

## Examples

**Without DISTINCT (shows duplicates):**
```sql
SELECT Country FROM Customers;
```

**With DISTINCT (removes duplicates):**
```sql
SELECT DISTINCT Country FROM Customers;
```

**Count distinct values:**
```sql
SELECT COUNT(DISTINCT Country) FROM Customers;
```

## Multiple Columns
When using DISTINCT with multiple columns, it returns distinct combinations:
```sql
SELECT DISTINCT Country, City FROM Customers;
```
This returns unique combinations of Country and City, not just unique values in each column separately.

## Related Concepts
- [[SQL SELECT Statement]] - Basic data selection
- [[SQL WHERE Clause]] - Filter before removing duplicates
- [[SQL COUNT Function]] - Count distinct values
- [[SQL GROUP BY]] - Alternative approach for finding unique values

Part of [[SQL Queries]] in [[SQL (Structured Query Language)]].
