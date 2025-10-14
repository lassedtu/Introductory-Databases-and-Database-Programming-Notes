SQL aliases are temporary names given to tables or columns for the duration of a query. They make queries easier to read and write, especially when dealing with complex joins or calculated fields.

## Examples

**Employees and their managers:**
```sql
SELECT e.FirstName + ' ' + e.LastName AS Employee,
       m.FirstName + ' ' + m.LastName AS Manager
FROM Employees e
JOIN Employees m ON e.ReportsTo = m.EmployeeID;
```

**Subquery with alias:**
```sql
SELECT CustomerName, 
       (SELECT COUNT(*) FROM Orders o WHERE o.CustomerID = c.CustomerID) AS OrderCount
FROM Customers c;
```

**CASE statement with alias:**
```sql
SELECT ProductName,
       Price,
       CASE 
         WHEN Price > 30 THEN 'Expensive'
         WHEN Price > 10 THEN 'Moderate'
         ELSE 'Cheap'
       END AS PriceCategory
FROM Products;
```

## Important Rules

### Column Alias Rules
- Cannot be used in the WHERE clause (use HAVING with GROUP BY instead)
- Can be used in the ORDER BY clause
- Must be quoted if containing spaces or special characters

```sql
-- This DOESN'T work:
SELECT ProductName, Price * 1.25 AS PriceWithTax
FROM Products
WHERE PriceWithTax > 50;  -- ERROR!

-- This WORKS:
SELECT ProductName, Price * 1.25 AS PriceWithTax
FROM Products
WHERE Price * 1.25 > 50;

-- This also WORKS:
SELECT ProductName, Price * 1.25 AS PriceWithTax
FROM Products
ORDER BY PriceWithTax;
```

### Table Alias Rules
- Once aliased, you must use the alias (not the original name)
- Aliases are case-sensitive in some databases
- Cannot use reserved keywords as aliases

## Database-Specific Syntax

**MySQL:**
```sql
-- Backticks for aliases with spaces/special chars
SELECT CustomerName AS `Customer Name` FROM Customers;
```

**SQL Server:**
```sql
-- Square brackets for aliases with spaces/special chars
SELECT CustomerName AS [Customer Name] FROM Customers;
```

**PostgreSQL:**
```sql
-- Double quotes for case-sensitive aliases
SELECT CustomerName AS "Customer Name" FROM Customers;
```

## Best Practices

- Use meaningful alias names
- Keep aliases short but descriptive
- Use consistent naming conventions
- Always use aliases in complex joins
- Use table aliases even in simple queries for clarity

## Related Concepts

- [[SQL SELECT Statement]] – Foundation for using aliases
- [[SQL JOIN]] – Common use case for table aliases
- [[SQL Aggregate Functions]] – Often need aliases for calculated results
- [[SQL ORDER BY]] – Can reference column aliases
- [[SQL GROUP BY]] – Works with aliases in SELECT clause
- [[SQL Subqueries]] – Can use aliases for derived tables

Aliases are essential for writing readable and maintainable [[SQL Queries]] in [[SQL (Structured Query Language)]].