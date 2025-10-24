## Overview

The BETWEEN operator selects values within a given range.  
BETWEEN is inclusive: both the start and end values are included.  
Works with numbers, text, and dates.

## Syntax

SELECT column1, column2  
FROM table_name  
WHERE column_name BETWEEN value1 AND value2

- BETWEEN checks if a value falls within a range.
- NOT BETWEEN excludes values in the range.

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

## Examples

**Example:**  
Select all products with a price between 10 and 20.

```sql
SELECT * FROM Products
WHERE Price BETWEEN 10 AND 20;
```

**Example:**  
Select all products with a price NOT between 10 and 20.

```sql
SELECT * FROM Products
WHERE Price NOT BETWEEN 10 AND 20;
```

**Example:**  
Select all products with a price between 10 and 20 and CategoryID 1, 2, or 3.

```sql
SELECT * FROM Products
WHERE Price BETWEEN 10 AND 20
AND CategoryID IN (1,2,3);
```

## BETWEEN with Text

BETWEEN can be used with text values.  
Text comparison is alphabetical.

**Example:**  
Select all products with ProductName between 'Carnarvon Tigers' and 'Mozzarella di Giovanni'.

```sql
SELECT * FROM Products
WHERE ProductName BETWEEN 'Carnarvon Tigers' AND 'Mozzarella di Giovanni'
ORDER BY ProductName;
```

**Example:**  
Select all products with ProductName NOT between 'Carnarvon Tigers' and 'Mozzarella di Giovanni'.

```sql
SELECT * FROM Products
WHERE ProductName NOT BETWEEN 'Carnarvon Tigers' AND 'Mozzarella di Giovanni'
ORDER BY ProductName;
```

## BETWEEN with Dates

BETWEEN can be used with date values.

**Example:**  
Select all orders with OrderDate between '1996-07-01' and '1996-07-31'.

```sql
SELECT * FROM Orders
WHERE OrderDate BETWEEN '1996-07-01' AND '1996-07-31';
```

## Key Points

- BETWEEN is inclusive.
- Works with numbers, text, and dates.
- NOT BETWEEN excludes the range.
- Can be combined with other operators like IN.