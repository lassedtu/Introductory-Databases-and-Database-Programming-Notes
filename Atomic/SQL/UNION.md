## Overview

The UNION operator combines the result sets of two or more SELECT statements.  
UNION removes duplicate rows from the final result.

- Each SELECT must have the same number of columns.
- Columns must have similar data types and be in the same order.

## Syntax

SELECT column_name(s) FROM table1  
UNION  
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
Get all unique cities from both Customers and Suppliers.

```sql
SELECT City FROM Customers
UNION
SELECT City FROM Suppliers
ORDER BY City;
```

- Only distinct cities are returned.
- If a city appears in both tables, it is listed once.

## UNION with WHERE

**Example:**  
Get all German cities from both tables.

```sql
SELECT City, Country FROM Customers
WHERE Country = 'Germany'
UNION
SELECT City, Country FROM Suppliers
WHERE Country = 'Germany'
ORDER BY City;
```

- Filters for German cities in both tables.
- Only unique city-country pairs are returned.

## UNION with Aliases

**Example:**  
List all customers and suppliers with their type.

```sql
SELECT 'Customer' AS Type, ContactName, City, Country
FROM Customers
UNION
SELECT 'Supplier', ContactName, City, Country
FROM Suppliers;
```

- The "Type" column shows if the row is a Customer or Supplier.
- SQL aliases give temporary names to columns.

## Key Points

- UNION removes duplicates. Use UNION ALL to keep duplicates.
- All SELECTs must have the same number and order of columns.
- Data types must be compatible.

This allows you to combine results from multiple tables into one set.  