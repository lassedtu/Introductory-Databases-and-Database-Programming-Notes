## Overview

![[right-join.png | center | 400]]

The RIGHT JOIN keyword returns all records from the right table and the matching records from the left table.  
If there is no match, the result is NULL from the left table.  
RIGHT JOIN is also called RIGHT OUTER JOIN in some databases.

## Syntax

SELECT column1, column2  
FROM table1  
RIGHT JOIN table2  
ON table1.column = table2.column

- All rows from the right table are included.
- Matching rows from the left table are included. If no match, left table columns are NULL.

## Demo Tables

Orders table:

- OrderID
- CustomerID
- EmployeeID
- OrderDate
- ShipperID

Employees table:

- EmployeeID
- LastName
- FirstName
- BirthDate
- Photo

**Example rows (Orders):**

| OrderID | CustomerID | EmployeeID | OrderDate   | ShipperID |
|---------|------------|------------|-------------|-----------|
| 10308   | 2          | 7          | 1996-09-18  | 3         |
| 10309   | 37         | 3          | 1996-09-19  | 1         |
| 10310   | 77         | 8          | 1996-09-20  | 2         |

**Example rows (Employees):**

| EmployeeID | LastName   | FirstName | BirthDate   | Photo      |
|------------|------------|-----------|-------------|------------|
| 1          | Davolio    | Nancy     | 12/8/1968   | EmpID1.pic |
| 2          | Fuller     | Andrew    | 2/19/1952   | EmpID2.pic |
| 3          | Leverling  | Janet     | 8/30/1963   | EmpID3.pic |

## Example

**Example:**  
Return all employees and any orders they might have placed.

```sql
SELECT Orders.OrderID, Employees.LastName, Employees.FirstName
FROM Orders
RIGHT JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
ORDER BY Orders.OrderID;
```

- All employees are listed.
- If an employee has no orders, OrderID is NULL.

## Key Points

- RIGHT JOIN returns all rows from the right table.
- Returns matching rows from the left table, or NULL if no match.
- Use RIGHT JOIN to find records in the right table without matches in the left table.

See also: [[SELECT DISTINCT]], [[DELETE]]