The `RIGHT JOIN` keyword returns all records from the right (second) table, and the matching records from the left (first) table. If there's no match, NULL values are returned for columns from the left table.

## Syntax
```sql
SELECT column_name(s)
FROM table1
RIGHT JOIN table2
ON table1.column_name = table2.column_name;
```

## Visual Representation
```
Left Table    Right Table
┌─────────┐   ┌─────────┐
│ A   B   │   │ B   C   │
├─────────┤   ├─────────┤
│ 1   X   │   │ X   10  │ ←
│ 2   Y   │ → │ Y   20  │ ← Returns ALL from right,
│ 3   Z   │   │ W   30  │ ← matching from left
└─────────┘   └─────────┘

Result: A=1,B=X,C=10 | A=2,B=Y,C=20 | A=NULL,B=W,C=30
```

## Examples

**All orders and their customer details (including orders without valid customers):**
```sql
SELECT c.CustomerName, o.OrderID, o.OrderDate
FROM Customers c
RIGHT JOIN Orders o ON c.CustomerID = o.CustomerID
ORDER BY o.OrderDate;
```

**All products and their order details (including products never ordered):**
```sql
SELECT p.ProductName, od.Quantity, od.UnitPrice
FROM OrderDetails od
RIGHT JOIN Products p ON od.ProductID = p.ProductID;
```

## Finding Unmatched Records

**Orders without valid customers (orphaned orders):**
```sql
SELECT o.OrderID, o.OrderDate
FROM Customers c
RIGHT JOIN Orders o ON c.CustomerID = o.CustomerID
WHERE c.CustomerID IS NULL;
```

**Products that exist but were never ordered:**
```sql
SELECT p.ProductName, p.Price
FROM OrderDetails od
RIGHT JOIN Products p ON od.ProductID = p.ProductID
WHERE od.ProductID IS NULL;
```

## RIGHT JOIN vs LEFT JOIN

These queries are equivalent:

**Using RIGHT JOIN:**
```sql
SELECT c.CustomerName, o.OrderID
FROM Orders o
RIGHT JOIN Customers c ON o.CustomerID = c.CustomerID;
```

**Using LEFT JOIN (preferred):**
```sql
SELECT c.CustomerName, o.OrderID
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID;
```

## Why LEFT JOIN is Preferred

Most developers prefer LEFT JOIN because:
- More intuitive to read (main table first)
- Consistent with natural reading order
- Easier to understand the primary table
- Better aligns with query logic

**Instead of this RIGHT JOIN:**
```sql
-- Less intuitive
SELECT c.CustomerName, COUNT(o.OrderID) as OrderCount
FROM Orders o
RIGHT JOIN Customers c ON o.CustomerID = c.CustomerID
GROUP BY c.CustomerID, c.CustomerName;
```

**Use this LEFT JOIN:**
```sql
-- More intuitive
SELECT c.CustomerName, COUNT(o.OrderID) as OrderCount
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
GROUP BY c.CustomerID, c.CustomerName;
```

## When RIGHT JOIN Might Be Useful

**Existing query modification:**
```sql
-- If you already have this query
SELECT od.Quantity, od.UnitPrice
FROM OrderDetails od
WHERE od.ProductID = 1;

-- You can easily add product details with RIGHT JOIN
SELECT od.Quantity, od.UnitPrice, p.ProductName, p.Price
FROM OrderDetails od
RIGHT JOIN Products p ON od.ProductID = p.ProductID
WHERE od.ProductID = 1 OR od.ProductID IS NULL;
```

**Specific analytical patterns:**
```sql
-- Finding all possible combinations where right table is complete
SELECT e.FirstName as Employee, m.FirstName as Manager
FROM Employees e
RIGHT JOIN Employees m ON e.ReportsTo = m.EmployeeID;
```

## Multiple RIGHT JOINs
```sql
-- All products with their category and supplier info
SELECT p.ProductName, 
       c.CategoryName, 
       s.CompanyName
FROM Categories c
RIGHT JOIN Products p ON c.CategoryID = p.CategoryID
RIGHT JOIN Suppliers s ON p.SupplierID = s.SupplierID;
```

## Important Notes
- Always returns all records from the right table
- Use `IS NULL` to find unmatched records from left table
- NULL values appear in columns from the left table when no match exists
- Less commonly used than LEFT JOIN
- Can always be rewritten as LEFT JOIN by switching table order

## Database Support
- MySQL: ✓ Supported
- PostgreSQL: ✓ Supported  
- SQL Server: ✓ Supported
- SQLite: ✗ Not supported (use LEFT JOIN instead)
- Oracle: ✓ Supported

## Related Concepts
- [[SQL LEFT JOIN]] - Preferred alternative that returns all left records
- [[SQL INNER JOIN]] - Returns only matching records
- [[SQL FULL OUTER JOIN]] - Returns all records from both tables
- [[SQL JOIN]] - General concept of combining tables
- [[NULL Values]] - Understanding NULL in RIGHT JOIN results

Part of the [[SQL JOINs]] family for combining data in [[SQL Queries]] and [[SQL (Structured Query Language)]].
