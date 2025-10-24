## Overview

The COUNT() function returns the number of rows that match a condition.

## Syntax

SELECT COUNT(column_name)  
FROM table_name  
WHERE condition

- COUNT(*) counts all rows.
- COUNT(column_name) counts only rows where the column is not NULL.

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

## COUNT(*) Example

Count all rows in the Products table.

```sql
SELECT COUNT(*)
FROM Products;
```

## COUNT(column_name) Example

Count rows where ProductName is not NULL.

```sql
SELECT COUNT(ProductName)
FROM Products;
```

## Add a WHERE Clause

Count products with Price greater than 20.

```sql
SELECT COUNT(ProductID)
FROM Products
WHERE Price > 20;
```

## Ignore Duplicates

Count the number of different prices.

```sql
SELECT COUNT(DISTINCT Price)
FROM Products;
```

## Use an Alias

Give the result a descriptive name.

```sql
SELECT COUNT(*) AS `Number of records`
FROM Products;
```

## Use COUNT() with GROUP BY

Count the number of products in each category.

```sql
SELECT COUNT(*) AS `Number of records`, CategoryID
FROM Products
GROUP BY CategoryID;
```

This allows you to count rows, filter results, ignore duplicates, and group counts by category.