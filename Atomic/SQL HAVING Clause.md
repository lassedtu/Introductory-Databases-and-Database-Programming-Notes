The `HAVING` clause is used to filter groups created by [[SQL GROUP BY]] statements. It's similar to the [[SQL WHERE Clause]], but WHERE filters individual rows while HAVING filters groups after aggregation.

## Syntax
```sql
SELECT column_name(s), aggregate_function(column_name)
FROM table_name
WHERE condition
GROUP BY column_name(s)
HAVING aggregate_condition
ORDER BY column_name(s);
```

## Key Differences: WHERE vs HAVING

| WHERE | HAVING |
|-------|--------|
| Filters individual rows | Filters groups |
| Applied before GROUP BY | Applied after GROUP BY |
| Cannot use aggregate functions | Can use aggregate functions |
| Processes individual records | Processes grouped results |

## Basic Examples

**Countries with more than 5 customers:**
```sql
SELECT Country, COUNT(*) AS CustomerCount
FROM Customers
GROUP BY Country
HAVING COUNT(*) > 5
ORDER BY CustomerCount DESC;
```

**Categories with average price above $25:**
```sql
SELECT CategoryID, AVG(Price) AS AveragePrice
FROM Products
GROUP BY CategoryID
HAVING AVG(Price) > 25;
```

**Customers who have spent more than $10,000:**
```sql
SELECT CustomerID, SUM(od.UnitPrice * od.Quantity) AS TotalSpent
FROM Orders o
JOIN OrderDetails od ON o.OrderID = od.OrderID
GROUP BY CustomerID
HAVING SUM(od.UnitPrice * od.Quantity) > 10000
ORDER BY TotalSpent DESC;
```

## Complex HAVING Conditions

**Multiple conditions with AND/OR:**
```sql
SELECT CategoryID, 
       COUNT(*) AS ProductCount,
       AVG(Price) AS AvgPrice,
       MAX(Price) AS MaxPrice
FROM Products
GROUP BY CategoryID
HAVING COUNT(*) >= 5 
   AND AVG(Price) > 20
   AND MAX(Price) < 100
ORDER BY AvgPrice DESC;
```

**Range conditions:**
```sql
-- Suppliers with 2-10 products
SELECT SupplierID, COUNT(*) AS ProductCount
FROM Products
GROUP BY SupplierID
HAVING COUNT(*) BETWEEN 2 AND 10;
```

**Pattern matching on aggregates:**
```sql
-- Cities where customer count ends in 5
SELECT City, COUNT(*) AS CustomerCount
FROM Customers
GROUP BY City
HAVING CAST(COUNT(*) AS VARCHAR) LIKE '%5';
```

## HAVING with Different Aggregate Functions

### Using COUNT
```sql
-- Customers with more than 10 orders
SELECT CustomerID, COUNT(*) AS OrderCount
FROM Orders
GROUP BY CustomerID
HAVING COUNT(*) > 10;
```

### Using SUM
```sql
-- Products with total orders over 1000 units
SELECT ProductID, SUM(Quantity) AS TotalOrdered
FROM OrderDetails
GROUP BY ProductID
HAVING SUM(Quantity) > 1000;
```

### Using AVG
```sql
-- Customers with above-average order values
SELECT CustomerID, AVG(od.UnitPrice * od.Quantity) AS AvgOrderValue
FROM Orders o
JOIN OrderDetails od ON o.OrderID = od.OrderID
GROUP BY CustomerID
HAVING AVG(od.UnitPrice * od.Quantity) > (
    SELECT AVG(UnitPrice * Quantity) FROM OrderDetails
);
```

### Using MIN/MAX
```sql
-- Countries where the cheapest product costs more than $10
SELECT c.Country, MIN(p.Price) AS CheapestProduct
FROM Customers c
JOIN Orders o ON c.CustomerID = o.CustomerID
JOIN OrderDetails od ON o.OrderID = od.OrderID
JOIN Products p ON od.ProductID = p.ProductID
GROUP BY c.Country
HAVING MIN(p.Price) > 10;
```

## Combining WHERE and HAVING

```sql
-- Active customers from Germany who spent more than €5000 in 2023
SELECT c.CustomerID, 
       c.CustomerName,
       SUM(od.UnitPrice * od.Quantity) AS TotalSpent
FROM Customers c
JOIN Orders o ON c.CustomerID = o.CustomerID
JOIN OrderDetails od ON o.OrderID = od.OrderID
WHERE c.Country = 'Germany'                    -- Filter before grouping
  AND YEAR(o.OrderDate) = 2023
  AND c.Status = 'Active'
GROUP BY c.CustomerID, c.CustomerName
HAVING SUM(od.UnitPrice * od.Quantity) > 5000  -- Filter after grouping
ORDER BY TotalSpent DESC;
```

## Advanced HAVING Examples

**Time-based analysis:**
```sql
-- Months with more orders than previous month
SELECT YEAR(OrderDate) AS Year,
       MONTH(OrderDate) AS Month,
       COUNT(*) AS OrderCount
FROM Orders
GROUP BY YEAR(OrderDate), MONTH(OrderDate)
HAVING COUNT(*) > (
    SELECT COUNT(*)
    FROM Orders o2
    WHERE YEAR(o2.OrderDate) = YEAR(Orders.OrderDate)
      AND MONTH(o2.OrderDate) = MONTH(Orders.OrderDate) - 1
);
```

**Statistical filtering:**
```sql
-- Products with sales significantly above average
SELECT ProductID, 
       SUM(Quantity) AS TotalSold,
       AVG(UnitPrice) AS AvgPrice
FROM OrderDetails
GROUP BY ProductID
HAVING SUM(Quantity) > (
    SELECT AVG(ProductTotal) * 1.5  -- 50% above average
    FROM (
        SELECT SUM(Quantity) AS ProductTotal
        FROM OrderDetails
        GROUP BY ProductID
    ) AS ProductSales
);
```

**Business rules enforcement:**
```sql
-- Categories that meet minimum diversity requirements
SELECT CategoryID,
       COUNT(DISTINCT SupplierID) AS SupplierCount,
       COUNT(*) AS ProductCount,
       AVG(Price) AS AvgPrice
FROM Products
GROUP BY CategoryID
HAVING COUNT(DISTINCT SupplierID) >= 3  -- At least 3 different suppliers
   AND COUNT(*) >= 5                    -- At least 5 products
   AND AVG(Price) BETWEEN 10 AND 100;   -- Average price in reasonable range
```

## Common Patterns

**Top N analysis:**
```sql
-- Top 5 customers by order count
SELECT TOP 5 CustomerID, COUNT(*) AS OrderCount
FROM Orders
GROUP BY CustomerID
HAVING COUNT(*) >= ALL (
    SELECT COUNT(*)
    FROM Orders
    GROUP BY CustomerID
    HAVING COUNT(*) NOT IN (
        SELECT DISTINCT TOP 4 COUNT(*)
        FROM Orders
        GROUP BY CustomerID
        ORDER BY COUNT(*) DESC
    )
)
ORDER BY OrderCount DESC;
```

**Threshold-based reporting:**
```sql
-- Alert: Suppliers with declining product availability
SELECT SupplierID,
       AVG(UnitsInStock) AS AvgStock,
       COUNT(*) AS ProductCount
FROM Products
GROUP BY SupplierID
HAVING AVG(UnitsInStock) < 10         -- Low average stock
   AND COUNT(*) > 5                   -- Significant product portfolio
   AND MAX(UnitsInStock) < 50;        -- Even highest stock is concerning
```

## Performance Tips
- Indexes on GROUP BY columns improve performance
- HAVING conditions are evaluated after grouping (can't use indexes directly)
- Consider moving conditions to WHERE clause when possible
- Use appropriate aggregate functions for the data type

## Common Mistakes
- Using HAVING without GROUP BY
- Putting non-aggregate conditions in HAVING instead of WHERE
- Forgetting that HAVING works on groups, not individual rows
- Using column aliases from SELECT in HAVING (not all databases support this)

## Related Concepts
- [[SQL GROUP BY]] - Creates groups that HAVING filters
- [[SQL WHERE Clause]] - Filters individual rows before grouping
- [[SQL Aggregate Functions]] - Used in HAVING conditions
- [[SQL Subqueries]] - Can be used in HAVING conditions
- [[SQL ORDER BY]] - Applied after HAVING filtering

Essential for advanced data filtering and analysis in [[SQL Queries]] and [[SQL (Structured Query Language)]].
