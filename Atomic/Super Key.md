A **superkey** is a set of attributes in a relation schema $R$ that uniquely identifies each tuple in any legal instance of $R$.

- **Original definition:**  
  $K$ is a superkey of $R$ if, in any legal instance of $R$, for all pairs $t_1$ and $t_2$ of tuples in $R$, if $t_1 \neq t_2$, then $t_1[K] \neq t_2[K]$.  
  In other words, a specific $K$ value will uniquely define a specific tuple in $R$.

- **Defined by functional dependencies:**  
  $K$ is a superkey of $R$ if $K \rightarrow X$ holds for every attribute $X$ of $R$ (i.e., $K$ functionally determines all attributes in $R$).

A superkey may contain extra attributes; a minimal superkey is called a [[Candidate Key]], [[Primary Key]]