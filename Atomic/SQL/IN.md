## Overview

The IN operator allows you to specify multiple values in a WHERE clause.  
IN is a shorthand for multiple OR conditions.

## Syntax

SELECT column1, column2  
FROM table_name  
WHERE column_name IN (value1, value2, ...)

- IN checks if a column matches any value in a list.
- Use NOT IN to exclude values from the list.
- IN can be used with subqueries.

## Demo Table

The Customers table contains these columns:

- CustomerID
- CustomerName
- ContactName
- Address
- City
- PostalCode
- Country

**Example rows:**

| CustomerID | CustomerName                       | ContactName      | Address                | City        | PostalCode | Country  |
|------------|------------------------------------|------------------|------------------------|-------------|------------|----------|
| 1          | Alfreds Futterkiste                | Maria Anders     | Obere Str. 57          | Berlin      | 12209      | Germany  |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo     | Avda. de la Constitución 2222 | México D.F. | 05021      | Mexico   |
| 3          | Antonio Moreno Taquería            | Antonio Moreno   | Mataderos 2312         | México D.F. | 05023      | Mexico   |
| 4          | Around the Horn                    | Thomas Hardy     | 120 Hanover Sq.        | London      | WA1 1DP    | UK       |
| 5          | Berglunds snabbköp                 | Christina Berglund | Berguvsvägen 8       | Luleå       | S-958 22   | Sweden   |

## Examples

**Example:**  
Return all customers from 'Germany', 'France', or 'UK'.

```sql
SELECT * FROM Customers
WHERE Country IN ('Germany', 'France', 'UK');
```

- Equivalent to using multiple OR conditions.

**Example:**  
Return all customers NOT from 'Germany', 'France', or 'UK'.

```sql
SELECT * FROM Customers
WHERE Country NOT IN ('Germany', 'France', 'UK');
```

- Excludes the listed countries.

**Example:**  
Return all customers that have an order in the Orders table.

```sql
SELECT * FROM Customers
WHERE CustomerID IN (SELECT CustomerID FROM Orders);
```

- IN can use a subquery to match values from another table.

**Example:**  
Return all customers that have NOT placed any orders.

```sql
SELECT * FROM Customers
WHERE CustomerID NOT IN (SELECT CustomerID FROM Orders);
```

- NOT IN with a subquery excludes matching values.

## Key Points

- IN simplifies queries with multiple possible values.
- NOT IN excludes values from the result.
- IN works with subqueries for flexible filtering.