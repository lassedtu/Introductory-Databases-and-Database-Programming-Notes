## Overview

The ANY and ALL operators compare a single value to a set of values returned by a subquery.

- ANY returns TRUE if the comparison is true for at least one value.
- ALL returns TRUE only if the comparison is true for every value.

## ANY Operator

- Used with standard comparison operators (=, <>, !=, >, >=, <, <=).
- Returns TRUE if any value in the subquery meets the condition.

### Syntax

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name operator ANY
  (SELECT column_name FROM table_name WHERE condition);
```

## ALL Operator

- Used with standard comparison operators.
- Returns TRUE only if all values in the subquery meet the condition.

### Syntax

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name operator ALL
  (SELECT column_name FROM table_name WHERE condition);
```

## Demo Tables

Products table:

| ProductID | ProductName                      | SupplierID | CategoryID | Unit                | Price  |
|-----------|----------------------------------|------------|------------|---------------------|--------|
| 1         | Chais                            | 1          | 1          | 10 boxes x 20 bags  | 18     |
| 2         | Chang                            | 1          | 1          | 24 - 12 oz bottles  | 19     |
| 3         | Aniseed Syrup                    | 1          | 2          | 12 - 550 ml bottles | 10     |
| 4         | Chef Anton's Cajun Seasoning     | 2          | 2          | 48 - 6 oz jars      | 22     |
| 5         | Chef Anton's Gumbo Mix           | 2          | 2          | 36 boxes            | 21.35  |
| 6         | Grandma's Boysenberry Spread     | 3          | 2          | 12 - 8 oz jars      | 25     |
| 7         | Uncle Bob's Organic Dried Pears  | 3          | 7          | 12 - 1 lb pkgs.     | 30     |
| 8         | Northwoods Cranberry Sauce       | 3          | 2          | 12 - 12 oz jars     | 40     |
| 9         | Mishi Kobe Niku                  | 4          | 6          | 18 - 500 g pkgs.    | 97     |

OrderDetails table:

| OrderDetailID | OrderID | ProductID | Quantity |
|---------------|---------|-----------|----------|
| 1             | 10248   | 11        | 12       |
| 2             | 10248   | 42        | 10       |
| 3             | 10248   | 72        | 5        |
| 4             | 10249   | 14        | 9        |
| 5             | 10249   | 51        | 40       |
| 6             | 10250   | 41        | 10       |
| 7             | 10250   | 51        | 35       |
| 8             | 10250   | 65        | 15       |
| 9             | 10251   | 22        | 6        |
| 10            | 10251   | 57        | 15       |

## Examples

### ANY Examples

**Example:**  
List products that appear in any order with quantity 10.

```sql
SELECT ProductName
FROM Products
WHERE ProductID = ANY
  (SELECT ProductID FROM OrderDetails WHERE Quantity = 10);
```

- Returns products with at least one order of quantity 10.

**Example:**  
List products that appear in any order with quantity greater than 99.

```sql
SELECT ProductName
FROM Products
WHERE ProductID = ANY
  (SELECT ProductID FROM OrderDetails WHERE Quantity > 99);
```

- Returns products with at least one order of quantity over 99.

**Example:**  
List products that appear in any order with quantity greater than 1000.

```sql
SELECT ProductName
FROM Products
WHERE ProductID = ANY
  (SELECT ProductID FROM OrderDetails WHERE Quantity > 1000);
```

- Returns no products if no order has quantity over 1000.

### ALL Examples

**Example:**  
List all product names.

```sql
SELECT ALL ProductName
FROM Products
WHERE TRUE;
```

- Returns all products. The ALL keyword is optional here.

**Example:**  
List products where all related order quantities are 10.

```sql
SELECT ProductName
FROM Products
WHERE ProductID = ALL
  (SELECT ProductID FROM OrderDetails WHERE Quantity = 10);
```

- Returns products only if every related order has quantity 10.
- Usually returns no rows unless all orders for a product have quantity 10.

## Key Points

- ANY returns TRUE if at least one value matches.
- ALL returns TRUE only if every value matches.
- Use with standard comparison operators.

This allows you to compare a value to a set of values from a subquery.