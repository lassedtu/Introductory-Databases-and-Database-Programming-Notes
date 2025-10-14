The `BETWEEN` operator selects values within a given range. The values can be numbers, text, or dates. It's inclusive, meaning it includes the boundary values.

## Syntax
```sql
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

## Examples

**Numeric ranges:**
```sql
-- Products with prices between 10 and 20 (inclusive)
SELECT * FROM Products 
WHERE Price BETWEEN 10 AND 20;
```

**Date ranges:**
```sql
-- Orders from July 1996
SELECT * FROM Orders 
WHERE OrderDate BETWEEN '1996-07-01' AND '1996-07-31';
```

**Text ranges (alphabetical):**
```sql
-- Customer names starting with letters A through M
SELECT * FROM Customers 
WHERE CustomerName BETWEEN 'A' AND 'N';  -- Note: 'N' is not included
```

## NOT BETWEEN
Exclude values within a range:

```sql
-- Products with prices NOT between 10 and 20
SELECT * FROM Products 
WHERE Price NOT BETWEEN 10 AND 20;

-- Equivalent to:
SELECT * FROM Products 
WHERE Price < 10 OR Price > 20;
```

## Important Notes

### Inclusive Boundaries
BETWEEN includes both boundary values:
```sql
WHERE Price BETWEEN 10 AND 20  -- Includes 10 and 20
-- Same as: Price >= 10 AND Price <= 20
```

### Text Boundaries
With text, the end value is usually exclusive:
```sql
WHERE CustomerName BETWEEN 'A' AND 'M'  
-- Includes names starting with A through L
-- Excludes names starting with M (unless they equal exactly 'M')
```

### Date Formats
Always use proper date formats:
```sql
-- Good formats:
WHERE OrderDate BETWEEN '1996-07-01' AND '1996-07-31'
WHERE OrderDate BETWEEN DATE('1996-07-01') AND DATE('1996-07-31')

-- Be careful with datetime - this excludes times on the last day:
WHERE OrderDateTime BETWEEN '1996-07-01' AND '1996-07-31'
-- Better for datetime:
WHERE OrderDateTime BETWEEN '1996-07-01' AND '1996-07-31 23:59:59'
```

## Advanced Examples

**Combining with other conditions:**
```sql
SELECT * FROM Products 
WHERE Price BETWEEN 10 AND 20 
  AND CategoryID IN (1, 2, 3);
```

**Using with calculations:**
```sql
SELECT * FROM OrderDetails 
WHERE (UnitPrice * Quantity) BETWEEN 100 AND 500;
```

**Date range with functions:**
```sql
-- Orders from last 30 days
SELECT * FROM Orders 
WHERE OrderDate BETWEEN DATE_SUB(NOW(), INTERVAL 30 DAY) AND NOW();
```

**Multiple BETWEEN conditions:**
```sql
SELECT * FROM Products 
WHERE Price BETWEEN 10 AND 50 
  AND UnitsInStock BETWEEN 5 AND 100;
```

## Database-Specific Considerations

**MySQL date ranges:**
```sql
WHERE OrderDate BETWEEN '2023-01-01' AND '2023-12-31'
```

**SQL Server date ranges:**
```sql
WHERE OrderDate BETWEEN '2023-01-01' AND '2023-12-31'
```

**Oracle date ranges:**
```sql
WHERE OrderDate BETWEEN DATE '2023-01-01' AND DATE '2023-12-31'
```

## Related Concepts
- [[SQL WHERE Clause]] - Foundation for BETWEEN operator
- [[SQL Comparison Operators]] - >= and <= equivalents
- [[SQL Date Functions]] - Working with date ranges
- [[SQL AND Operator]] - BETWEEN uses AND logic internally
- [[SQL IN Operator]] - Alternative for discrete value lists

Useful for range-based filtering in [[SQL Queries]] and [[SQL (Structured Query Language)]].
