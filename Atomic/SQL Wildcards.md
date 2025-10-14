Wildcards are special characters used with the [[SQL LIKE Operator]] to search for patterns in text data. They provide flexible string matching capabilities in SQL queries.

## Wildcard Characters

### % (Percent Sign)
Represents zero, one, or multiple characters.

**Examples:**
```sql
-- Names starting with "A"
SELECT * FROM Customers WHERE CustomerName LIKE 'A%';

-- Names ending with "son"  
SELECT * FROM Customers WHERE CustomerName LIKE '%son';

-- Names containing "market"
SELECT * FROM Customers WHERE CustomerName LIKE '%market%';
```

### _ (Underscore)
Represents exactly one character.

**Examples:**
```sql
-- Names starting with "A" and exactly 3 characters long
SELECT * FROM Customers WHERE CustomerName LIKE 'A__';

-- Names with "o" as second character
SELECT * FROM Customers WHERE CustomerName LIKE '_o%';

-- Phone numbers in format XXX-XXXX
SELECT * FROM Customers WHERE Phone LIKE '___-____';
```

### [] (Brackets) - SQL Server/MS Access
Represents any single character within the brackets.

**Examples:**
```sql
-- Names starting with A, B, or C
SELECT * FROM Customers WHERE CustomerName LIKE '[ABC]%';

-- Names starting with any letter from A to M
SELECT * FROM Customers WHERE CustomerName LIKE '[A-M]%';

-- Names starting with any digit
SELECT * FROM Customers WHERE CustomerName LIKE '[0-9]%';
```

### [^] or [!] (NOT Brackets) - SQL Server/MS Access
Represents any character NOT in the brackets.

**Examples:**
```sql
-- Names NOT starting with A, B, or C
SELECT * FROM Customers WHERE CustomerName LIKE '[^ABC]%';

-- Names NOT starting with letters A through M
SELECT * FROM Customers WHERE CustomerName LIKE '[!A-M]%';
```

## Practical Examples

**Email validation pattern:**
```sql
SELECT * FROM Users 
WHERE Email LIKE '%@%.%' 
AND Email NOT LIKE '%@%@%';  -- No multiple @ symbols
```

**Product codes with specific format:**
```sql
-- Product codes like "AB-1234"
SELECT * FROM Products 
WHERE ProductCode LIKE '__-____';
```

**Date patterns (as text):**
```sql
-- Dates in YYYY-MM-DD format
SELECT * FROM Orders 
WHERE OrderDate LIKE '____-__-__';
```

**Combining wildcards:**
```sql
-- Names starting with A, second character is vowel, minimum 4 characters
SELECT * FROM Customers 
WHERE CustomerName LIKE 'A[AEIOU]_%';
```

## Database-Specific Differences

| Database | % | _ | [] | [^] | Notes |
|----------|---|---|----|----|-------|
| MySQL | ✓ | ✓ | ✗ | ✗ | Use REGEXP for advanced patterns |
| SQL Server | ✓ | ✓ | ✓ | ✓ | Full wildcard support |
| PostgreSQL | ✓ | ✓ | ✗ | ✗ | Use SIMILAR TO or ~ for regex |
| Oracle | ✓ | ✓ | ✗ | ✗ | Use REGEXP_LIKE for patterns |

## Escaping Wildcards
To search for literal wildcard characters:

```sql
-- Search for names containing actual % character
SELECT * FROM Customers 
WHERE CustomerName LIKE '%[%]%';  -- SQL Server

-- Or using ESCAPE clause
SELECT * FROM Customers 
WHERE CustomerName LIKE '%\%%' ESCAPE '\';  -- Standard SQL
```

## Related Concepts
- [[SQL LIKE Operator]] - Primary operator using wildcards
- [[SQL WHERE Clause]] - Context for wildcard usage
- [[SQL Regular Expressions]] - More powerful pattern matching
- [[SQL Text Functions]] - Other string manipulation tools
- [[SQL Pattern Matching]] - General concept of pattern searching

Essential for flexible text searching and pattern matching in [[SQL (Structured Query Language)]] and [[SQL Queries]].
