> Note 5 Discussion 5

 
# Unary Operators
## Projection($\pi$)
> Summary:
> 1. Select a subset of columns(vertical).
> 2. Use set semantics, dropping duplicates.
> 3. Correspond to `SELECT` keyword.
> 4. Example: `SELECT name FROM R` becomes $\pi_{name}(R)$


## Selection$(\sigma)$
> Summary:
> 1. Select a subset of rows(horizontal).
> 2. Use set semantics, dropping duplicates.
> 3. Correspond to `WHERE` keyword.
> 4. Example: `SELECT * FROM R WHERE id = 100` becomes $\sigma_{id=100}(R)$


## Renaming$(\rho)$
> Summary:
> 1. Rename a column.
> 2. Correspond to `AS` keyword.
> 3. Example: $ρ((1→sid1,4→sid2),S)$ renames the 1st and 4th columns to `sid1` and `sid2` respectively



# Binary Operators
Join










# Compound Operators
Union


Intersect





# Extended Operators





# Convert SQL to Relational Algebra


