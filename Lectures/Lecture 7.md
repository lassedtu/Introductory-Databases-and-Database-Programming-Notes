## How to Convert ER Diagrams to Tables

There are two main steps.

1. Convert entity sets to tables (handle complex attributes carefully)
2. Convert relationship sets to tables

---

## Converting Entity Sets to Tables

### Order of Conversion
- Start with strong entity sets
- Then convert weak entity sets
- If a weak entity set depends on another weak entity set, convert the one it depends on first

### Strong Entity Sets (simple attributes)
- Make a table with the same attributes and primary key
- Example:
  ```
  course(course_id, title, credits)
  ```
  Here, course_id is the primary key

### Weak Entity Sets (simple attributes)
- Make a table that also includes the primary key of the identifying entity set as a foreign key
- Example:
  ```
  section(course_id, sec_id, semester, year)
  ```
  course_id is both part of the primary key and a foreign key

---

## Handling Complex Attributes

### 1. Composite Attributes
- If an attribute has sub-parts (like address), only store the smallest parts
- For address, store street_name, street_number, city, zip, and so on

### 2. Multivalued Attributes
- If an attribute can have many values (like phone numbers), make a new table
- The new table has the primary key and the multivalued attribute
- Example:
  ```
  phones(ID, phone_number)
  ```
  ID is a foreign key to instructor

### 3. Derived Attributes
- If an attribute can be calculated from others (like age), do not store it
- Only store the base attribute (like date_of_birth)
- Calculate age when you need it

### Example: Instructor Entity Set
After conversion:
```
instructor(ID, first_name, ..., street_number, ..., zip, date_of_birth)
phones(ID, phone_number)
```

---

## Clean Up Extra Tables

- Do not just follow the conversion rules without thinking
- Remove tables you do not need

### Example: Time Slot
You might get:
```
time_slot1(time_slot_id)
time_slot2(time_slot_id, day, start_time, end_time)
```
But you can simplify to:
```
time_slot(time_slot_id, day, start_time, end_time)
```
time_slot_id is the primary key

Note: A timeslot with the same day and start time cannot have different end times

---

## Converting Binary Relationship Sets

How you convert depends on the type of relationship:
- Many-to-Many
- Many-to-One
- One-to-One

You only need to convert relationships that are not identifying relationships for weak entity sets

---

## Many-to-Many Relationships

For a many-to-many relationship between E₁ and E₂:

- Make a table with the primary keys of E₁ and E₂
- Add any attributes of the relationship
- The primary key is the combination of the primary keys of E₁ and E₂
- Both keys are also foreign keys

Example:
```
advisor(student_ID, instructor_ID, date)
```
student_ID and instructor_ID are both primary and foreign keys

---

## Many-to-One Relationships

For a many-to-one relationship from E₁ (many side) to E₂ (one side):

### Option 1: Make a Separate Table
- Like many-to-many, but the primary key is just the key of E₁

### Option 2: Merge into Many Side (usually better)
- Add the attributes of the relationship and the primary key of E₂ to the table for E₁
- The key from E₂ is a foreign key in E₁

Example:
```
department(dept_name, building, budget)
instructor(ID, name, dept_name, salary)
```
instructor.dept_name is a foreign key to department

If every instructor must belong to a department, make dept_name NOT NULL

---

## One-to-One Relationships

For a one-to-one relationship between E₁ and E₂:

- Add the primary key from one table (plus any relationship attributes) to the other table as a foreign key

There are two ways:
1. Add E₂'s key to E₁
2. Add E₁'s key to E₂

Choose the way that gives the fewest NULL values

- If E₁ always participates and E₂ does not, add E₂'s key to E₁

---

## Example Scenarios

### MyCO Conference Room Management

- Store rooms: name, floor, capacity, telephone (with extension if any), video projector (with serial number)
- Track events in each room
- Events: name, description, start date, end date
- Organizers for each event: CPR number, name, surname, role, telephone, email

### TV3 News Tracking

- Register news editions: date/time, host journalist (max 30 minutes)
- News items per edition: time, description, topic, viewer count
- Topics: title, description, curating journalists (with roles)
- Footages: title, date, duration (max 3 minutes), reporter journalist
- Same footage can be used for more than one news item
- Journalists: CPR, first name, last name, address (street, number, city, zip, country), phone numbers, emails

### Love4Sail Boat Rental

- Register customers and boat owners: CPR, name, address, phone, email
- Boats: WIN code, description (type and length), daily price
- Each owner can have many boats
- Rentals: boats rented, customer, start date, end date
- Each customer can have many rentals
- Damage tracking: damage info, repair cost

### DKAvisen Newspaper Publisher

- Newspapers: title, founding date, periodicity
- Editions: publication date, editor journalist
- Articles: title, text, topic, read count, writer journalists (with roles)
- Photos: title, date, reporter journalist
- Same photo can be used in more than one article
- Journalists: CPR, first name, last name, address (street, number, city, zip, country), phone numbers, emails

Performance queries needed:
- Most read article per topic
- Top 10 journalists by total reads
- Reporters whose photos were never used more than once
- Topics with below-average reads
- Journalists who were both writers and reporters for the same article