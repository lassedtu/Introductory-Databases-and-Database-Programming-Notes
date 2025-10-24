## What is database design

Database design is about figuring out what data you need to store and how it all fits together. There are three steps:

### 1. Conceptual design
- Make a simple model of your data
- Use ER diagrams for this
- Focus on what entities and relationships you need
- Do not think about tables or how to store the data yet

### 2. Logical design
- Make a logical model for a specific type of database (like relational)
- Still do not worry about which DBMS you will use
- For relational databases, this means making table schemas

### 3. Physical design
- Decide how to actually store the data in a specific DBMS
- Choose things like file structure and indexes

This lecture is about the first step: how to use ER diagrams to make a conceptual model.

---

## Entities and relationships

### Entity
- A thing or object you want to store info about (like a student)

### Entity set
- A group of entities of the same type (like all students)
- All entities in a set have the same attributes

### Entity attributes
- Properties of an entity (like ID, name for a student)

### Relationship
- A connection between entities (like a student has an advisor who is an instructor)

### Relationship set
- All relationships of the same type (like all advisor relationships between students and instructors)

### Relationship attributes
- Properties of the relationship itself (like the date when a student got an advisor)

---

## Types of attributes

### Domain
- The set of allowed values for an attribute

### Simple (atomic) attribute
- Cannot be split into smaller parts (like ID, salary)

### Composite attribute
- Made up of smaller parts (like name = first_name, last_name)

### Multivalued attribute
- Can have more than one value (like phone_numbers for a person)

### Derived attribute
- Can be calculated from other attributes (like age from date_of_birth)

---

## Relationships: order, cardinality, participation

### Order (degree) of a relationship
- How many entity sets are involved
- Binary = 2, ternary = 3, etc.

### Cardinality (for binary relationships)

#### One-to-one (1:1)
- Each entity in set A can be related to at most one in set B, and vice versa

#### One-to-many (1:N)
- Each entity in set A can be related to many in set B, but each in B to at most one in A

#### Many-to-one (N:1)
- Each entity in set A can be related to at most one in set B, but each in B to many in A

#### Many-to-many (N:M)
- Each entity in set A can be related to many in set B, and vice versa

### Participation

#### Total participation
- Every entity in the set must participate in the relationship (no exceptions)
- Shown with a double line in ER diagrams

#### Partial participation
- Some entities might not participate
- Shown with a single line

---

## Keys in ER models

### Entity set keys

#### Super key
- One or more attributes that uniquely identify an entity

#### Candidate key
- A minimal super key (no unnecessary attributes)

#### Primary key
- The candidate key you choose to use as the main key

### Relationship set keys

- Usually a combination of the primary keys of the participating entity sets
- Sometimes relationship attributes are needed too (especially if they are multivalued)

---

## ER diagrams: how to draw them

### Entity sets
- Drawn as rectangles
- Attributes listed inside
- Primary key is underlined

### Relationship sets
- Drawn as diamonds
- Connected to entity sets with lines
- Relationship attributes in a box, linked with a dashed line

### Cardinality
- Arrow means "one"
- No arrow means "many"
- Example: instructor ←→ advisor → student (means one instructor can advise many students, but each student has at most one advisor)

### Participation
- Double line = total participation
- Single line = partial participation

### Attributes
- Simple: just write the name
- Composite: indent sub-attributes under the main one
- Multivalued: use curly braces {phone_numbers}
- Derived: use parentheses (age)

---

## Roles in relationships

- Sometimes the same entity set appears more than once in a relationship, but with different roles
- Example: course prerequisites (a course can be a prerequisite for another course)

---

## Ternary and higher-order relationships

- Sometimes a relationship involves more than two entity sets (like instructor, student, and project)
- You can always turn a ternary (or higher) relationship into binary ones by making a new entity set for the relationship and connecting it to the original sets

---

## Strong and weak entity sets

### Strong entity set
- Has its own primary key

### Weak entity set
- Cannot be uniquely identified by its own attributes alone
- Needs a strong entity set to help identify it

#### Identifying entity set
- The strong entity set that helps identify the weak one

#### Identifying relationship
- The relationship that connects the weak entity set to its identifying entity set
- Must be one-to-many from the strong to the weak set
- Must have total participation from the weak set
- Shown with a double diamond

#### Discriminator (partial key)
- The attribute(s) that distinguish weak entities that depend on the same strong entity
- Shown with a dashed underline

#### Primary key of weak entity set
- Combination of the primary key of the strong entity set and the partial key of the weak entity set

---

## Example: university database ER diagram

- Entity sets: instructor, student, course, section, department, classroom, time_slot
- Relationship sets: advisor, teaches, takes, course_dept, sec_course, sec_time_slot, sec_class
- Weak entity set: section (depends on course)

---

## Notation summary

- Entity set: rectangle, attributes inside, primary key underlined
- Relationship set: diamond
- Identifying relationship: double diamond
- Total participation: double line
- Partial participation: single line
- Many-to-many: no arrows
- Many-to-one: arrow to "one" side
- One-to-one: arrows both ways
- Multivalued attribute: {attribute}
- Derived attribute: (attribute)
- Partial key: dashed underline

---

## Other ER diagram notations

### UML class diagrams
- Cardinality is shown near the entity, not the relationship

### Crow's foot notation
- Uses special symbols for "one" and "many"
- Popular in industry
