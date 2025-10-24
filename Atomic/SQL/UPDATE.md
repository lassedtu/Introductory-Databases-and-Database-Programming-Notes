## Overview

The UPDATE statement changes existing records in a table.

## Syntax

UPDATE table_name  
SET column1 = value1, column2 = value2  
WHERE condition

- SET assigns new values to columns.
- WHERE specifies which rows to update.
- If you omit WHERE, all rows are updated.

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

| CustomerID | CustomerName         | ContactName      | Address           | City      | PostalCode | Country  |
|------------|---------------------|------------------|-------------------|-----------|------------|----------|
| 1          | Alfreds Futterkiste | Maria Anders     | Obere Str. 57     | Berlin    | 12209      | Germany  |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo | Avda. de la Constitución 2222 | México D.F. | 05021 | Mexico   |
| 3          | Antonio Moreno Taquería | Antonio Moreno | Mataderos 2312   | México D.F. | 05023    | Mexico   |
| 4          | Around the Horn     | Thomas Hardy     | 120 Hanover Sq.   | London    | WA1 1DP    | UK       |
| 5          | Berglunds snabbköp  | Christina Berglund | Berguvsvägen 8 | Luleå     | S-958 22   | Sweden   |

## Update a Single Record

Update the first customer’s contact name and city.

```sql
UPDATE Customers
SET ContactName = 'Alfred Schmidt', City = 'Frankfurt'
WHERE CustomerID = 1;
```

- Only the row with CustomerID = 1 is updated.

## Update Multiple Records

Update all customers in Mexico to have ContactName 'Juan'.

```sql
UPDATE Customers
SET ContactName = 'Juan'
WHERE Country = 'Mexico';
```

- All rows where Country is 'Mexico' are updated.

## Update All Records

If you omit the WHERE clause, every row is updated.

```sql
UPDATE Customers
SET ContactName = 'Juan';
```

- All ContactName values in the table become 'Juan'.

## Warning

Always use a WHERE clause to avoid updating all records by mistake.

This allows you to change data in one or more rows as needed.