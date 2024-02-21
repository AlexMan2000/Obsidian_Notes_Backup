# Relational Operators
## Query Plans
> [!def]
> ![](2_Iterators&Joins.assets/image-20240220093034358.png)![](2_Iterators&Joins.assets/image-20240220093048649.png)
> Basically parent relational operator will call child relational operator and execute them and then collect results from the child operators' results.



## Iterator Interface
> [!def]
> ![](2_Iterators&Joins.assets/image-20240220092851531.png)
> **In other words:**
> - Streaming operator will return a result from its requestee immediately after it receives that result.
> - Blocking operator will not return the results until the requestee has returned all the results. Like a greedy collector.




# Iteration Algorithms
## Select Operator
> [!example] Streaming Operator
> ![](2_Iterators&Joins.assets/image-20240220093725921.png)



## Heap Scan Operator
> [!example] Streaming Operator
> ![](2_Iterators&Joins.assets/image-20240220094913167.png)




## Sort Operator
> [!example] Blocking Operator
> ![](2_Iterators&Joins.assets/image-20240220094957252.png)


## Group By Operator
> [!example] Blocking Operator
> ![](2_Iterators&Joins.assets/image-20240220100535013.png)![](2_Iterators&Joins.assets/image-20240220100543001.png)



## Single-Threaded Summary
> [!summary]
> ![](2_Iterators&Joins.assets/image-20240220103203082.png)




# Loop-based Join Algorithms
## Schema&Costing 
> [!def]
> ![](2_Iterators&Joins.assets/image-20240220103434028.png)


## Simple Theta Join
### Simple Nested Loops Theta Join
> [!def]
> ![](2_Iterators&Joins.assets/image-20240220104035399.png)


### Changing Join Order
> [!def]
> ![](2_Iterators&Joins.assets/image-20240220104147463.png)


## Page Nested Loop Join
> [!def]
> ![](2_Iterators&Joins.assets/image-20240220104606589.png)



## Chunk Nested Loop Join
> [!def]
> ![](2_Iterators&Joins.assets/image-20240220104628252.png)
> **Note:** B-2 = Buffer page size - input frame for S - buffer frame for output


## Index Nested Loops Join
> [!def]
> ![](2_Iterators&Joins.assets/image-20240220104647536.png)![](2_Iterators&Joins.assets/image-20240220104653362.png)
> For unclustered index, since the pointer to RID is in random manner, in order to find all the matching records we have to traverse multiple pages while for clustered index, the record is clustered so we expect less page I/Os to happen.



# Sort-Merge Join Algorithms
## Algorithm Procedures
> [!algo]
> ![](2_Iterators&Joins.assets/image-20240220131556432.png)![](2_Iterators&Joins.assets/image-20240220132045580.png)
> **Note** that the reason why we have to go back to mark(S) is that in sql join we want all the tuples that satisfies the $r_i=s_j$ to be in the result set. In other words, sort-merge join treats records from $R$ and $S$ as different(so we have to include matching records from $S$ multiple times by moving back to mark(S) first) while merge sort treat records from $R$ and $S$ as the same.
> 
> ![](2_Iterators&Joins.assets/image-20240220134050800.png)
> The worst case could be that we are joining a table with itself, and the joining key of this table contains only one value. In this case we are just doing a cross product.
> 
> Note that the final expression for the I/O cost is computed using the formula:
> ![](2_Iterators&Joins.assets/image-20240220135653879.png)


> [!example]
> ![](2_Iterators&Joins.assets/image-20240220133358784.png)![](2_Iterators&Joins.assets/image-20240220133406700.png)![](2_Iterators&Joins.assets/image-20240220133415612.png)



## Comparisons
### Join First, Sort Later - NLJ + SMJ
> [!algo]
> ![](2_Iterators&Joins.assets/image-20240220135932083.png)![](2_Iterators&Joins.assets/image-20240220135946019.png)






### Sort First, Join Later - SMJ
> [!important]
> ![](2_Iterators&Joins.assets/image-20240220140059867.png)





## Refinements
> [!concept]
> In SMJ, we have two phases, we first sort $R$ and $S$ independently, then merge them using the algorithm.
> 
> But we could improve the runtime performance by doing the merging across $R$ and $S$ while sorting. In other words, each sorted run now contains both records from $R$ and $S$.
> ![](2_Iterators&Joins.assets/image-20240220140206901.png)




# Hash Join Algorithms
## Naive Hash Join
> [!def]
> ![](2_Iterators&Joins.assets/image-20240220142036296.png)![](2_Iterators&Joins.assets/image-20240220142057644.png)![](2_Iterators&Joins.assets/image-20240220142133852.png)

> [!bug] Caveats
> ![](2_Iterators&Joins.assets/image-20240220142114842.png)


## Grace Hash Join
### Motivation
> [!property]
> ![](2_Iterators&Joins.assets/image-20240220163720478.png)
> The idea behind grace hash join is the property above where we can divide the hash join algorithm into smaller subproblems without losing integrity and correctness.



### Algorithm Procedures
> [!algo]
> ![](2_Iterators&Joins.assets/image-20240220155842988.png)![](2_Iterators&Joins.assets/image-20240220155820010.png)

> [!def] Sketch
> ![](2_Iterators&Joins.assets/image-20240220160758589.png)![](2_Iterators&Joins.assets/image-20240220161140234.png)![](2_Iterators&Joins.assets/image-20240220160808985.png)


### Example
> [!example]
> See [11-iterators-joins-2](11-iterators-joins-2.pdf)
> ![](2_Iterators&Joins.assets/image-20240220163046433.png)
> Note that the only requirement of this method is that the partition of the smaller relation should fit into the B-2 buffers.
> 
> If in some table for some attribute(like gender), we cannot partition it into small partitions that fit into the B-2 buffers, then we cannot use this method at all, there is no way to build in-memory hashtable.


### Cost of Grace Hash Join
> [!code] Runtime Analysis
> ![](2_Iterators&Joins.assets/image-20240220163204185.png)![](2_Iterators&Joins.assets/image-20240220163854837.png)![](2_Iterators&Joins.assets/image-20240220163903834.png)


# Summary
> [!concept]
> ![](2_Iterators&Joins.assets/image-20240220164336256.png)![](2_Iterators&Joins.assets/image-20240220164416876.png)














