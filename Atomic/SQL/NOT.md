## Overview

The NOT operator reverses a condition. It returns rows where the condition is false.

## Syntax

SELECT column1, column2  
FROM table_name  
WHERE NOT condition

- NOT is used with other operators to get the opposite result.

## Example: NOT Operator

Select all customers that are not from Spain.

```sql
SELECT * FROM Customers
WHERE NOT Country = 'Spain';
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

## NOT with Other Operators

You can use NOT with LIKE, BETWEEN, IN, and comparison operators.

### NOT LIKE

Select customers whose names do not start with 'A'.

```sql
SELECT * FROM Customers
WHERE CustomerName NOT LIKE 'A%';
```

### NOT BETWEEN

Select customers with CustomerID not between 10 and 60.

```sql
SELECT * FROM Customers
WHERE CustomerID NOT BETWEEN 10 AND 60;
```

### NOT IN

Select customers not from Paris or London.

```sql
SELECT * FROM Customers
WHERE City NOT IN ('Paris', 'London');
```

### NOT Greater Than

Select customers with CustomerID not greater than 50.

```sql
SELECT * FROM Customers
WHERE NOT CustomerID > 50;
```

### NOT Less Than

Select customers with CustomerID not less than 50.

```sql
SELECT * FROM Customers
WHERE NOT CustomerID < 50;
```

This allows you to filter out rows that match a specific condition.