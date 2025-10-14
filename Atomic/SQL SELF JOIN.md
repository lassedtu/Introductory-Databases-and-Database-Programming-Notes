A `SELF JOIN` is a regular [[SQL JOIN]] in which a table is joined with itself. This is useful for comparing rows within the same table or finding hierarchical relationships.

## Syntax
```sql
SELECT a.column_name, b.column_name
FROM table1 a, table1 b
WHERE condition;

-- Or using explicit JOIN syntax (preferred)
SELECT a.column_name, b.column_name
FROM table1 a
JOIN table1 b ON condition;
```

## Key Concepts
- Must use [[SQL Aliases]] to distinguish between the two instances of the same table
- Can use any type of JOIN (INNER, LEFT, RIGHT, FULL OUTER)
- Commonly used for hierarchical data and comparisons within the same dataset

## Examples

### Employee-Manager Relationships
**Find employees and their managers:**
```sql
SELECT e.FirstName + ' ' + e.LastName AS Employee,
       m.FirstName + ' ' + m.LastName AS Manager
FROM Employees e
INNER JOIN Employees m ON e.ReportsTo = m.EmployeeID;
```

**Include employees without managers:**
```sql
SELECT e.FirstName + ' ' + e.LastName AS Employee,
       COALESCE(m.FirstName + ' ' + m.LastName, 'No Manager') AS Manager
FROM Employees e
LEFT JOIN Employees m ON e.ReportsTo = m.EmployeeID;
```

### Comparing Records Within Same Table

**Find customers from the same city:**
```sql
SELECT DISTINCT a.CustomerName AS Customer1,
                b.CustomerName AS Customer2,
                a.City
FROM Customers a
JOIN Customers b ON a.City = b.City
WHERE a.CustomerID < b.CustomerID  -- Avoid duplicates and self-matches
ORDER BY a.City;
```

**Find products with similar prices:**
```sql
SELECT a.ProductName AS Product1,
       b.ProductName AS Product2,
       a.Price
FROM Products a
JOIN Products b ON ABS(a.Price - b.Price) <= 5  -- Within $5 of each other
WHERE a.ProductID < b.ProductID
ORDER BY a.Price;
```

### Hierarchical Queries

**Organization chart (multi-level):**
```sql
-- Find all employees and their management chain
WITH EmployeeHierarchy AS (
    -- Base case: Top-level managers
    SELECT EmployeeID, FirstName, LastName, ReportsTo, 
           FirstName + ' ' + LastName AS ManagerChain,
           0 AS Level
    FROM Employees 
    WHERE ReportsTo IS NULL
    
    UNION ALL
    
    -- Recursive case: Add subordinates
    SELECT e.EmployeeID, e.FirstName, e.LastName, e.ReportsTo,
           eh.ManagerChain + ' -> ' + e.FirstName + ' ' + e.LastName,
           eh.Level + 1
    FROM Employees e
    INNER JOIN EmployeeHierarchy eh ON e.ReportsTo = eh.EmployeeID
)
SELECT * FROM EmployeeHierarchy ORDER BY Level, LastName;
```

### Finding Sequences and Patterns

**Consecutive dates:**
```sql
-- Find orders placed on consecutive days
SELECT a.OrderID AS Order1,
       b.OrderID AS Order2,
       a.OrderDate AS Date1,
       b.OrderDate AS Date2
FROM Orders a
JOIN Orders b ON DATEDIFF(day, a.OrderDate, b.OrderDate) = 1
ORDER BY a.OrderDate;
```

**Customer referral chains:**
```sql
-- If customers table has ReferredBy column
SELECT referrer.CustomerName AS Referrer,
       referred.CustomerName AS Referred
FROM Customers referrer
JOIN Customers referred ON referrer.CustomerID = referred.ReferredBy;
```

### Data Quality Checks

**Find potential duplicate customers:**
```sql
SELECT a.CustomerID AS ID1,
       b.CustomerID AS ID2,
       a.CustomerName,
       a.Phone,
       a.Email
FROM Customers a
JOIN Customers b ON (
    a.CustomerName = b.CustomerName OR 
    a.Phone = b.Phone OR 
    a.Email = b.Email
)
WHERE a.CustomerID < b.CustomerID;  -- Avoid showing same pair twice
```

**Inconsistent data detection:**
```sql
-- Find products with same name but different prices
SELECT DISTINCT a.ProductName,
                a.Price AS Price1,
                b.Price AS Price2
FROM Products a
JOIN Products b ON a.ProductName = b.ProductName
WHERE a.Price != b.Price
  AND a.ProductID < b.ProductID;
```

## Advanced Self-Join Patterns

### Running Comparisons
```sql
-- Compare each order with previous order for same customer
SELECT curr.CustomerID,
       prev.OrderDate AS PreviousOrder,
       curr.OrderDate AS CurrentOrder,
       DATEDIFF(day, prev.OrderDate, curr.OrderDate) AS DaysBetween
FROM Orders curr
JOIN Orders prev ON curr.CustomerID = prev.CustomerID
                AND curr.OrderDate > prev.OrderDate
WHERE NOT EXISTS (
    SELECT 1 FROM Orders middle
    WHERE middle.CustomerID = curr.CustomerID
      AND middle.OrderDate > prev.OrderDate
      AND middle.OrderDate < curr.OrderDate
);
```

### Ranking Without Window Functions
```sql
-- Find rank of each product by price (before ROW_NUMBER was available)
SELECT p1.ProductName,
       p1.Price,
       COUNT(p2.ProductID) + 1 AS PriceRank
FROM Products p1
LEFT JOIN Products p2 ON p2.Price > p1.Price
GROUP BY p1.ProductID, p1.ProductName, p1.Price
ORDER BY PriceRank;
```

## Performance Considerations
- Self-joins can be expensive on large tables
- Always use appropriate indexes on join columns
- Consider using CTEs or window functions for complex hierarchical queries
- Be careful with the join condition to avoid Cartesian products
- Use `WHERE a.ID < b.ID` pattern to avoid duplicate pairs

## Common Pitfalls
- Forgetting to use aliases (will cause errors)
- Creating accidental Cartesian products
- Not handling NULL values properly in hierarchical data
- Showing duplicate pairs (A-B and B-A)

## Related Concepts
- [[SQL Aliases]] - Essential for distinguishing table instances
- [[SQL JOIN]] - Foundation concept
- [[SQL INNER JOIN]] - Most common type used with self-joins
- [[SQL LEFT JOIN]] - Useful for including unmatched records
- [[SQL Hierarchical Queries]] - Advanced tree traversal
- [[SQL Common Table Expressions (CTE)]] - Better for complex hierarchies
- [[SQL Window Functions]] - Modern alternative for some self-join patterns

Powerful technique for analyzing relationships within single tables in [[SQL Queries]] and [[SQL (Structured Query Language)]].
