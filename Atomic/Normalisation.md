- Normalisation is a technique to organise data in a database.
- The main goal: reduce [[Redundancy]] and prevent update problems.

### What does normalisation do?

- Breaks a big table into smaller tables.
- Each table stores related information.
- Uses foreign keys to connect the tables.

### Why normalise?

- Makes sure each piece of data is stored in only one place.
- When you add, update, or delete data, you only need to do it once.
- Changes automatically flow to related tables using foreign keys.
- Helps keep data consistent and avoids searching through lots of data.

### Example: Normalisation

Suppose you have a table:

| StudentID | StudentName | CourseID | CourseName |
| --------- | ----------- | -------- | ---------- |
|           |             |          |            |

Problems:
- If a student takes two courses, their name is repeated.
- If you want to change a course name, you have to update every row.

After normalisation:

- Student(StudentID, StudentName)
- Course(CourseID, CourseName)
- Enrollment(StudentID, CourseID)

Now:
- Each student and course is stored once.
- To find which courses a student takes, use Enrollment.
- To change a course name, update it in