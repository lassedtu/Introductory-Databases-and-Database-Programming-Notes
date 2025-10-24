## Overview

![[left-join.png | center | 400]]

The LEFT JOIN keyword returns all records from the left table and the matching records from the right table.  
If there is no match, the result is NULL from the right table.

## Syntax

SELECT column1, column2  
FROM table1  
LEFT JOIN table2  
ON table1.column = table2.column

- LEFT JOIN is also called LEFT OUTER JOIN in some databases.
- All rows from the left table are included.
- Matching rows from the right table are included. If no match, right table columns are NULL.

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
Select all customers and any orders they might have.

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID
ORDER BY Customers.CustomerName;
```

- All customers are listed.
- If a customer has no orders, OrderID is NULL.

## Key Points

- LEFT JOIN returns all rows from the left table.
- Returns matching rows from the right table, or NULL if no match.
- Use LEFT JOIN to find records in the left table without matches in the right table.