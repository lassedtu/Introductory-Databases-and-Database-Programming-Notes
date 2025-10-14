The `AVG()` function returns the average (arithmetic mean) value of numeric values in a column. It's one of the key [[SQL Aggregate Functions]] for statistical analysis.

## Syntax
```sql
SELECT AVG(column_name) FROM table_name WHERE condition;
```

## Examples

**Calculate average product price:**
```sql
SELECT AVG(Price) AS AveragePrice FROM Products;
```

**Average with condition:**
```sql
SELECT AVG(Price) AS AverageCategoryPrice
FROM Products
WHERE CategoryID = 1;
```

**Average by group:**
```sql
SELECT CategoryID, AVG(Price) AS AveragePrice
FROM Products
GROUP BY CategoryID
ORDER BY AveragePrice DESC;
```

**Round average to 2 decimal places:**
```sql
SELECT ROUND(AVG(Price), 2) AS AveragePrice FROM Products;
```

## Important Notes
- Only works with numeric data types
- Automatically ignores NULL values
- Returns NULL if no rows match or all values are NULL
- Result may have many decimal places (use ROUND() if needed)

## Advanced Examples

**Compare individual prices to average:**
```sql
SELECT ProductName, Price,
       AVG(Price) OVER() AS OverallAverage,
       Price - AVG(Price) OVER() AS DifferenceFromAverage
FROM Products;
```

**Products above average price:**
```sql
SELECT ProductName, Price
FROM Products
WHERE Price > (SELECT AVG(Price) FROM Products);
```

**Average with calculations:**
```sql
SELECT AVG(Price * Quantity) AS AverageOrderValue
FROM OrderDetails;
```

**Conditional average using CASE:**
```sql
SELECT 
    AVG(CASE WHEN Price > 20 THEN Price END) AS AvgExpensive,
    AVG(CASE WHEN Price <= 20 THEN Price END) AS AvgCheap
FROM Products;
```

## Related Concepts
- [[SQL Aggregate Functions]] - Family of calculation functions
- [[SQL COUNT Function]] - Count records
- [[SQL SUM Function]] - Calculate totals
- [[SQL MIN and MAX Functions]] - Find extremes
- [[SQL GROUP BY]] - Calculate averages for groups
- [[SQL Window Functions]] - Advanced average calculations
- [[SQL ROUND Function]] - Format decimal results

Essential for statistical analysis and data insights in [[SQL (Structured Query Language)]] and [[SQL Queries]].
