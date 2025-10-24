## Overview

SQL uses operators to perform calculations, compare values, and control logic in queries.

## Arithmetic Operators

| Operator | Description   | Example   |
|----------|--------------|-----------|
| +        | Add          | a + b     |
| -        | Subtract     | a - b     |
| *        | Multiply     | a * b     |
| /        | Divide       | a / b     |
| %        | Modulo       | a % b     |

**Example:**  
Add two columns.

```sql
SELECT Price + Tax AS Total FROM Products;
```

## Bitwise Operators

| Operator | Description           |
|----------|----------------------|
| &        | Bitwise AND          |
| \|       | Bitwise OR           |
| ^        | Bitwise exclusive OR |

## Comparison Operators

| Operator | Description               | Example   |
|----------|--------------------------|-----------|
| =        | Equal to                 | a = b     |
| >        | Greater than             | a > b     |
| <        | Less than                | a < b     |
| >=       | Greater than or equal to | a >= b    |
| <=       | Less than or equal to    | a <= b    |
| <>       | Not equal to             | a <> b    |

**Example:**  
Select rows where price is greater than 100.

```sql
SELECT * FROM Products WHERE Price > 100;
```

## Compound Operators

| Operator | Description                |
|----------|---------------------------|
| +=       | Add equals                |
| -=       | Subtract equals           |
| *=       | Multiply equals           |
| /=       | Divide equals             |
| %=       | Modulo equals             |
| &=       | Bitwise AND equals        |
| ^=       | Bitwise exclusive equals  |
| \|=      | Bitwise OR equals         |

## Logical Operators

| Operator | Description                                         | Example                |
|----------|-----------------------------------------------------|------------------------|
| ALL      | TRUE if all subquery values meet the condition      | a > ALL (subquery)     |
| AND      | TRUE if all conditions are TRUE                     | a = 1 AND b = 2        |
| ANY      | TRUE if any subquery value meets the condition      | a = ANY (subquery)     |
| BETWEEN  | TRUE if value is within a range                     | a BETWEEN 1 AND 10     |
| EXISTS   | TRUE if subquery returns one or more records        | EXISTS (subquery)      |
| IN       | TRUE if value matches any in a list                 | a IN (1, 2, 3)         |
| LIKE     | TRUE if value matches a pattern                     | a LIKE 'A%'            |
| NOT      | TRUE if condition is NOT TRUE                       | NOT a = 1              |
| OR       | TRUE if any condition is TRUE                       | a = 1 OR b = 2         |
| SOME     | TRUE if any subquery value meets the condition      | a > SOME (subquery)    |

## Key Points

- Arithmetic operators perform math.
- Comparison operators compare values.
- Logical operators control query logic.
- Compound and bitwise operators are used for advanced operations.

**Example:**  
Select products with price between 10 and 20.

```sql
SELECT * FROM Products WHERE Price BETWEEN 10 AND 20;
```

This allows you to filter, calculate, and control data in your SQL queries.