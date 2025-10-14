The `INNER JOIN` keyword selects records that have matching values in both tables. It's the most common type of join.

## Syntax
```sql
SELECT column_name(s)
FROM table1
INNER JOIN table2 ON table1.column_name = table2.column_name;
```

Note: `INNER JOIN` is the same as `JOIN` - the INNER keyword is optional.

## Example

**Tables:**
Orders: OrderID, CustomerID, OrderDate
Customers: CustomerID, CustomerName, ContactName, Country

**Query:**
```sql
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
```

**Result:**
Only shows orders that have a matching customer in the Customers table.

## JOIN Multiple Tables
```sql
SELECT Orders.OrderID, Customers.CustomerName, Shippers.ShipperName
FROM ((Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID)
INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID);
```

## Using Table Aliases
```sql
SELECT o.OrderID, c.CustomerName, o.OrderDate
FROM Orders o
INNER JOIN Customers c ON o.CustomerID = c.CustomerID;
```

## When to Use INNER JOIN
- When you only want records that exist in both tables
- Most common join type
- Filters out unmatched records from both tables

## Visual Representation
```
Table A    INNER JOIN    Table B
   A             B             Result
   1 ---------> 1      -->      1
   2             2      -->      2  
   3 ---------> 3      -->      3
   4                            
```
Only matching records (1, 2, 3) are returned.

## Related Concepts
- [[SQL JOINs]] - Overview of all join types
- [[SQL LEFT JOIN]] - Include all from left table
- [[SQL RIGHT JOIN]] - Include all from right table
- [[SQL FULL OUTER JOIN]] - Include all records
- [[Keys]] - Primary and foreign keys enable joins

Part of [[SQL JOINs]] in [[SQL (Structured Query Language)]] for combining related data.
