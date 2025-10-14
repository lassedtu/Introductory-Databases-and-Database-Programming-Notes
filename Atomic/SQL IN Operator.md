The `IN` operator allows you to specify multiple values in a [[SQL WHERE Clause]]. It's a shorthand for multiple OR conditions and makes queries more readable and efficient.

## Syntax
```sql
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1, value2, ...);
```

## Examples

**Select customers from specific countries:**
```sql
SELECT * FROM Customers 
WHERE Country IN ('Germany', 'France', 'UK');
```

**Equivalent to multiple OR conditions:**
```sql
-- The above is the same as:
SELECT * FROM Customers 
WHERE Country = 'Germany' 
   OR Country = 'France' 
   OR Country = 'UK';
```

**With numbers:**
```sql
SELECT * FROM Products 
WHERE CategoryID IN (1, 3, 5);
```

**NOT IN (exclude values):**
```sql
SELECT * FROM Customers 
WHERE Country NOT IN ('Germany', 'France', 'UK');
```

## IN with Subqueries
Use IN with a subquery to compare against dynamic values:

```sql
-- Find customers who have placed orders
SELECT * FROM Customers 
WHERE CustomerID IN (SELECT CustomerID FROM Orders);
```

```sql
-- Find products that have been ordered
SELECT * FROM Products 
WHERE ProductID IN (
    SELECT DISTINCT ProductID 
    FROM OrderDetails
);
```

**NOT IN with subquery:**
```sql
-- Find customers who have NOT placed orders
SELECT * FROM Customers 
WHERE CustomerID NOT IN (
    SELECT CustomerID FROM Orders 
    WHERE CustomerID IS NOT NULL
);
```

## Important Notes with NULL Values

**NULL handling with IN:**
```sql
-- This works fine
SELECT * FROM Customers 
WHERE City IN ('London', 'Paris', NULL);  -- Ignores NULL comparison
```

**NULL handling with NOT IN:**
```sql
-- DANGER: This may return no results if subquery contains NULL
SELECT * FROM Customers 
WHERE CustomerID NOT IN (
    SELECT CustomerID FROM Orders
    -- If any CustomerID in Orders is NULL, entire result becomes empty!
);

-- Safe version:
SELECT * FROM Customers 
WHERE CustomerID NOT IN (
    SELECT CustomerID FROM Orders 
    WHERE CustomerID IS NOT NULL
);
```

## Performance Considerations
- IN is generally faster than multiple OR conditions
- For large lists, consider JOIN instead of IN with subquery
- EXISTS may be more efficient than IN with subqueries

**IN vs EXISTS comparison:**
```sql
-- Using IN
SELECT * FROM Customers 
WHERE CustomerID IN (SELECT CustomerID FROM Orders);

-- Using EXISTS (often more efficient)
SELECT * FROM Customers c
WHERE EXISTS (SELECT 1 FROM Orders o WHERE o.CustomerID = c.CustomerID);
```

## Related Concepts
- [[SQL WHERE Clause]] - Foundation for IN operator
- [[SQL OR Operator]] - Alternative to IN for multiple conditions
- [[SQL Subqueries]] - Dynamic value lists for IN
- [[SQL EXISTS]] - Alternative existence checking
- [[SQL JOIN]] - Alternative to IN with subqueries for performance
- [[SQL NOT Operator]] - Negation with NOT IN

Essential tool for filtering multiple values in [[SQL Queries]] and [[SQL (Structured Query Language)]].
