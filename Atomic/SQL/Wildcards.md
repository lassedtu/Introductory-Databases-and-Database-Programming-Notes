## Overview

A wildcard character is used to substitute one or more characters in a string.  
Wildcards are used with the LIKE operator in a WHERE clause to search for a specified pattern in a column.

## Wildcard Characters

| Symbol | Description                                   | Supported In                |
|--------|-----------------------------------------------|-----------------------------|
| %      | Represents zero or more characters            | All SQL databases           |
| _      | Represents a single character                 | All SQL databases           |
| []     | Any single character within the brackets      | Not in PostgreSQL/MySQL     |
| -      | Any single character within a specified range | Not in PostgreSQL/MySQL     |
| ^      | Any character not in the brackets             | Not in PostgreSQL/MySQL     |
| { }    | Escaped character (Oracle only)               | Oracle only                 |

## Syntax

SELECT column1, column2  
FROM table_name  
WHERE columnN LIKE pattern

- LIKE matches a pattern in a column.
- Wildcards can be combined for flexible matching.

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

## Using the % Wildcard

% matches any number of characters, including zero.

**Example:**  
Return all customers whose name ends with 'es'.

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '%es';
```

**Example:**  
Return all customers whose name contains 'mer'.

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '%mer%';
```

## Using the _ Wildcard

_ matches exactly one character.

**Example:**  
Return all customers with a City starting with any character, followed by "ondon".

```sql
SELECT * FROM Customers
WHERE City LIKE '_ondon';
```

**Example:**  
Return all customers with a City starting with "L", followed by any 3 characters, ending with "on".

```sql
SELECT * FROM Customers
WHERE City LIKE 'L___on';
```

## Using the [] Wildcard

[] matches any single character inside the brackets.  
Not supported in PostgreSQL and MySQL.

**Example:**  
Return all customers whose name starts with "b", "s", or "p".

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '[bsp]%';
```

## Using the - Wildcard

- inside [] matches any single character within the specified range.  
Not supported in PostgreSQL and MySQL.

**Example:**  
Return all customers whose name starts with "a", "b", "c", "d", "e", or "f".

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE '[a-f]%';
```

## Combine Wildcards

Wildcards can be combined for more complex patterns.

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

## Without Wildcard

If no wildcard is used, LIKE works as an exact match.

**Example:**  
Return all customers from Spain.

```sql
SELECT * FROM Customers
WHERE Country LIKE 'Spain';
```

## Microsoft Access Wildcards

| Symbol | Description                                   | Example                        |
|--------|-----------------------------------------------|--------------------------------|
| *      | Zero or more characters                       | bl* finds bl, black, blue      |
| ?      | Single character                              | h?t finds hot, hat, hit        |
| []     | Any single character within the brackets      | h[oa]t finds hot, hat          |
| !      | Any character not in the brackets             | h[!oa]t finds hit              |
| -      | Any single character within a specified range | c[a-b]t finds cat, cbt         |
| #      | Any single numeric character                  | 2#5 finds 205, 215, ..., 295   |

## Key Points

- Wildcards allow flexible pattern matching with LIKE.
- % and _ are standard in all SQL databases.
- [], -, and ^ are not supported in PostgreSQL and MySQL.
- Without wildcards, LIKE is the same as =.