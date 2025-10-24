## Overview

The CASE expression returns a value based on conditions.  
It works like an if-then-else statement.  
The first true condition determines the result.  
If no condition is true, the ELSE value is returned.  
If there is no ELSE and no condition is true, the result is NULL.

## Syntax

```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    ...
    ELSE result
END
```

- You can use CASE in SELECT, ORDER BY, and other clauses.

## Demo Table

OrderDetails table:

| OrderDetailID | OrderID | ProductID | Quantity |
|---------------|---------|-----------|----------|
| 1             | 10248   | 11        | 12       |
| 2             | 10248   | 42        | 10       |
| 3             | 10248   | 72        | 5        |
| 4             | 10249   | 14        | 9        |
| 5             | 10249   | 51        | 40       |

## Examples

**Example:**  
Label each order by quantity.

```sql
SELECT OrderID, Quantity,
CASE
    WHEN Quantity > 30 THEN 'The quantity is greater than 30'
    WHEN Quantity = 30 THEN 'The quantity is 30'
    ELSE 'The quantity is under 30'
END AS QuantityText
FROM OrderDetails;
```

- Returns a text label for each row based on Quantity.

**Example:**  
Order customers by City, but use Country if City is NULL.

```sql
SELECT CustomerName, City, Country
FROM Customers
ORDER BY
(CASE
    WHEN City IS NULL THEN Country
    ELSE City
END);
```

- If City is NULL, sorting uses Country instead.

## Key Points

- CASE checks conditions in order.
- Returns the result for the first true condition.
- ELSE is optional. If omitted and no condition is true, returns NULL.

This allows you to add conditional logic to your SQL queries.