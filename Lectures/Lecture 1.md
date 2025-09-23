What is a database system?
- A Database System contains a Database and a Database Management System (DBMS).
- A Database is a collection of structured and related data. It consists primarily of entities and relations.
	- A university database could contain info about entities like students and relations between entities like which courses students take.
- A Database Management System (DBMS) is a collection of programs or "layer" that is used to access and manipulate data inside the database. A DBMS sits between the application and the filesystem.

# What can a database system be used for?
Database systems have many applications.
- Banking: Transactions
- Banking: Transactions
- Airlines: Reservations, schedules
- Universities: Registration, grades
- Sales: Customers, products, purchases
- Online retailers: Order tracking, customized recommendations
- Manufacturing: Production, inventory, orders, supply chain
- Human resources: Employee records, salaries, tax deductions
- Internet: Google, Facebook, …

# Data models
A data model is a way to organise the data inside databases.
- **Relational model**: the most commonly used, the one used in the course.
- Object-based data models.
- Network model (obsolete).
- Hierarchical model (obsolete).
- Many more...

# The relational model
If you learn how to deal with a relational database. The move from this type of model to another will not be very hard.

The relational model is a simple model based on set theory.
- All data is structured in relations (tables). These relations represent both entities and relationships.
- A database can be seen as a set of relations.
- Relational algebra offers simple operations on data in databases.

Databases based on the relational models are called relational database.

## A relation is seen as a Table
- with a name
- with named Attributes (columns) of data
- the rows are called tuples and each represent an entity or a relationship.

![[relational-database-example.png | center | 300 ]]

## Domains
A domain is similar to a type. It's a set of allowed values (like datatypes) inside attributes (columns of the schema). An attribute value can only hold a single variable. A domain is a type of constraint which can be put on a database. If the domain isn't correct in what you're attempting to put into the database, the database will not allow you.

All domains (unless you explicitly forbid it) allow a specific value called `NULL`. This value means that the value is unknown or unspecified.

## NULL
You may use `NULL` to indicate that you don't know some piece of information or that it doesen't exist.

**Example**:
To insert Hansen with ID `79797` in MySQL,  insert the tuple `('79797', 'Hansen', NULL, NULL)`
```MySQL
INSERT Instructor VALUES ('79797', 'Hansen', NULL, NULL);
```


## Relations
- If $D_1$ and $D_2$ are sets of values then the Cartesian Product $D_1 \times D_2$  is the set of Tuples $(a_1, a_2,...)$ where reach value $a_i \in D_i$
- A relation $r$ is a subset of the cartesian product: $r \subseteq D_1 \times D_2$

## Relation Schema and Relation Instance

A relation schema defines the overall design of a relation. It consists of:
- the name of the relation, 
- the attribute names, 
- a domain for each attribute where attributes constituting primary keys are underlined

A relation instance $r$ of a relation $R$ is the data stored in the relation at a particular moment in time. The relation instance may change frequently over time.

## Keys
A key is the attribute or set of attributes which makes relation tuples unique. No two tuples may share the same key. Sometimes it takes more than one attribute to make a key.
**Example**:
Classroom($\underline{\text{Building}}$, $\underline{\text{Room}}$, Capacity)

A weak key is a key which could be duplicated such as a name.
A stronger key could be a combination of your name and birthdate however there could still be a student with the same name and birthday. This means that the key is stronger but not robust.

If you want a strong key you want to use something that will never repeat. Things unique student numbers and social security numbers are examples of strong keys.

An artificial key (also called a surrogated key) is a key which is generated automatically by a system to be unique.

A natural key is something that you own such as your email address, government name, etc. If a key is not an artificial ID then it is a natural key.

There are some cases where an artificial key doesen't need to be used.

**Example**:
There is no reason to create an artificial ID for a classroom because if we know where the building is and we know where the classroom number is then the ID can be a combination of the building number and the classroom number since each of these combinations are unique.

### Foreign Keys
A foreign key is a key that rerences another relation where the foreign key is a primary key. This also implies that if the primary key is removed, you are not allowed to use the foreign key anymore. This is called a referential integrity constraint.

![[foreign-keys-diagram.png | center | 400]]

## Relational Database Schemas and Diagrams.
- A Database Schema consists of the relation schemas of all database tables
- A Database Schema Diagram depicts the relation schemas + primary keys foreign keys of all database tables.

![[database-schema.png | center]]

Table names (entities) are shown in blue boxes. 
Primary key attributes are underlined and foreign keys are shown with arrows.

# SQL (Structured Query Language).
This is the most widely used language to extract data from a database.
**Example**:
An example of a query to find physics instructors with a salary < 80000

```SQL
SELECT InstID, InstName FROM Instructor
WHERE DeptName = ‘Physics’ AND Salary < 80000;
```

- SQL is a special purpose programming language designed for managing data stored inside of a relational database.
- SQL is the most widely used database language (the top 4 types of databases are SQL based).
	- SQL is mostly portable among different database systems without adjustments.

## SQL Command Categories

### Data Definition Language (DDL)
CREATE DATABASE, DROP DATABASE,
CREATE TABLE, ALTER TABLE, DROP TABLE,
CREATE INDEX, ALTER INDEX, DROP INDEX,
CREATE VIEW and DROP VIEW

### Data Manipulation Language (DML)
INSERT, UPDATE and DELETE

### Data Query Language
SELECT (i.e. SELECT attributes FROM tables WHERE condition GROUP BY attributes

### Data Control Language
CREATE USER, RENAME USER, DROP USER
ALTER PASSWORD, GRANT, REVOKE and CREATE SYNONYM

### Data Administration Commands
START AUDIT and STOP AUDIT

### Transactional Control Commands
SET TRANSACTION, COMMIT, ROLLBACK and SAVEPOINT