## Representing ER Diagrams

An Entity-Relationship (ER) diagram is a visual tool for modeling the structure of a database. It shows entities, their attributes, relationships between entities, and important constraints like cardinality and participation.

---

### Entities

Entities are represented as rectangles.  
The name of the entity set is written inside the rectangle.  
Example: A rectangle labeled "Student" represents the Student entity set.

---

### Attributes

Attributes are shown as ovals connected to their entity (or relationship) by a straight line.

- Primary key attributes are underlined.
- Composite attributes have their sub-attributes connected as smaller ovals branching from the main attribute.
- Multivalued attributes are shown as double ovals.
- Derived attributes are shown as dashed ovals.

---

### Relationships

Relationship sets are represented as diamonds.  
The name of the relationship is written inside the diamond.  
Diamonds are connected to the participating entity sets by straight lines.  
Relationship attributes (if any) are shown as ovals connected to the diamond.

---

### Cardinality

Cardinality specifies how many entities can participate in a relationship.

- One: Arrowhead or a single line (→)
- Many: No arrow, or a crow’s foot (in Crow’s Foot notation)
- One-to-one: Arrows on both sides
- One-to-many: Arrow on the "one" side, none on the "many" side
- Many-to-many: No arrows

---

### Participation

Participation describes whether all or only some entities participate in a relationship.

- Total participation: Every entity must participate; shown with a double line.
- Partial participation: Some entities may not participate; shown with a single line.

---

### [[Keys]]

- Primary key: Underlined attribute(s) in the entity rectangle or attribute oval.
- Partial key (for weak entities): Dashed underline.
- Foreign keys: Not shown directly in ER diagrams, but implied by relationships.

---

### Notation Summary Table

| Component         | Symbol/Shape         | Notation Example                |
| - | - | -  |
| Entity set        | Rectangle            | Student                        |
| Attribute         | Oval                 | name, ID                       |
| Primary key       | Underlined oval      | ID                             |
| Composite attr.   | Ovals branching      | address → street, city         |
| Multivalued attr. | Double oval          | {phone_number}                 |
| Derived attr.     | Dashed oval          | (age)                          |
| Relationship      | Diamond              | Enrolls                        |
| Relationship attr.| Oval on diamond      | date                           |
| Cardinality       | Arrow/crow’s foot    | →, crow’s foot                 |
| Participation     | Single/double line   | —, ═                           |

---

### Visual Example

![[database-schema.png]]

ER diagrams are essential for designing, analyzing, and communicating the structure of a database before implementation. They help clarify how data is organized and how different parts of the system interact.