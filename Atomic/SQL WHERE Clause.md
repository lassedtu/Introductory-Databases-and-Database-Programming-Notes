The `WHERE` clause is used to filter records. It extracts only those records that fulfill a specified condition.

## Syntax
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

## Common Operators

| Operator | Description |
|----------|-------------|
| = | Equal |
| <> or != | Not equal |
| > | Greater than |
| < | Less than |
| >= | Greater than or equal |
| <= | Less than or equal |
| BETWEEN | Between two values |
| LIKE | Search for a pattern |
| IN | Match any value in a list |
| IS NULL | Check for NULL values |

## Examples

**Text values (use single quotes):**
```sql
SELECT * FROM Customers 
WHERE Country = 'Mexico';
```

**Numeric values:**
```sql
SELECT * FROM Products 
WHERE Price > 20;
```

**Date values:**
```sql
SELECT * FROM Orders 
WHERE OrderDate = '1996-07-04';
```

## Related Concepts
- [[SQL AND Operator]] - Multiple conditions (all must be true)
- [[SQL OR Operator]] - Multiple conditions (any can be true) 
- [[SQL NOT Operator]] - Negates a condition
- [[SQL LIKE Operator]] - Pattern matching with wildcards
- [[SQL IN Operator]] - Match multiple values
- [[SQL BETWEEN Operator]] - Range of values
- [[SQL IS NULL]] - Handle NULL values

Essential part of [[SQL Queries]] and [[SQL (Structured Query Language)]] for data filtering.
