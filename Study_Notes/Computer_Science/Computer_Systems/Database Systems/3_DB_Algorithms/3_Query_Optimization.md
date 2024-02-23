# Query Lifecycle
> [!overview] 
> ![](3_Query_Optimization.assets/image-20240220165006458.png)![](3_Query_Optimization.assets/image-20240220165423283.png)![](3_Query_Optimization.assets/image-20240220165430708.png)![](3_Query_Optimization.assets/image-20240220165436910.png)



# Query Parsing
> [!overview] 
> ![](3_Query_Optimization.assets/image-20240220165019453.png)








# Query Rewriting
> [!overview]
> ![](3_Query_Optimization.assets/image-20240220165035567.png)


## Relational Algebra Equivalences
> [!def]
> ![](3_Query_Optimization.assets/image-20240220165626360.png)
> Join is communicative but not necessarily associative:
> 
> ![](3_Query_Optimization.assets/image-20240220194452351.png)


## Join Ordering
> [!important] 
> ![](3_Query_Optimization.assets/image-20240220200145058.png)![](3_Query_Optimization.assets/image-20240220201811691.png)




## Rewriting Selection
> [!example]
> ![](3_Query_Optimization.assets/image-20240220201008551.png)


## Rewriting Projections
> [!example]
> ![](3_Query_Optimization.assets/image-20240220201044286.png)



## Integrated Example
> [!example]
> ![](3_Query_Optimization.assets/image-20240220202602771.png)


### Naive Plan
> [!example] Plan 1
> ![](3_Query_Optimization.assets/image-20240220203253097.png)![](3_Query_Optimization.assets/image-20240220203259526.png)![](3_Query_Optimization.assets/image-20240220203345549.png)


### Selection Pushdown
> [!example] Plan 2
> ![](3_Query_Optimization.assets/image-20240220203427059.png)![](3_Query_Optimization.assets/image-20240220203812602.png)

> [!example] Plan 3
> ![](3_Query_Optimization.assets/image-20240220203532456.png)
> Here if we are using NLJ(nested loop join), we could scan less pages such that total I/Os would be $500+250\times (\leq 1000)$.



### Join Ordering
> [!example] Plan 4
> ![](3_Query_Optimization.assets/image-20240220205127263.png)![](3_Query_Optimization.assets/image-20240220205436330.png)

### Materialization for Selection On-the-fly
> [!example] Plan 5
> ![](3_Query_Optimization.assets/image-20240220205549364.png)![](3_Query_Optimization.assets/image-20240220205556876.png)![](3_Query_Optimization.assets/image-20240220205759845.png)



### Mat + Join Ordering
> [!example]
> ![](3_Query_Optimization.assets/image-20240220205934146.png)![](3_Query_Optimization.assets/image-20240220205944777.png)


### Sort-Merge Join Algorithms
> [!example] Plan 7
> ![](3_Query_Optimization.assets/image-20240220210226163.png)![](3_Query_Optimization.assets/image-20240220210255325.png)![](3_Query_Optimization.assets/image-20240220210904654.png)



### Mat + Block Nested Loop
> [!example]
> ![](3_Query_Optimization.assets/image-20240220211253900.png)![](3_Query_Optimization.assets/image-20240220211301106.png)


### Projection Cascade&Pushdown
> [!example]
> ![](3_Query_Optimization.assets/image-20240220211625302.png)![](3_Query_Optimization.assets/image-20240220211630378.png)



### Index Nest Loop
> [!example]
> ![](3_Query_Optimization.assets/image-20240220212033312.png)![](3_Query_Optimization.assets/image-20240220212038928.png)![](3_Query_Optimization.assets/image-20240220212044643.png)




### Summary
> [!summary]
> ![](3_Query_Optimization.assets/image-20240220212730595.png)![](3_Query_Optimization.assets/image-20240220212735513.png)










# Query Optimizations
## System R Optimizer Framework
> [!overview]
> ![](3_Query_Optimization.assets/image-20240220165047890.png)
> In System R:
> 1. The **query parser** first checks for correctness and authorization (user permissions to access the table). It then generates a parse tree out of the query. This step is usually fairly straightforward, since it’s just breaking up the query into chunks that our programming language can understand, without having to make any decisions.
> 2. Next, the **query rewriter** converts queries into even smaller query blocks (like a single WHERE clause), and flattens the views.
> 3. Once the query is rewritten, it gets passed into the **query optimizer**. The primary goal of a query optimizer is to translate a simple query plan into a better query plan. A cost-based query optimizer processes one query block at a time (e.g. select, project, join, group by, order by)


## Components of Query Optimizer
### Query Plan Space
> [!def]
> ![](3_Query_Optimization.assets/image-20240221143557154.png)





### Query Blocks
> [!def]
> ![](3_Query_Optimization.assets/image-20240221143653178.png)![](3_Query_Optimization.assets/image-20240221143704192.png)
> Left-deep tree ensures that we will always have tuples from the right hand side of the operator.

### Cost Estimation
> [!def]
> ![](3_Query_Optimization.assets/image-20240221155811414.png)





 
## Selectivity Estimation wit Formulas
> [!overview]
> Since the number of rows in our output depends heavily on the data and what selections we make out of it, we need a way to estimate the size of outputs after each operation. This is known as **selectivity estimation.**
> 
> Like evaluating query cost, selectivity estimation is very rough and generally prioritizes speed over accuracy- so much so that **if we don’t have enough information, we just assign an operation the arbitrary selectivity value of** 1/101/101/10 (meaning that the the output has 1/10 of the number of rows as the input).


### Common Formulas
> [!thm]
> ![](3_Query_Optimization.assets/image-20240221155946642.png)![](3_Query_Optimization.assets/image-20240221155955116.png)![](3_Query_Optimization.assets/image-20240221160006045.png)![](3_Query_Optimization.assets/image-20240221160015601.png)![](3_Query_Optimization.assets/image-20240221160022854.png)



### Join Selectvity
> [!def]
> ![](3_Query_Optimization.assets/image-20240221154341381.png)![](3_Query_Optimization.assets/image-20240221154409153.png)




### Result Size Estimation
> [!def]
> ![](3_Query_Optimization.assets/image-20240221154845620.png)


### Practice Examples
> [!example] Fa20 Disc07 P1
> 




## Selectivity Estimation with Statistics
### Assumptions
> [!important]
> ![](3_Query_Optimization.assets/image-20240221155053638.png)





### Selectivity of Conjunction
> [!def]
> ![](3_Query_Optimization.assets/image-20240221155006199.png)


### Selectivity of Disjunction
> [!def]
> ![](3_Query_Optimization.assets/image-20240221155025306.png)




### Column Equality
> [!def]
> ![](3_Query_Optimization.assets/image-20240221154444226.png)![](3_Query_Optimization.assets/image-20240221154424777.png)
> The reason why we divide by n is that we want to normalize it to a probability distribution. Here height(binp(40)) is the number of samples within the bin that contains 40, n is the total number of samples. So `height(binp(40)) / n` is the probability that a sample belongs to the bin that contains 40.




## Cost Estimation
> [!overview]
> ![](3_Query_Optimization.assets/image-20240221161234420.png)

> [!def]
> ![](3_Query_Optimization.assets/image-20240221161240752.png)

> [!example]
> ![](3_Query_Optimization.assets/image-20240221161250473.png)




## Search Algorithms
### System R Heuristics
> [!def]
> ![](3_Query_Optimization.assets/image-20240221161551051.png)![](3_Query_Optimization.assets/image-20240221161558692.png)


### Join: Enumeration of Left-Deep Plans
> [!def]
> ![](3_Query_Optimization.assets/image-20240221161509682.png)




