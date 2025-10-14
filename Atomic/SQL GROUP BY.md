The `GROUP BY` statement groups rows that have the same values into summary rows. It's typically used with [[SQL Aggregate Functions]] to perform calculations on each group of data.

## Syntax
```sql
SELECT column_name(s), aggregate_function(column_name)
FROM table_name
WHERE condition
GROUP BY column_name(s)
ORDER BY column_name(s);
```

## Basic Examples

**Count customers by country:**
```sql
SELECT Country, COUNT(*) AS CustomerCount
FROM Customers
GROUP BY Country
ORDER BY CustomerCount DESC;
```

**Average product price by category:**
```sql
SELECT CategoryID, AVG(Price) AS AveragePrice
FROM Products
GROUP BY CategoryID;
```

**Total sales by customer:**
```sql
SELECT CustomerID, SUM(od.UnitPrice * od.Quantity) AS TotalSpent
FROM Orders o
JOIN OrderDetails od ON o.OrderID = od.OrderID
GROUP BY CustomerID
ORDER BY TotalSpent DESC;
```

## Multiple Column Grouping

**Sales by country and city:**
```sql
SELECT Country, City, COUNT(*) AS CustomerCount
FROM Customers
GROUP BY Country, City
ORDER BY Country, City;
```

**Orders by year and month:**
```sql
SELECT YEAR(OrderDate) AS OrderYear,
       MONTH(OrderDate) AS OrderMonth,
       COUNT(*) AS OrderCount,
       SUM(od.UnitPrice * od.Quantity) AS MonthlyTotal
FROM Orders o
JOIN OrderDetails od ON o.OrderID = od.OrderID
GROUP BY YEAR(OrderDate), MONTH(OrderDate)
ORDER BY OrderYear, OrderMonth;
```

## Common Aggregate Functions with GROUP BY

### COUNT
```sql
-- Count orders per customer
SELECT CustomerID, COUNT(*) AS OrderCount
FROM Orders
GROUP BY CustomerID;
```

### SUM
```sql
-- Total quantity ordered per product
SELECT ProductID, SUM(Quantity) AS TotalOrdered
FROM OrderDetails
GROUP BY ProductID;
```

### AVG
```sql
-- Average order value per customer
SELECT CustomerID, AVG(od.UnitPrice * od.Quantity) AS AvgOrderValue
FROM Orders o
JOIN OrderDetails od ON o.OrderID = od.OrderID
GROUP BY CustomerID;
```

### MIN/MAX
```sql
-- First and last order dates per customer
SELECT CustomerID, 
       MIN(OrderDate) AS FirstOrder,
       MAX(OrderDate) AS LastOrder
FROM Orders
GROUP BY CustomerID;
```

## Filtering Groups with HAVING

Use [[SQL HAVING Clause]] to filter groups after grouping:

```sql
-- Countries with more than 5 customers
SELECT Country, COUNT(*) AS CustomerCount
FROM Customers
GROUP BY Country
HAVING COUNT(*) > 5
ORDER BY CustomerCount DESC;
```

```sql
-- Products with average price over $20
SELECT CategoryID, AVG(Price) AS AvgPrice
FROM Products
GROUP BY CategoryID
HAVING AVG(Price) > 20;
```

## Advanced Grouping Examples

**Complex business analysis:**
```sql
SELECT c.Country,
       COUNT(DISTINCT c.CustomerID) AS CustomerCount,
       COUNT(o.OrderID) AS TotalOrders,
       SUM(od.UnitPrice * od.Quantity) AS TotalRevenue,
       AVG(od.UnitPrice * od.Quantity) AS AvgOrderValue
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
LEFT JOIN OrderDetails od ON o.OrderID = od.OrderID
GROUP BY c.Country
HAVING SUM(od.UnitPrice * od.Quantity) > 10000
ORDER BY TotalRevenue DESC;
```

**Time-based analysis:**
```sql
-- Quarterly sales performance
SELECT YEAR(o.OrderDate) AS Year,
       CASE WHEN MONTH(o.OrderDate) IN (1,2,3) THEN 'Q1'
            WHEN MONTH(o.OrderDate) IN (4,5,6) THEN 'Q2'
            WHEN MONTH(o.OrderDate) IN (7,8,9) THEN 'Q3'
            ELSE 'Q4' END AS Quarter,
       COUNT(DISTINCT o.OrderID) AS Orders,
       SUM(od.UnitPrice * od.Quantity) AS Revenue
FROM Orders o
JOIN OrderDetails od ON o.OrderID = od.OrderID
GROUP BY YEAR(o.OrderDate), 
         CASE WHEN MONTH(o.OrderDate) IN (1,2,3) THEN 'Q1'
              WHEN MONTH(o.OrderDate) IN (4,5,6) THEN 'Q2'
              WHEN MONTH(o.OrderDate) IN (7,8,9) THEN 'Q3'
              ELSE 'Q4' END
ORDER BY Year, Quarter;
```

## GROUP BY with Expressions

**Grouping by calculated fields:**
```sql
-- Group products by price range
SELECT CASE 
         WHEN Price < 20 THEN 'Budget'
         WHEN Price < 50 THEN 'Standard'
         ELSE 'Premium'
       END AS PriceCategory,
       COUNT(*) AS ProductCount,
       AVG(Price) AS AvgPrice
FROM Products
GROUP BY CASE 
           WHEN Price < 20 THEN 'Budget'
           WHEN Price < 50 THEN 'Standard'
           ELSE 'Premium'
         END;
```

**Date/time grouping:**
```sql
-- Orders by day of week
SELECT DATENAME(WEEKDAY, OrderDate) AS DayOfWeek,
       COUNT(*) AS OrderCount
FROM Orders
GROUP BY DATENAME(WEEKDAY, OrderDate), DATEPART(WEEKDAY, OrderDate)
ORDER BY DATEPART(WEEKDAY, OrderDate);
```

## Important Rules and Notes

### Column Selection Rules
- Every column in SELECT must be either:
  - Listed in GROUP BY clause, OR
  - An aggregate function

```sql
-- This is WRONG:
SELECT CustomerID, CustomerName, COUNT(*)
FROM Orders o
JOIN Customers c ON o.CustomerID = c.CustomerID
GROUP BY CustomerID;  -- CustomerName not in GROUP BY

-- This is CORRECT:
SELECT CustomerID, MAX(CustomerName), COUNT(*)
FROM Orders o
JOIN Customers c ON o.CustomerID = c.CustomerID
GROUP BY CustomerID;
```

### NULL Handling
```sql
-- NULLs are grouped together
SELECT Region, COUNT(*)
FROM Customers
GROUP BY Region;  -- All NULL regions count as one group
```

### Order of Operations
1. WHERE clause filters rows before grouping
2. GROUP BY groups the filtered rows
3. Aggregate functions calculate values for each group
4. HAVING clause filters the groups
5. ORDER BY sorts the final result

## Performance Considerations
- Index columns used in GROUP BY for better performance
- Consider the order of columns in composite indexes
- Large GROUP BY operations may require temporary disk space
- Use LIMIT/TOP to restrict results when testing

## Common Mistakes
- Forgetting to include non-aggregate columns in GROUP BY
- Using WHERE instead of HAVING to filter groups
- Incorrect aggregate function usage
- Not handling NULL values properly

## Related Concepts
- [[SQL Aggregate Functions]] - Used with GROUP BY for calculations
- [[SQL HAVING Clause]] - Filter groups after grouping
- [[SQL WHERE Clause]] - Filter rows before grouping
- [[SQL ORDER BY]] - Sort grouped results
- [[SQL DISTINCT]] - Alternative for simple unique counts
- [[SQL Window Functions]] - Advanced grouping and analysis

Essential for data analysis and reporting in [[SQL Queries]] and [[SQL (Structured Query Language)]].
