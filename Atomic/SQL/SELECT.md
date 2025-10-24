## Overview

The SELECT statement retrieves data from a table in a database.

## Syntax

SELECT column1, column2  
FROM table_name

- column1, column2: Names of the fields to return.
- table_name: Name of the table to query.

**Example:**  
Return CustomerName and City from the Customers table.

```sql
SELECT CustomerName, City FROM Customers;
```

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

## Select All Columns

Use * to select every column from a table.

**Example:**  
Return all columns from the Customers table.

```sql
SELECT * FROM Customers;
```

This returns every field for each row in the table.