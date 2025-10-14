A JOIN clause is used to combine rows from two or more tables, based on a related column between them. JOINs are essential for working with normalized relational databases where data is spread across multiple tables.

## Types of JOINs

There are four main types of JOINs in SQL: INNER JOIN, OUTER JOIN, CROSS JOIN, and SELF JOIN. OUTER JOINs can be further divided into three subtypes: LEFT OUTER JOIN, RIGHT OUTER JOIN, and FULL OUTER JOIN.

### Visual Summary
| JOIN Type | Description |
|-----------|-------------|
| [[SQL INNER JOIN]] | Returns records with matching values in both tables |
| [[SQL LEFT JOIN]] | Returns all records from left table + matched from right |
| [[SQL RIGHT JOIN]] | Returns all records from right table + matched from left |
| [[SQL FULL OUTER JOIN]] | Returns all records when match in either table |
| [[SQL SELF JOIN]] | Table joined with itself |
| [[SQL CROSS JOIN]] | Cartesian product of both tables |

## Basic JOIN Syntax
```sql
SELECT columns
FROM table1
JOIN table2 ON table1.column = table2.column;
```

## Example Tables
**Orders table:**
| OrderID | CustomerID | OrderDate |
|---------|------------|-----------|
| 1 | 3 | 1996-07-04 |
| 2 | 4 | 1996-07-05 |

**Customers table:**
| CustomerID | CustomerName | Country |
|------------|--------------|---------|
| 3 | Ana Trujillo | Mexico |
| 4 | Antonio Moreno | Mexico |

## Basic JOIN Example
```sql
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
```

## Related Concepts
- [[SQL INNER JOIN]] - Most common join type
- [[SQL LEFT JOIN]] - Include all from left table
- [[SQL RIGHT JOIN]] - Include all from right table  
- [[SQL FULL OUTER JOIN]] - Include all from both tables
- [[SQL SELF JOIN]] - Join table with itself
- [[Keys]] - Understanding primary and foreign keys
- [[Relations]] - Relational database theory

JOINs are fundamental to [[SQL (Structured Query Language)]] and working with [[The Relational Model]].
