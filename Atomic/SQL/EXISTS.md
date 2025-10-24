## Overview

The EXISTS operator checks if a subquery returns any records.  
If the subquery returns at least one row, EXISTS returns TRUE.

- EXISTS is used in the WHERE clause.
- Commonly used to test for related data in another table.

## Syntax

```sql
SELECT column_name(s)
FROM table_name
WHERE EXISTS
  (SELECT column_name FROM table_name WHERE condition);
```

- The subquery can select any column. Only the existence of rows matters.

## Demo Tables

Products table:

| ProductID | ProductName                      | SupplierID | CategoryID | Unit                | Price  |
|-----------|----------------------------------|------------|------------|---------------------|--------|
| 1         | Chais                            | 1          | 1          | 10 boxes x 20 bags  | 18     |
| 2         | Chang                            | 1          | 1          | 24 - 12 oz bottles  | 19     |
| 3         | Aniseed Syrup                    | 1          | 2          | 12 - 550 ml bottles | 10     |
| 4         | Chef Anton's Cajun Seasoning     | 2          | 2          | 48 - 6 oz jars      | 22     |
| 5         | Chef Anton's Gumbo Mix           | 2          | 2          | 36 boxes            | 21.35  |

Suppliers table:

| SupplierID | SupplierName                  | ContactName      | Address         | City        | PostalCode | Country |
|------------|-------------------------------|------------------|-----------------|-------------|------------|---------|
| 1          | Exotic Liquid                  | Charlotte Cooper | 49 Gilbert St.  | London      | EC1 4SD    | UK      |
| 2          | New Orleans Cajun Delights     | Shelley Burke    | P.O. Box 78934  | New Orleans | 70117      | USA     |
| 3          | Grandma Kelly's Homestead      | Regina Murphy    | 707 Oxford Rd.  | Ann Arbor   | 48104      | USA     |
| 4          | Tokyo Traders                  | Yoshi Nagase     | 9-8 Sekimai Musashino-shi | Tokyo | 100 | Japan   |

## How EXISTS Works

- The subquery runs for each row in the outer query.
- If the subquery finds a matching row, the outer row is included.

## Examples

**Example:**  
List suppliers with at least one product priced less than 20.

```sql
SELECT SupplierName
FROM Suppliers
WHERE EXISTS (
  SELECT ProductName
  FROM Products
  WHERE Products.SupplierID = Suppliers.SupplierID
    AND Price < 20
);
```

- For each supplier, the subquery checks if there is a product with Price < 20.
- If at least one product matches, the supplier is included.

**Example:**  
List suppliers with a product priced exactly 22.

```sql
SELECT SupplierName
FROM Suppliers
WHERE EXISTS (
  SELECT ProductName
  FROM Products
  WHERE Products.SupplierID = Suppliers.SupplierID
    AND Price = 22
);
```

- Only suppliers with a product priced at 22 are listed.

## Key Points

- EXISTS returns TRUE if the subquery returns any rows.
- The subquery does not need to return specific columns.
- EXISTS is efficient for checking related data.

This allows you to filter rows based on the presence of related records in another table.