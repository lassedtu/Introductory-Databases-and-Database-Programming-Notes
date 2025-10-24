## Overview

The LIKE operator is used in a WHERE clause to search for a specified pattern in a column.  
LIKE supports wildcards for flexible matching.

## Syntax

SELECT column1, column2  
FROM table_name  
WHERE columnN LIKE pattern

- LIKE matches a pattern in a column.
- % matches zero, one, or multiple characters.
- _ matches exactly one character.
- WHERE filters which rows are included.

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

## Wildcards

- % matches any number of characters (including zero).
- _ matches exactly one character.

## Examples

**Example:**  
Return all customers whose name starts with "a".

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE 'a%';
```

**Example:**  
Return all customers from a city that starts with 'L', followed by one character, then 'nd', then two characters.

```sql
SELECT * FROM Customers
WHERE City LIKE 'L_nd__';
```

**Example:**  
Return all customers from a city that contains the letter 'L'.

```sql
SELECT * FROM Customers
WHERE City LIKE '%L%';
```

**Example:**  
Return all customers whose name starts with 'La'.

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE 'La%';
```

**Example:**  
Return all customers whose name starts with 'a' or 'b'.

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE 'a%' OR CustomerName LIKE 'b%';
```

**Example:**  
Return all customers whose name ends with 'a'.

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '%a';
```

**Example:**  
Return all customers whose name starts with 'b' and ends with 's'.

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE 'b%s';
```

**Example:**  
Return all customers whose name contains 'or'.

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '%or%';
```

**Example:**  
Return all customers whose name starts with "a" and is at least 3 characters long.

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE 'a__%';
```

**Example:**  
Return all customers with "r" in the second position.

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '_r%';
```

**Example:**  
Return all customers from Spain (no wildcard).

```sql
SELECT * FROM Customers
WHERE Country LIKE 'Spain';
```

## Key Points

- LIKE is used for pattern matching in SQL.
- % and _ are the main wildcards.
- Patterns can be combined for flexible searches.
- Without wildcards, LIKE works as an exact match.