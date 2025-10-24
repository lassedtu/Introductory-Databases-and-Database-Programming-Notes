## Overview

SQL provides functions to handle NULL values.  
These functions let you replace NULL with a default value.  
This is useful when calculations or results should not be NULL.

## Common Functions

- IFNULL() — MySQL
- ISNULL() — SQL Server
- COALESCE() — Standard SQL, supported in most databases
- NVL() — Oracle

## Demo Table

| P_Id | ProductName  | UnitPrice | UnitsInStock | UnitsOnOrder |
|------|--------------|-----------|--------------|--------------|
| 1    | Jarlsberg    | 10.45     | 16           | 15           |
| 2    | Mascarpone   | 32.56     | 23           | NULL         |
| 3    | Gorgonzola   | 15.67     | 9            | 20           |

- "UnitsOnOrder" can be NULL.

## Problem

If you add a NULL value in a calculation, the result is NULL.

**Example:**

```sql
SELECT ProductName, UnitPrice * (UnitsInStock + UnitsOnOrder)
FROM Products;
```

- If UnitsOnOrder is NULL, the result is NULL.

## Solutions by Database

### MySQL

- Use IFNULL() or COALESCE().

```sql
SELECT ProductName, UnitPrice * (UnitsInStock + IFNULL(UnitsOnOrder, 0))
FROM Products;
```

```sql
SELECT ProductName, UnitPrice * (UnitsInStock + COALESCE(UnitsOnOrder, 0))
FROM Products;
```

### SQL Server

- Use ISNULL() or COALESCE().

```sql
SELECT ProductName, UnitPrice * (UnitsInStock + ISNULL(UnitsOnOrder, 0))
FROM Products;
```

```sql
SELECT ProductName, UnitPrice * (UnitsInStock + COALESCE(UnitsOnOrder, 0))
FROM Products;
```

### MS Access

- Use IIF() with IsNull().

```sql
SELECT ProductName, UnitPrice * (UnitsInStock + IIF(IsNull(UnitsOnOrder), 0, UnitsOnOrder))
FROM Products;
```

### Oracle

- Use NVL() or COALESCE().

```sql
SELECT ProductName, UnitPrice * (UnitsInStock + NVL(UnitsOnOrder, 0))
FROM Products;
```

```sql
SELECT ProductName, UnitPrice * (UnitsInStock + COALESCE(UnitsOnOrder, 0))
FROM Products;
```

## Function Comparison

| Function   | Database      | Usage Example                                  |
|------------|--------------|------------------------------------------------|
| IFNULL()   | MySQL        | IFNULL(UnitsOnOrder, 0)                        |
| ISNULL()   | SQL Server   | ISNULL(UnitsOnOrder, 0)                        |
| COALESCE() | All          | COALESCE(UnitsOnOrder, 0)                      |
| NVL()      | Oracle       | NVL(UnitsOnOrder, 0)                           |
| IIF/IsNull | MS Access    | IIF(IsNull(UnitsOnOrder), 0, UnitsOnOrder)     |

## Key Points

- Use these functions to replace NULL with a default value.
- COALESCE() is standard and works in most databases.
- This allows calculations to work even if some values are missing.