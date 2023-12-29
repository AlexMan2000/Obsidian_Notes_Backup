  # Basic Definitions
## Directedness
> [!def]
> ![](Directed%20Graph.assets/image-20231211230846730.png)


## Directed Degrees
> [!def]
> ![](Directed%20Graph.assets/image-20231211230920807.png)![](Directed%20Graph.assets/image-20231211230928606.png)


## Directed Walks&Paths&Cycles
> [!def]
> ![](Directed%20Graph.assets/image-20231211231013289.png)![](Directed%20Graph.assets/image-20231211231026741.png)

> [!example]
> ![](Directed%20Graph.assets/image-20231211231159827.png)![](Directed%20Graph.assets/image-20231211231207246.png)



## Hamiltonian/Eulerian
> [!def]
> ![](Directed%20Graph.assets/image-20231211231242698.png)![](Directed%20Graph.assets/image-20231211231251673.png)



## Adjacency Matrix
> [!def]
> ![](Directed%20Graph.assets/image-20231211231310949.png)




# Reachablility
## Definition
> [!def]
> ![](Directed%20Graph.assets/image-20231211230740126.png)


## Properties
> [!property] 
> ![](Directed%20Graph.assets/image-20231211230804116.png)

> [!proof]
> 




# Strong Connectivity
> [!def]
> ![](Directed%20Graph.assets/image-20231212201611591.png)

> [!thm]
> ![](Directed%20Graph.assets/image-20231212201659614.png)

> [!proof]
> 




## Strongly Connected Graph
> [!def]
> ![](Directed%20Graph.assets/image-20231212201741480.png)

> [!important] Negation on the defintion
> A directed graph $G=(V,E)$ is not strongly connected if there exists some $u,v\in V$ such that either there is no path from u to v or there is no path from v to u.

> [!example]
> ![](Directed%20Graph.assets/image-20231212201824810.png)


## Strongly Connected Components
> [!def]
> ![](Directed%20Graph.assets/image-20231212201939426.png)![](Directed%20Graph.assets/image-20231212202335200.png)![](Directed%20Graph.assets/image-20231212202346566.png)



## SCC are not mutually reachable
> [!important]
> Two disjoint SCCs can't be mutually reachable from one another





# Directed Acyclic Graphs(DAGs)
## Topological Orderings
> [!def]
> ![](Directed%20Graph.assets/image-20231212203100980.png)![](Directed%20Graph.assets/image-20231212203413917.png)![](Directed%20Graph.assets/image-20231212203425416.png)
> Note that topological ordering is for all the nodes. In other words, it must be a sequence of nodes that covers all the nodes in the graph.


## Definition of DAG
> [!def]
> ![](Directed%20Graph.assets/image-20231212203640400.png)![](Directed%20Graph.assets/image-20231212203835935.png)![](Directed%20Graph.assets/image-20231212203859225.png)



## Has Topological Ordering -> DAG
> [!thm]
> ![](Directed%20Graph.assets/image-20231212204250316.png)

> [!proof] Proof Sketch
> ![](Directed%20Graph.assets/image-20231212204336177.png)

> [!proof] Formal Proof
> ![](Directed%20Graph.assets/image-20231212204345916.png)

> [!proof] Proof Techniques
> ![](Directed%20Graph.assets/image-20231213094015586.png)![](Directed%20Graph.assets/image-20231213094030793.png)


## Properties of DAGs
### Sources and Sinks
> [!important] Topological Sorting Order Picking Process
> ![](Directed%20Graph.assets/image-20231213103911019.png)![](Directed%20Graph.assets/image-20231213103919925.png)![](Directed%20Graph.assets/image-20231213104035155.png)


### DAG -> At least one source
> [!property]
> ![](Directed%20Graph.assets/image-20231213104157016.png)

> [!proof] Proof Sketch
> ![](Directed%20Graph.assets/image-20231213104918591.png)

> [!proof] Formal Proof
> ![](Directed%20Graph.assets/image-20231213104950022.png)

> [!summary] Intuition of the Lemma
> ![](Directed%20Graph.assets/image-20231213105116110.png)



### DAG -> Removing Source Preserves DAG
> [!property]
> ![](Directed%20Graph.assets/image-20231213105131877.png)

> [!proof] Formal Proof
> ![](Directed%20Graph.assets/image-20231213105144975.png)


## DAG -> Topological Ordering
> [!thm]
> ![](Directed%20Graph.assets/image-20231213105345027.png)



# Condensations of Digraphs
## Definition
> [!def]
> ![](Directed%20Graph.assets/image-20231213110605064.png)

> [!example] Example Condensation
> ![](Directed%20Graph.assets/image-20231213110635052.png)![](Directed%20Graph.assets/image-20231213110640354.png)![](Directed%20Graph.assets/image-20231213110653430.png)


## Condensation is a DAG
> [!thm]
> ![](Directed%20Graph.assets/image-20231213110732872.png)

> [!proof] Proof Sketch
> ![](Directed%20Graph.assets/image-20231221074948213.png)![](Directed%20Graph.assets/image-20231221074955815.png)

> [!proof] Formal Proof
> ![](Directed%20Graph.assets/image-20231221075034981.png)![](Directed%20Graph.assets/image-20231221075040780.png)
> **Proof of the main theorem:**
> 
> ![](Directed%20Graph.assets/image-20231221075533522.png)


# Tournament Graphs
## Round-Robin Tournament
> [!def]
> ![](Directed%20Graph.assets/image-20231224172153272.png)![](Directed%20Graph.assets/image-20231224172157630.png)
> The definition of the tournament graph goes like the following:
> For every pair of nodes $u$ and $v$, either $u\rightarrow v$ or $u\leftarrow v$.






## Finding Hamiltonian Path in a Tournament Graph
> [!thm]
> **Recall:** Hamiltonian Path is a path that traverses each node exactly once.
> ![](Directed%20Graph.assets/image-20231224172225289.png)

> [!proof]
> ![](Directed%20Graph.assets/image-20231224172235585.png)![](Directed%20Graph.assets/image-20231224172241653.png)![](Directed%20Graph.assets/image-20231224172246705.png)


## King Chicken Theorem
> [!motiv] Motivation
> ![](Directed%20Graph.assets/image-20231225124418634.png)![](Directed%20Graph.assets/image-20231225124427567.png)


## Theorem - Largest Outdegree <=> King
> [!thm]
> ![](Directed%20Graph.assets/image-20231225125034564.png)

> [!proof]
> ![](Directed%20Graph.assets/image-20231225125159562.png)![](Directed%20Graph.assets/image-20231225125207712.png)












# Communication Networks

