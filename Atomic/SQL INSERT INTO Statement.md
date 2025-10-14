The `INSERT INTO` statement is used to insert new records in a table.

## Syntax

**Specify both columns and values:**
```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

**Insert into all columns (same order as table):**
```sql
INSERT INTO table_name
VALUES (value1, value2, value3, ...);
```

## Examples

**Insert specific columns:**
```sql
INSERT INTO Customers (CustomerName, ContactName, Country)
VALUES ('Cardinal', 'Tom B. Erichsen', 'Norway');
```

**Insert all columns:**
```sql
INSERT INTO Customers
VALUES ('Cardinal', 'Tom B. Erichsen', 'Address', 'Stavanger', '4006', 'Norway');
```

**Insert multiple rows:**
```sql
INSERT INTO Customers (CustomerName, ContactName, Country)
VALUES 
    ('Cardinal', 'Tom B. Erichsen', 'Norway'),
    ('Greasy Burger', 'Per Olsen', 'Denmark'),
    ('Tasty Donuts', 'Georg Pipps', 'Germany');
```

## Insert with NULL Values
When not specifying all columns, unspecified columns will get [[NULL]] values (if allowed):
```sql
INSERT INTO Customers (CustomerName, Country)
VALUES ('White Cliffs', 'UK');
-- ContactName and other columns will be NULL
```

## Insert from Another Table
See [[SQL INSERT INTO SELECT]] for copying data from another table.

## Data Types
Values must match the [[Domain Types]] of their columns:
- Text values: Use single quotes `'text'`
- Numeric values: No quotes `123` or `45.67`
- Date values: Use single quotes `'2023-12-25'`

## Related Concepts
- [[SQL UPDATE Statement]] - Modify existing records
- [[SQL DELETE Statement]] - Remove records
- [[SQL INSERT INTO SELECT]] - Insert from query results
- [[NULL]] - Handling missing values
- [[Data Manipulation Language (DML)]] - Category of SQL commands

Part of [[Data Manipulation Language (DML)]] in [[SQL (Structured Query Language)]] for adding data.
