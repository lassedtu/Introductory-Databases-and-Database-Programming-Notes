A table is said to be in a certain normal form if it satisfies specific rules about how attributes depend on keys. These rules are based on the idea of functional dependencies.

2NF and 3NF are defined using the concept of [[functional dependencies]]. The starting point is a relational schema $R$ and a cover set $FD$ of functional dependencies for $R$. The original definitions assume the table has one candidate key, chosen as the primary key (called "the key"). The generalised definitions, as found in the book, take all candidate keys into account. When there is only one candidate key, the original and generalised definitions are equivalent.

If a table/relation schema is in e.g. 3NF, then by definition it is also in 2NF and 1NF
Databases in higher normal forms are also implacably in lower normal forms as seen on this diagram:

![[normalisation.png | center | 600]]

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

## [[Normalisation]] of Normal Forms

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