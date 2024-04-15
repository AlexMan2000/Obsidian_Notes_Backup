# Parallel Architectures
> [!def]
> ![](Parallel_Query_Processing.assets/image-20240414151343896.png)![](Parallel_Query_Processing.assets/image-20240414151351861.png)


# Types of Parallelism
## Intra-Query Parallelism
> [!def]
> Intra-query parallelism attempts to make one query run as fast as possible by spreading the work over multiple computers.
> 
> Within intra-query parallelism, we have two subcategories:
> - **Intra-operator parallelism:** Intra-operator parallelism is dividing up the data onto several machines and having them sort the data in parallel. This parallelism makes sorting (**one operation**) as fast as possible.
> - **Inter-operator parallelism:** Inter-operator parallelism involves executing multiple independent operations in parallel. This form of parallelism operates between different operators or functions in a process or query. This is useful in processes where several operations are independent and can be executed simultaneously without waiting for the results of others.
> - Within inter-operator parallism, we have two subtypes:
> 	- Pipeline Parallelism
> 	- Bushy Tree Parallelism


### Inter-Operator Parallelism
> [!overview]
> ![](Parallel_Query_Processing.assets/image-20240414153946240.png)



#### Pipeline Parallelism
> [!def]
> The first type is pipeline parallelism. In pipeline parallelism records are passed to the parent operator as soon as they are done. The parent operator can work on a record that its child has already processed while the child operator is working on a different record.
> ![](Parallel_Query_Processing.assets/image-20240414154008987.png)
> In pipeline parallelism the project and filter can run at the same time because as soon as filter finishes a record, project can operate on it while filter picks up a new record to operate on.



#### Bushy Tree Parallelism
> [!def]
> The other type of inter-operator parallelism is bushy tree parallelism in which different branches of the tree are run in parallel.
> ![](Parallel_Query_Processing.assets/image-20240414154051977.png)
> One machine can work on sorting R and another machine can sort S at the same time.






### Intra-Operator Parallelism
See [Data Partitioning](Parallel_Query_Processing.md#Data%20Partioning)





## Inter-Query Parallelism
> [!def]
> Inter-query parallelism gives each machine different queries to work on so that the system can achieve a high throughput and complete as many queries as possible.




# Data Partitioning
## Sharding, Replication, Partitioning
> [!def]
> **Data Sharding:** Sharding typically involves dividing data horizontally, where each shard holds a subset of the rows from the entire dataset but maintains the same schema. This is also known as "data sharding."
> 
> **Data Replication:** Copying data from one database to one or more other databases. It is primarily used to improve the availability and fault tolerance of a system, ensuring that data remains accessible even in the case of a server failure or during maintenance activities.
> 
> **Data Partitioning:** To decide what machines get what data we will use a partitioning scheme. A partitioning scheme is a rule that determines what machine a certain record will end up on. The three we will study are range partitioning, hash partitioning, and round-robin.


## Range Partitioning
> [!def]
> ![](Parallel_Query_Processing.assets/image-20240414155519767.png)


## Hash Partitioning
> [!def]
> ![](Parallel_Query_Processing.assets/image-20240414155526464.png)



## Round Robin Partitioning
> [!def]
> ![](Parallel_Query_Processing.assets/image-20240414155608765.png)![](Parallel_Query_Processing.assets/image-20240414155614148.png)



## Comparisons
> [!important]
> ![](Parallel_Query_Processing.assets/image-20240414161047008.png)
> Here balance load means the amount of task that is distributed to the particular machine. Because round robin partitioning basically use a modulus operation on each row of data to decide where it should reside. As a result, each machine has roughly the same amount of data.
> - Shared nothing particularly benefits from "good" partitioning
> 	- Reduces network traffic
> 	- Better if operations are “localized” to certain nodes
> - Indexes can be built at each partition
> 	- E.g., a B+tree at each node


### Look Up Operation
> [!def]
> ![](Parallel_Query_Processing.assets/image-20240414164436227.png)
> To look up for a particular key, range/hash partitioning works better since we know the key will reside in just one machine. The function that maps the key to partitioning should be one-to-one, each key gets mapped to exactly one partitioning.
> 
> In contrast, round-robin will distribute the key among multiple machines.






### Insert Operation
> [!def]
> ![](Parallel_Query_Processing.assets/image-20240414164918441.png)![](Parallel_Query_Processing.assets/image-20240414164941262.png)![](Parallel_Query_Processing.assets/image-20240414164952980.png)




### Scans
> [!def]
> ![](Parallel_Query_Processing.assets/image-20240414165239898.png)




# Parallelized Algorithms
## Parallel Sorting
> [!important]
> ![](Parallel_Query_Processing.assets/image-20240414190858363.png)![](Parallel_Query_Processing.assets/image-20240414192638032.png)![](Parallel_Query_Processing.assets/image-20240414192649978.png)![](Parallel_Query_Processing.assets/image-20240414193121253.png)![](Parallel_Query_Processing.assets/image-20240414193127811.png)




## Parallel Hashing
> [!important]
> ![](Parallel_Query_Processing.assets/image-20240414190723953.png)![](Parallel_Query_Processing.assets/image-20240414190732200.png)![](Parallel_Query_Processing.assets/image-20240414190749214.png)![](Parallel_Query_Processing.assets/image-20240414190759998.png)
> Have to want for all machines to finish phase 1 in order for data to be synced before we move onto the phase 2.




## Parallel Sort Merge Join
> [!important]
> ![](Parallel_Query_Processing.assets/image-20240414191008699.png)![](Parallel_Query_Processing.assets/image-20240414193159759.png)![](Parallel_Query_Processing.assets/image-20240414193210133.png)![](Parallel_Query_Processing.assets/image-20240414193220215.png)![](Parallel_Query_Processing.assets/image-20240414195123446.png)






## Parallel Naive Hash Join
> [!important]
> ![](Parallel_Query_Processing.assets/image-20240414192020958.png)






## Parallel Grace Hash Join
> [!important]
> ![](Parallel_Query_Processing.assets/image-20240414191020435.png)![](Parallel_Query_Processing.assets/image-20240414191025188.png)



## Broadcast Join
> [!important]
> ![](Parallel_Query_Processing.assets/image-20240414194053491.png)![](Parallel_Query_Processing.assets/image-20240414194935526.png)
> Since R is small enough to fit into the memory, we can simply just send the copy of $R$ to every machine instead of partitioning them.
> - Then we don't need to worry about data skew and histogram.




## Symmetric Hash Join
> [!important]
> ![](Parallel_Query_Processing.assets/image-20240414194059448.png)![](Parallel_Query_Processing.assets/image-20240414194110456.png)



# Parallel Aggregation
## Hierarchical Aggregation
> [!important]
> ![](Parallel_Query_Processing.assets/image-20240414194225975.png)



## Parallel GroupBy
> [!important]
> ![](Parallel_Query_Processing.assets/image-20240414194303543.png)![](Parallel_Query_Processing.assets/image-20240414194327429.png)






