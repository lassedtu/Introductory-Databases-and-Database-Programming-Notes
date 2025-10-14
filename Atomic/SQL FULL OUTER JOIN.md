The `FULL OUTER JOIN` keyword returns all records when there is a match in either left or right table. It combines the results of both [[SQL LEFT JOIN]] and [[SQL RIGHT JOIN]].

## Syntax
```sql
SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2
ON table1.column_name = table2.column_name;
```

## Visual Representation
```
Left Table    Right Table
┌─────────┐   ┌─────────┐
│ A   B   │   │ B   C   │
├─────────┤   ├─────────┤
│ 1   X   │ ← │ X   10  │ → Returns ALL from both tables
│ 2   Y   │ ← │ Y   20  │ → with NULLs where no match
│ 3   Z   │ ← │ W   30  │ ←
└─────────┘   └─────────┘

Result: A=1,B=X,C=10 | A=2,B=Y,C=20 | A=3,B=Z,C=NULL | A=NULL,B=W,C=30
```

## Examples

**All customers and all orders (whether matched or not):**
```sql
SELECT c.CustomerName, o.OrderID, o.OrderDate
FROM Customers c
FULL OUTER JOIN Orders o ON c.CustomerID = o.CustomerID
ORDER BY c.CustomerName, o.OrderDate;
```

**Complete inventory analysis:**
```sql
SELECT COALESCE(p.ProductName, 'Unknown Product') as Product,
       COALESCE(od.Quantity, 0) as Ordered,
       COALESCE(p.UnitsInStock, 0) as InStock
FROM Products p
FULL OUTER JOIN OrderDetails od ON p.ProductID = od.ProductID;
```

## Finding All Unmatched Records

**Records that exist in either table but not both:**
```sql
SELECT c.CustomerName, o.OrderID
FROM Customers c
FULL OUTER JOIN Orders o ON c.CustomerID = o.CustomerID
WHERE c.CustomerID IS NULL OR o.CustomerID IS NULL;
```

**Data quality check - mismatched foreign keys:**
```sql
-- Find orphaned orders and customers without orders
SELECT CASE 
         WHEN c.CustomerID IS NULL THEN 'Orphaned Order: ' + CAST(o.OrderID AS VARCHAR)
         WHEN o.CustomerID IS NULL THEN 'Customer without orders: ' + c.CustomerName
       END AS DataIssue
FROM Customers c
FULL OUTER JOIN Orders o ON c.CustomerID = o.CustomerID
WHERE c.CustomerID IS NULL OR o.CustomerID IS NULL;
```

## Simulating FULL OUTER JOIN

For databases that don't support FULL OUTER JOIN (like MySQL), use UNION:

```sql
-- MySQL alternative using UNION
SELECT c.CustomerName, o.OrderID
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID

UNION

SELECT c.CustomerName, o.OrderID
FROM Customers c
RIGHT JOIN Orders o ON c.CustomerID = o.CustomerID
WHERE c.CustomerID IS NULL;
```

## Advanced Examples

**Complete sales analysis:**
```sql
SELECT COALESCE(c.CustomerName, 'Unknown Customer') as Customer,
       COUNT(o.OrderID) as OrderCount,
       COALESCE(SUM(od.Quantity * od.UnitPrice), 0) as TotalSpent
FROM Customers c
FULL OUTER JOIN Orders o ON c.CustomerID = o.CustomerID
FULL OUTER JOIN OrderDetails od ON o.OrderID = od.OrderID
GROUP BY c.CustomerID, c.CustomerName
ORDER BY TotalSpent DESC;
```

**Comparing two time periods:**
```sql
SELECT COALESCE(q1.ProductID, q2.ProductID) as ProductID,
       COALESCE(q1.Q1Sales, 0) as Q1Sales,
       COALESCE(q2.Q2Sales, 0) as Q2Sales,
       COALESCE(q2.Q2Sales, 0) - COALESCE(q1.Q1Sales, 0) as GrowthChange
FROM (
    -- Q1 Sales
    SELECT p.ProductID, SUM(od.Quantity * od.UnitPrice) as Q1Sales
    FROM Products p
    JOIN OrderDetails od ON p.ProductID = od.ProductID
    JOIN Orders o ON od.OrderID = o.OrderID
    WHERE QUARTER(o.OrderDate) = 1
    GROUP BY p.ProductID
) q1
FULL OUTER JOIN (
    -- Q2 Sales
    SELECT p.ProductID, SUM(od.Quantity * od.UnitPrice) as Q2Sales
    FROM Products p
    JOIN OrderDetails od ON p.ProductID = od.ProductID
    JOIN Orders o ON od.OrderID = o.OrderID
    WHERE QUARTER(o.OrderDate) = 2
    GROUP BY p.ProductID
) q2 ON q1.ProductID = q2.ProductID;
```

## COALESCE Function Usage

FULL OUTER JOIN often pairs with COALESCE to handle NULL values:

```sql
SELECT COALESCE(c.CustomerName, 'No Customer') as CustomerName,
       COALESCE(o.OrderDate, 'No Order') as OrderDate,
       COALESCE(c.City, 'Unknown') as City
FROM Customers c
FULL OUTER JOIN Orders o ON c.CustomerID = o.CustomerID;
```

## Database Support

| Database | Support | Alternative |
|----------|---------|-------------|
| SQL Server | ✓ FULL OUTER JOIN | - |
| PostgreSQL | ✓ FULL OUTER JOIN | - |
| Oracle | ✓ FULL OUTER JOIN | - |
| MySQL | ✗ Not supported | UNION of LEFT and RIGHT JOIN |
| SQLite | ✗ Not supported | UNION of LEFT and RIGHT JOIN |

## Performance Considerations
- Most expensive type of JOIN
- Returns potentially large result sets
- Consider if you actually need all unmatched records
- Use appropriate WHERE clauses to filter results
- Ensure proper indexing on join columns

## Common Use Cases
- Data reconciliation between systems
- Finding gaps or inconsistencies in data
- Complete reporting where all entities must be shown
- Merging datasets from different sources
- Audit trails and data quality checks

## Related Concepts
- [[SQL LEFT JOIN]] - Returns all left table records + matches
- [[SQL RIGHT JOIN]] - Returns all right table records + matches  
- [[SQL INNER JOIN]] - Returns only matching records
- [[SQL UNION]] - Alternative method for unsupported databases
- [[SQL COALESCE Function]] - Handle NULL values in results
- [[NULL Values]] - Understanding NULL handling in FULL OUTER JOIN

Essential for comprehensive data analysis in [[SQL Queries]] and [[SQL (Structured Query Language)]].
