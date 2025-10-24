## Overview

The MIN() function returns the smallest value in a column.  
The MAX() function returns the largest value in a column.

## Syntax

SELECT MIN(column_name)  
FROM table_name  
WHERE condition

SELECT MAX(column_name)  
FROM table_name  
WHERE condition

## Demo Table

The Products table contains these columns:

- ProductID
- ProductName
- SupplierID
- CategoryID
- Unit
- Price

**Example rows:**

| ProductID | ProductName                    | SupplierID | CategoryID | Unit                | Price  |
|-----------|-------------------------------|------------|------------|---------------------|--------|
| 1         | Chais                         | 1          | 1          | 10 boxes x 20 bags  | 18     |
| 2         | Chang                         | 1          | 1          | 24 - 12 oz bottles  | 19     |
| 3         | Aniseed Syrup                 | 1          | 2          | 12 - 550 ml bottles | 10     |
| 4         | Chef Anton's Cajun Seasoning  | 2          | 2          | 48 - 6 oz jars      | 22     |
| 5         | Chef Anton's Gumbo Mix        | 2          | 2          | 36 boxes            | 21.35  |

## MIN() Example

Find the lowest price in the Price column.

```sql
SELECT MIN(Price)
FROM Products;
```

## MAX() Example

Find the highest price in the Price column.

```sql
SELECT MAX(Price)
FROM Products;
```

## Set Column Name (Alias)

Use AS to give the result a descriptive name.

**Example:**  
Return the smallest price as SmallestPrice.

```sql
SELECT MIN(Price) AS SmallestPrice
FROM Products;
```

## Use MIN() with GROUP BY

Return the smallest price for each category.

```sql
SELECT MIN(Price) AS SmallestPrice, CategoryID
FROM Products
GROUP BY CategoryID;
```

This allows you to find minimum and maximum values in a column, with or without grouping.