## Overview

A JOIN clause combines rows from two or more tables based on a related column.  
JOINs are used to retrieve data that spans multiple tables.

## Syntax

SELECT column1, column2  
FROM table1  
JOIN_TYPE table2  
ON table1.column = table2.column

- JOIN_TYPE can be INNER JOIN, LEFT JOIN, RIGHT JOIN, or FULL JOIN.
- ON specifies the related columns.

## Demo Tables

Orders table:

- OrderID
- CustomerID
- OrderDate

Customers table:

- CustomerID
- CustomerName
- ContactName
- Country

**Example rows (Orders):**

| OrderID | CustomerID | OrderDate   |
|---------|------------|-------------|
| 10308   | 2          | 1996-09-18  |
| 10309   | 37         | 1996-09-19  |
| 10310   | 77         | 1996-09-20  |

**Example rows (Customers):**

| CustomerID | CustomerName                       | ContactName      | Country  |
|------------|------------------------------------|------------------|----------|
| 1          | Alfreds Futterkiste                | Maria Anders     | Germany  |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo     | Mexico   |
| 3          | Antonio Moreno Taquería            | Antonio Moreno   | Mexico   |

## Examples

**Example:**  
Select orders with customer names using INNER JOIN.

```sql
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
```

- Returns only rows with matching CustomerID in both tables.

## Types of JOINs

| JOIN Type      | Description                                                         | Visual Representation                     |
| -------------- | ------------------------------------------------------------------- | ----------------------------------------- |
| [[INNER JOIN]] | Returns records with matching values in both tables                 | ![[inner-join.png\| center \| 200]]       |
| [[LEFT JOIN]]  | Returns all records from the left table, matched records from right | ![[left-join.png \| center \| 200]]       |
| [[RIGHT JOIN]] | Returns all records from the right table, matched records from left | ![[right-join.png \| center \| 200]]      |
| [[FULL JOIN]]  | Returns all records with a match in either left or right table      | ![[full-outer-join.png \| center \| 200]] |

## Key Points

- JOINs combine data from multiple tables.
- INNER JOIN returns only matching rows.
- LEFT JOIN returns all rows from the left table.
- RIGHT JOIN returns all rows from the right table.
- FULL JOIN returns all rows from both tables.