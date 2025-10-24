## Overview

The SELECT DISTINCT statement returns only unique values from a column.

## Syntax

SELECT DISTINCT column1, column2  
FROM table_name

- DISTINCT removes duplicate rows from the result.
- column1, column2: Fields to check for uniqueness.
- table_name: Table to query.

## Example

Return all unique countries from the Customers table.

```sql
SELECT DISTINCT Country FROM Customers;
```

This returns each country only once, even if it appears in multiple rows.

## Demo Table

The Customers table contains these columns:

- CustomerID
- CustomerName
- ContactName
- Address
- City
- PostalCode
- Country

**Example rows:**

| CustomerID | CustomerName                       | ContactName      | Address                | City        | PostalCode | Country  |
|------------|------------------------------------|------------------|------------------------|-------------|------------|----------|
| 1          | Alfreds Futterkiste                | Maria Anders     | Obere Str. 57          | Berlin      | 12209      | Germany  |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo     | Avda. de la Constitución 2222 | México D.F. | 05021      | Mexico   |
| 3          | Antonio Moreno Taquería            | Antonio Moreno   | Mataderos 2312         | México D.F. | 05023      | Mexico   |
| 4          | Around the Horn                    | Thomas Hardy     | 120 Hanover Sq.        | London      | WA1 1DP    | UK       |
| 5          | Berglunds snabbköp                 | Christina Berglund | Berguvsvägen 8       | Luleå       | S-958 22   | Sweden   |

## Without DISTINCT

If you do not use DISTINCT, all values are returned, including duplicates.

**Example:**  
Return every country value from the Customers table.

```sql
SELECT Country FROM Customers;
```

## Counting Distinct Values

Use COUNT with DISTINCT to count the number of unique values.

**Example:**  
Return the number of different countries.

```sql
SELECT COUNT(DISTINCT Country) FROM Customers;
```

This returns the count of unique countries.

**Note:**  
COUNT(DISTINCT column_name) is not supported in Microsoft Access.

**Workaround for MS Access:**  
Count unique countries using a subquery.

```sql
SELECT Count(*) AS DistinctCountries
FROM (SELECT DISTINCT Country FROM Customers);
```

This allows you to count unique values in Access.