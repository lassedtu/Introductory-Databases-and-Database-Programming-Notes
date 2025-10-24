## Overview

The AVG() function returns the average value of a numeric column.  
NULL values are ignored.

## Syntax

SELECT AVG(column_name)  
FROM table_name  
WHERE condition

- AVG() calculates the mean of a numeric column.
- WHERE filters which rows are included.
- NULL values are not counted.

## Demo Table

The Products table contains these columns:

- ProductID
- ProductName
- SupplierID
- CategoryID
- Unit
- Price

**Example rows:**

| ProductID | ProductName                   | SupplierID | CategoryID | Unit                | Price  |
|-----------|-------------------------------|------------|------------|---------------------|--------|
| 1         | Chais                         | 1          | 1          | 10 boxes x 20 bags  | 18     |
| 2         | Chang                         | 1          | 1          | 24 - 12 oz bottles  | 19     |
| 3         | Aniseed Syrup                 | 1          | 2          | 12 - 550 ml bottles | 10     |
| 4         | Chef Anton's Cajun Seasoning  | 2          | 2          | 48 - 6 oz jars      | 22     |
| 5         | Chef Anton's Gumbo Mix        | 2          | 2          | 36 boxes            | 21.35  |

## Example

Return the average price of all products.

```sql
SELECT AVG(Price)
FROM Products;
```

- Returns the mean value of the Price column.

## Add a WHERE Clause

Return the average price of products in category 1.

```sql
SELECT AVG(Price)
FROM Products
WHERE CategoryID = 1;
```

- Only rows with CategoryID = 1 are included.

## Use an Alias

Name the result column "average price".

```sql
SELECT AVG(Price) AS [average price]
FROM Products;
```

- The result column is labeled "average price".

## Higher Than Average

Return all products with a price higher than the average.

```sql
SELECT *
FROM Products
WHERE Price > (SELECT AVG(Price) FROM Products);
```

- Only products with a Price above the average are returned.

## Use AVG() with GROUP BY

Return the average price for each category.

```sql
SELECT AVG(Price) AS AveragePrice, CategoryID
FROM Products
GROUP BY CategoryID;
```

- Returns the average price for each CategoryID.

## Key Points

- AVG() returns the mean of a numeric column.
- Ignores NULL values.
- Use WHERE to filter rows.
- Use GROUP BY to get averages for groups.
- Use AS to rename the result column.