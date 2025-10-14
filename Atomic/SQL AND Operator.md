The `AND` operator is used to filter records based on more than one condition. It displays a record if ALL the conditions separated by AND are TRUE.

## Syntax
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1 AND condition2 AND condition3 ...;
```

## Examples

**Two conditions:**
```sql
SELECT * FROM Customers
WHERE Country = 'Germany' AND City = 'Berlin';
```

**Multiple conditions:**
```sql
SELECT * FROM Products
WHERE Price >= 20 AND Price <= 40 AND CategoryID = 1;
```

**With other operators:**
```sql
SELECT * FROM Customers
WHERE Country = 'Germany' AND (City = 'Berlin' OR City = 'München');
```

## Truth Table
| Condition1 | Condition2 | AND Result |
|------------|------------|------------|
| TRUE | TRUE | TRUE |
| TRUE | FALSE | FALSE |
| FALSE | TRUE | FALSE |
| FALSE | FALSE | FALSE |

## Precedence
AND has higher precedence than OR. Use parentheses for clarity:
```sql
-- Without parentheses (might be confusing)
WHERE Country = 'USA' OR Country = 'UK' AND City = 'London'

-- With parentheses (clearer intent)
WHERE Country = 'USA' OR (Country = 'UK' AND City = 'London')
```

## Related Concepts
- [[SQL OR Operator]] - Alternative conditions
- [[SQL NOT Operator]] - Negating conditions
- [[SQL WHERE Clause]] - Main filtering mechanism
- [[SQL Operators]] - All logical operators

Used in [[SQL WHERE Clause]] as part of [[SQL (Structured Query Language)]] for complex filtering.
