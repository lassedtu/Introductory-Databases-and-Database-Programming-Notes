SQL stands for Structured Query Language. It is the most widely used language used to create modify and query relational databases. SQL lets you define tables insert and update data and ask questions to get information from your data. SQL is used by almost all relational database systems ([[The Relational Model]]).

**Example**:
An example of an SQL query to find physics instructors with a salary < 80000
```SQL
SELECT InstID InstName FROM Instructor
WHERE DeptName = ‘Physics’ AND Salary < 80000;
```


As useful as queries are for retrieving information SQL also provides commands to define and structure the database itself.

## [[Data Definition Language (DDL)]]

DDL commands are used to define and change the structure of the database. You use DDL to create databases create tables set up primary and foreign keys and change or remove tables. Common DDL commands are:

- `CREATE DATABASE` to make a new database
- `USE` to select a database
- `DROP DATABASE` to remove a database
- `CREATE TABLE` to make a new table with columns and constraints
- `DROP TABLE` to remove a table
- `ALTER TABLE` to change a table (add or remove columns add keys)
- `DELETE FROM` to remove all rows from a table but keep the table
![[ddl-operations.png| center]]
You can set rules like primary keys foreign keys and not null constraints. You can also control what happens when data is deleted or updated using ON DELETE and ON UPDATE policies like CASCADE or SET NULL.

Once the database structure is in place the next step is to work with the actual data inside those tables.

## [[Data Manipulation Language (DML)]]

DML commands are used to add change or remove data in tables. The main DML commands are:

- `INSERT` to add new rows to a table  
- `DELETE` to remove rows from a table  
- `UPDATE` to change values in existing rows  

![[dml-operations.png | center]]
You can insert one row multiple rows or copy rows from another table. You can delete or update rows based on conditions. For example to increase all salaries over 80000 by 3%:

```SQL
UPDATE Instructor
SET Salary = Salary * 1.03
WHERE Salary > 80000;
```

After data is inserted and maintained we often want to extract meaningful information from it. That’s where queries come in.
## [[SQL Queries]]

SQL queries let you ask questions and get data from tables. The main command is `SELECT`. You can choose which columns to see filter rows with `WHERE` sort results with `ORDER BY` and use built-in functions.

- `SELECT` chooses columns  
- `FROM` lists tables  
- `WHERE` sets conditions  
- `ORDER BY` sorts the result  
- `AS` gives new names to columns or tables  
- `DISTINCT` removes duplicate rows  
- Built-in functions like `CURDATE()` or `TIMESTAMPDIFF()` can be used in queries
![[sql-operations.png | center]]
Example: Find all instructor names in alphabetical order

```SQL
SELECT DISTINCT InstName FROM Instructor ORDER BY InstName;
```

For queries to work correctly it’s important to understand the types of data stored in each column.
## [[Domain Types]]

Each column in a table has a type. SQL has many types for different kinds of data:

- String types like CHAR VARCHAR TEXT for text
- Date and time types like DATE TIME TIMESTAMP DATETIME YEAR
- Numeric types like INT SMALLINT BIGINT DECIMAL FLOAT DOUBLE
- Other types like BOOLEAN BLOB ENUM SET
![[domain-types.png | center]]
Each type has its own rules and uses. For example use VARCHAR for variable-length text DATE for calendar dates and INT for whole numbers.

But data rarely exists in isolation. Relationships between tables are a core strength of SQL and they are managed using joins.
## [[Joins and Relationships]]

Joins combine rows from two or more tables based on related columns. You can use:

- Regular joins with `WHERE` to match columns  
- `NATURAL JOIN` to join on all columns with the same name  
- `AS` to rename tables or columns in queries

Example: Find all instructors who have taught some course

```SQL
SELECT InstName, CourseID
FROM Instructor NATURAL JOIN Teaches;
```

Beyond simply querying and joining SQL also lets you build new tables directly from existing ones which is powerful for restructuring data.
## [[Creating Tables from Existing Data]]

You can create new tables based on existing tables. Use `CREATE TABLE ... LIKE` to copy the structure or `CREATE TABLE ... SELECT` to make a new table with data from a query. You can also add keys to new tables.

Example: Make a new table with all Comp. Sci. instructors

```SQL
CREATE TABLE Specialist1 LIKE Instructor;
INSERT Specialist1 SELECT * FROM Instructor WHERE DeptName = 'Comp. Sci.';
```