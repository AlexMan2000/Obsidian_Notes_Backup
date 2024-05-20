# ER_Models
## Entity
> [!def]
> ![](DB_Design.assets/image-20240411220205643.png)


## Relationship
> [!def]
> ![](DB_Design.assets/image-20240411220214802.png)




## Relational Constraints
> [!def]
> ![](DB_Design.assets/image-20240411220804579.png)![](DB_Design.assets/image-20240411221944776.png)![](DB_Design.assets/image-20240411221950790.png)![](DB_Design.assets/image-20240411221957191.png)![](DB_Design.assets/image-20240411222127055.png)![](DB_Design.assets/image-20240411222137314.png)![](DB_Design.assets/image-20240411222145552.png)





## Weak Entity
> [!def]
> ![](DB_Design.assets/image-20240411222200698.png)![](DB_Design.assets/image-20240411222207723.png)



## Exercises
> [!example] CS186 Fa20 Disc10 P1
> ![](DB_Design.assets/image-20240411223036515.png)
> **Note:**
> 1. When we say relation A needs relation B, we mean that each entry in relation A should relate to at least one entry in B, which is a participation constraint.
> 2. "Exactly One" means key constraint with total participation.
> 3. When we say that relation A is uniquely identified by relation B, we mean that each entry in A should correspond to exactly one entry in relation B.




# Functional Dependencies
## Basic Definition
> [!motiv]
> - In some data sets, if you already know a set of columns, you can use that information to infer the other columns.
> - Example: imagine that you have birthday and age columns in a table. Birthday uniquely determines age.
> - These relationships are called functional dependencies. We want to use them to eliminate redundancy.

> [!def]
> A functional dependency X → Y means that the X column determines Y column in a table R. This means given any two tuples in table R, if their X values are the same, then their Y values must be the same (but not vice versa).
> ![](DB_Design.assets/image-20240411223905230.png)![](DB_Design.assets/image-20240411224311655.png)![](DB_Design.assets/image-20240411224323095.png)
> If t and t' doesn't agree at A, then t and t' can agree/or not at B, and this FD holds. 

> [!example]
> ![](DB_Design.assets/image-20240411224438352.png)![](DB_Design.assets/image-20240411224617385.png)

> [!example] CS186 Fa20 Disc10 P3.1~ P3.2
> ![](DB_Design.assets/image-20240412111451814.png)


## Anomalies
> [!def]
> ![](DB_Design.assets/image-20240412103216342.png)![](DB_Design.assets/image-20240412103224915.png)




## Terminologies
> [!important]
> ![](DB_Design.assets/image-20240411224758856.png)



## Inference Rules
> [!def]
> ![](DB_Design.assets/image-20240411224823452.png)![](DB_Design.assets/image-20240411225029536.png)

> [!example]
> Consider the set $F=\{A\to B, AB\to AC, BC\to BD, DA\to C\}$ of functional dependencies, compute:
> 1. $A+$: By reflexivity, we have $A\to A$. By union we know $A\to AB$. By transitivity we know $A\to AB\to AC$, which implies $A\to C$ by decomposition. By $A\to B$ and $A\to C$ we have $A\to BC$, which implies $A\to BD$ and $A\to D$. Thus $A+=\{A,B,C,D\}$.
> 2. $B+,C+,D+$: $B,C,D$ only determine themselves, which means $B+=\{B\}$, $C+=\{C\}$ and $D+=\{D\}$.
> 3. $AB+,AC+,AD+$: Since $A+=\{A,B,C,D\}$, we have that the closure of all these set of attributes are $\{A,B,C,D\}$.
> 4. $BC+$: $\{B,C,D\}$, since $BC\to B, BC\to C, BC\to BD\to D$.
> 5. $BD+$: $\{B,D\}$ since there is no clue for $BD\to C$.
> 6. $CD+$: $\{C,D\}$.
> 7. $BCD+$: $\{B,C,D\}$.



## Closure
> [!def]
> There are two kinds of closure:
> - FD Closure, which turns out to be a set of FDs.
> - Attribute Closure, which turns out to be a set of attributes.
> 
> ![](DB_Design.assets/image-20240412103550864.png)![](DB_Design.assets/image-20240412103556503.png)![](DB_Design.assets/image-20240412104124307.png)

> [!algo]
> ![](DB_Design.assets/image-20240412104129719.png)








## Super/Candidate Key
> [!def]
> ![](DB_Design.assets/image-20240411224051651.png)![](DB_Design.assets/image-20240412104247108.png)![](DB_Design.assets/image-20240412104520779.png)

> [!example]
> ![](DB_Design.assets/image-20240412105135065.png)

> [!example] CS186 Fa20 Disc10 P3.4
> Consider the set $F=\{A\to B, AB\to AC, BC\to BD, DA\to C\}$ of functional dependencies, compute:
> ![](DB_Design.assets/image-20240412113406711.png)



  


# Normal Form
## Boyce-Codd Normal Form
> [!def]
> ![](DB_Design.assets/image-20240412113504407.png)![](DB_Design.assets/image-20240412115218739.png)



## Decomposition Algorithm
> [!def]
> ![](DB_Design.assets/image-20240412115434285.png)

> [!example] CS186 Fa20 Disc10 P3
> ![](DB_Design.assets/image-20240412122000560.png)





## Reversibility
> [!def]
> ![](DB_Design.assets/image-20240412121000680.png)

> [!example]
> ![](DB_Design.assets/image-20240412121017343.png)




## Dependency Preserving Decompositions
> [!important]
> ![](DB_Design.assets/image-20240412121042546.png)



## Properties of BCNF
> [!property]
> ![](DB_Design.assets/image-20240412122058336.png)




# Other Normal Form
## 3rd NF







