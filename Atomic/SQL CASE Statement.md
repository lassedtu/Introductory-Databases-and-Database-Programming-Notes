The `CASE` statement allows you to add conditional logic to SQL queries. It works like an if-then-else statement, returning different values based on specified conditions.

## Syntax

### Simple CASE
```sql
CASE expression
    WHEN value1 THEN result1
    WHEN value2 THEN result2
    ...
    ELSE result
END
```

### Searched CASE (more flexible)
```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    ...
    ELSE result
END
```

## Basic Examples

**Categorize products by price:**
```sql
SELECT ProductName,
       Price,
       CASE
           WHEN Price < 20 THEN 'Budget'
           WHEN Price < 50 THEN 'Standard'
           ELSE 'Premium'
       END AS PriceCategory
FROM Products;
```

**Simple CASE with status codes:**
```sql
SELECT OrderID,
       CustomerID,
       CASE OrderStatus
           WHEN 1 THEN 'Pending'
           WHEN 2 THEN 'Processing'
           WHEN 3 THEN 'Shipped'
           WHEN 4 THEN 'Delivered'
           ELSE 'Unknown'
       END AS Status
FROM Orders;
```

## Advanced CASE Examples

**Complex business logic:**
```sql
SELECT CustomerName,
       Country,
       CASE
           WHEN Country IN ('USA', 'Canada') THEN 'North America'
           WHEN Country IN ('UK', 'Germany', 'France') THEN 'Europe'
           WHEN Country IN ('Brazil', 'Argentina') THEN 'South America'
           ELSE 'Other'
       END AS Region,
       CASE
           WHEN Country = 'USA' THEN 'USD'
           WHEN Country IN ('Germany', 'France') THEN 'EUR'
           WHEN Country = 'UK' THEN 'GBP'
           ELSE 'USD'
       END AS Currency
FROM Customers;
```

**Date-based conditions:**
```sql
SELECT OrderID,
       OrderDate,
       CASE
           WHEN OrderDate >= DATEADD(day, -30, GETDATE()) THEN 'Recent'
           WHEN OrderDate >= DATEADD(day, -90, GETDATE()) THEN 'This Quarter'
           WHEN OrderDate >= DATEADD(year, -1, GETDATE()) THEN 'This Year'
           ELSE 'Older'
       END AS Recency
FROM Orders;
```

## CASE in Different Clauses

### In SELECT clause
```sql
SELECT ProductName,
       UnitsInStock,
       CASE
           WHEN UnitsInStock = 0 THEN 'Out of Stock'
           WHEN UnitsInStock < 10 THEN 'Low Stock'
           ELSE 'In Stock'
       END AS StockStatus
FROM Products;
```

### In WHERE clause
```sql
SELECT * FROM Employees
WHERE CASE
        WHEN DATEDIFF(year, BirthDate, GETDATE()) < 30 THEN 'Young'
        WHEN DATEDIFF(year, BirthDate, GETDATE()) < 50 THEN 'Middle'
        ELSE 'Senior'
      END = 'Young';
```

### In ORDER BY clause
```sql
SELECT CustomerName, Country
FROM Customers
ORDER BY CASE Country
           WHEN 'USA' THEN 1
           WHEN 'Canada' THEN 2
           WHEN 'UK' THEN 3
           ELSE 4
         END,
         CustomerName;
```

### In GROUP BY clause
```sql
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

## CASE with Aggregate Functions

**Conditional counting:**
```sql
SELECT Country,
       COUNT(*) AS TotalCustomers,
       COUNT(CASE WHEN City = 'London' THEN 1 END) AS LondonCustomers,
       COUNT(CASE WHEN City = 'Berlin' THEN 1 END) AS BerlinCustomers
FROM Customers
GROUP BY Country;
```

**Conditional summing:**
```sql
SELECT ProductID,
       SUM(Quantity) AS TotalQuantity,
       SUM(CASE WHEN YEAR(OrderDate) = 2023 THEN Quantity ELSE 0 END) AS Qty2023,
       SUM(CASE WHEN YEAR(OrderDate) = 2024 THEN Quantity ELSE 0 END) AS Qty2024
FROM OrderDetails od
JOIN Orders o ON od.OrderID = o.OrderID
GROUP BY ProductID;
```

## Nested CASE Statements

```sql
SELECT CustomerName,
       Country,
       CASE
           WHEN Country = 'USA' THEN
               CASE
                   WHEN City IN ('New York', 'Los Angeles') THEN 'Major City'
                   ELSE 'Other City'
               END
           WHEN Country = 'UK' THEN
               CASE
                   WHEN City = 'London' THEN 'Capital'
                   ELSE 'Other City'
               END
           ELSE 'International'
       END AS LocationType
FROM Customers;
```

## CASE with NULL Handling

```sql
SELECT CustomerName,
       CASE
           WHEN Region IS NULL THEN 'No Region Specified'
           WHEN Region = '' THEN 'Empty Region'
           ELSE Region
       END AS CleanRegion,
       CASE
           WHEN PostalCode IS NULL OR PostalCode = '' THEN 'No Postal Code'
           ELSE PostalCode
       END AS CleanPostalCode
FROM Customers;
```

## Performance Optimization with CASE

**Avoiding multiple scans:**
```sql
-- Instead of multiple queries, use CASE for efficiency
SELECT COUNT(CASE WHEN Price < 20 THEN 1 END) AS BudgetProducts,
       COUNT(CASE WHEN Price BETWEEN 20 AND 50 THEN 1 END) AS StandardProducts,
       COUNT(CASE WHEN Price > 50 THEN 1 END) AS PremiumProducts,
       AVG(Price) AS OverallAvgPrice
FROM Products;
```

## CASE vs Other Approaches

**CASE vs Multiple UNION queries:**
```sql
-- Efficient CASE approach
SELECT 'Q1' AS Quarter, SUM(Amount) AS Sales
FROM Sales
WHERE CASE
        WHEN MONTH(SaleDate) IN (1,2,3) THEN 'Q1'
        WHEN MONTH(SaleDate) IN (4,5,6) THEN 'Q2'
        WHEN MONTH(SaleDate) IN (7,8,9) THEN 'Q3'
        ELSE 'Q4'
      END = 'Q1'

-- vs Multiple queries with UNION
SELECT 'Q1' AS Quarter, SUM(Amount) AS Sales FROM Sales WHERE MONTH(SaleDate) IN (1,2,3)
UNION ALL
SELECT 'Q2' AS Quarter, SUM(Amount) AS Sales FROM Sales WHERE MONTH(SaleDate) IN (4,5,6)
-- ... etc
```

## Data Quality and Transformation

**Data cleansing:**
```sql
SELECT CustomerID,
       CASE
           WHEN UPPER(TRIM(CustomerName)) = '' THEN 'UNKNOWN CUSTOMER'
           ELSE UPPER(TRIM(CustomerName))
       END AS CleanCustomerName,
       CASE
           WHEN Phone LIKE '[0-9][0-9][0-9]-[0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]' 
                THEN Phone
           WHEN Phone LIKE '[0-9][0-9][0-9][0-9][0-9][0-9][0-9][0-9][0-9][0-9]'
                THEN SUBSTRING(Phone,1,3) + '-' + SUBSTRING(Phone,4,3) + '-' + SUBSTRING(Phone,7,4)
           ELSE 'INVALID PHONE'
       END AS FormattedPhone
FROM Customers;
```

## Best Practices
- Always include an ELSE clause to handle unexpected values
- Use meaningful names for calculated columns
- Consider performance impact of complex CASE logic
- Use simple CASE when comparing against literal values
- Use searched CASE for complex conditions
- Avoid deeply nested CASE statements (consider lookup tables instead)

## Common Use Cases
- Data categorization and segmentation
- Status and flag interpretation
- Data transformation and cleansing
- Conditional aggregation
- Report formatting
- Business rule implementation

## Related Concepts
- [[SQL IF Statement]] - Database-specific conditional logic
- [[SQL COALESCE Function]] - Handle NULL values
- [[SQL IIF Function]] - Simple conditional expression (SQL Server)
- [[SQL Conditional Functions]] - Other conditional operators
- [[SQL Aggregate Functions]] - Often used with CASE
- [[SQL Subqueries]] - Can contain CASE statements

Essential tool for adding conditional logic to [[SQL Queries]] and [[SQL (Structured Query Language)]].
