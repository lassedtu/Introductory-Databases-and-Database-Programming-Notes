## Overview

The ORDER BY clause sorts query results. You can sort in ascending or descending order.

## Syntax

SELECT column1, column2  
FROM table_name  
ORDER BY column1, column2 ASC|DESC

- ORDER BY defines the columns to sort by.
- ASC sorts in ascending order (default).
- DESC sorts in descending order.

## Example: Sort by Price

Sort products by price in ascending order.

```sql
SELECT * FROM Products
ORDER BY Price;
```

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

## Sort Descending

Use DESC to sort from highest to lowest.

**Example:**  
Sort products by price, highest first.

```sql
SELECT * FROM Products
ORDER BY Price DESC;
```

## Sort Alphabetically

ORDER BY sorts text columns alphabetically.

**Example:**  
Sort products by ProductName.

```sql
SELECT * FROM Products
ORDER BY ProductName;
```

## Sort Reverse Alphabetically

Use DESC to sort text columns in reverse order.

**Example:**  
Sort products by ProductName in reverse order.

```sql
SELECT * FROM Products
ORDER BY ProductName DESC;
```

## Sort by Multiple Columns

You can sort by more than one column. The first column is sorted first. If there are duplicates, the next column is used.

**Example:**  
Sort customers by Country, then by CustomerName.

```sql
SELECT * FROM Customers
ORDER BY Country, CustomerName;
```

## Use ASC and DESC Together

You can specify ASC or DESC for each column.

**Example:**  
Sort customers by Country (ascending) and CustomerName (descending).

```sql
SELECT * FROM Customers
ORDER BY Country ASC, CustomerName DESC;
```

This allows you to control the sort order for each column.