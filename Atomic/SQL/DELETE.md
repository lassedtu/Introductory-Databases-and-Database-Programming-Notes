## Overview

The DELETE statement removes records from a table.

## Syntax

DELETE FROM table_name  
WHERE condition

- WHERE specifies which rows to delete.
- If you omit WHERE, all rows are deleted.

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

## Delete a Specific Record

Delete the customer "Alfreds Futterkiste".

```sql
DELETE FROM Customers
WHERE CustomerName = 'Alfreds Futterkiste';
```

- Only the row with CustomerName 'Alfreds Futterkiste' is deleted.

## Delete All Records

Delete every row in the table, but keep the table structure.

```sql
DELETE FROM Customers;
```

- All rows are removed.
- Table structure and indexes remain.

## Delete a Table

Remove the entire table, including its structure.

```sql
DROP TABLE Customers;
```

- The table and all its data are deleted.

## Warning

Always use a WHERE clause to avoid deleting all records by mistake.  
Use DROP TABLE only if you want to remove the table completely.