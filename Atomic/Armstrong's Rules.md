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