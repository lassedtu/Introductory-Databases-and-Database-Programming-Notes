## Overview

The INSERT INTO statement adds new records to a table.

## Syntax

There are two ways to use INSERT INTO.

### 1. Specify Columns

INSERT INTO table_name (column1, column2, column3)  
VALUES (value1, value2, value3)

- List the columns to insert data into.
- Provide values in the same order as the columns.

### 2. All Columns

INSERT INTO table_name  
VALUES (value1, value2, value3)

- Do not list columns.
- Provide values for every column, in the correct order.

## Demo Table

The Customers table contains these columns:

- CustomerID (auto-increment)
- CustomerName
- ContactName
- Address
- City
- PostalCode
- Country

**Example rows:**

| CustomerID | CustomerName         | ContactName      | Address                      | City      | PostalCode | Country |
|------------|---------------------|------------------|------------------------------|-----------|------------|---------|
| 89         | White Clover Markets | Karl Jablonski   | 305 - 14th Ave. S. Suite 3B  | Seattle   | 98128      | USA     |
| 90         | Wilman Kala         | Matti Karttunen  | Keskuskatu 45                | Helsinki  | 21240      | Finland |
| 91         | Wolski              | Zbyszek          | ul. Filtrowa 68              | Walla     | 01-012     | Poland  |

## Insert Example

Add a new customer with all details except CustomerID.

```sql
INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway');
```

- CustomerID is auto-incremented and does not need to be specified.

## Insert Data in Specific Columns

You can insert data into only some columns.

```sql
INSERT INTO Customers (CustomerName, City, Country)
VALUES ('Cardinal', 'Stavanger', 'Norway');
```

- Other columns will be set to NULL or default values.
- CustomerID is still auto-incremented.

## Insert Multiple Rows

You can insert several records in one statement.

```sql
INSERT INTO Customers (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES
('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway'),
('Greasy Burger', 'Per Olsen', 'Gateveien 15', 'Sandnes', '4306', 'Norway'),
('Tasty Tee', 'Finn Egan', 'Streetroad 19B', 'Liverpool', 'L1 0AA', 'UK');
```

- Separate each set of values with a comma.

## Result

After inserting, the Customers table will include the new rows. CustomerID values are assigned automatically.

This allows you to add one or more records to a table.