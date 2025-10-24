## Overview

The SUM() function returns the total sum of a numeric column.

## Syntax

SELECT SUM(column_name)  
FROM table_name  
WHERE condition

- SUM() adds up all values in the specified column.

## Demo Table

The OrderDetails table contains these columns:

- OrderDetailID
- OrderID
- ProductID
- Quantity

**Example rows:**

| OrderDetailID | OrderID | ProductID | Quantity |
|---------------|---------|-----------|----------|
| 1             | 10248   | 11        | 12       |
| 2             | 10248   | 42        | 10       |
| 3             | 10248   | 72        | 5        |
| 4             | 10249   | 14        | 9        |
| 5             | 10249   | 51        | 40       |

## SUM() Example

Return the sum of all Quantity values.

```sql
SELECT SUM(Quantity)
FROM OrderDetails;
```

## Add a WHERE Clause

Return the sum of Quantity for ProductID 11.

```sql
SELECT SUM(Quantity)
FROM OrderDetails
WHERE ProductID = 11;
```

## Use an Alias

Give the result a descriptive name.

```sql
SELECT SUM(Quantity) AS total
FROM OrderDetails;
```

## Use SUM() with GROUP BY

Return the total quantity for each order.

```sql
SELECT OrderID, SUM(Quantity) AS `Total Quantity`
FROM OrderDetails
GROUP BY OrderID;
```

## SUM() With an Expression

You can use an expression inside SUM().

**Example:**  
Assume each product costs $10. Find total earnings.

```sql
SELECT SUM(Quantity * 10)
FROM OrderDetails;
```

**Example:**  
Join OrderDetails with Products to find the actual total amount.

```sql
SELECT SUM(Price * Quantity)
FROM OrderDetails
LEFT JOIN Products ON OrderDetails.ProductID = Products.ProductID;
```

This allows you to calculate totals, filter results, group by columns, and use expressions in your sums.