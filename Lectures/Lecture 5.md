# Advanced SQL: Procedural Programming

Modern SQL (e.g., MariaDB, MySQL) supports **procedural programming** features, allowing you to write routines with variables, control flow, and error handling—similar to general-purpose languages. This is essential for defining advanced database objects like **Procedures**, **Functions**, **Triggers**, and **Transactions**.

---

# Blocks, Variables, and Delimiters

Procedural SQL logic is written in blocks and often uses variables for intermediate results.

### Code Blocks and Delimiters

- **`BEGIN ... END`**: Groups multiple statements into a block.
- **Delimiter Problem**: Inside a block, semicolons (`;`) are used to end statements, but the SQL client also uses `;` to end the entire routine definition.
- **Solution**: Temporarily change the delimiter (e.g., `DELIMITER $$`) before the routine, and reset it after.

```MySQL
DELIMITER $$
CREATE PROCEDURE hello_world()
BEGIN
    SELECT 'Hello, world!';
END$$
DELIMITER ;
```

---

### Variables

- **Local Variables**: Declared with `DECLARE` inside a block.
- **Assignment**: Use `SET` or assign from a query.
- **User-Defined Variables**: Use `@varName` (session-scoped, no declaration needed).
- **Parameters**: Procedures and functions receive input via parameters.

```MySQL
DELIMITER $$
CREATE PROCEDURE variable_demo()
BEGIN
    DECLARE x INT DEFAULT 10;
    SET x = x + 5;
    SELECT x;
END$$
DELIMITER ;
```

---

# Control Flow

Procedural SQL supports standard control flow:

- **Conditional:** `IF ... THEN ... ELSEIF ... ELSE ... END IF`
- **Loops:** `WHILE`, `REPEAT ... UNTIL`, and `LOOP` (with `LEAVE`/`ITERATE` for control)

```MySQL
DELIMITER $$
CREATE PROCEDURE check_number(IN num INT)
BEGIN
    IF num > 0 THEN
        SELECT 'Positive';
    ELSEIF num < 0 THEN
        SELECT 'Negative';
    ELSE
        SELECT 'Zero';
    END IF;
END$$
DELIMITER ;
```

---

# Procedures (`CREATE PROCEDURE`)

**Procedures** are routines that can perform actions (including data modification) and return result sets. They can have multiple input/output parameters and are invoked with `CALL`.

### Good Practice: Dropping Existing Procedures

When developing or updating stored procedures, it’s a good habit to drop the existing procedure before creating a new version. This avoids errors if the procedure already exists.

```MySQL
DROP PROCEDURE IF EXISTS TimeTable;
```

### Example: Student Timetable Procedure

Suppose you want to display a student's timetable for a given semester and year:

```MySQL
DROP PROCEDURE IF EXISTS TimeTable;
DELIMITER $$
CREATE PROCEDURE TimeTable(
    IN p_StudID VARCHAR(5),
    IN p_Semester ENUM('Fall','Winter','Spring','Summer'),
    IN p_StudyYear YEAR
)
BEGIN
    SELECT Building, Room, TimeslotID
    FROM Section NATURAL JOIN Takes
    WHERE StudID = p_StudID AND Semester = p_Semester AND StudyYear = p_StudyYear;
END$$
DELIMITER ;
```

To call this procedure:

```MySQL
CALL TimeTable('12345', 'Fall', 2009);
```

- Procedures can return multiple rows and columns (result sets).
- They are ideal for encapsulating business logic that involves actions, not just calculations.

### Example: Procedure with Side Effects

Procedures can perform actions that modify the database, such as updating or deleting records. These actions are called **side effects**. They change the state of the database beyond just returning a value.

**Side effects** refer to any operation that changes data or the environment outside the procedure itself (e.g., updating tables, inserting rows, deleting data, or even writing to logs).

For example, the following procedure increases the salary of all instructors in a given department by 10%:

```MySQL
DROP PROCEDURE IF EXISTS IncreaseSalary;
DELIMITER $$
CREATE PROCEDURE IncreaseSalary(IN p_DeptName VARCHAR(20))
BEGIN
    UPDATE Instructor
    SET Salary = Salary * 1.1
    WHERE DeptName = p_DeptName;
END$$
DELIMITER ;
```

To call this procedure:

```MySQL
CALL IncreaseSalary('Comp. Sci.');
```

- This procedure has a side effect: it modifies the `Salary` values in the `Instructor` table.
- **Note:** Functions, in contrast, should not have side effects, they are intended only to compute and return a value.

---

# Functions (`CREATE FUNCTION`)

**Functions** compute and return a single value. They are used in SQL expressions (e.g., in `SELECT` or `WHERE` clauses) and must not have side effects.

### Example: Simple Function

```MySQL
DELIMITER $$
CREATE FUNCTION add_one(x INT)
RETURNS INT
DETERMINISTIC
BEGIN
    RETURN x + 1;
END$$
DELIMITER ;
```

### Good Practice: Dropping Existing Functions

When developing or updating stored functions, it’s a good habit to drop the existing function before creating a new version. This avoids errors if the function already exists.

```MySQL
DROP FUNCTION IF EXISTS StudentsMentored;
```

### Example: Using a Function in a SELECT Statement

Suppose you want to count how many students each instructor mentors:

```MySQL
DROP FUNCTION IF EXISTS StudentsMentored;
DELIMITER $$
CREATE FUNCTION StudentsMentored(p_InstID VARCHAR(5)) RETURNS INT
BEGIN
    DECLARE p_StudCount INT;
    SELECT COUNT(*) INTO p_StudCount
    FROM Advisor
    WHERE InstID = p_InstID;
    RETURN p_StudCount;
END$$
DELIMITER ;
```

Use it in a query:

```MySQL
SELECT InstID, InstName, DeptName, Salary, StudentsMentored(InstID) AS NumStudentsMentored
FROM Instructor;
```

You can use the same pattern for other functions as well, e.g.:

```MySQL
DROP FUNCTION IF EXISTS IsWithinBudget;
DELIMITER $$
CREATE FUNCTION IsWithinBudget(p_DeptName VARCHAR(20)) RETURNS INT
...
END$$
DELIMITER ;
```

### Example: Aggregation and Control Flow in a Function

Check if a department is within its salary budget:

```MySQL
DELIMITER $$
CREATE FUNCTION IsWithinBudget(p_DeptName VARCHAR(20)) RETURNS INT
BEGIN
    DECLARE p_Offset INT;
    SELECT Budget - SUM(Salary) INTO p_Offset
    FROM Department NATURAL LEFT JOIN Instructor
    WHERE DeptName = p_DeptName;
    IF p_Offset >= 0 THEN
        RETURN 1;
    ELSE
        RETURN 0;
    END IF;
END$$
DELIMITER ;
```

Or, more concisely, using the IF() function:

```MySQL
RETURN IF(p_Offset >= 0, 1, 0);
```

- The `IF(expr, val_true, val_false)` function acts like a ternary operator, returning `val_true` if `expr` is true, else `val_false`.
- This makes code more concise for simple conditional returns.

Use in a query:

```MySQL
SELECT DeptName, IsWithinBudget(DeptName) AS WithinBudget
FROM Department;
```

---

# Custom Error Handling

Procedural SQL allows you to raise custom errors:

- **`SIGNAL`**: Raises an error with a specific SQLSTATE and message.

```MySQL
DELIMITER $$
CREATE PROCEDURE check_age(IN age INT)
BEGIN
    IF age < 18 THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Age must be at least 18';
    END IF;
END$$
DELIMITER ;
```

---
# Triggers (`CREATE TRIGGER`)

**Triggers** are special routines that are automatically executed by the database in response to certain events on a table, such as `INSERT`, `UPDATE`, or `DELETE`. Triggers are commonly used for enforcing business rules, maintaining audit trails, or validating data before changes are committed.

- Triggers can be defined to run **BEFORE** or **AFTER** the triggering event.
- They operate on each affected row (`FOR EACH ROW`).

### Example: Enforcing Classroom Capacity with a Trigger

Suppose you want to prevent students from enrolling in a course section if the classroom is already at capacity. You can use a trigger to enforce this rule automatically:

```MySQL
DELIMITER $$
CREATE TRIGGER Takes_Before_Insert
BEFORE INSERT ON Takes FOR EACH ROW
BEGIN
    IF EXISTS (
        SELECT Section.*, Capacity, COUNT(*)
        FROM Section NATURAL JOIN Classroom NATURAL JOIN Takes
        WHERE 
            CourseID = NEW.CourseID 
        AND 
            SectionID = NEW.SectionID 
        AND
            Semester = NEW.Semester
        AND
            StudyYear = NEW.StudyYear
        GROUP BY CourseID, SectionID, Semester, StudyYear
        HAVING COUNT(*) >= Capacity
    )
    THEN SIGNAL SQLSTATE "HY0000" 
        SET MYSQL_ERRNO = 1525, 
        MESSAGE_TEXT="Course exceeds classroom capacity";
    END IF;
END $$
DELIMITER ;
```

- This trigger runs **before** a new row is inserted into the `Takes` table.
- It checks if the number of students already enrolled in the section has reached the classroom's capacity.
- If the section is full, it raises an error and prevents the insert.

**Key Points:**
- Triggers are powerful for enforcing constraints that go beyond what standard SQL constraints (like `CHECK` or `FOREIGN KEY`) can do.
- Use triggers carefully, as they can make debugging and maintenance more complex if overused.


---

## Procedures vs. Functions

| Feature         | Procedure                | Function                        |
|-----------------|-------------------------|---------------------------------|
| Returns         | Result set or nothing   | Single value                    |
| Invocation      | CALL statement          | Used in SQL expressions         |
| Side Effects    | Allowed                 | Not allowed (should be pure)    |
| Parameters      | IN, OUT, INOUT          | Only IN                         |
