## Overview

The SELECT TOP clause limits the number of rows returned by a query.  
In MariaDB and MySQL, use the LIMIT clause to control the number of results.

## Syntax

SELECT column_name(s)  
FROM table_name  
WHERE condition  
LIMIT number

- LIMIT number: Returns the specified number of rows.

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

## Select Top N Rows

Return the first 3 records.

```sql
SELECT * FROM Customers
LIMIT 3;
```

## Add a WHERE Clause

Return the first 3 German customers.

```sql
SELECT * FROM Customers
WHERE Country = 'Germany'
LIMIT 3;
```

## Add ORDER BY

Sort by CustomerName in reverse order and return the first 3 records.

```sql
SELECT * FROM Customers
ORDER BY CustomerName DESC
LIMIT 3;
```