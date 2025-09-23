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