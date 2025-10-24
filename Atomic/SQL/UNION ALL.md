## Overview

The UNION ALL operator combines the result sets of two or more SELECT statements.  
UNION ALL includes all rows, including duplicates.

- Each SELECT must have the same number of columns.
- Columns must have similar data types and be in the same order.

## Syntax

SELECT column_name(s) FROM table1  
UNION ALL  
SELECT column_name(s) FROM table2;

- The result uses the column names from the first SELECT.

## Demo Tables

Customers table:

- CustomerID
- CustomerName
- ContactName
- Address
- City
- PostalCode
- Country

Suppliers table:

- SupplierID
- SupplierName
- ContactName
- Address
- City
- PostalCode
- Country

**Example rows (Customers):**

| CustomerID | CustomerName                       | ContactName      | Address                | City        | PostalCode | Country  |
|------------|------------------------------------|------------------|------------------------|-------------|------------|----------|
| 1          | Alfreds Futterkiste                | Maria Anders     | Obere Str. 57          | Berlin      | 12209      | Germany  |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo     | Avda. de la Constitución 2222 | México D.F. | 05021      | Mexico   |
| 3          | Antonio Moreno Taquería            | Antonio Moreno   | Mataderos 2312         | México D.F. | 05023      | Mexico   |

**Example rows (Suppliers):**

| SupplierID | SupplierName                | ContactName      | Address         | City        | PostalCode | Country |
|------------|-----------------------------|------------------|-----------------|-------------|------------|---------|
| 1          | Exotic Liquid                | Charlotte Cooper | 49 Gilbert St.  | London      | EC1 4SD    | UK      |
| 2          | New Orleans Cajun Delights   | Shelley Burke    | P.O. Box 78934  | New Orleans | 70117      | USA     |
| 3          | Grandma Kelly's Homestead    | Regina Murphy    | 707 Oxford Rd.  | Ann Arbor   | 48104      | USA     |

## Example

**Example:**  
Get all cities from both Customers and Suppliers, including duplicates.

```sql
SELECT City FROM Customers
UNION ALL
SELECT City FROM Suppliers
ORDER BY City;
```

- All city values are included, even if they appear in both tables.

## UNION ALL with WHERE

**Example:**  
Get all German cities from both tables, including duplicates.

```sql
SELECT City, Country FROM Customers
WHERE Country = 'Germany'
UNION ALL
SELECT City, Country FROM Suppliers
WHERE Country = 'Germany'
ORDER BY City;
```

- Filters for German cities in both tables.
- Duplicate city-country pairs are included.

## Key Points

- UNION ALL keeps all rows, including duplicates.
- All SELECTs must have the same number and order of columns.
- Data types must be compatible.

This allows you to combine results from multiple tables and keep all data, even if some rows are repeated.  