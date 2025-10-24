## Overview

A NULL value means a field has no value. It represents missing or unknown data.

- NULL is not the same as zero or a field with spaces.
- If a field is optional and left blank, it is saved as NULL.

## Testing for NULL

You cannot use =, <, or <> to test for NULL.  
Use IS NULL or IS NOT NULL.

### IS NULL Syntax

SELECT column_names  
FROM table_name  
WHERE column_name IS NULL

### IS NOT NULL Syntax

SELECT column_names  
FROM table_name  
WHERE column_name IS NOT NULL

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

## IS NULL Example

List customers with a NULL value in the Address field.

```sql
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NULL;
```

- Use IS NULL to find fields with no value.

## IS NOT NULL Example

List customers with a value in the Address field.

```sql
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NOT NULL;
```

- Use IS NOT NULL to find fields that are not empty.

This allows you to filter records based on whether a field has a value or not.