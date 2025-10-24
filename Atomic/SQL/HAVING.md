## Overview

The HAVING clause filters groups created by GROUP BY.  
WHERE cannot be used with aggregate functions, but HAVING can.

- HAVING is used after GROUP BY.
- HAVING works with aggregate functions like COUNT(), SUM(), AVG(), etc.

## Syntax

SELECT column_name(s)  
FROM table_name  
WHERE condition  
GROUP BY column_name(s)  
HAVING condition  
ORDER BY column_name(s);

- HAVING comes after GROUP BY and before ORDER BY.

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

Employees table:

- EmployeeID
- LastName
- FirstName
- BirthDate
- Photo
- Notes

## Examples

**Example:**  
List the number of customers in each country, only including countries with more than 5 customers.

```sql
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5;
```

- Groups customers by country.
- Only countries with more than 5 customers are shown.

**Example:**  
List the number of customers in each country, sorted from highest to lowest, only including countries with more than 5 customers.

```sql
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5
ORDER BY COUNT(CustomerID) DESC;
```

- Adds ORDER BY to sort by the count.

**Example:**  
List employees who have registered more than 10 orders.

```sql
SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberOfOrders
FROM Orders
INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
GROUP BY LastName
HAVING COUNT(Orders.OrderID) > 10;
```

- Joins Orders and Employees.
- Groups by employee last name.
- Only employees with more than 10 orders are shown.

**Example:**  
Check if "Davolio" or "Fuller" have registered more than 25 orders.

```sql
SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberOfOrders
FROM Orders
INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
WHERE LastName = 'Davolio' OR LastName = 'Fuller'
GROUP BY LastName
HAVING COUNT(Orders.OrderID) > 25;
```

- Filters for specific employees.
- Only shows if they have more than 25 orders.

## Key Points

- Use HAVING to filter groups after aggregation.
- WHERE filters rows before grouping.
- HAVING filters groups after grouping.

This allows you to control which groups appear in your results based on aggregate values.