The `ORDER BY` keyword is used to sort the result-set in ascending or descending order. By default, it sorts records in ascending order.

## Syntax
```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column1, column2, ... ASC|DESC;
```

## Examples

**Ascending order (default):**
```sql
SELECT * FROM Customers
ORDER BY Country;
```

**Descending order:**
```sql
SELECT * FROM Customers
ORDER BY Country DESC;
```

**Multiple columns:**
```sql
SELECT * FROM Customers
ORDER BY Country, CustomerName;
```

**Mixed sorting:**
```sql
SELECT * FROM Customers
ORDER BY Country ASC, CustomerName DESC;
```

## Sorting by Column Position
You can also order by column position:
```sql
SELECT CustomerName, ContactName, Country
FROM Customers
ORDER BY 3;  -- Orders by the 3rd column (Country)
```

## Related Concepts
- [[SQL SELECT Statement]] - Basic data selection before sorting
- [[SQL WHERE Clause]] - Filter before sorting
- [[SQL LIMIT]] - Limit sorted results
- [[SQL TOP]] - Get top N records after sorting

Part of [[SQL Queries]] in [[SQL (Structured Query Language)]] for organizing result sets.
