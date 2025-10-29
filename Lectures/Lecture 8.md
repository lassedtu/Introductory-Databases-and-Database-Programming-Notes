## Normalisation

- Normalisation is a technique to organise data in a database.
- The main goal: reduce redundancy and prevent update problems.

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

---

## Redundancy

Redundancy is a major problem in databases. It means the same data is stored in more than one place. For example, imagine a table where a student's address appears in every row for every course they take. If the student moves and you update their address in only some rows, the database now has two different addresses for the same student. This is called a modification anomaly.

Why is this bad? If you ask the database, "What is the student's address?" you might get different answers depending on which row is used. This makes the database inconsistent.

| StudentID | Name   | Address      | CourseID |
|-----------|--------|-------------|----------|
| 101       | Alice  | 1 Main St   | CS101    |
| 101       | Alice  | 99 Elm Ave  | MATH201  |

If Alice’s address is updated in only one row, the database now has conflicting information.

A redundancy-free database avoids this problem. Each piece of information is stored only once, so when you update it, you only need to change it in one place. The DBMS can then update data efficiently and keep everything consistent. This is why normalisation is so important: it helps eliminate redundancy and keeps your data reliable.

### Redundancy and Modification Anomalies

Suppose we try to combine instructor and department information into a single table:

![[redundant-table.png| center | 600]]

This design has two main problems:

1. **Redundancy:** The building and budget for each department are repeated for every instructor in that department. If you need to update the budget for Physics, you have to change it in every row where DeptName is Physics. If you miss one, the data becomes inconsistent.

2. **Incomplete Information:** You cannot store information about a department unless at least one instructor works there. For example, if the Philosophy department has no instructors yet, there is no way to record its building or budget.

Combining instructor and department in one table leads to repeated data and makes it impossible to store departments without instructors. This is why we separate them into different tables and use relationships to connect them.

---
## Good Relational Design

To avoid modification anomalies, we add extra restrictions to our table designs. When a table meets these restrictions, it is said to be in a certain normal form, such as Third Normal Form (3NF). Normalisation is the process of reorganising tables to reach higher normal forms and remove redundancy. This usually involves splitting a table into two or more smaller tables. Importantly, normalisation is information preserving: you can always reconstruct the original table by joining the smaller tables back together, so no data is lost in the process.

![[fixed-redundant-table.png | center | 600]]

If a table/relation schema is in e.g. 3NF, then by definition it is also in 2NF and 1NF
Databases in higher normal forms are also implacably in lower normal forms as seen on this diagram:

![[normalisation.png | center | 600]]

---
## Functional Dependencies

Functional dependencies describe how attributes are related within a table. If you know the value of one attribute (or a set of attributes), you can determine the value of another attribute. This is a key concept for understanding how to design good relational schemas.

### Formal Definition of Functional Dependency

Let $X$ and $Y$ be subsets of the set of attributes of a relation schema $R$.

- A functional dependency $X \rightarrow Y$ holds for $R$ if and only if, in every legal instance of $R$, each $X$ value has associated precisely one $Y$ value (i.e., whenever two rows have the same $X$ value, they also have the same $Y$ values).
- When $X \rightarrow Y$ holds for $R$, we say:
    - $Y$ is functionally dependent on $X$ and $X$ functionally determines $Y$.
    - $X$ is called the determinant and $Y$ the dependent.
    - If $X = \{A_1, \ldots, A_n\}$ and $Y = \{B_1, \ldots, B_m\}$, we sometimes write $A_1, \ldots, A_n \rightarrow B_1, \ldots, B_m$ or $A

### Trivial and Nontrivial Functional Dependencies

A functional dependency is **trivial** if the attribute(s) on the right side are already included in the left side.  
A functional dependency is **nontrivial** if the right side contains attributes not found on the left side.  
Nontrivial dependencies are the ones that usually matter for database design.

### Keys and Functional Dependencies

A key is a set of attributes that uniquely determines all other attributes in the table.  
Keys are defined using functional dependencies: if a set of attributes functionally determines every other attribute in the relation, it is a key.

### Armstrong’s Axioms

Armstrong’s axioms are a set of rules for reasoning about functional dependencies.  
They allow us to derive all possible functional dependencies that hold in a relation, based on a given set.  
Using these axioms, we can find out which dependencies are implied by the ones we already know.

---
### Example: Describing Dependencies Between Attribute Sets

Functional dependencies describe associations between two sets of attributes, A and B, within a relation schema R.
This is essentially a many-to-one relationship from one set of attributes (A) to another set (B) in the same relation.
Example: Consider the relation Shipments(Vendor, Part, Qty):

![[attribute-sets.png | center | 600]]

$\{Vendor, Part\} \rightarrow \{Qty\}$ is a functional dependency holding for Shipments.
The attribute set $\{Vendor, Part\}$ functionally determines the attribute set $\{Qty\}$.
The attribute set $\{Qty\}$ is functionally dependent on the attribute set $\{Vendor, Part\}$.

Certainly! Here’s the new example section, written as a standalone piece and referencing a diagram:

---
### Example: Valid and Canonical Functional Dependencies

Many functional dependencies can be proposed for a relation schema, but not all are valid. To determine whether a functional dependency (FD) is valid (i.e., legal for all relation instances), you must consider the real-world meaning of the data.

Suppose we have the relation: Shipment1(Vendor, City, Part, Qty), where each vendor can only be in one city.

![[shipment1-fd-diagram.png | center | 600]]

- For a set of 4 attributes, there are $2^4 = 16$ possible subsets.
- Combining 16 possible determinants with 16 possible dependents gives $16 \cdot 16 = 256$ potential FDs.
- Of these 256 potential FDs, some are valid and some are not, depending on the real-world constraints.

#### Canonical Cover Set

A (canonical) cover set is an irreducible or minimal set of valid functional dependencies from which all valid FDs can be determined.

In this example, a canonical cover set is:
- $\{\{Vendor, Part\} \rightarrow \{Qty\},\ \{Vendor\} \rightarrow \{City\}\}$

#### Closure Set

The closure set $F^+$ of a set $F$ of functional dependencies is the set of all valid FDs that can be logically derived from $F$.

---
### Super Key and Functional Dependencies

Let $R$ be a relation schema and let $K$ be a subset of the set $A_R$ of attributes of $R$.

- **Super key, original definition:**  
  $K$ is a superkey of $R$ if, in any legal instance of $R$, for all pairs $t_1$ and $t_2$ of tuples in the instance of $R$, if $t_1 \neq t_2$, then $t_1[K] \neq t_2[K]$.  
  In other words, a specific $K$ value will uniquely define a specific tuple in $R$.

- **Super key defined by functional dependencies:**  
  $K$ is a superkey of $R$ if $K \rightarrow X$ holds for every attribute $X$ of $R$.

#### Super Key Examples for Shipment1(Vendor, City, Part, Qty)

- $\{Vendor, City, Part\}$  
  Knowing the values of Vendor, City, and Part, the value of Qty is defined.

- However, we are usually interested in a super key with a minimum set of attributes (i.e., a candidate key):  
  $\{Vendor, Part\}$  
  Knowing the values of Vendor and Part, the values of City and Qty are defined.

Certainly! Here’s the "Candidate Key and Functional Dependencies" section in your note’s style, ready to follow the Super Key section:

---

### Candidate Key and Functional Dependencies

**Candidate key is a minimal super key:**
$K$ is a candidate key for $R$ if and only if
$K \rightarrow A_R$ and for no $\alpha \subset K$, $\alpha \rightarrow A_R$
(i.e., $K$ functionally determines all attributes of $R$, and no proper subset of $K$ does).

**Candidate key example for Shipment1(Vendor, City, Part, Qty):**
$\{Vendor, Part\}$
This is a minimal super key: knowing Vendor and Part determines City and Qty.

In some cases, $R$ can have several candidate keys!

**Primary key:**
A candidate key is selected by the DBA to be the primary key for a relation.

---
## Armstrong’s Rules

Let $R$ be a relation schema and let $F$ be a set of functional dependencies on $R$.

- **Armstrong’s Rules** are a set of axioms and derived theorems for deriving functional dependencies from $F$.
- They are:
    - **Sound:** Only valid FDs are derived from valid FDs.
    - **Complete:** All valid FDs (the closure set of $F$) can be derived from a cover set $F$.
    - Can be used, for example, to find candidate keys.

### Armstrong’s Axioms and Derived Theorems

Let $X$, $Y$, $Z$, and $V$ be sets of attributes.

**Armstrong’s axioms:**
1. **Reflexivity:** If $Y$ is a subset of $X$, then $X \rightarrow Y$
2. **Augmentation:** If $X \rightarrow Y$, then $XZ \rightarrow YZ$  
   (Note: $XZ$ is shorthand for $X \cup Z$; sets have no order or repetitions)
3. **Transitivity:** If $X \rightarrow Y$ and $Y \rightarrow Z$, then $X \rightarrow Z$

**Derived theorems:**
4. **Self-determination:** $X \rightarrow X$
5. **Decomposition:** If $X \rightarrow YZ$, then $X \rightarrow Y$ and $X \rightarrow Z$
6. **Union:** If $X \rightarrow Y$ and $X \rightarrow Z$, then $X \rightarrow YZ$
7. **Composition:** If $X \rightarrow Y$ and $Z \rightarrow V$, then $XZ \rightarrow YV$
8. **General Unification:** If $X \rightarrow Y$ and $Z \rightarrow V$, then $X \cup (Z - Y) \rightarrow YV$  
   (where $\cup$ is set union and $-$ is set difference)

---

### Using Armstrong’s Rules

Armstrong’s rules can be used to propose candidate keys.  
For example, given $R(A, B, C, D, E)$ with functional dependencies:  
$A \rightarrow BC$, $CD \rightarrow E$, $B \rightarrow D$, $E \rightarrow A$

1. $A \rightarrow A$ (Rule 4: Self-determination)
2. $A \rightarrow B$ (Rule 5: Decomposition of $A \rightarrow BC$)
3. $A \rightarrow C$ (Rule 5: Decomposition of $A \rightarrow BC$)
4. $A \rightarrow D$ (Rule 3: Transitivity of $A \rightarrow B$ and $B \rightarrow D$)
5. $A \rightarrow CD$ (Rule 6: Union)
6. $A \rightarrow E$ (Rule 3: Transitivity of $A \rightarrow CD$ and $CD \rightarrow E$)
7. $A \rightarrow ABCDE$ (Rule 6: Union)
8. $E \rightarrow ABCDE$ (Rule 3: Transitivity of $E \rightarrow A$ and $A \rightarrow ABCDE$)
9. $BC \rightarrow ABCDE$ can also be proved
10. $CD \rightarrow ABCDE$ can also be proved
11. **Candidate Keys:** $\{A\}$, $\{E\}$, $\{B, C\}$, and $\{C, D\}$. Select one for the primary key!
12. **Relation Schema:** One of the following: $R(A, B, C, D, E)$, $R(E, A, B, C, D)$, $R(B, C, A, D, E)$, or $R(C, D, A, B, E)$

---

## Normal Forms 1NF-3NF

A table is said to be in a certain normal form if it satisfies specific rules about how attributes depend on keys. These rules are based on the idea of functional dependencies.

2NF and 3NF are defined using the concept of functional dependencies. The starting point is a relational schema $R$ and a cover set $FD$ of functional dependencies for $R$. The original definitions assume the table has one candidate key, chosen as the primary key (called "the key"). The generalised definitions, as found in the book, take all candidate keys into account. When there is only one candidate key, the original and generalised definitions are equivalent.

### First Normal Form (1NF)
A table is in first normal form if all attributes depend on the key. This means every column contains only atomic (indivisible) values, and there are no repeating groups or arrays.

![[1nf-example-diagram-2.png | center | 400]]
### Second Normal Form (2NF)
A table is in second normal form if it is already in 1NF, and all attributes depend on the whole key. In other words, there are no partial dependencies: no non-key attribute depends on just part of a composite key.

![[2nf-example-diagram-2.png | center | 400]]

### Third Normal Form (3NF)
A table is in third normal form if it is in 2NF, and all attributes depend on nothing but the key. This means there are no transitive dependencies: non-key attributes do not depend on other non-key attributes.

![[3nf-example-diagram-2.png | center | 400]]

In summary:
- 1NF: All attributes depend on the key.
- 2NF: All attributes depend on the whole key.
- 3NF: All attributes depend on nothing but the key.

These normal forms help ensure that data is stored efficiently, without unnecessary redundancy or update anomalies.

## Normalisation of Normal Forms

## To 1NF

To bring a table into first normal form (1NF), you need to make sure that every column contains only atomic (indivisible) values. This means there should be no repeating groups, arrays, or lists in any cell—each cell should hold just a single value.

If you find a column that contains multiple values (for example, a list of phone numbers or a set of courses in one cell), you need to split these values into separate rows. Sometimes, this also means creating a new table to store the repeating information, with a foreign key linking back to the original table.

### Example

OrdersTable below is not in 1NF as the values of the attribute ItemNos are not atomic.

![[1nf-example-diagram-1.png | center | 400]]

Normalisation to 1NF

![[1nf-example-diagram-2.png | center | 400]]

## 1NF to 2NF

To convert a table from first normal form (1NF) to second normal form (2NF), you need to remove partial dependencies. A partial dependency happens when an attribute depends on only part of a composite key, not the whole key.

The process works like this:  
If you find an attribute (or a set of attributes) that depends only on a part of the primary key (let’s call that part $K_{part}$), you move that attribute and $K_{part}$ into a new table. In this new table, $K_{part}$ becomes the primary key. It also acts as a foreign key in the original table, linking the two tables together.

For example, suppose you have a table $R(K, ..., A)$, where $A$ depends only on $K_{part} \subset K$. You split it into two tables:
- $R_1(K, ...)$, which keeps the original key and the remaining attributes, and includes a foreign key reference to $R_2$.
- $R_2(K_{part}, A)$, where $K_{part}$ is the primary key.

If there are several attributes with partial dependencies, you repeat this process for each one until all attributes in every table depend on the whole key. This step-by-step decomposition is guaranteed to be lossless, meaning you can always reconstruct the original table by joining the new tables together. In other words,  
$$(\text{select } K, ... \text{ from } R) \text{ natural join } (\text{select } K_{part}, A \text{ from } R) = \text{select } * \text{ from } R$$

This ensures that no data is lost during the normalisation process, and your tables are now in 2NF.

### Example

Orders1NF is in 1NF, but not 2NF

- The table Orders1NF has columns: OrderNo, ItemNo, and ItemName.
- The primary key is (OrderNo, ItemNo).
- There is a functional dependency: ItemNo → ItemName.

This means that ItemName depends only on ItemNo, not on both OrderNo and ItemNo together.  
Because ItemName does not depend on the whole primary key, the table is not in 2NF. This is called a partial dependency, which is not allowed in 2NF.

![[2nf-example-diagram-1.png | center | 400]]


Normalization to 2NF (Orders2NF and Items)

- We split the original table into two tables:
    - Orders2NF(OrderNo, ItemNo)
    - Items(ItemNo, ItemName)
- Orders2NF keeps track of which items are in each order.  
- Items stores information about each item (like its name).
- Orders2NF has a foreign key (ItemNo) that links to Items.
- ItemNo is part of the key in Orders2NF, because knowing just the OrderNo does not tell you which ItemNo it is (OrderNo does not determine ItemNo).

This removes the partial dependency and puts the data in 2NF.

![[2nf-example-diagram-2.png| center | 400]]

## 2NF to 3NF

To bring a table from second normal form (2NF) to third normal form (3NF), you need to remove transitive dependencies. A transitive dependency happens when a non-key attribute depends on another non-key attribute, which in turn depends on the primary key. In other words, some attribute $A$ depends on $B$, and $B$ depends on the key $K$, but $A$ does not depend directly on $K$.

To fix this, you move any attributes that are transitively dependent on the key into a new table. Specifically, if you have a situation where $K \rightarrow B \rightarrow A$, you create a new table with $B$ as the primary key and $A$ as an attribute. In your original table, you keep $K$ and $B$, and $B$ now acts as a foreign key referencing the new table.

For example, suppose you have a table $R(K, ..., B, A)$, where $A$ depends on $B$, and $B$ depends on $K$. You split it into two tables:
- $R_1(K, ..., B)$, which keeps the original key and $B$, and includes a foreign key reference to $R_2$.
- $R_2(B, A)$, where $B$ is the primary key.

If there are several attributes with transitive dependencies, you repeat this process for each one until all non-key attributes in every table depend directly on the whole key, and not on other non-key attributes. This step-by-step decomposition is also lossless, so you can always reconstruct the original table by joining the new tables together:
$$(\text{select } K, ..., B \text{ from } R) \text{ natural join } (\text{select } B, A \text{ from } R) = \text{select } * \text{ from } R$$

After this process, your tables are in third normal form, which means all non-key attributes depend only on the key, and nothing but the key. This helps eliminate redundancy and makes your database easier to maintain.

### Example

Customers2NF is in 2NF

- The table Customers2NF has columns: CustomerNo, PostNo, and CityName.
- Functional dependencies:
    - CustomerNo → PostNo
    - PostNo → CityName

CityName depends on CustomerNo, but only through PostNo (not directly).  
This is called a transitive dependency, which is not allowed in 3NF.  
So, Customers2NF is in 2NF, but not in 3NF.

![[3nf-example-diagram-1.png | center | 400]]

Normalisation to 3NF

- We split the table into two:
    - Customers3NF(CustomerNo, PostNo)
    - Post(PostNo, CityName)
- Customers3NF stores each customer and their post code.
- Post stores each post code and its city name.
- Customers3NF has a foreign key (PostNo) that links to Post.

Now, CityName is stored only once for each PostNo, and there are no transitive dependencies. The tables are in 3NF.

![[3nf-example-diagram-2.png | center | 400]]
