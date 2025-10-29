The relational model is a way of structuring data. Data is stored in tables. Each table has rows. Each row represents a record. Each row has columns. Each column represents an attribute. Tables can be related through [[Keys]]. Keys link rows across tables. This allows structured querying. This allows consistency. This allows abstraction.

If you learn how to deal with a relational database. The move from this type of model to another will not be very hard.

The relational model is a simple model based on set theory.
- All data is structured in [[Relations]] (tables). These relations represent both entities and relationships.
- A database can be seen as a set of [[Relations]].
- Relational algebra offers simple operations on data in databases.

Databases based on the relational models are called relational database.

## Relation Schema and Relation Instance

A relation schema defines the overall design of a relation. It consists of:
- the name of the relation, 
- the attribute names, 
- a domain ([[Domains]]) for each attribute where attributes constituting primary [[Keys]] are underlined

![[relational-database-example.png | center | 300 ]]