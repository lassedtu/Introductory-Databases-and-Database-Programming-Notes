- If we have sets of values $D_1, D_2, \dots, D_n$
  Then the Cartesian Product is:  
  $$D_1 \times D_2 \times \dots \times D_n = \{ (a_1, a_2, \dots, a_n) \mid a_1 \in D_1 \ $$
  This means we take every possible combination of values from each domain.

- A **Relation** $r$ is a subset of this Cartesian Product:  
  $$ r \subseteq D_1 \times D_2 \times \dots \times D_n $$
  In other words, not every possible tuple needs to be in the relation only the ones that actually exist in the data.

- A **Relation Instance** `r` of a relation `R` is the set of tuples stored at a specific point in time.  
  - The schema `R` defines the structure (attributes and domains).  
  - The instance `r` defines the actual data (rows).  
  - Instances can change over time while the schema usually remains fixed.

## Explanation with No Math

- Think of a [[domain]] as the set of all possible values for something.  
    Example: the set of all names, or the set of all ages.

- If you combine domains, you get all possible ways values could be paired or grouped together.  
    Example: every possible pairing of a name with an age.

- A relation is just a [[table]] that picks some of those possible combinations and stores them.  
    Example: not every name-age pairing is real, only the ones that correspond to actual people.
    
- A relation instance is the actual data in that table at a certain moment.  
    Example: today the table has 3 rows of students, but tomorrow it might have 4 if a new student is added.

### Connection to ER Diagrams
[[Database Schema Diagram]]s are a way to **visually design** how [[data]] should be organised.  
- Entities in an ER diagram become [[table]]s in [[the relational model]].
- Attributes in an ER diagram become columns.  
- Relationships in an ER diagram become foreign [[keys]] or linking tables.  

So ER diagrams describe the design and [[the relational model]] describes the mathematical structure that stores the data.