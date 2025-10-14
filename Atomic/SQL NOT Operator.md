The `NOT` operator is used to negate a condition in a WHERE clause. It displays records for which the condition is NOT TRUE.

## Syntax
```sql
SELECT column1, column2, ...
FROM table_name
WHERE NOT condition;
```

## Examples

**Basic NOT:**
```sql
SELECT * FROM Customers
WHERE NOT Country = 'Germany';
```

**NOT with LIKE:**
```sql
SELECT * FROM Customers
WHERE CustomerName NOT LIKE 'A%';
```

**NOT with IN:**
```sql
SELECT * FROM Customers
WHERE Country NOT IN ('Germany', 'France', 'UK');
```

**NOT with BETWEEN:**
```sql
SELECT * FROM Products
WHERE Price NOT BETWEEN 10 AND 20;
```

**NOT with EXISTS:**
```sql
SELECT * FROM Customers
WHERE NOT EXISTS (SELECT * FROM Orders WHERE Orders.CustomerID = Customers.CustomerID);
```

## Combining with AND/OR
```sql
-- NOT with AND
SELECT * FROM Customers
WHERE NOT (Country = 'Germany' AND City = 'Berlin');

-- NOT with OR  
SELECT * FROM Customers
WHERE NOT (Country = 'Germany' OR Country = 'Spain');
```

## Alternative Operators
Some NOT conditions can be written using other operators:

| NOT Expression | Equivalent |
|----------------|------------|
| `NOT =` | `<>` or `!=` |
| `NOT <` | `>=` |
| `NOT >` | `<=` |
| `NOT IN` | Use AND with `<>` |
| `NOT BETWEEN` | `< min OR > max` |

## Related Concepts
- [[SQL AND Operator]] - Combine conditions
- [[SQL OR Operator]] - Alternative conditions  
- [[SQL WHERE Clause]] - Main filtering mechanism
- [[SQL IN Operator]] - Match multiple values
- [[SQL BETWEEN Operator]] - Range conditions
- [[SQL LIKE Operator]] - Pattern matching

Used in [[SQL WHERE Clause]] as part of [[SQL (Structured Query Language)]] for exclusion filtering.
