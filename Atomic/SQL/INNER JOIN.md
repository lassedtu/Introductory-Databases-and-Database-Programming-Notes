## Overview

![[inner-join.png| center | 400]]

The INNER JOIN keyword selects records that have matching values in both tables.  
INNER JOIN is the default join type for JOIN.

## Syntax

SELECT column1, column2  
FROM table1  
INNER JOIN table2  
ON table1.column = table2.column

- Only rows with matching values in both tables are returned.
- Use table names to avoid ambiguity, especially if columns have the same name.

## Demo Tables

Products table:

- ProductID
- ProductName
- CategoryID
- Price

Categories table:

- CategoryID
- CategoryName
- Description

Shippers table:

- ShipperID
- ShipperName
- Phone

**Example rows (Products):**

| ProductID | ProductName    | CategoryID | Price |
|-----------|---------------|------------|-------|
| 1         | Chais         | 1          | 18    |
| 2         | Chang         | 1          | 19    |
| 3         | Aniseed Syrup | 2          | 10    |

**Example rows (Categories):**

| CategoryID | CategoryName | Description                                    |
|------------|--------------|------------------------------------------------|
| 1          | Beverages    | Soft drinks, coffees, teas, beers, and ales    |
| 2          | Condiments   | Sweet and savory sauces, relishes, spreads     |
| 3          | Confections  | Desserts, candies, and sweet breads            |

**Example rows (Shippers):**

| ShipperID | ShipperName      | Phone         |
|-----------|------------------|--------------|
| 1         | Speedy Express   | (503) 555-9831|
| 2         | United Package   | (503) 555-3199|
| 3         | Federal Shipping | (503) 555-9931|

## Examples

**Example:**  
Join Products and Categories with INNER JOIN.

```sql
SELECT ProductID, ProductName, CategoryName
FROM Products
INNER JOIN Categories ON Products.CategoryID = Categories.CategoryID;
```

- Returns only products with a matching CategoryID in Categories.

**Example:**  
Specify table names for clarity.

```sql
SELECT Products.ProductID, Products.ProductName, Categories.CategoryName
FROM Products
INNER JOIN Categories ON Products.CategoryID = Categories.CategoryID;
```

- Required if you select columns with the same name from both tables.

**Example:**  
JOIN is the same as INNER JOIN.

```sql
SELECT Products.ProductID, Products.ProductName, Categories.CategoryName
FROM Products
JOIN Categories ON Products.CategoryID = Categories.CategoryID;
```

**Example:**  
Join three tables: Orders, Customers, and Shippers.

```sql
SELECT Orders.OrderID, Customers.CustomerName, Shippers.ShipperName
FROM ((Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID)
INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID);
```

## Key Points

- INNER JOIN returns only rows with a match in both tables.
- JOIN and INNER JOIN are equivalent.
- Use table names to avoid ambiguity.
- Can join more than two tables.