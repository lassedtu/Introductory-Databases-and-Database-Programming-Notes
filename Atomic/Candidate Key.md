A **candidate key** is a minimal superkey for a relation schema $R$.

- $K$ is a candidate key for $R$ if:
    - $K \rightarrow A_R$ (i.e., $K$ functionally determines all attributes of $R$)
    - For no $\alpha \subset K$, $\alpha \rightarrow A_R$ (no proper subset of $K$ functionally determines all attributes of $R$)

In other words, a candidate key uniquely identifies each tuple in $R$, and no subset of its attributes can do the same.

A relation can have multiple candidate keys. One of them is chosen as the [[Primary Key]].

See also: [[Super Key]]