The `LEFT JOIN` keyword returns all records from the left (first) table, and the matching records from the right (second) table. If there's no match, NULL values are returned for columns from the right table.

## Syntax
```sql
SELECT column_name(s)
FROM table1
LEFT JOIN table2
ON table1.column_name = table2.column_name;
```

## Visual Representation
```
Left Table    Right Table
┌─────────┐   ┌─────────┐
│ A   B   │   │ B   C   │
├─────────┤   ├─────────┤
│ 1   X   │   │ X   10  │
│ 2   Y   │ ← │ Y   20  │ → Returns ALL from left,
│ 3   Z   │   │ W   30  │   matching from right
└─────────┘   └─────────┘

Result: A=1,B=X,C=NULL | A=2,B=Y,C=20 | A=3,B=Z,C=NULL
```

## Examples

**All customers and their orders (including customers with no orders):**
```sql
SELECT c.CustomerName, o.OrderID, o.OrderDate
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
ORDER BY c.CustomerName;
```

**Count orders per customer (including customers with 0 orders):**
```sql
SELECT c.CustomerName, COUNT(o.OrderID) AS OrderCount
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
GROUP BY c.CustomerID, c.CustomerName
ORDER BY OrderCount DESC;
```

## Finding Records That Don't Match

**Customers who have never placed an order:**
```sql
SELECT c.CustomerName
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
WHERE o.CustomerID IS NULL;
```

**Products that have never been ordered:**
```sql
SELECT p.ProductName
FROM Products p
LEFT JOIN OrderDetails od ON p.ProductID = od.ProductID
WHERE od.ProductID IS NULL;
```

## Multiple LEFT JOINs
```sql
SELECT c.CustomerName, 
       o.OrderDate, 
       od.Quantity,
       p.ProductName
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
LEFT JOIN OrderDetails od ON o.OrderID = od.OrderID
LEFT JOIN Products p ON od.ProductID = p.ProductID
ORDER BY c.CustomerName, o.OrderDate;
```

## LEFT JOIN vs INNER JOIN

**INNER JOIN (only matching records):**
```sql
SELECT c.CustomerName, o.OrderID
FROM Customers c
INNER JOIN Orders o ON c.CustomerID = o.CustomerID;
-- Returns: Only customers who have orders
```

**LEFT JOIN (all left records + matches):**
```sql
SELECT c.CustomerName, o.OrderID
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID;
-- Returns: All customers, with NULL for those without orders
```

## Common Use Cases

**Reporting with optional data:**
```sql
-- Monthly sales report including months with no sales
SELECT m.MonthName, COALESCE(SUM(od.Quantity * od.UnitPrice), 0) AS MonthlySales
FROM Months m
LEFT JOIN Orders o ON MONTH(o.OrderDate) = m.MonthNumber
LEFT JOIN OrderDetails od ON o.OrderID = od.OrderID
GROUP BY m.MonthNumber, m.MonthName
ORDER BY m.MonthNumber;
```

**Finding gaps in data:**
```sql
-- All categories and their product count (including empty categories)
SELECT cat.CategoryName, COUNT(p.ProductID) AS ProductCount
FROM Categories cat
LEFT JOIN Products p ON cat.CategoryID = p.CategoryID
GROUP BY cat.CategoryID, cat.CategoryName;
```

## Performance Considerations
- LEFT JOINs can be slower than INNER JOINs
- Ensure proper indexing on join columns
- Consider the size difference between left and right tables
- NULL checks in WHERE clause can affect performance

## Important Notes
- Always returns all records from the left table
- Use `IS NULL` to find unmatched records (not `= NULL`)
- NULL values in result don't mean empty strings
- Order of tables matters: `A LEFT JOIN B` ≠ `B LEFT JOIN A`

## Related Concepts
- [[SQL INNER JOIN]] - Returns only matching records
- [[SQL RIGHT JOIN]] - Returns all records from right table
- [[SQL FULL OUTER JOIN]] - Returns all records from both tables
- [[SQL JOIN]] - General concept of combining tables
- [[NULL Values]] - Understanding NULL in LEFT JOIN results
- [[SQL WHERE Clause]] - Filtering LEFT JOIN results