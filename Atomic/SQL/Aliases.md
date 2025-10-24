## Overview

SQL aliases give a table or column a temporary name.  
Aliases make column names more readable.  
An alias only exists for the duration of the query.

## Syntax

Alias for a column:

SELECT column_name AS alias_name  
FROM table_name

Alias for a table:

SELECT column1, column2  
FROM table_name AS alias_name

- AS is optional in most databases.
- Use square brackets [ ] or double quotes " " for aliases with spaces.

## Demo Tables

Customers table:

- CustomerID
- CustomerName
- ContactName
- Address
- City
- PostalCode
- Country

Orders table:

- OrderID
- CustomerID
- EmployeeID
- OrderDate
- ShipperID

**Example rows (Customers):**

| CustomerID | CustomerName                       | ContactName      | Address                | City        | PostalCode | Country  |
|------------|------------------------------------|------------------|------------------------|-------------|------------|----------|
| 1          | Alfreds Futterkiste                | Maria Anders     | Obere Str. 57          | Berlin      | 12209      | Germany  |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo     | Avda. de la Constitución 2222 | México D.F. | 05021      | Mexico   |
| 3          | Antonio Moreno Taquería            | Antonio Moreno   | Mataderos 2312         | México D.F. | 05023      | Mexico   |

**Example rows (Orders):**

| OrderID | CustomerID | EmployeeID | OrderDate  | ShipperID |
|---------|------------|------------|------------|-----------|
| 10248   | 90         | 5          | 7/4/1996   | 3         |
| 10249   | 81         | 6          | 7/5/1996   | 1         |
| 10250   | 34         | 4          | 7/8/1996   | 2         |

## Examples

**Example:**  
Alias for a column.

```sql
SELECT CustomerID AS ID
FROM Customers;
```

**Example:**  
Alias for a column without AS.

```sql
SELECT CustomerID ID
FROM Customers;
```

**Example:**  
Alias for multiple columns.

```sql
SELECT CustomerID AS ID, CustomerName AS Customer
FROM Customers;
```

**Example:**  
Alias with spaces using square brackets.

```sql
SELECT ProductName AS [My Great Products]
FROM Products;
```

**Example:**  
Alias with spaces using double quotes.

```sql
SELECT ProductName AS "My Great Products"
FROM Products;
```

**Example:**  
Concatenate columns with an alias (SQL Server syntax).

```sql
SELECT CustomerName, Address + ', ' + PostalCode + ' ' + City + ', ' + Country AS Address
FROM Customers;
```

**Example:**  
Concatenate columns with an alias (MySQL syntax).

```sql
SELECT CustomerName, CONCAT(Address,', ',PostalCode,', ',City,', ',Country) AS Address
FROM Customers;
```

**Example:**  
Alias for a table.

```sql
SELECT * FROM Customers AS Persons;
```

**Example:**  
Table aliases in a multi-table query.

```sql
SELECT o.OrderID, o.OrderDate, c.CustomerName
FROM Customers AS c, Orders AS o
WHERE c.CustomerName='Around the Horn' AND c.CustomerID=o.CustomerID;
```

**Example:**  
Same query without aliases.

```sql
SELECT Orders.OrderID, Orders.OrderDate, Customers.CustomerName
FROM Customers, Orders
WHERE Customers.CustomerName='Around the Horn' AND Customers.CustomerID=Orders.CustomerID;
```

## Key Points

- Aliases improve readability.
- Use AS or omit it (optional).
- Use [ ] or " " for aliases with spaces.
- Table aliases are useful in multi-table queries and with long table names.