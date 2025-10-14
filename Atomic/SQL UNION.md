The SQL UNION operator combines the result sets of two or more SELECT statements into a single result set. Each SELECT must have the same number of columns, and corresponding columns must have compatible data types.

## Basic Examples

**Combining contacts from multiple tables:**
```sql
SELECT FirstName + ' ' + LastName AS FullName, 
       Phone, 
       Email, 
       'Employee' AS ContactType
FROM Employees
UNION
SELECT ContactName AS FullName, 
       Phone, 
       Email, 
       'Customer' AS ContactType
FROM Customers
UNION
SELECT ContactName AS FullName, 
       Phone, 
       Email, 
       'Supplier' AS ContactType
FROM Suppliers
ORDER BY FullName;
```

**Product availability report:**
```sql
SELECT ProductName, 'In Stock' AS Status
FROM Products 
WHERE UnitsInStock > 0
UNION
SELECT ProductName, 'Out of Stock' AS Status
FROM Products 
WHERE UnitsInStock = 0
UNION
SELECT ProductName, 'Discontinued' AS Status
FROM Products 
WHERE Discontinued = 1;
```

**Historical and current data:**
```sql
SELECT OrderID, OrderDate, 'Current' AS DataSource
FROM Orders
WHERE OrderDate >= '2023-01-01'
UNION
SELECT OrderID, OrderDate, 'Archive' AS DataSource
FROM OrdersArchive
WHERE OrderDate < '2023-01-01'
ORDER BY OrderDate DESC;
```

## Advanced UNION Techniques

**Creating summary rows:**
```sql
SELECT CategoryName AS Item, 
       CAST(COUNT(*) AS VARCHAR) + ' products' AS Details
FROM Categories c
JOIN Products p ON c.CategoryID = p.CategoryID
GROUP BY CategoryName
UNION
SELECT 'TOTAL' AS Item,
       CAST(COUNT(*) AS VARCHAR) + ' total products' AS Details
FROM Products
ORDER BY Item;
```

**Simulating FULL OUTER JOIN (for MySQL):**
```sql
-- All customers with their orders
SELECT c.CustomerName, o.OrderID
FROM Customers c
LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
UNION
SELECT c.CustomerName, o.OrderID
FROM Customers c
RIGHT JOIN Orders o ON c.CustomerID = o.CustomerID
WHERE c.CustomerID IS NULL;
```

**Creating calculated fields:**
```sql
SELECT 'High Price' AS Category, 
       ProductName, 
       Price
FROM Products 
WHERE Price > 50
UNION
SELECT 'Medium Price' AS Category, 
       ProductName, 
       Price
FROM Products 
WHERE Price BETWEEN 20 AND 50
UNION
SELECT 'Low Price' AS Category, 
       ProductName, 
       Price
FROM Products 
WHERE Price < 20
ORDER BY Category, Price DESC;
```

## Data Type Considerations

- All SELECT statements must have the same number of columns.
- Corresponding columns must have compatible data types.

**Compatible data types:**
```sql
-- This works - VARCHAR and VARCHAR
SELECT CustomerName FROM Customers
UNION
SELECT CompanyName FROM Suppliers;

-- This works - INT and INT
SELECT CustomerID FROM Customers
UNION
SELECT SupplierID FROM Suppliers;
```

**Incompatible data types require casting:**
```sql
-- Convert numbers to strings
SELECT CustomerName FROM Customers
UNION
SELECT CAST(ProductID AS VARCHAR) FROM Products;

-- Convert dates to strings
SELECT CustomerName FROM Customers
UNION
SELECT CONVERT(VARCHAR, OrderDate) FROM Orders;
```

## NULL Handling

```sql
SELECT CustomerName, Region FROM Customers
UNION
SELECT CompanyName, NULL FROM Suppliers  -- NULL for missing Region column
ORDER BY 1;
```

## Performance Considerations

- **UNION** removes duplicates, which can be slower.
- **UNION ALL** keeps all rows (including duplicates) and is faster.
- Large UNIONs can be memory intensive.
- Consider indexing columns used in ORDER BY.
- Break complex UNIONs into smaller parts if needed.

**Performance comparison:**
```sql
-- Slower (removes duplicates)
SELECT City FROM Customers
UNION
SELECT City FROM Suppliers;

-- Faster (keeps all rows)
SELECT City FROM Customers
UNION ALL
SELECT City FROM Suppliers;
```

## Common Use Cases

- Combining similar data from multiple tables
- Creating comprehensive reports
- Merging historical and current data
- Building lookup lists
- Data migration and consolidation
- Creating views that span multiple tables

## Limitations and Notes

- Cannot use ORDER BY in individual SELECT statements (only at the end)
- Column names come from the first SELECT
- All SELECT statements must have the same number of columns
- Cannot directly use UNION in subqueries in some databases
- Some databases limit the number of UNION operations

## Alternative Approaches

**Using CASE instead of UNION:**
```sql
-- Instead of UNION for status reports
SELECT ProductName,
       CASE 
         WHEN UnitsInStock > 0 THEN 'In Stock'
         WHEN UnitsInStock = 0 THEN 'Out of Stock'
         WHEN Discontinued = 1 THEN 'Discontinued'
       END AS Status
FROM Products;
```

## Related Concepts

- [[SQL UNION ALL]] – Include duplicate rows
- [[SQL SELECT Statement]] – Foundation for UNION operations
- [[SQL JOIN]] – Alternative for combining table data
- [[SQL CASE Statement]] – Alternative for conditional data
- [[SQL Subqueries]] – Can contain UNION operations
- [[SQL Views]] – Can be built using UNION

The UNION operator is essential for combining result sets in [[SQL Queries]] and [[SQL (Structured Query Language)]].