# Tuples
> [!def]
> ![](Relations_Partial_Orders.assets/image-20231222091414314.png)![](Relations_Partial_Orders.assets/image-20231222091441822.png)


# Cartesian Products
## Two Sets
> [!def]
> ![](Relations_Partial_Orders.assets/image-20231222091501865.png)
> Side Notes about empty sets:
> 
> ![](Relations_Partial_Orders.assets/image-20231222091542080.png)


## Formal Definition of N-Tuples
> [!def]
> ![](Relations_Partial_Orders.assets/image-20231222091728781.png)![](Relations_Partial_Orders.assets/image-20231222092207288.png)



## Cartesian Powers
> [!def] Cartesian Square
> ![](Relations_Partial_Orders.assets/image-20231222092255502.png)![](Relations_Partial_Orders.assets/image-20231222092435742.png)



# Some Types of Relations
## Reflex Relations
> [!def]
> ![](Relations_Partial_Orders.assets/image-20231223115614112.png)



## Irreflexive Relations
> [!def]
> ![](Relations_Partial_Orders.assets/image-20231223115846571.png)![](Relations_Partial_Orders.assets/image-20231223115852315.png)![](Relations_Partial_Orders.assets/image-20231223120342651.png)
> A critical detail here is that reflexive and irreflexive are not opposites of one another. 
> 
> There may still exist some relations that are neither reflexive nor irreflexive, where some objects are related to itself while others are not.


## Transitive Relations
> [!def]
> ![](Relations_Partial_Orders.assets/image-20231223121449018.png)


## Symmetric Relations
> [!def]
> ![](Relations_Partial_Orders.assets/image-20231223121702848.png)


## Asymmetric Relations
> [!def]
> ![](Relations_Partial_Orders.assets/image-20231223121716344.png)




# Binary Relations and Graphs
## Reflexive Relations <=> Self Loop
> [!example]
> ![](Relations_Partial_Orders.assets/image-20231223122617227.png)
> The graph represents a reflexive relation over the nodes.


## Not Reflexive Relations <=> At least one no self-loop
> [!example]
> ![](Relations_Partial_Orders.assets/image-20231223122703552.png)



## Irreflexive Relations <=> All nodes no self-loop
> [!example]
> ![](Relations_Partial_Orders.assets/image-20231223122738825.png)![](Relations_Partial_Orders.assets/image-20231223122742933.png)


## Transitivity <=> Short-Cut
> [!example]
> ![](Relations_Partial_Orders.assets/image-20231223122831401.png)![](Relations_Partial_Orders.assets/image-20231223123034910.png)



## Symmetry <=> Strongly Connected
> [!def]
> ![](Relations_Partial_Orders.assets/image-20231223123503009.png)![](Relations_Partial_Orders.assets/image-20231223123523677.png)



# Equivalence Relations
## Definition
> [!def]
> ![](Relations_Partial_Orders.assets/image-20231223124231249.png)




## Partitions of Sets
> [!def]
> ![](Relations_Partial_Orders.assets/image-20231224100045727.png)![](Relations_Partial_Orders.assets/image-20231224100103121.png)
> **Notes about empty set:**
> 
> ![](Relations_Partial_Orders.assets/image-20231224100253223.png)

> [!proof] Each Element can only belong to exactly one set
> ![](Relations_Partial_Orders.assets/image-20231224101008994.png)



## Sets that contain the element
> [!def]
> ![](Relations_Partial_Orders.assets/image-20231224101110551.png)





## Equivalence Relation over Sets
> [!def]
> ![](Relations_Partial_Orders.assets/image-20231224101209422.png)

> [!proof] Proof for equivalence relations - Proof Sketch
> ![](Relations_Partial_Orders.assets/image-20231224101323875.png)![](Relations_Partial_Orders.assets/image-20231224101327974.png)

> [!proof] Formal Proof
> ![](Relations_Partial_Orders.assets/image-20231224101400542.png)




## Equivalence Class of an Element
> [!def]
> ![](Relations_Partial_Orders.assets/image-20231224101728943.png)
> What this means is that when we want to construct the equivalence class of an arbitrary element $x$, we just have to look for all the elements that has the equivalence relation with $x$ and collect all these elements in a set.



# Turn Equivalent Relations into Partitions
> [!motiv] Motivation
> ![](Relations_Partial_Orders.assets/image-20231224103513053.png)![](Relations_Partial_Orders.assets/image-20231224103548513.png)


## Prove that equivalent class forms a partition
> [!def] Rigorous Definition of Union
> ![](Relations_Partial_Orders.assets/image-20231224103723499.png)

> [!lemma] Union of Equivalant Classes is the Original Set
> 
> ![](Relations_Partial_Orders.assets/image-20231224103752389.png)

> [!lemma] Equivalent Classes of Equivalent Relations are non-empty
> ![](Relations_Partial_Orders.assets/image-20231224120127158.png)

> [!lemma] Equivalent Classes are Disjoint
> ![](Relations_Partial_Orders.assets/image-20231224120621127.png)![](Relations_Partial_Orders.assets/image-20231224120634079.png)![](Relations_Partial_Orders.assets/image-20231224120754872.png)

> [!thm] Main Theorem
> ![](Relations_Partial_Orders.assets/image-20231224121156595.png)![](Relations_Partial_Orders.assets/image-20231224121253811.png)![](Relations_Partial_Orders.assets/image-20231224121327953.png)


## Equivalence Classes and Graph Connectivity
> [!important]
> ![](Relations_Partial_Orders.assets/image-20231224171315958.png)



# Order Relations
## Strict Order Relations
> [!def]
> ![](Relations_Partial_Orders.assets/image-20231226203404541.png)
> A quick example of strict order relation $R$ is $<$, which is clearly irreflexive, asymetric and transitive. First, for any 2-tuple over $\mathbb{R}$, we don't have $(x,x)$ that satisfies $x<x$. Morevoer, for any $(x,y)$ that satisfies $x<y$, $y\not<x$. Finally, for any $xRy$ and $yRz$, we have $x<y<z$ and $xRz$.
> 
> A quick counter-example of strict order is $\subseteq$ since it is clearly not irreflexive.



## Proper Subset
> [!thm]
> ![](Relations_Partial_Orders.assets/image-20231226204348920.png)


## Trichotomous Relations
> [!important]
> ![](Relations_Partial_Orders.assets/image-20231226205440645.png)

> [!example] Graph Examples
> ![](Relations_Partial_Orders.assets/image-20231226205633133.png)![](Relations_Partial_Orders.assets/image-20231226205703449.png)



## Strict Total Order
> [!def]
> ![](Relations_Partial_Orders.assets/image-20231226205802859.png)



# Partial Orders
