## Overview

A self join is a join where a table is joined with itself.  
This allows you to compare rows within the same table.

- You use table aliases to distinguish between the two instances.
- Self joins are useful for finding related rows in the same table.

## Syntax

SELECT column1, column2  
FROM table1 T1, table1 T2  
WHERE condition;

- T1 and T2 are aliases for the same table.
- The WHERE clause defines how rows are matched.

## Demo Table

Customers table:

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

## Example

**Example:**  
Find customers from the same city.

```sql
SELECT A.CustomerName AS CustomerName1, B.CustomerName AS CustomerName2, A.City
FROM Customers A, Customers B
WHERE A.CustomerID <> B.CustomerID
AND A.City = B.City
ORDER BY A.City;
```

- A and B are aliases for the Customers table.
- The query matches customers with different IDs but the same city.

## Key Points

- Self joins use aliases to refer to the same table twice.
- Useful for comparing rows within a table.
- The WHERE clause usually prevents matching a row with itself.