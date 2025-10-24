## Overview

The AND operator filters records based on multiple conditions. All conditions must be true for a row to be included.

## Syntax

SELECT column1, column2  
FROM table_name  
WHERE condition1 AND condition2 AND condition3 ...

- Use AND to combine conditions in the WHERE clause.

## Example: AND Operator

Select all customers from Spain whose names start with 'G'.

```sql
SELECT *
FROM Customers
WHERE Country = 'Spain' AND CustomerName LIKE 'G%';
```

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

## All Conditions Must Be True

All conditions joined by AND must be true.

**Example:**  
Select customers from Brazil, in Rio de Janeiro, with CustomerID greater than 50.

```sql
SELECT * FROM Customers
WHERE Country = 'Brazil'
AND City = 'Rio de Janeiro'
AND CustomerID > 50;
```

## AND vs OR

- AND: All conditions must be true.
- OR: At least one condition must be true.

## Combining AND and OR

Use parentheses to control the logic when combining AND and OR.

**Example:**  
Select all Spanish customers whose names start with "G" or "R".

```sql
SELECT * FROM Customers
WHERE Country = 'Spain' AND (CustomerName LIKE 'G%' OR CustomerName LIKE 'R%');
```

Without parentheses, the logic changes.

**Example:**  
Select all customers who are from Spain and start with "G", or start with "R" (from any country).

```sql
SELECT * FROM Customers
WHERE Country = 'Spain' AND CustomerName LIKE 'G%' OR CustomerName LIKE 'R%';
```

This means the placement of parentheses affects which records are returned.