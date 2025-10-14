The `COUNT()` function returns the number of rows that matches a specified criterion. It's one of the most commonly used [[SQL Aggregate Functions]].

## Syntax
```sql
SELECT COUNT(column_name) FROM table_name WHERE condition;
```

## COUNT Variations

### COUNT(*)
Counts all rows, including those with NULL values:
```sql
SELECT COUNT(*) FROM Customers;
```

### COUNT(column_name)  
Counts only non-NULL values in the specified column:
```sql
SELECT COUNT(CustomerName) FROM Customers;
```

### COUNT(DISTINCT column_name)
Counts only distinct non-NULL values:
```sql
SELECT COUNT(DISTINCT Country) FROM Customers;
```

## Examples

**Count total customers:**
```sql
SELECT COUNT(*) AS TotalCustomers FROM Customers;
```

**Count customers from specific country:**
```sql
SELECT COUNT(*) AS GermanCustomers 
FROM Customers 
WHERE Country = 'Germany';
```

**Count non-NULL values:**
```sql
SELECT COUNT(PostalCode) AS CustomersWithPostalCode 
FROM Customers;
```

**Count distinct countries:**
```sql
SELECT COUNT(DISTINCT Country) AS NumberOfCountries 
FROM Customers;
```

## With GROUP BY
Count records in each group:
```sql
SELECT Country, COUNT(*) AS CustomerCount
FROM Customers
GROUP BY Country
ORDER BY CustomerCount DESC;
```

## Important Notes
- `COUNT(*)` includes NULL values
- `COUNT(column)` excludes NULL values  
- `COUNT(DISTINCT column)` excludes NULL and duplicate values
- Returns 0 if no rows match the condition

## Related Concepts
- [[SQL Aggregate Functions]] - Family of calculation functions
- [[SQL MIN and MAX Functions]] - Find extremes
- [[SQL SUM Function]] - Calculate totals
- [[SQL AVG Function]] - Calculate averages
- [[SQL GROUP BY]] - Count records per group
- [[SQL DISTINCT]] - Remove duplicates before counting

Fundamental tool for data analysis in [[SQL Queries]] and [[SQL (Structured Query Language)]].
