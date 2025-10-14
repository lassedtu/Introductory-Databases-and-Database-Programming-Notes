The `IS NULL` operator is used to test for empty values ([[NULL]] values). A field with a NULL value is a field with no value.

## Syntax
```sql
SELECT column_names
FROM table_name
WHERE column_name IS NULL;
```

## Examples

**Find records with NULL values:**
```sql
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NULL;
```

**Find records without NULL values:**
```sql
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NOT NULL;
```

## Important Notes

**Cannot use = or <> with NULL:**
```sql
-- WRONG - This will not work
WHERE Address = NULL

-- CORRECT - Use IS NULL
WHERE Address IS NULL
```

**NULL in calculations:**
Any arithmetic operation with NULL results in NULL:
```sql
SELECT Price, Discount, (Price - Discount) AS FinalPrice
FROM Products
WHERE Discount IS NOT NULL;  -- Avoid NULL calculations
```

## Handling NULL Values
See [[SQL NULL Functions]] for functions that handle NULL values:
- `ISNULL()` - Replace NULL with specified value
- `COALESCE()` - Return first non-NULL value
- `NULLIF()` - Return NULL if values are equal

## Related Concepts
- [[NULL]] - Understanding NULL values
- [[SQL NULL Functions]] - Functions to handle NULLs
- [[SQL WHERE Clause]] - Main filtering mechanism
- [[SQL CASE Statement]] - Conditional logic for NULLs
- [[Domains]] - Domain constraints and NULL handling

Essential for handling missing data in [[SQL (Structured Query Language)]] queries.
