The `SUM()` function returns the total sum of numeric values in a column. It's one of the essential [[SQL Aggregate Functions]] for mathematical calculations on data.

## Syntax
```sql
SELECT SUM(column_name) FROM table_name WHERE condition;
```

## Examples

**Calculate total of all product prices:**
```sql
SELECT SUM(Price) AS TotalPrice FROM Products;
```

**Sum with condition:**
```sql
SELECT SUM(Quantity) AS TotalQuantity 
FROM OrderDetails 
WHERE ProductID = 11;
```

**Sum by category:**
```sql
SELECT CategoryID, SUM(Price) AS TotalCategoryPrice
FROM Products
GROUP BY CategoryID;
```

**Sum with calculation:**
```sql
SELECT SUM(Price * Quantity) AS TotalOrderValue
FROM OrderDetails;
```

## Important Notes
- Only works with numeric data types
- Ignores NULL values automatically
- Returns NULL if no rows match or all values are NULL
- Can be combined with mathematical operations

## Advanced Examples

**Sum with multiple conditions:**
```sql
SELECT SUM(Price) AS ExpensiveProductsTotal
FROM Products
WHERE Price > 20 AND CategoryID = 1;
```

**Conditional sum using CASE:**
```sql
SELECT 
    SUM(CASE WHEN Price > 20 THEN Price ELSE 0 END) AS ExpensiveSum,
    SUM(CASE WHEN Price <= 20 THEN Price ELSE 0 END) AS CheapSum
FROM Products;
```

**Sum across joined tables:**
```sql
SELECT c.CategoryName, SUM(p.Price) AS TotalPrice
FROM Categories c
JOIN Products p ON c.CategoryID = p.CategoryID
GROUP BY c.CategoryName;
```

## Related Concepts
- [[SQL Aggregate Functions]] - Family of calculation functions
- [[SQL COUNT Function]] - Count records
- [[SQL AVG Function]] - Calculate averages
- [[SQL MIN and MAX Functions]] - Find extremes
- [[SQL GROUP BY]] - Calculate sums for groups
- [[SQL CASE Statement]] - Conditional summation

Essential for financial calculations and data analysis in [[SQL (Structured Query Language)]] and [[SQL Queries]].
