Keys are attributes or sets of attributes that uniquely identify tuples (rows) in a relation or entities in an entity set. They are essential for ensuring data integrity and supporting relationships between data.

---

## Types of Keys

### [[Super Key]]
- One or more attributes that uniquely identify an entity in an entity set.
- May contain unnecessary attributes.
- **Example:** $\{\text{Building}, \text{Room}, \text{Capacity}\}$ for a Classroom entity.

### [[Candidate Key]]
- A minimal super key (no unnecessary attributes).
- There can be multiple candidate keys in an entity set.
- **Example:** $\{\text{Building}, \text{Room}\}$ if this combination is unique for each classroom.

### [[Primary Key]]
- The candidate key chosen to uniquely identify entities in an entity set.
- Used as the main reference for relationships.
- **Example:** $\{\text{Building}, \text{Room}\}$ as the primary key for Classroom.

### Alternate Key
- Candidate keys that are not chosen as the primary key.

### Composite Key
- A key consisting of more than one attribute.
- Often used when a single attribute is not sufficient to uniquely identify an entity.

### Natural Key
- A key formed of attributes that naturally exist in the real world (e.g., email address, government ID).

### Artificial (Surrogate) Key
- A system-generated key (e.g., auto-incremented ID) used when no natural key is suitable.

### Weak Key
- A key that is not guaranteed to be unique by itself (e.g., name).
- May require additional attributes to ensure uniqueness.

---

## Keys in Relationship Sets

- Relationship set keys are usually a combination of the primary keys of the participating entity sets.
- Sometimes, relationship attributes are also needed, especially if they are multivalued.
- Ensures that each relationship instance is uniquely identifiable.

---

## Foreign Keys

A foreign key is an attribute (or set of attributes) in one relation that references the primary key of another relation.  
- Enforces referential integrity: if the referenced primary key is deleted, the foreign key must be updated or removed.
- **Example:** If a Classroom references a Building, the Building's primary key is a foreign key in the Classroom relation.

![[foreign-keys-diagram.png|center|400]]

---

## Examples

- **Classroom($\underline{\text{Building}}, \underline{\text{Room}}, \text{Capacity}$):**
  - Primary Key: $\{\text{Building}, \text{Room}\}$
  - No need for an artificial key if this combination is unique.

- **Student:**
  - Weak Key: Name (not unique)
  - Stronger Key: Name + Birthdate (still not robust)
  - Strong Key: Student Number or Social Security Number (unique)
