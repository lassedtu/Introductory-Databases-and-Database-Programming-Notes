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
Using these axioms, we can find out which dependencies are implied by the ones we already know. (See: [[Armstrong's Rules]])

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
### [[Super Key]] and Functional Dependencies

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

### [[Candidate Key]] and Functional Dependencies

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