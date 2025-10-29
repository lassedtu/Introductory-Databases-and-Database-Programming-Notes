A **primary key** is a candidate key that has been selected by the database designer (DBA) to uniquely identify tuples in a relation schema $R$.

- Every relation must have exactly one primary key.
- The primary key is used to enforce entity integrity: no two tuples can have the same primary key value, and primary key values cannot be NULL.
- The primary key is chosen from among the [[Candidate Key|candidate keys]] of the relation.

See also: [[Candidate Key]], [[Super Key]]