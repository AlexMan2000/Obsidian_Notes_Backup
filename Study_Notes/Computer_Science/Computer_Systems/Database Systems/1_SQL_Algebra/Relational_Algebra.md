> Note 5 Discussion 5



# Overview
> [!overview]
> ![](Relational_Algebra.assets/image-20240209080738119.png)


# Unary Operators
## Projection($\pi$)
> [!def]
> ![](Relational_Algebra.assets/image-20240209082354269.png)![](Relational_Algebra.assets/image-20240209082403920.png)
> 
> **Summary:**
> 1. Select a subset of columns(vertical).
> 2. Use set semantics, dropping duplicates.
> 3. Correspond to `SELECT` keyword.
> 4. Example: `SELECT name FROM R` becomes $\pi_{name}(R)$


## Selection$(\sigma)$
> [!def]
> ![](Relational_Algebra.assets/image-20240209082726699.png)![](Relational_Algebra.assets/image-20240209082744664.png)
> **Summary:**
> 1. Select a subset of rows(horizontal).
> 2. Use set semantics, dropping duplicates.
> 3. Correspond to `WHERE` keyword.
> 4. Example: `SELECT * FROM R WHERE id = 100` becomes $\sigma_{id=100}(R)$
> 5. Multiple Condition Example: `SELECT * FROM R WHERE id = 100 and state = 'NJ'` becomes $\sigma_{id=100\lor state='NJ'}(R)$


## Renaming$(\rho)$
> [!def]
> ![](Relational_Algebra.assets/image-20240209084804648.png)![](Relational_Algebra.assets/image-20240209084848082.png)
> **Summary:**
> 1. Rename columns in a relation.
> 2. Correspond to `AS` keyword.
> 
> **Remaing with Join:**
> ![](Relational_Algebra.assets/image-20240209085051357.png)






# Binary Operators
## Union($\cup$)

> [!def]
> ![](Relational_Algebra.assets/image-20240209083726350.png)![](Relational_Algebra.assets/image-20240209084146861.png)![](Relational_Algebra.assets/image-20240209083721081.png)
> **Summary:**
> 1. Union two relations, which must be compatible(same sequence of attributes and types thereof, i.e. perfectly aligned)
> 2. Use **set semantics**. So union doesn't always produce more rows after the operations since it may drop duplicates.
> 3. Correspond to `UNION` keyword.
> 4. Example: $\pi_{col}(R1)\cup\pi_{col}(R2)$ union the rows from two tables.



## Set-Difference($-$)
> [!def]
> ![](Relational_Algebra.assets/image-20240209084242574.png)![](Relational_Algebra.assets/image-20240209084248280.png)
> **Summary:**
> 1. Compute set difference of two relations, which must be compatible(same sequence of attributes and types thereof, i.e. perfectly aligned)
> 2. Use **set semantics**. Always produce less rows than the first operator after the operations since first it compute difference then it may drop duplicates.
> 3. Correspond to `EXCEPT` keyword.
> 4. Example: $\pi_{col}(R1)-\pi_{col}(R2)$ union the rows from two tables.





## Cross-Product($\times$)
> [!def]
> ![](Relational_Algebra.assets/image-20240209084455491.png)
> **Summary:**
> 1. Compute row cartesian product of two relations.
> 2. Use **set semantics**. Since the inputs are relations, they cannot have any duplicates.
> 3. Correspond to `,` keyword.
> 4. Example: $R1\times R2$ union the rows from two tables.





# Compound Operators
> [!important]
> These are shortcut operations, exist because they are very frequently used and can be implemented using unary and binary operators.

## Join($\bowtie$)
> [!def]
> ![](Relational_Algebra.assets/image-20240209085824482.png)
> **Takeaways:**
> 1. Equality Join only have equality join conditions across relations.
> 2. Theta Join can specify inequality join conditions across relations.



### Theta Join
> [!def]
> ![](Relational_Algebra.assets/image-20240209085927343.png)![](Relational_Algebra.assets/image-20240209085938986.png)![](Relational_Algebra.assets/image-20240209085945699.png)![](Relational_Algebra.assets/image-20240209085958105.png)



### Natural Join
> [!def]
> ![](Relational_Algebra.assets/image-20240209090003872.png)![](Relational_Algebra.assets/image-20240209090011519.png)![](Relational_Algebra.assets/image-20240209090025789.png)




### Other Joins
> [!def]
> ![](Relational_Algebra.assets/image-20240209090035700.png)



## Intersection$(\cap)$
> [!def]
> ![](Relational_Algebra.assets/image-20240209085558211.png)![](Relational_Algebra.assets/image-20240209085604608.png)
> Must be compatible.
> 
> It can be realized using binary and unary operators. For example, using **set difference**.
> 
> ![](Relational_Algebra.assets/image-20240209085625045.png)




# Expressions
## Expression Tree
> [!def]
> ![](Relational_Algebra.assets/image-20240209090506136.png)![](Relational_Algebra.assets/image-20240209090511559.png)



## Rewriting Queries
> [!def]
> ![](Relational_Algebra.assets/image-20240209090934021.png)


### Push Down
> [!def]
> ![](Relational_Algebra.assets/image-20240209091012235.png)

> [!example] Fa23 Disc04 P2
> 

### Eliminate Nesting
> [!def]
> ![](Relational_Algebra.assets/image-20240209091037283.png)![](Relational_Algebra.assets/image-20240209091044386.png)
> Here we also use push down of predicate.
> 
> There is a typo, the algebra should be $\pi_{sid}S-\pi_{sid}((\sigma_{bid=103}(R)\bowtie S))$.
> 
> This is **NOT** ok $\pi_{sid}(S-\sigma_{bid=103}(R)\bowtie S)$ since set difference should be defined on perfectly aligned relation columns.
> 



# Extended Operators
> [!def]
> ![](Relational_Algebra.assets/image-20240209091054571.png)



# Convert SQL to Relational Algebra
> [!example] Fa20 Disc02 P2
> ![](Relational_Algebra.assets/image-20240209170500038.png)



# Appendix
## Latex Shorcuts
> [!concept]
> ![](Relational_Algebra.assets/image-20240209091616464.png)



