 # Transactions
## Dangerous Operations on DB
> [!motiv] Motivation
> Many users can make requests to a database at a time which can cause concurrency issues. What happens when one user writes and then another user reads from the same resource? 
> 
> What if both users try to write to the same resource? There are several problems we can run into when several users are using the database at the same time if we’re not careful:
> ![](1_Transactions_Concurrency.assets/image-20240304133420825.png)
> **Note:**
> 1. **Inconsistent Reads** means we have two transactions A and B, B reads from the database while A is still updating(transaction A not finished yet).
> 2. **Lost Update** is like two transactions first read the same value from database at the same time, then one of the update overwrite the other's.
> 3. **Dirty Read** means even if I read the updated value from the database(different from inconsistent read), the update is then rolled back due to internal errors.


### Inconsistent Reads
> [!example]
> ![](1_Transactions_Concurrency.assets/image-20240304135011697.png)
> Now suppose the user 2 read from product again he would get a different result, so different reads give different results, which is an instance of inconsistent read.



### Lost Updates
> [!example]
> ![](1_Transactions_Concurrency.assets/image-20240304135244164.png)
> The right logic should be user 1 made his change, and based on user1's change, user 2 made his change. 
> 
> But in the above scheme, user 1 and user 2 are making their changes independently.




### Dirty Reads
> [!example]
> ![](1_Transactions_Concurrency.assets/image-20240304135355344.png)
> User 2 reads an invalid number(updated failure) from the data base.




## Transaction Definition
> [!def]
> ![](1_Transactions_Concurrency.assets/image-20240304135614299.png)
> Can be understood as a bunch of CPU instructions that has its logic flow. 
> 
> But the execution flow of these instructions depends on the scheduling of processes by CPU.
> ![](1_Transactions_Concurrency.assets/image-20240304135746214.png)![](1_Transactions_Concurrency.assets/image-20240304135916922.png)




## ACID Properties
> [!property]
> ![](1_Transactions_Concurrency.assets/image-20240304133445214.png)


### Isolation
> [!def]
> ![](1_Transactions_Concurrency.assets/image-20240304140123436.png)![](1_Transactions_Concurrency.assets/image-20240304140050934.png)
> In short, isolation preserves the logic flow of each transaction despite the interleaving essense of their execution flow.





### Atomicity and Durability
> [!def]
> ![](1_Transactions_Concurrency.assets/image-20240304140502435.png)![](1_Transactions_Concurrency.assets/image-20240304140556328.png)
> This means that if after committing the current transaction but before writing the update to the disk, the DBMS should do a sanity check(keep a log of actions) to see if there is any failure in the current commission. 
> - If there is, then DBMS should roll back to the most recently committed consistent state.
> - If no, just proceed and do nothing more and user can rest assured that the content in DB is consistent and most updated.




### Consistency
> [!def]
> ![](1_Transactions_Concurrency.assets/image-20240304144031976.png)
> It means when user try to insert some records that don't satisfy the schema, the trasaction will be inconsistent and thus aborted by DBMS.
> 
> ![](1_Transactions_Concurrency.assets/image-20240514161459182.png)











# Serializability
## Why Concurrency?
> [!concept]
> Multiple queries are allowed to run concurrently in the system. Advantages are twofold:
> - **Throughput** (queries per second): Increase processor/disk utilization
> 	- Single core: one query can use the CPU while another is reading to/writing from the disk
> 	- Multicore: ideally, scale throughput in the number of processors
> - **Latency** (response time per query start request):
> 	- Lower latency means we can initiate a query as fast as possible as long as there is resources instead of waiting for previous queries to finish.
> 	- Multiple queries can run at the same time rather than waiting for earlier ones to finish
> 	- So one query’s latency need not be dependent on another unrelated one’s
> 	- Lightweight queries are not bottlenecked on more time-consuming ones to finish


## Transaction Schedules
> [!def]
> ![](1_Transactions_Concurrency.assets/image-20240304144613881.png)



## Serializability
### Definition
> [!def]
> ![](1_Transactions_Concurrency.assets/image-20240304144732723.png)




### Serializability
> [!def]
> ![](1_Transactions_Concurrency.assets/image-20240304144833285.png)



## Conflict Serialiability
### Conflict Operations
> [!def]
> ![](1_Transactions_Concurrency.assets/image-20240304145315837.png)
> Conflict Equivalence Test不放过一个坏人但是会冤枉一些好人.
> 
> More conservative, like strengthened induction.


### Conflict Serializable Schedules
> [!def]
> ![](1_Transactions_Concurrency.assets/image-20240304145421088.png)

> [!example] Conflict Serializable -> Seralizable
> ![](1_Transactions_Concurrency.assets/image-20240304145841731.png)
> We could first swap W(A) with R(B) and W(B), then swap R(A) with R(B) and W(B).
> 
> All of the swaps are non-conflicting since they are operating on different relations.

> [!example] Non Conflict-Serializable 
> ![](1_Transactions_Concurrency.assets/image-20240304150056869.png)



## Conflict Dependency Graph
### Theorem
> [!thm] 
> ![](1_Transactions_Concurrency.assets/image-20240304150450484.png)
> (=>) Acyclic makes sure that for any operations $O_i$ in $T_i$, all the conflicting operations $O_j$ in $T_j$ appears after $O_i$ and so that there are no more conflicting operations before $O_i$, which means we can swap $O_i$ backward, making it conflict equivalent and thus serial equivalent.
> 
> (<=) But if it is not acyclic, then $O_i$ get stuck when trying to swap backward, making it not conflict equivalent to a serial schedule, only conflict equivalent to some other non-serial schedules.
> 
> **In other words, a serial schedule is a topological ordering of the dependency graph of any of its conflict-serializable schedules.**
> 


### Examples
> [!example] Conflict Serializable
> ![](1_Transactions_Concurrency.assets/image-20240304151209688.png)

> [!example] Non-conflict Serializable
> ![](1_Transactions_Concurrency.assets/image-20240304151232523.png)



## View Serializability
### Definition
> [!def]
> ![](1_Transactions_Concurrency.assets/image-20240309131838931.png)![](1_Transactions_Concurrency.assets/image-20240309132252685.png)




### Dependency Graph
> [!def]
> View Serializability is a looser condition than conflict serializability. **If the dependency graph contains cycles, then it is certainly not conflict serializable, but may still be view serializable.**
> ![](1_Transactions_Concurrency.assets/image-20240309132208219.png)![](1_Transactions_Concurrency.assets/image-20240309132234622.png)

> [!quiz] 
> ![](1_Transactions_Concurrency.assets/image-20240309140137980.png)






### Summary
> [!summary]
> ![](1_Transactions_Concurrency.assets/image-20240304152315589.png)![](1_Transactions_Concurrency.assets/image-20240304152337320.png)


## Summary
> [!summary]
> ![](1_Transactions_Concurrency.assets/image-20240308115045475.png)




# Locking Mechanism
## Use locks to change CG
> [!motiv] Motivations
> ![](1_Transactions_Concurrency.assets/image-20240308115150518.png)
> We have seen some non conflict serializable schedules, but using locks we can change the direction of the edges in our conflict dependency graph to make it a DAG.
> 
> But note, simply using lock won't be a panacea, as we will see in the following examples:

> [!example] Success
>  ![](1_Transactions_Concurrency.assets/image-20240308114102121.png)
>  In this example, think of $L_i(T)$ as a function call that will block if the lock on $T$ is not yet released.
>  
>  Without locking, the dependency graph looks like the following, we see that it is cyclic:
>  
>  ![](1_Transactions_Concurrency.assets/image-20240308114333829.png)
>  But with locking, we effectively make `WRITE(B)` in `T1` to appear before `READ(B)` in `T2`, making the dependency graph look like the following:
>  
>  ![](1_Transactions_Concurrency.assets/image-20240308114445488.png)
>  This is an example of successfully serialize a non-conflict serializable schedule with lock mechanism.

> [!bug] Failed Attempt
> ![](1_Transactions_Concurrency.assets/image-20240308114541104.png)![](1_Transactions_Concurrency.assets/image-20240308114610925.png)
> This failed attempt shows that simply using lock won't save our lives, and we have to enforce some rules when using locking to ensure conflict serializability.


## Lock Types
> [!important]
> ![](1_Transactions_Concurrency.assets/image-20240308115225029.png)


## Lock Management
### Hash Table Implementation
> [!def]
> ![](1_Transactions_Concurrency.assets/image-20240308194146556.png)![](1_Transactions_Concurrency.assets/image-20240308194449824.png)



### W.O. Queue Skipping
> [!important]
> ![](1_Transactions_Concurrency.assets/image-20240308194534122.png)




### W Queue Skipping
> [!important]
> ![](1_Transactions_Concurrency.assets/image-20240308194543852.png)



## 2PL Rules 
### Definition
> [!def]
> Two phase locking (2PL) is a scheme that **ensures the database uses conflict serializable schedules.** The two rules for 2PL are:
> - Transactions must obtain a S (shared) lock before reading, and an X (exclusive) lock before writing.
> - Transactions cannot get new locks after releasing any locks – this is the key to enforcing serializability through locking!
> - In every transaction, all lock actions precede all unlock actions.
> 
> ![](1_Transactions_Concurrency.assets/image-20240308115916704.png)
> 
> Phase 1 here means if a transaction involves reading or writing data from some table T, then it should acquire all the locks before the first operation on this table.
> 
> Phase 2 means that after the last operation on each table has finished execution, we should release the lock on that table before commit. As is shown in the 2PL Abortion example.
> 
> 
> ![](1_Transactions_Concurrency.assets/image-20240308120013463.png)![](1_Transactions_Concurrency.assets/image-20240308120022546.png)
> Note that the two phases are partitioned by time(splitted at `T`), which means lock manager may move `LOCK` operation ahead of time to make sure **all `LOCK` operations happen before `T` and all `UNLOCK` operations happen after `T` <font color="#ff0000">in the same transaction</font>** As the following 2PL example shows:

> [!example]
> ![](1_Transactions_Concurrency.assets/image-20240308120126539.png)
> 





### 2PL ensures Conflict Serializability
> [!important]
> **Theorem: 2PL ensures conflict serializability.**
> 
> To prove this theorem, we have to use the facts:
> 1. Across different transactions, In terms of time, all successful unlocking operations happen before successful locking operations.
> 2. In the same transaction, In terms of time, due to the properties of 2PL, locking events always happen before unlocking events.
> 

> [!proof] Proof Sketch
> ![](1_Transactions_Concurrency.assets/image-20240308163830403.png)
> We only explain the first two lines, since the rest are the same:
> 
> 1. $U_{1}(A)\to L_{2}(A)$: Since in terms of time, for different transactions `T1` and `T2`, since there is a forward edge from `T1` to `T2` on `A`, then there has to be an unlocking event on `A` of `T1` happening before a locking event on `A` of `T2`. Since we can only grab the key after the lock is released.
> 2. $L_{2}(A)\to U_{2}(B)$: Since in the same transaction, all the locking events happens after unlocking events, so this is trivially true.
> 
> By going through the dependence graph, we notice that $U_{1}(A)\to U_{1}(A)$, which is a self-contradiction.

> [!important]
> - If we have a 2PL schedule, it is certainly conflict-serializability.
> - Equivalently, if a schedule is not conflict-serializable, then it is not in 2PL.
> 
> But the converse is not true in general. Every conflict-serializable schedule may or may not be in 2PL.



### Dirty Reads Problem
> [!bug] Cascading Aborts
> ![](1_Transactions_Concurrency.assets/image-20240308120205242.png)![](1_Transactions_Concurrency.assets/image-20240308120154308.png)![](1_Transactions_Concurrency.assets/image-20240308120818826.png)![](1_Transactions_Concurrency.assets/image-20240308120835496.png)
> What this example shows is an example of dirty reads from T2 on T1. Since T2 already read the updated value from A, but since A aborts and has to roll back all the updates. But B got the updated value, so in order for B not to leak that value, we have to abort B in a cascading way.


### DeadLock Problems
> [!important]
> See [Deadlocks](1_Transactions_Concurrency.md#Deadlocks)


## Strict 2PL Rules
### Definition
> [!def]
> ![](1_Transactions_Concurrency.assets/image-20240308171025226.png)![](1_Transactions_Concurrency.assets/image-20240308171039470.png)


### DeadLock Problems
> [!important]
> See [Deadlocks](1_Transactions_Concurrency.md#Deadlocks)




## Comparison
> [!important]
> ![](1_Transactions_Concurrency.assets/image-20240308184754744.png)![](1_Transactions_Concurrency.assets/image-20240308184805033.png)![](1_Transactions_Concurrency.assets/image-20240308184940314.png)![](1_Transactions_Concurrency.assets/image-20240308184948330.png)

> [!example] UCB_CS186 Fa20 Disc08 P3
> ![](1_Transactions_Concurrency.assets/image-20240309151550213.png)




# Deadlocks
## Definition
> [!def]
> ![](1_Transactions_Concurrency.assets/image-20240308194928315.png)![](1_Transactions_Concurrency.assets/image-20240308194919563.png)

> [!quiz]
>  ![](1_Transactions_Concurrency.assets/image-20240309140236892.png)
>  Here in strict 2PL, we are sure not to have unrepeatable reads(inconsistent read) since it is designed to rule out the possibility of cascading aborts, but we can still have deadlock problem.



## Deadlock Detection
### Method: Wait-for Graph
> [!def]
> ![](1_Transactions_Concurrency.assets/image-20240308195126653.png)![](1_Transactions_Concurrency.assets/image-20240308195156331.png)

  
### Proof of Correctness
> [!proof] Proof of Correctness
> ![](1_Transactions_Concurrency.assets/image-20240308213914268.png)![](1_Transactions_Concurrency.assets/image-20240308213920719.png)






## Deadlock Avoidance
> [!def]
>  ![](1_Transactions_Concurrency.assets/image-20240308195549380.png)![](1_Transactions_Concurrency.assets/image-20240308195801712.png)







# Lock Granularity
## Definition
> [!def]
> ![](1_Transactions_Concurrency.assets/image-20240308205631016.png)



## Database Lock Hierarchy
> [!def]
> ![](1_Transactions_Concurrency.assets/image-20240308210357186.png)


## Lock Modes Compatibility
> [!def]
> ![](1_Transactions_Concurrency.assets/image-20240308213139063.png)![](1_Transactions_Concurrency.assets/image-20240308210421046.png)![](1_Transactions_Concurrency.assets/image-20240308210431784.png)![](1_Transactions_Concurrency.assets/image-20240308210439416.png)
> **Just remember the following:**
> 1. Each entry in the compatibility matrix indicates whether two locks can be applied at same level.
> 2. If we request a lock at some level, we automatically assume that we lock all the subsequent lower levels. For example, if we use S lock at table level, then it automatically lock all the tuples with S lock.
> 
> ![](1_Transactions_Concurrency.assets/28c3273c639335179d2477e2a708416d_MD5.jpeg)![](1_Transactions_Concurrency.assets/e3030b8f5681913739a97cf064ea7f5a_MD5.jpeg)








## Multi-Granularity Locking Protocol
> [!def]
> ![](1_Transactions_Concurrency.assets/image-20240308211900217.png)![](1_Transactions_Concurrency.assets/image-20240308211424570.png)![](1_Transactions_Concurrency.assets/image-20240308211436681.png)

> [!example] Example 1
> ![](1_Transactions_Concurrency.assets/image-20240308213407000.png)![](1_Transactions_Concurrency.assets/image-20240308213415390.png)


> [!example] Example 2
> ![](1_Transactions_Concurrency.assets/image-20240308213502464.png)![](1_Transactions_Concurrency.assets/image-20240308213539992.png)![](1_Transactions_Concurrency.assets/image-20240308213620729.png)![](1_Transactions_Concurrency.assets/image-20240308213631207.png)



## Lock Table
> [!example]
> ![](1_Transactions_Concurrency.assets/image-20240308213758435.png)![](1_Transactions_Concurrency.assets/image-20240308213805348.png)



## Practice Exercises
### Exercise 1
> [!example] CMU15445 HW4
> ![](1_Transactions_Concurrency.assets/image-20240309150706463.png)![](1_Transactions_Concurrency.assets/image-20240309150714338.png)![](1_Transactions_Concurrency.assets/image-20240309150721364.png)![](1_Transactions_Concurrency.assets/image-20240309150729110.png)![](1_Transactions_Concurrency.assets/image-20240309150737584.png)![](1_Transactions_Concurrency.assets/image-20240309150743640.png)



### Exercise 2
> [!example] EECS186 Fa20 Disc08 P4
> ![](1_Transactions_Concurrency.assets/image-20240402085405809.png)












# Phantom Problem
## Problem Definition
> [!def]
> ![](1_Transactions_Concurrency.assets/image-20240308220716407.png)

> [!example]
> ![](1_Transactions_Concurrency.assets/image-20240308220659147.png)![](1_Transactions_Concurrency.assets/image-20240308220704462.png)


## Dealing With Phantoms
> [!def]
> ![](1_Transactions_Concurrency.assets/image-20240308220750730.png)




## Dynamic Database
> [!important]
> ![](1_Transactions_Concurrency.assets/image-20240308220909410.png)![](1_Transactions_Concurrency.assets/image-20240308220919915.png)




