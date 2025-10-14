The `MIN()` and `MAX()` functions return the smallest and largest values in a selected column, respectively. These aggregate functions are useful for finding extremes in your data.

## Syntax
```sql
SELECT MIN(column_name) FROM table_name WHERE condition;
SELECT MAX(column_name) FROM table_name WHERE condition;
```

## Examples

**Find lowest price:**
```sql
SELECT MIN(Price) AS SmallestPrice 
FROM Products;
```

**Find highest price:**
```sql
SELECT MAX(Price) AS LargestPrice 
FROM Products;
```

**Combine with other columns:**
```sql
SELECT CategoryID, MIN(Price) AS LowestPrice, MAX(Price) AS HighestPrice
FROM Products
GROUP BY CategoryID;
```

**Find product with minimum price:**
```sql
SELECT ProductName, Price
FROM Products
WHERE Price = (SELECT MIN(Price) FROM Products);
```

## Data Type Compatibility
- **Numeric**: Returns actual min/max values
- **Text**: Returns alphabetically first/last values  
- **Date**: Returns earliest/latest dates

## Examples by Data Type

**Text columns:**
```sql
SELECT MIN(ProductName), MAX(ProductName) 
FROM Products;
-- Returns alphabetically first and last product names
```

**Date columns:**
```sql
SELECT MIN(OrderDate) AS EarliestOrder, 
       MAX(OrderDate) AS LatestOrder
FROM Orders;
```

## Related Concepts
- [[SQL Aggregate Functions]] - Family of calculation functions
- [[SQL COUNT Function]] - Count records
- [[SQL SUM Function]] - Calculate totals
- [[SQL AVG Function]] - Calculate averages
- [[SQL GROUP BY]] - Calculate min/max for groups
- [[SQL Subqueries]] - Use min/max values in other queries

Essential tools for data analysis in [[SQL (Structured Query Language)]] and [[SQL Queries]].
