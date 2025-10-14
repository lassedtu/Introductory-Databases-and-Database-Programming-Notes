The `LIKE` operator is used in a [[SQL WHERE Clause]] to search for a specified pattern in a column. It's commonly used with wildcards for flexible text matching.

## Syntax
```sql
SELECT column1, column2, ...
FROM table_name
WHERE column_name LIKE pattern;
```

## Wildcard Characters

| Wildcard | Description | Example |
|----------|-------------|---------|
| % | Represents zero, one, or multiple characters | `'a%'` - starts with "a" |
| _ | Represents exactly one character | `'a_'` - "a" followed by one character |
| [] | Represents any single character within brackets | `'[abc]%'` - starts with a, b, or c |
| [^] or [!] | Represents any character NOT in brackets | `'[^abc]%'` - does NOT start with a, b, or c |

## Common Patterns

**Starts with:**
```sql
SELECT * FROM Customers 
WHERE CustomerName LIKE 'A%';  -- Names starting with A
```

**Ends with:**
```sql
SELECT * FROM Customers 
WHERE CustomerName LIKE '%son';  -- Names ending with "son"
```

**Contains:**
```sql
SELECT * FROM Customers 
WHERE CustomerName LIKE '%market%';  -- Names containing "market"
```

**Specific position:**
```sql
SELECT * FROM Customers 
WHERE CustomerName LIKE 'A__%';  -- Names starting with A, at least 3 characters
```

**Exact length:**
```sql
SELECT * FROM Customers 
WHERE CustomerName LIKE '____';  -- Names with exactly 4 characters
```

## Advanced Examples

**Multiple patterns with OR:**
```sql
SELECT * FROM Customers 
WHERE CustomerName LIKE 'A%' OR CustomerName LIKE 'B%';
```

**NOT LIKE:**
```sql
SELECT * FROM Customers 
WHERE CustomerName NOT LIKE 'A%';  -- Names NOT starting with A
```

**Bracket wildcards (SQL Server):**
```sql
SELECT * FROM Customers 
WHERE CustomerName LIKE '[ABC]%';  -- Names starting with A, B, or C
```

**Range in brackets:**
```sql
SELECT * FROM Customers 
WHERE CustomerName LIKE '[A-M]%';  -- Names starting with A through M
```

## Case Sensitivity
- MySQL: Case-insensitive by default
- SQL Server: Depends on collation settings
- PostgreSQL: Case-sensitive (use ILIKE for case-insensitive)

## Related Concepts
- [[SQL Wildcards]] - Pattern matching characters
- [[SQL WHERE Clause]] - Foundation for LIKE operator
- [[SQL Regular Expressions]] - More advanced pattern matching
- [[SQL IN Operator]] - Match exact values from a list
- [[SQL BETWEEN Operator]] - Range matching
- [[SQL Text Functions]] - Other string manipulation functions

Essential for flexible text searching in [[SQL Queries]] and [[SQL (Structured Query Language)]].
