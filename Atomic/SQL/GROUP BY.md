## Overview

The GROUP BY statement groups rows with the same values into summary rows.  
GROUP BY is used with aggregate functions like COUNT(), MAX(), MIN(), SUM(), and AVG().

- GROUP BY collects rows by one or more columns.
- Often used to get totals or counts for each group.

## Syntax

SELECT column_name(s)  
FROM table_name  
WHERE condition  
GROUP BY column_name(s)  
ORDER BY column_name(s);

- GROUP BY comes after WHERE and before ORDER BY.

## Demo Tables

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
| 4          | Around the Horn                    | Thomas Hardy     | 120 Hanover Sq.        | London      | WA1 1DP    | UK       |
| 5          | Berglunds snabbköp                 | Christina Berglund | Berguvsvägen 8       | Luleå       | S-958 22   | Sweden   |

Orders table:

- OrderID
- CustomerID
- EmployeeID
- OrderDate
- ShipperID

Shippers table:

- ShipperID
- ShipperName

## Examples

**Example:**  
Count the number of customers in each country.

```sql
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country;
```

- Groups customers by country.
- Shows the count for each country.

**Example:**  
Count the number of customers in each country, sorted from highest to lowest.

```sql
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
ORDER BY COUNT(CustomerID) DESC;
```

- Adds ORDER BY to sort by the count.

**Example:**  
Count the number of orders sent by each shipper.

```sql
SELECT Shippers.ShipperName, COUNT(Orders.OrderID) AS NumberOfOrders
FROM Orders
LEFT JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID
GROUP BY ShipperName;
```

- Joins Orders and Shippers.
- Groups by shipper name.
- Shows the number of orders for each shipper.

## Key Points

- GROUP BY is used with aggregate functions to summarize data.
- Each group contains rows with the same value in the grouped column(s).
- Use ORDER BY to sort the grouped results.

This allows you to create summary reports and totals from your data.