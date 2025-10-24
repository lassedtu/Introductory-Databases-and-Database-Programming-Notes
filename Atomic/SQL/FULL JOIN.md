## Overview

The FULL OUTER JOIN keyword returns all records from both tables. If there is a match between the tables, the rows are combined. If there is no match, the result is NULL on the side without a match.

- FULL OUTER JOIN and FULL JOIN are the same.
- Some databases do not support FULL OUTER JOIN directly.

![[full-outer-join.png | center | 400]]

## Syntax

SELECT column1, column2  
FROM table1  
FULL OUTER JOIN table2  
ON table1.column = table2.column  
WHERE condition;

- Returns all rows from both tables.
- If there is no match, missing side columns are NULL.

## Demo Tables

Customers table:

- CustomerID
- CustomerName
- ContactName
- Address
- City
- PostalCode
- Country

Orders table:

- OrderID
- CustomerID
- EmployeeID
- OrderDate
- ShipperID

**Example rows (Customers):**

| CustomerID | CustomerName                       | ContactName      | Address                | City        | PostalCode | Country  |
|------------|------------------------------------|------------------|------------------------|-------------|------------|----------|
| 1          | Alfreds Futterkiste                | Maria Anders     | Obere Str. 57          | Berlin      | 12209      | Germany  |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo     | Avda. de la Constitución 2222 | México D.F. | 05021      | Mexico   |
| 3          | Antonio Moreno Taquería            | Antonio Moreno   | Mataderos 2312         | México D.F. | 05023      | Mexico   |

**Example rows (Orders):**

| OrderID | CustomerID | EmployeeID | OrderDate   | ShipperID |
|---------|------------|------------|-------------|-----------|
| 10308   | 2          | 7          | 1996-09-18  | 3         |
| 10309   | 37         | 3          | 1996-09-19  | 1         |
| 10310   | 77         | 8          | 1996-09-20  | 2         |

## Example

**Example:**  
Select all customers and all orders, matching where possible.

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
FULL OUTER JOIN Orders ON Customers.CustomerID = Orders.CustomerID
ORDER BY Customers.CustomerName;
```

**Sample result:**

| CustomerName                       | OrderID |
|-------------------------------------|---------|
| NULL                                | 10309   |
| NULL                                | 10310   |
| Alfreds Futterkiste                 | NULL    |
| Ana Trujillo Emparedados y helados  | 10308   |
| Antonio Moreno Taquería             | NULL    |

- Rows with no match in Customers show NULL for CustomerName.
- Rows with no match in Orders show NULL for OrderID.

## Key Points

- FULL OUTER JOIN returns all rows from both tables.
- If there is no match, missing values are NULL.
- Use FULL OUTER JOIN to find unmatched rows in either table.
- Result sets can be large if both tables have many rows.