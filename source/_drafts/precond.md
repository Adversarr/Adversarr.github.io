# Preconditioners

> SIAM: Factorization-based Sparse Solvers and Preconditions, 2013

- imporve efficiency and robustness of iterative Solvers
- Solve a transformed linear sys, Left/Right Preconditioning.
- Goal: Find a matrix M that approximates A, that is 
    1. cheap to compute, store, and "invert", and Parallelize!
    2. Good approximation.
- Standard Design Strategy:
    1. Start with a complete factorization
    2. Add approximation, that is cheap to compute and store (1), and hopefully good (2).

This lecture:
1. Incomplete Factorization
2. Low-rank Approximation

## Incomplete LU

Structure-based dropping, level of fill:

- $ILU(0), ILU(k)$
- Rationale: The higher the level, the smaller the entry is.
- Separate symbolic factorization to determine fill-in pattern!

More powerful: Value-based dropping: drop truly small entries.

- Fill-in pattern must be determined on the fly.

ILUTP(Sadd): ILU with threshold pivoting.

- Remove elements smaller than $\tau$
- at most $p$ largest kept in each row/column.

Further on, Super ILU.



