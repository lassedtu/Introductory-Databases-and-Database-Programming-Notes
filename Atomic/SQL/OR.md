## Overview

The OR operator filters records based on multiple conditions. At least one condition must be true for a row to be included.

## Syntax

SELECT column1, column2  
FROM table_name  
WHERE condition1 OR condition2 OR condition3 ...

- Use OR to combine conditions in the WHERE clause.

## Example: OR Operator

Select all customers from Germany or Spain.

```sql
SELECT *
FROM Customers
WHERE Country = 'Germany' OR Country = 'Spain';
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

## At Least One Condition Must Be True

OR returns a row if any condition is true.

**Example:**  
Select customers where City is "Berlin", CustomerName starts with "G", or Country is "Norway".

```sql
SELECT * FROM Customers
WHERE City = 'Berlin' OR CustomerName LIKE 'G%' OR Country = 'Norway';
```

## OR vs AND

- OR: At least one condition must be true.
- AND: All conditions must be true.

## Combining AND and OR

Use parentheses to control logic when combining AND and OR.

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

This means parentheses are important for correct filtering.