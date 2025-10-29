To avoid [[Modification Anomalies]], we add extra restrictions to our table designs. When a table meets these restrictions, it is said to be in a certain normal form, such as Third Normal Form (3NF) (See: [[Normal Forms]]). [[Normalisation]] is the process of reorganising tables to reach higher normal forms and remove [[Redundancy]]. This usually involves splitting a table into two or more smaller tables. Importantly, normalisation is information preserving: you can always reconstruct the original table by joining the smaller tables back together, so no data is lost in the process.

![[fixed-redundant-table.png | center | 600]]

If a [[Entity-Relationship (ER) Diagrams| table/relation schema ]] is in e.g. 3NF, then by definition it is also in 2NF and 1NF
Databases in higher normal forms are also implacably in lower normal forms as seen on this diagram:

![[normalisation.png | center | 600]]
