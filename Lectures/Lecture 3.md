# SQL Data Queries (Revisited)

SQL queries are used to retrieve data from one or more tables in a database. The general form is:

``` SQL
SELECT A1, A2, ..., An
FROM r1, r2, ..., rm
WHERE P;
```

- $A_i$: An attribute (column) you want to retrieve.
- $r_i$: A relation, which can be a table or the result of a join between tables.
- $P$: A predicate, which is a condition that each row must satisfy (evaluates to TRUE or FALSE).

**Key Points:**
- The result of a SELECT query is always a table (even if it has only one row or column).
- The WHERE clause filters rows based on the predicate $P$.

---

# String Operations (sec. 3.4.2)

Strings in SQL are sequences of characters, typically enclosed in single quotes (' ').

- **Escaping Characters:**  
  To include a single quote or backslash in a string, use \' or \\, respectively.
- **Comparison Operators:**  
  = (equal), <> (not equal), < (less than), > (greater than).  
  *Note:* By SQL standard, string comparisons are case-sensitive, but some databases like MySQL are case-insensitive by default.
- **String Functions:**  
  - `CONCAT(s1, s2, ...)` – Concatenates strings.
  - `LENGTH(s)` – Returns the length of a string.
  - `SUBSTRING(s, start, length)` – Extracts a substring.

## Pattern Matching with LIKE

The `LIKE` operator is used for pattern matching in strings.

- `%` matches any sequence of zero or more characters.
- `_` matches exactly one character.

**Examples:**
- `'Intro%'` matches any string starting with "Intro" (e.g., "Introduction").
- `'%duc%'` matches any string containing "duc" anywhere.
- `'___'` (three underscores) matches any string of exactly three characters.
- `'___%'` matches any string of at least three characters.

**Sample Query:**
``` SQL
SELECT InstName FROM Instructor
WHERE InstName LIKE '%ri%';
```
This finds all instructor names containing "ri".

---

# NULL Values (sec. 3.6)

NULL represents missing, unknown, or inapplicable data.

- **Arithmetic with NULL:**  
  Any arithmetic operation involving NULL results in NULL (unknown).
- **Testing for NULL:**  
  Use `IS NULL` or `IS NOT NULL` in conditions.

**Example:**
``` SQL
SELECT InstName FROM Instructor
WHERE Salary IS NULL;
```
Finds instructors whose salary is unknown.

## Three-Valued Logic

SQL uses three-valued logic: TRUE, FALSE, and UNKNOWN (when NULL is involved).

- Any comparison with NULL yields UNKNOWN.
- In WHERE and HAVING clauses, only rows where the condition is TRUE are included; UNKNOWN is treated as FALSE.

---

# Aggregate Functions (sec. 3.7)

Aggregate functions compute a single result from a set of input values.

- `AVG(A)`: Average value of A.
- `MIN(A)`: Minimum value of A.
- `MAX(A)`: Maximum value of A.
- `SUM(A)`: Sum of values in A.
- `COUNT(A)`: Number of non-NULL values in A.

**Important:**
- Aggregate functions ignore NULL values (except `COUNT(*)`, which counts all rows, including those with NULLs).

**Example:**
``` SQL
SELECT AVG(Salary), MIN(Salary), MAX(Salary), SUM(Salary), COUNT(Salary)
FROM Instructor;
```

- `COUNT(*)` counts all rows.
- `COUNT(Salary)` counts only rows where Salary is not NULL.

---

# GROUP BY and HAVING

`GROUP BY` is used to group rows that have the same values in specified columns, so aggregate functions can be applied to each group.

**Example:**
``` SQL
SELECT DeptName, AVG(Salary)
FROM Instructor
GROUP BY DeptName;
```
- Groups instructors by department and computes the average salary for each department.

## HAVING

`HAVING` is used to filter groups after aggregation (unlike WHERE, which filters rows before grouping).

**Example:**
``` SQL
SELECT DeptName, AVG(Salary)
FROM Instructor
GROUP BY DeptName
HAVING AVG(Salary) > 65000;
```
- Only departments with an average salary above 65,000 are included.

---

# Subqueries (sec. 3.8)

A subquery is a SELECT statement nested inside another query.

- Can appear in WHERE, FROM, HAVING, or SELECT clauses.

## Scalar Subqueries

A scalar subquery returns a single value.

**Example:**
``` SQL
SELECT InstName FROM Instructor
WHERE Salary > (SELECT AVG(Salary) FROM Instructor);
```
- Finds instructors whose salary is above the average.

---

# IN / NOT IN (sec. 3.8.1)

`IN` checks if a value matches any value in a list or subquery result.

**Examples:**
``` SQL
SELECT InstName FROM Instructor
WHERE InstName NOT IN ('Mozart', 'Einstein');
```
- Finds instructors whose names are not Mozart or Einstein.

``` SQL
SELECT DISTINCT CourseID
FROM Section
WHERE CourseID NOT IN
 (SELECT CourseID FROM Section
  WHERE (Semester='Spring' AND StudyYear=2010)
     OR (Semester='Fall' AND StudyYear=2009));
```
- Finds courses not offered in Spring 2010 or Fall 2009.

---

# SOME / ALL (sec. 3.8.2)

- `A op SOME (subquery)`: TRUE if the comparison is true for at least one value returned by the subquery.
- `A op ALL (subquery)`: TRUE if the comparison is true for every value returned by the subquery.

**Example:**
``` SQL
SELECT InstName FROM Instructor
WHERE Salary > SOME
 (SELECT Salary FROM Instructor WHERE DeptName='Finance');
```
- Finds instructors whose salary is higher than at least one instructor in the Finance department.

---

# EXISTS / NOT EXISTS (sec. 3.8.3)

`EXISTS` checks if a subquery returns any rows.

**Example:**
``` SQL
SELECT CourseID FROM Section AS S
WHERE Semester='Fall' AND StudyYear=2009
AND EXISTS
 (SELECT * FROM Section AS T
  WHERE Semester='Spring' AND StudyYear=2010
  AND S.CourseID = T.CourseID);
```
- Finds courses offered in Fall 2009 that were also offered in Spring 2010.

---

# UNION, INTERSECT, EXCEPT (sec. 3.5)

These operators combine results from multiple SELECT queries. The queries must have the same number and type of columns.

- `UNION`: Combines results, removing duplicates.
- `INTERSECT`: Returns only rows present in both queries, removing duplicates.
- `EXCEPT`: Returns rows from the first query that are not in the second, removing duplicates.

**Examples:**
``` SQL
-- Courses in Fall 2009 or Spring 2010
(SELECT CourseID FROM Section WHERE Semester='Fall' AND StudyYear=2009)
UNION
(SELECT CourseID FROM Section WHERE Semester='Spring' AND StudyYear=2010);
```

``` SQL
-- Courses in Fall 2009 but not Spring 2010
(SELECT CourseID FROM Section WHERE Semester='Fall' AND StudyYear=2009)
EXCEPT
(SELECT CourseID FROM Section WHERE Semester='Spring' AND StudyYear=2010);
```
