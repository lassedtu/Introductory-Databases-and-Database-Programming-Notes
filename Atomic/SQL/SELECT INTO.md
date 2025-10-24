## Overview

The SELECT INTO statement copies data from one table into a new table.  
The new table is created with the same column names and data types as the source.

- You can copy all columns or only selected columns.
- You can filter rows using WHERE.
- You can copy data into another database using the IN clause.

## Syntax

Copy all columns:

```sql
SELECT *
INTO newtable
FROM oldtable
WHERE condition;
```

Copy selected columns:

```sql
SELECT column1, column2
INTO newtable
FROM oldtable
WHERE condition;
```

- The new table is created automatically.
- You can use AS to rename columns.

## Examples

**Example:**  
Create a backup of the Customers table.

```sql
SELECT * INTO CustomersBackup2017
FROM Customers;
```

**Example:**  
Copy the table into another database.

```sql
SELECT * INTO CustomersBackup2017 IN 'Backup.mdb'
FROM Customers;
```

**Example:**  
Copy only selected columns.

```sql
SELECT CustomerName, ContactName INTO CustomersBackup2017
FROM Customers;
```

**Example:**  
Copy only German customers.

```sql
SELECT * INTO CustomersGermany
FROM Customers
WHERE Country = 'Germany';
```

**Example:**  
Copy data from multiple tables using a join.

```sql
SELECT Customers.CustomerName, Orders.OrderID
INTO CustomersOrderBackup2017
FROM Customers
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```

**Example:**  
Create a new, empty table with the same structure.

```sql
SELECT * INTO newtable
FROM oldtable
WHERE 1 = 0;
```

- No rows are copied, only the schema.

## Key Points

- SELECT INTO creates a new table and copies data.
- The new table gets column names and types from the source.
- Use WHERE to filter rows.
- Use IN to copy to another database.

This allows you to quickly back up or duplicate tables.