Aggregate functions perform calculations on multiple rows of a table's column and return a single value. They are commonly used with the `GROUP BY` clause to perform calculations on each group of rows.

## Common Aggregate Functions

| Function | Description | Example |
|----------|-------------|---------|
| COUNT() | Returns the number of rows | `SELECT COUNT(*) FROM Customers;` |
| SUM() | Returns the sum of numeric values | `SELECT SUM(Price) FROM Products;` |
| AVG() | Returns the average value | `SELECT AVG(Price) FROM Products;` |
| MIN() | Returns the smallest value | `SELECT MIN(Price) FROM Products;` |
| MAX() | Returns the largest value | `SELECT MAX(Price) FROM Products;` |

## Examples

**Count total customers:**
```sql
SELECT COUNT(*) AS TotalCustomers 
FROM Customers;
```

**Find average product price:**
```sql
SELECT AVG(Price) AS AveragePrice 
FROM Products;
```

**Multiple aggregates:**
```sql
SELECT COUNT(*) as ProductCount,
       AVG(Price) as AvgPrice,
       MIN(Price) as MinPrice,
       MAX(Price) as MaxPrice
FROM Products;
```

## Important Notes
- Aggregate functions ignore NULL values (except COUNT(*))
- Cannot be used in WHERE clause directly (use HAVING instead)
- Often used with GROUP BY to calculate aggregates for each group

## Related Concepts
- [[SQL COUNT Function]] - Count rows or non-null values
- [[SQL SUM Function]] - Calculate totals
- [[SQL AVG Function]] - Calculate averages  
- [[SQL MIN and MAX Functions]] - Find minimum and maximum values
- [[SQL GROUP BY]] - Group data for aggregate calculations
- [[SQL HAVING Clause]] - Filter groups based on aggregate conditions

Core component of [[SQL Queries]] and data analysis in [[SQL (Structured Query Language)]].
