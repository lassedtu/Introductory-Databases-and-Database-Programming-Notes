Redundancy is a major problem in databases. It means the same data is stored in more than one place. For example, imagine a table where a student's address appears in every row for every course they take. If the student moves and you update their address in only some rows, the database now has two different addresses for the same student. This is called a [[Modification Anomalies|modification anomaly]].

Why is this bad? If you ask the database, "What is the student's address?" you might get different answers depending on which row is used. This makes the database inconsistent.

| StudentID | Name   | Address      | CourseID |
|-----------|--------|-------------|----------|
| 101       | Alice  | 1 Main St   | CS101    |
| 101       | Alice  | 99 Elm Ave  | MATH201  |

If Alice’s address is updated in only one row, the database now has conflicting information.

A redundancy-free database avoids this problem. Each piece of information is stored only once, so when you update it, you only need to change it in one place. The DBMS can then update data efficiently and keep everything consistent. This is why [[normalisation]] is so important: it helps eliminate redundancy and keeps your data reliable.

### [[Redundancy]] and [[Modification Anomalies]]

Suppose we try to combine instructor and department information into a single table:

![[redundant-table.png| center | 600]]

This design has two main problems:

1. **Redundancy:** The building and budget for each department are repeated for every instructor in that department. If you need to update the budget for Physics, you have to change it in every row where DeptName is Physics. If you miss one, the data becomes inconsistent.

2. **Incomplete Information:** You cannot store information about a department unless at least one instructor works there. For example, if the Philosophy department has no instructors yet, there is no way to record its building or budget.

Combining instructor and department in one table leads to repeated data and makes it impossible to store departments without instructors. This is why we separate them into different tables and use relationships to connect them. (See: [[Good Relational Design]])