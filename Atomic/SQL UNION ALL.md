The `UNION ALL` operator combines the result-set of two or more [[SQL SELECT Statement]]s, including all duplicate rows. Unlike [[SQL UNION]], it does not remove duplicates, making it faster for large datasets.

## Syntax
```sql
SELECT column_name(s) FROM table1
UNION ALL
SELECT column_name(s) FROM table2;
```

## Key Differences from UNION

| Feature | UNION | UNION ALL |
|---------|-------|-----------|
| Duplicate handling | Removes duplicates | Keeps all rows |
| Performance | Slower (sorting required) | Faster (no duplicate check) |
| Memory usage | Higher (for sorting) | Lower |
| Use case | When duplicates matter | When all rows needed |

## Examples

**All customer and supplier cities (with duplicates):**
```sql
SELECT City, 'Customer' AS Source FROM Customers
UNION ALL
SELECT City, 'Supplier' AS Source FROM Suppliers
ORDER BY City;
```

**Complete transaction history:**
```sql
SELECT TransactionDate, Amount, 'Sale' AS Type
FROM Sales
UNION ALL
SELECT TransactionDate, Amount, 'Refund' AS Type  
FROM Refunds
UNION ALL
SELECT TransactionDate, Amount, 'Adjustment' AS Type
FROM Adjustments
ORDER BY TransactionDate DESC;
```

## Performance Benefits

**Large dataset combination:**
```sql
-- Faster - no duplicate removal overhead
SELECT OrderID, CustomerID, OrderDate FROM Orders2023
UNION ALL
SELECT OrderID, CustomerID, OrderDate FROM Orders2024
UNION ALL  
SELECT OrderID, CustomerID, OrderDate FROM Orders2025;

-- vs slower UNION version
SELECT OrderID, CustomerID, OrderDate FROM Orders2023
UNION
SELECT OrderID, CustomerID, OrderDate FROM Orders2024
UNION
SELECT OrderID, CustomerID, OrderDate FROM Orders2025;
```

## Practical Applications

**Data aggregation across time periods:**
```sql
SELECT 'Q1' AS Quarter, SUM(Amount) AS Total
FROM Sales WHERE QUARTER(SaleDate) = 1
UNION ALL
SELECT 'Q2' AS Quarter, SUM(Amount) AS Total
FROM Sales WHERE QUARTER(SaleDate) = 2
UNION ALL
SELECT 'Q3' AS Quarter, SUM(Amount) AS Total
FROM Sales WHERE QUARTER(SaleDate) = 3
UNION ALL
SELECT 'Q4' AS Quarter, SUM(Amount) AS Total
FROM Sales WHERE QUARTER(SaleDate) = 4;
```

**Audit trail creation:**
```sql
SELECT 'INSERT' AS Action, 
       ProductID, 
       ProductName, 
       GETDATE() AS ActionDate
FROM ProductsNew
UNION ALL
SELECT 'UPDATE' AS Action,
       ProductID,
       ProductName,
       GETDATE() AS ActionDate  
FROM ProductsModified
UNION ALL
SELECT 'DELETE' AS Action,
       ProductID,
       ProductName,
       GETDATE() AS ActionDate
FROM ProductsDeleted;
```

**Multi-source reporting:**
```sql
-- Combine data from different regional databases
SELECT CustomerName, OrderTotal, 'North' AS Region
FROM NorthRegion.Orders
UNION ALL
SELECT CustomerName, OrderTotal, 'South' AS Region  
FROM SouthRegion.Orders
UNION ALL
SELECT CustomerName, OrderTotal, 'East' AS Region
FROM EastRegion.Orders
UNION ALL
SELECT CustomerName, OrderTotal, 'West' AS Region
FROM WestRegion.Orders;
```

## When to Use UNION ALL

### Choose UNION ALL when:
- You need all rows, including duplicates
- Performance is critical
- Working with large datasets
- Combining partitioned data
- Creating audit trails
- You know duplicates don't exist

### Choose UNION when:
- Duplicates must be removed
- Data quality is more important than performance
- Working with smaller datasets
- Creating unique lists

## Memory and Performance Considerations

```sql
-- Efficient for data warehousing
SELECT ProductID, SalesAmount, '2023' AS Year
FROM Sales2023
UNION ALL
SELECT ProductID, SalesAmount, '2024' AS Year  
FROM Sales2024
UNION ALL
SELECT ProductID, SalesAmount, '2025' AS Year
FROM Sales2025;

-- This creates a complete dataset without duplicate removal overhead
```

## Data Validation Example

**Check for data consistency:**
```sql
-- Find all records to verify totals
SELECT 'Orders' AS TableName, COUNT(*) AS RecordCount
FROM Orders
UNION ALL
SELECT 'OrderDetails' AS TableName, COUNT(*) AS RecordCount
FROM OrderDetails
UNION ALL  
SELECT 'Products' AS TableName, COUNT(*) AS RecordCount
FROM Products
UNION ALL
SELECT 'Customers' AS TableName, COUNT(*) AS RecordCount
FROM Customers;
```

## Creating Summary Reports

**Detailed financial summary:**
```sql
SELECT 'Revenue' AS Category, 
       SUM(Amount) AS Total,
       'Actual' AS Type
FROM Sales
UNION ALL
SELECT 'Expenses' AS Category,
       SUM(Amount) AS Total,
       'Actual' AS Type
FROM Expenses  
UNION ALL
SELECT 'Profit' AS Category,
       (SELECT SUM(Amount) FROM Sales) - (SELECT SUM(Amount) FROM Expenses) AS Total,
       'Calculated' AS Type;
```

## Best Practices
- Use UNION ALL when you know duplicates don't matter
- Always specify column aliases for clarity
- Use ORDER BY only at the final level
- Consider indexing on commonly filtered columns
- Test performance differences with your data volumes
- Document why UNION ALL was chosen over UNION

## Common Patterns

**Time series data combination:**
```sql
SELECT Date, Value, 'Daily' AS Granularity FROM DailyMetrics
UNION ALL  
SELECT Date, Value, 'Weekly' AS Granularity FROM WeeklyMetrics
UNION ALL
SELECT Date, Value, 'Monthly' AS Granularity FROM MonthlyMetrics;
```

**Multi-tenant data access:**
```sql
SELECT * FROM TenantA.Orders
UNION ALL
SELECT * FROM TenantB.Orders  
UNION ALL
SELECT * FROM TenantC.Orders
WHERE CustomerRegion = @UserRegion;
```

## Related Concepts
- [[SQL UNION]] - Removes duplicate rows
- [[SQL SELECT Statement]] - Foundation for UNION ALL operations
- [[SQL Performance Optimization]] - UNION ALL performance benefits
- [[SQL Data Warehousing]] - Common use case
- [[SQL Partitioning]] - Often used with partitioned data

Essential for efficient data combination in [[SQL Queries]] and [[SQL (Structured Query Language)]].
