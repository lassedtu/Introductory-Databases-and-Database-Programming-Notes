# JOINs (section 4.1)

- There are different types of JOIN operations in SQL.
- A JOIN takes two tables as input and gives back a new table as the result.

## What does a JOIN do?

- The result of a JOIN is a subset of the Cartesian Product of the two tables.
    - The Cartesian Product means all possible pairs of rows from both tables.
- A JOIN combines rows from the two tables if they match a certain condition (called the join condition).
- Rows that do not match may or may not be included in the result, depending on the type of JOIN.
    - If a row does not have a match in the other table, the missing values can be filled with NULLs.
- You can choose which columns (attributes) to include in the result.

## Where are JOINs used?

- JOIN operations are usually written in the FROM clause of a SELECT statement.

### Example: Basic JOIN

Suppose you have two tables:

- Instructor(InstID, InstName, DeptName, Salary)
- Teaches(InstID, CourseID, SectionID, Semester, StudyYear)

To find all instructors who have taught a course, and show their names and course IDs:

```SQL
SELECT InstName, CourseID
FROM Instructor, Teaches
WHERE Instructor.InstID = Teaches.InstID;
```

- This combines rows from Instructor and Teaches where InstID matches.
- Only instructors who have taught at least one course are shown.

### Example: JOIN with unmatched rows

- If you want to keep rows that do not have a match in the other table (and fill missing values with NULL), you can use an OUTER JOIN (see Lecture 4 for details).

Here are the explanations in your style, each with its own section and examples:

## Cartesian Product = (INNER) JOIN

- The Cartesian Product of two tables means every row from the first table is combined with every row from the second table.
- In SQL, if you write two tables in the FROM clause without a join condition, you get the Cartesian Product.
- Usually, you use a WHERE clause to filter the pairs and get only the rows that match a condition. This is called an INNER JOIN.

### Example: Cartesian Product

```SQL
SELECT * FROM Instructor, Teaches;
```
- This gives all possible pairs of Instructor and Teaches rows.
- If Instructor has 5 rows and Teaches has 3 rows, the result has 5 × 3 = 15 rows.

### Example: INNER JOIN

```SQL
SELECT * FROM Instructor, Teaches
WHERE Instructor.InstID = Teaches.InstID;
```
- This only keeps pairs where InstID matches.
- This is called an INNER JOIN. Only matching rows are shown.

## NATURAL (INNER) JOIN

- A NATURAL JOIN automatically joins tables using all columns with the same name.
- Only rows with equal values in all common columns are combined.
- The result has only one copy of each common column.

### Example: NATURAL JOIN

```SQL
SELECT * FROM Instructor NATURAL JOIN Teaches;
```
- Joins on InstID (since both tables have InstID).
- Only rows with the same InstID in both tables are shown.
- The result has only one InstID column.

## OUTER JOINs

- OUTER JOINs keep rows even if there is no match in the other table.
- Missing values are filled with NULLs.
- There are three types:
    - LEFT OUTER JOIN: keeps all rows from the left table.
    - RIGHT OUTER JOIN: keeps all rows from the right table.
    - FULL OUTER JOIN: keeps all rows from both tables.

## NATURAL LEFT OUTER JOIN

- A NATURAL LEFT OUTER JOIN keeps all rows from the left table.
- If there is no match in the right table, columns from the right table are filled with NULL.

### Example: NATURAL LEFT OUTER JOIN

```SQL
SELECT * FROM Instructor NATURAL LEFT OUTER JOIN Teaches;
```
- All instructors are shown, even if they have not taught any course.
- If an instructor has not taught, columns from Teaches are NULL.

## NATURAL RIGHT OUTER JOIN

- A NATURAL RIGHT OUTER JOIN keeps all rows from the right table.
- If there is no match in the left table, columns from the left table are filled with NULL.

### Example: NATURAL RIGHT OUTER JOIN

```SQL
SELECT * FROM Instructor NATURAL RIGHT OUTER JOIN Teaches;
```
- All rows from Teaches are shown, even if there is no matching instructor.
- If a course is taught by someone not in Instructor, columns from Instructor are NULL.

## NATURAL FULL OUTER JOIN

- A NATURAL FULL OUTER JOIN keeps all rows from both tables.
- If there is no match, missing columns are filled with NULL.

### Example: NATURAL FULL OUTER JOIN

```SQL
SELECT * FROM Instructor NATURAL FULL OUTER JOIN Teaches;
```
- All instructors and all teaching assignments are shown.
- If there is no match, missing values are NULL.

## JOIN Conditions

- A JOIN condition tells SQL how to match rows from two tables.
- You write the condition after ON or in the WHERE clause.

### Example: JOIN ON Predicate

```SQL
SELECT * FROM Instructor INNER JOIN Teaches
ON Instructor.InstID = Teaches.InstID;
```
- Joins rows where InstID matches.

### Example: JOIN with multiple conditions

```SQL
SELECT * FROM Section INNER JOIN Course
ON Section.CourseID = Course.CourseID AND Course.DeptName = 'Comp. Sci.';
```
- Joins Section and Course where CourseID matches and department is 'Comp. Sci.'.



# Constraints (section 4.4-4.5)


# Views (section 4.2)


# Authorization (section 4.6)


# Demo Exercises & Exercises


# Appendix: University Database

