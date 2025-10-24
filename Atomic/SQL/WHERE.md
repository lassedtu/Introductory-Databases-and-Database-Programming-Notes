## Overview

The WHERE clause filters records in a table. It returns only rows that meet a specified condition.

## Syntax

SELECT column1, column2  
FROM table_name  
WHERE condition

- WHERE defines the condition to filter rows.
- Used in SELECT, UPDATE, DELETE, and other statements.

## Example

Select all customers from Mexico.

```sql
SELECT * FROM Customers
WHERE Country = 'Mexico';
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

## Text Fields vs. Numeric Fields

- Use single quotes for text values.
- Do not use quotes for numeric values.

**Example:**  
Select the customer with CustomerID 1.

```sql
SELECT * FROM Customers
WHERE CustomerID = 1;
```

## Operators in WHERE

You can use different operators to filter data.

| Operator | Description               | Example                |
|----------|--------------------------|------------------------|
| =        | Equal                    | Country = 'Mexico'     |
| >        | Greater than             | CustomerID > 80        |
| <        | Less than                | CustomerID < 10        |
| >=       | Greater than or equal    | CustomerID >= 5        |
| <=       | Less than or equal       | CustomerID <= 20       |
| <>       | Not equal                | Country <> 'UK'        |
| BETWEEN  | Between a range          | CustomerID BETWEEN 1 AND 10 |
| LIKE     | Pattern search           | City LIKE 'M%'         |
| IN       | Multiple values          | Country IN ('Mexico', 'UK') |

This allows you to filter records based on different conditions.