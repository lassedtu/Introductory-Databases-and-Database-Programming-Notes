- teacher birthday 21/01
# Write / update these notes
- [[Database Schema]]
- [[Database Schema Diagram]] $\ \checkmark$
- [[Database Instance]]

- [[SQL (Structured Query Language)]] UPDATE $\rightarrow$ (book sec 3.1)

# DDL (Data Definition Language)

### `CREATE [NAME]`
Creates a Database with the name `[NAME]`
```SQL 
CREATE DATABASE University;
```

### `USE [NAME]`
Instructs the DBMS to use the database titled `[NAME]` as the default database (it will be used for subsequent statements). The database remains the default until the end of the session or another USE statement is
issued.
```SQL 
USE University;
```

### `DROP [NAME]`
Drops the database with the title `[NAME]`
```SQL
DROP DATABASE University;
```

---

# Domain Types in SQL

## String Types
### `CHAR(n)`
Fixed length character string. The length is always n. If the value is shorter it is padded with spaces.  
Example: `CHAR(5)` can store "cat  " or "apple"

### `VARCHAR(n)`
Variable length character string. The maximum length is n. The value uses only as much space as needed.  
Example: `VARCHAR(10)` can store "dog" or "elephant"

### `TEXT`
Stores long variable length character strings. Used for large text blocks.  
Example: `TEXT` can store a paragraph or an article

### `NCHAR(n)`
Fixed length Unicode character string. The length is always n. Used for international text.  
Example: `NCHAR(4)` can store "猫  " or "test"

### `NVARCHAR(n)`
Variable length Unicode character string. The maximum length is n. Used for international text.  
Example: `NVARCHAR(10)` can store "こんにちは" or "hello"

## Date and Time
### `DATE`
Stores a date in the format YYYY-MM-DD. Used for calendar dates.  
Example: `DATE` can store "2024-09-10"

### `TIME`
Stores a time of day in the format HH:MM:SS.  
Example: `TIME` can store "14:30:00"

### `TIMESTAMP`
Stores a date and time together. Used for recording events.  
Example: `TIMESTAMP` can store "2024-09-10 14:30:00"

### `DATETIME`
Stores a date and time together. Similar to TIMESTAMP but with a wider range.  
Example: `DATETIME` can store "2024-09-10 14:30:00"

### `YEAR`
Stores a year as a 2-digit or 4-digit number.  
Example: `YEAR` can store 2024

## Numeric Types
### `INT`
Stores whole numbers. The range depends on the system.  
Example: `INT` can store 42 or -1000

### `SMALLINT`
Stores smaller whole numbers. Uses less storage than INT. The range is also system-dependent.  
Example: `SMALLINT` can store 12 or -50

### `BIGINT`
Stores very large whole numbers. Used when INT is not enough.  
Example: `BIGINT` can store 9000000000

### `TINYINT`
Stores very small whole numbers. Uses very little storage.  
Example: `TINYINT` can store 0 or 255

### `DECIMAL(p, d)`
Stores numbers with a fixed number of digits. p is the total number of digits. d is the number of digits after the decimal point. Used for precise values like money.  
Example: `DECIMAL(5 2)` can store 123.45 or 9.99

### `NUMERIC(p, d)`
Same as DECIMAL. Used for precise fixed-point numbers.  
Example: `NUMERIC(6 3)` can store 123.456

### `FLOAT(n)`
Stores approximate numbers with decimals. Can represent very large or very small values. n is the minimum number of digits of precision. Used for scientific or engineering data.  
Example: `FLOAT(7)` can store 3.14159 or 2.5E8

### `REAL`
Stores approximate floating point numbers. Precision is system-dependent.  
Example: `REAL` can store 1.23 or -0.001

### `DOUBLE`
Stores double-precision floating point numbers. Used for more accuracy than FLOAT.  
Example: `DOUBLE` can store 3.1415926535

## Other Types
### `BOOLEAN`
Stores true or false values.  
Example: `BOOLEAN` can store TRUE or FALSE

### `BLOB`
Stores binary large objects. Used for images or files.  
Example: `BLOB` can store a photo or a PDF

### `ENUM`
Stores one value from a list of allowed values.  
Example: `ENUM("red" "green" "blue")` can store "red"

### `SET`
Stores zero or more values from a list of allowed values.  
Example: `SET("a" "b" "c")` can store "a" or "a, c"

---

# CREATE TABLE

- The `CREATE TABLE` command is used to make a new table in SQL.
- You give the table a name.
- You list the columns. For each column you give a name and a data type.
- You can add rules for the table. These rules are called constraints. Common constraints are primary key, foreign key and not null.

Example:

```SQL
CREATE TABLE Classroom
(Building VARCHAR(15),
Room VARCHAR(7),
Capacity DECIMAL(4,0),
PRIMARY KEY(Building, Room))
```

- This makes a table called Classroom.
- It has three columns: Building, Room and Capacity.
- Building is text up to 15 letters.
- Room is text up to 7 letters.
- Capacity is a number with up to 4 digits and no decimals.
- The primary key is Building and Room together. This means each pair of Building and Room must be unique.

## How to write a primary key in SQL

- A primary key is a rule that says each row in the table must be unique.
- The primary key is one or more columns.
- No two rows can have the same values in the primary key columns.
- The primary key columns cannot be empty.

You add `PRIMARY KEY(NAME)` in the `CREATE TABLE` command.

### Example with one column as primary key

```SQL
CREATE TABLE Student
(ID INT,
Name VARCHAR(20),
PRIMARY KEY(ID))
```
- Here ID is the primary key.

### Example with two columns as primary key

```SQL
CREATE TABLE Enrollment
(StudentID INT,
CourseID INT,
PRIMARY KEY(StudentID, CourseID))
```
- Here the pair `(StudentID, CourseID)` is the primary key.

### Example with primary key defined on the same line

- You can also write PRIMARY KEY next to the column in its definition.

```SQL
CREATE TABLE Department
(ID INT PRIMARY KEY,
Name VARCHAR(30))
```
- Here ID is the primary key. The PRIMARY KEY is written on the same line as the column.

### Example with an artificial or surrogate key

- Sometimes you make a new column just for the primary key. This is called an artificial key or surrogate key.
- It is usually an integer that goes up by one for each row.

```SQL
CREATE TABLE Course
(CourseID INT AUTO_INCREMENT,
Title VARCHAR(50),
Credits INT,
PRIMARY KEY(CourseID))
```
- Here CourseID is the surrogate key. It is not based on real data. It is just a unique number for each course.
- AUTO_INCREMENT means the value goes up by one for each new row.
- This can be a bad practice in certain cases and should therefore be used with caution.

## Not Null

- You can use NOT NULL to make sure a column cannot be empty.
- If a column is NOT NULL, every row must have a value for that column.

### Example

```SQL
CREATE TABLE Teacher
(ID INT PRIMARY KEY,
Name VARCHAR(30) NOT NULL)
```
- Here Name must always have a value. You cannot insert a row with Name missing.

## Foreign Key Constraint

- A foreign key links one table to another table.
- It makes sure that a value in one table must already exist in another table.
- This keeps data consistent between tables.

### Example

Suppose you have a table Department:

```SQL
CREATE TABLE Department
(ID INT PRIMARY KEY,
Name VARCHAR(30))
```

Now you want to make a table Teacher. Each teacher belongs to a department. You use a foreign key for this:

```SQL
CREATE TABLE Teacher
(ID INT PRIMARY KEY,
Name VARCHAR(30) NOT NULL,
DepartmentID INT,
FOREIGN KEY(DepartmentID) REFERENCES Department(ID))
```
- Here DepartmentID in Teacher must match an ID in Department.
- You cannot add a teacher with a DepartmentID that does not exist in Department.

# ON DELETE

## Cascade Policy

- The cascade policy controls what happens to rows in a child table when the related row in the parent table is deleted or updated.
- You use `ON DELETE CASCADE` or `ON UPDATE CASCADE` with a foreign key.

- The `ON UPDATE CASCADE` policy updates the foreign key in the child table if the referenced value in the parent table changes.
- This keeps the link between tables correct if you change the primary key value in the parent table.

### Example: ON DELETE CASCADE

```SQL
CREATE TABLE Teacher
(ID INT PRIMARY KEY,
Name VARCHAR(30) NOT NULL,
DepartmentID INT,
FOREIGN KEY(DepartmentID) REFERENCES Department(ID) ON DELETE CASCADE)
```
- If a department is deleted from Department, all teachers in that department are also deleted from Teacher.
- This keeps the data consistent and avoids orphan records.

### Example: ON UPDATE CASCADE

```SQL
CREATE TABLE Teacher
(ID INT PRIMARY KEY,
Name VARCHAR(30) NOT NULL,
DepartmentID INT,
FOREIGN KEY(DepartmentID) REFERENCES Department(ID) ON UPDATE CASCADE)
```
- If the ID of a department is changed in Department, the DepartmentID for all teachers in that department is also updated automatically.

### Example: Both

You can add both policies to the foreign key like this:

```sql
CREATE TABLE Teacher
(ID INT PRIMARY KEY,
Name VARCHAR(30) NOT NULL,
DepartmentID INT,
FOREIGN KEY(DepartmentID) REFERENCES Department(ID)
  ON DELETE CASCADE
  ON UPDATE CASCADE)
```

- Now if a department is deleted, all teachers in that department are deleted.
- If a department ID is changed, all DepartmentID values in Teacher are updated too.

## Set Null Policy

- The set null policy sets the foreign key column to NULL if the related row in the parent table is deleted.
- You use `ON DELETE SET NULL` with a foreign key.

### Example: ON DELETE SET NULL

```SQL
CREATE TABLE Teacher
(ID INT PRIMARY KEY,
Name VARCHAR(30) NOT NULL,
DepartmentID INT,
FOREIGN KEY(DepartmentID) REFERENCES Department(ID) ON DELETE SET NULL)
```
- If a department is deleted from Department, the DepartmentID for those teachers becomes NULL.
- This means the teacher no longer belongs to any department.

---

# DROP TABLE and ALTER TABLE

## DROP TABLE

- Removes the table and all its data from the database.
```SQL
DROP TABLE Student;
```

## DELETE FROM

- Removes all rows from the table but keeps the table structure.
```SQL
DELETE FROM Student;
```

## ALTER TABLE

- Adds a new column to the table. The new column will have NULL values at first.
```SQL
ALTER TABLE Student ADD Shoesize DECIMAL(2,0);
```

- Removes a column from the table.
```SQL
ALTER TABLE Student DROP Shoesize;
```

---
# INSERT

- The `INSERT` command adds new rows to a table.
- You can choose which columns to fill and give values for them.

### Basic form

```SQL
INSERT INTO TableName (Column1, Column2, ...)
VALUES (Value1, Value2, ...);
```

- `TableName` is the table to add data to.
- `Column1, Column2` are the columns to fill.
- `Value1, Value2` are the values for those columns.

### Example: Add a new course

```SQL
INSERT INTO Course (CourseID, Title, DeptName, Credits)
VALUES ('CS-437', 'Database Systems', 'Comp. Sci.', 4);
```

### Short form if all columns are filled in order

```SQL
INSERT INTO Course
VALUES ('CS-437', 'Database Systems', 'Comp. Sci.', 4);
```

### Example: Add a student with NULL value

```SQL
INSERT INTO Student
VALUES ('3003', 'Green', '1993-04-16', 'Finance', NULL);
```

### Insert multiple rows at once

```SQL
INSERT INTO Course
VALUES
('CS-437', 'Database Systems', 'Comp. Sci.', 4),
('CS-528', 'Big Data Systems', 'Comp. Sci.', 5),
('CS-530', 'Data Warehouse', 'Comp. Sci.', 4);
```

### Insert from another table

```SQL
INSERT INTO TableName (Column1, Column2, ...)
SELECT ColumnA, ColumnB
FROM OtherTable
WHERE condition;
```

---

# DELETE

- The `DELETE` command removes rows from a table.
- You specify which rows to remove using a condition.

### Basic form

```SQL
DELETE FROM TableName WHERE condition;
```

- `TableName` is the table to delete from.
- `condition` decides which rows to remove.

### Example: Delete one row

```SQL
DELETE FROM Instructor WHERE InstID = 45565;
```

### Example: Delete multiple rows

```SQL
DELETE FROM Instructor WHERE DeptName = 'Finance';
```

### Example: Delete all rows

```SQL
DELETE FROM Instructor;
```

---

# UPDATE

- The `UPDATE` command changes values in existing rows of a table.
- You specify which rows to change using a condition.
- You set new values for one or more columns.

### Basic form

```SQL
UPDATE TableName
SET Column1 = Value1, Column2 = Value2, ...
WHERE condition;
```

- `TableName` is the table to update.
- `Column1 = Value1` sets a new value for a column.
- `condition` decides which rows to update.

### Example: Update one row

```SQL
UPDATE Instructor
SET Salary = 85000, DeptName = 'Physics'
WHERE InstID = 45565;
```

### Example: Update multiple rows with different conditions

- Increase salaries over 80000 by 3%

```SQL
UPDATE Instructor
SET Salary = Salary * 1.03
WHERE Salary > 80000;
```

- Increase salaries 80000 or less by 5%

```SQL
UPDATE Instructor
SET Salary = Salary * 1.05
WHERE Salary <= 80000;
```

---

# SQL Data Queries
Reference: (book sec 3.3, 3.4.1, 3.4.3, 3.4.4, 4.1.1, 4.1.2)

- SQL lets you ask questions to get data from tables.
- The answer to a query is always a table.

### Basic query form

```SQL
SELECT Column_1, Column_2, ..., Column_N
FROM Table_1, Table_2, ..., Table_M
WHERE condition;
```

- `Column1, Column2` are the columns you want to see in the result. You choose which pieces of information to get from the tables  
- `Table1, Table2` represent relations or tables where the data comes from. You can get data from one or more tables at the same time  
- `condition` is a rule that decides which rows to include in the result. Only rows that meet this rule are shown  
- For each row the condition is checked and is either true or false. If true the row is included. If false it is left out

---

# SELECT

- The `SELECT` clause lists the columns you want to see in the query result  
- This is like choosing which pieces of information to get from the tables  
- It corresponds to the projection operation in relational algebra  

### Example: Get names of all instructors

```SQL
SELECT InstName FROM Instructor;
```

- SQL names are not case sensitive. For example `InstName`, `INSTNAME` and `instname` mean the same  

---

# SELECT DISTINCT and ALL

- By default SQL allows duplicate rows in results  
- Use `DISTINCT` after `SELECT` to remove duplicates  

### Example: Get unique department names from Instructor

```SQL
SELECT DISTINCT DeptName FROM Instructor;
```

- Use `ALL` to keep duplicates (this is the default)  

```SQL
SELECT ALL DeptName FROM Instructor;
```

---

# SELECT Using `*` expressions and AS

- `*` means select all columns  

```SQL
SELECT * FROM Instructor;
```

- You can use arithmetic expressions in `SELECT`  

### Example: Calculate monthly salary

```SQL
SELECT InstID, Salary / 12 AS Monthly FROM Instructor;
```

- `AS` gives a new name (alias) to a column or expression in the result  

---

# SELECT Using built-in functions

- You can use built-in functions in `SELECT`  

### Example: Get current date

```SQL
SELECT CURDATE();
```

### Example: Calculate age from birth date

- Store birth date not age because age changes over time  
- Calculate age when needed

```SQL
SELECT StudName, Birth,
TIMESTAMPDIFF(YEAR, Birth, CURDATE()) AS Age
FROM Student;
```
#### TIMESTAMPDIFF
- `TIMESTAMPDIFF` calculates the difference between two dates or times
- The first argument is the unit to measure the difference (like YEAR, MONTH, DAY)
- The second argument is the start date or time
- The third argument is the end date or time
- It returns how many units (years, months, days, etc.) are between the two dates

```SQL
TIMESTAMPDIFF(YEAR, Birth, CURDATE())
```

Calculates the age in years by finding the number of years between the birth date and today.

---

# WHERE

- The `WHERE` clause sets conditions for which rows to include in the result  
- Only rows that meet these conditions are shown  

### Example: Find instructors in Comp. Sci. with salary over 70000

```SQL
SELECT InstName FROM Instructor
WHERE DeptName = 'Comp. Sci.' AND Salary > 70000;
```

- You can use comparison operators like `<`, `<=`, `>`, `>=`, `=`, `<>` on numbers or text  
- Combine conditions with `AND`, `OR`, and `NOT`  

---

# FROM

- The `FROM` clause lists the tables used in the query  
- You can list one or more tables separated by commas  
- This creates a Cartesian Product (all possible pairs) of the tables  

### Example: Cartesian Product of Instructor and Teaches

- Combines each row in Instructor with all rows in Teaches
- Instructor(InstID, InstName, DeptName, Salary)
- Teaches(InstID, CourseID, SectionID, Semester, StudyYear)

```sql
SELECT * FROM Instructor, Teaches LIMIT 14;
SELECT COUNT(*) FROM Instructor, Teaches;
```

- The result has all columns from both tables
- The number of rows is the product of the number of rows in each table
- Be careful: Cartesian Products can create huge results and slow queries
- Usually you use `WHERE` to limit the rows after the Cartesian Product


---
# More JOIN Examples

# Example: 1. Instructor and Teaches
- Given tables  
  Instructor(InstID, InstName, DeptName, Salary)  
  Teaches(InstID, CourseID, SectionID, Semester, StudyYear)  

- Find all instructors who have taught some course  
- Show their names and the course IDs they taught  

```SQL
SELECT InstName, CourseID
FROM Instructor, Teaches
WHERE Instructor.InstID = Teaches.InstID;
```

- This joins Instructor and Teaches on matching InstID  
- Only instructors who have taught courses appear  
- Shows instructor names with their course IDs  
## Example: Section and Course
- Given tables  
  Section(CourseID, SectionID, Semester, StudyYear, Building, Room, TimeSlotID)  
  Course(CourseID, Title, DeptName, Credits)  

- Find the CourseID, Semester, StudyYear and Title of each course offered by the Comp. Sci. department  

```SQL
SELECT Section.CourseID, Semester, StudyYear, Title
FROM Section, Course
WHERE Section.CourseID = Course.CourseID AND DeptName = 'Comp. Sci.';
```

- This joins Section and Course on CourseID  
- Shows courses offered by Comp. Sci. with their details  

---

# NATURAL JOIN

- `NATURAL JOIN` matches rows with the same values in all common columns  
- It keeps only one copy of each common column in the result  

### Example

```SQL
SELECT * FROM Instructor NATURAL JOIN Teaches;
```

- Here the join is done on the common column `InstID`  
- Rows with matching `InstID` in both tables are combined  
- Only one `InstID` column appears in the result  

---

# NATURAL JOIN versus JOIN

- To find all instructors who have taught some course and show their names and course IDs you can write:

```SQL
SELECT InstName, CourseID
FROM Instructor, Teaches
WHERE Instructor.InstID = Teaches.InstID;
```

- This is equivalent to using NATURAL JOIN:

```SQL
SELECT InstName, CourseID
FROM Instructor NATURAL JOIN Teaches;
```

- `NATURAL JOIN` automatically joins tables on all common columns (here `InstID`)  
- It keeps only one copy of the common columns in the result  
- This makes the query simpler and easier to read  

---

# Renaming: AS in SELECT and FROM
Referenced in section 3.4.1

- You can rename columns or tables using `AS`  
- Syntax: `OldName AS NewName`  
- `AS` is optional and doesen't have to be used. It is to be used to make queries more compact.

### Example: Rename column in SELECT

- You can give a new name (alias) to a column or expression in the result using `AS`
- This helps make the output clearer or more meaningful
- In the example:

```sql
SELECT InstID, InstName, Salary / 12 AS Monthly
FROM Instructor;
```

- The column `Salary / 12` is renamed to `Monthly`
- This shows the monthly salary instead of the yearly salary
- The alias `Monthly` will be the column header in the result table

### Example: Rename tables in FROM

- You can give a new name (alias) to a table in the query using `AS`  
- This helps make queries shorter and easier to read  
- In the example:

```SQL
SELECT DISTINCT T.InstName
FROM Instructor AS T, Instructor AS S
WHERE T.Salary > S.Salary AND S.DeptName = 'Comp. Sci.';
```

- `T` and `S` are aliases for the Instructor table  
- You can refer to the tables by these shorter names in the query  
- This is useful when you use the same table more than once or want clearer code  


---

# SELECT revisited: use of *
Referenced in section 3.4.3

- Use `*` to select all columns from a table  
- Useful when you want all attributes of a table  

### Example: Select all columns of instructors who have taught some course

```SQL
SELECT Instructor.*
FROM Instructor, Teaches
WHERE Instructor.InstID = Teaches.InstID;
```

- This returns all columns from Instructor for matching rows  

---

# ORDER BY 
Referenced in section 3.4.4

- Use `ORDER BY` to sort the rows in the query result by one or more columns  
- By default sorting is ascending (from smallest to largest or A to Z)  
- Use `DESC` to sort in descending order (largest to smallest or Z to A)  

### Example: List all instructor names in alphabetical order

```SQL
SELECT DISTINCT InstName FROM Instructor ORDER BY InstName;
```

- This shows unique instructor names sorted from A to Z  

### Example: List all instructor names in reverse alphabetical order

```SQL
SELECT DISTINCT InstName FROM Instructor ORDER BY InstName DESC;
```

- This shows unique instructor names sorted from Z to A  

### Example: Sort by multiple columns

```SQL
SELECT DeptName, InstName
FROM Instructor
ORDER BY DeptName, InstName;
```

- This sorts first by department name  
- Then within each department it sorts by instructor name  

---

# Making New Tables from Old Tables

- You can create a new table with the same structure as an existing table using `CREATE TABLE ... LIKE`  
- Then copy rows from the old table into the new one using `INSERT ... SELECT`  

### Create an empty table like Instructor

```SQL
CREATE TABLE Specialist1 LIKE Instructor;
```

- This makes a new empty table Specialist1 with the same columns and keys as Instructor  

### Insert rows from Instructor where DeptName is 'Comp. Sci.'

```SQL
INSERT Specialist1 SELECT * FROM Instructor WHERE DeptName = 'Comp. Sci.';
```

- This copies all instructors from the Comp. Sci. department into Specialist1  

### Create a new table with data from Instructor where DeptName is 'Physics'

```SQL
CREATE TABLE Specialist2 SELECT * FROM Instructor WHERE DeptName = 'Physics';
```

- This creates Specialist2 and fills it with instructors from the Physics department  
- Note Specialist2 does not have keys or constraints copied  

### View the new tables

```SQL
SELECT * FROM Specialist1;
SELECT * FROM Specialist2;
```

- Specialist1 has the primary key from Instructor  
- Specialist2 does not have a primary key yet  

### Add a primary key to Specialist2

```SQL
ALTER TABLE Specialist2 ADD PRIMARY KEY(InstID);
```

- This defines InstID as the primary key for Specialist2  

### Add a foreign key to Specialist1

```SQL
ALTER TABLE Specialist1 ADD FOREIGN KEY(DeptName) REFERENCES Department(DeptName);
```

- This links DeptName in Specialist1 to DeptName in Department to keep data consistent  