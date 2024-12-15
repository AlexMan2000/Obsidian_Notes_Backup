# Crash Classification






# Buffer Pool Management Policies
## Force/No Force
> [!def]
> - **Force**: Make sure all the modifications are flushed to disk before COMMIT.
> 	- Ensure durability. If the machine crashes after COMMIT, the bits in the memory are "erased", so flushing to disk before COMMIT make sures all updates are reflected in disk and no data loss happened.
> 	- Performance is bad, have to do lots of writes I/O.
> - **No Force**: Don't have to flush all modifications to disk before COMMIT.
> 	- Allow some modifications to be flushed to disk after COMMIT.
> 	- Doesn't guarantee durability due to data loss.
> 
> ![](1_Recovery.assets/image-20240314123452467.png)


## Steal/No Steal
> [!def]
> - **Steal**: Can one transaction write uncommitted changes belonging to a different transaction to disk? Yes, we can.
> 	- Doesn't guarantee atomicity. Create intermediate states.
> - **No Steal**: No, we don't allow.
> 	- Ensure atomicity, no intermediate states.
> 	- Bad performance, we may have to wait until there are free pages to evict. We may have to keep every modified page in memory until a transaction completes. Page eviction operation is exclusive to one transaction at a time.
> 
> ![](1_Recovery.assets/image-20240314123441160.png)


## Summary
> [!summary]
> ![](1_Recovery.assets/image-20240314123553062.png)




# Shadow Paging
> [!overview]
> Use the `NO-STEAL` + `FORCE` policy.

## No Steal + Force Example
> [!def]
> ![](1_Recovery.assets/image-20240314124947410.png)![](1_Recovery.assets/image-20240314124952697.png)

> [!example]
> ![](1_Recovery.assets/image-20240314124402963.png)![](1_Recovery.assets/image-20240314124409350.png)![](1_Recovery.assets/image-20240314124414791.png)![](1_Recovery.assets/image-20240314124421189.png)![](1_Recovery.assets/image-20240314124431023.png)![](1_Recovery.assets/image-20240314124438648.png)![](1_Recovery.assets/image-20240314124459430.png)




## Shadow Paging Example
> [!def]
> ![](1_Recovery.assets/image-20240314124902074.png)



# Undo/Redo Logging
## Undo Logging
### Components
> [!def]
> ![](1_Recovery.assets/image-20240314130445362.png)![](1_Recovery.assets/image-20240314130152995.png)![](1_Recovery.assets/image-20240314130409594.png)


### Walkthrough
> [!example] EECS186 Fa20 Disc09 P1
> ![](1_Recovery.assets/image-20240402093127779.png)![](1_Recovery.assets/image-20240402093144169.png)
> If system crashes while we are undoing, we simply redo all the undos again since we have no idea what has been undone before this crash, so it's better to redo all the undos.




### Recovery
> [!example]
> ![](1_Recovery.assets/image-20240314130420573.png)




## Redo Logging
### Components
> [!def]
> ![](1_Recovery.assets/image-20240314130504798.png)![](1_Recovery.assets/image-20240314130610775.png)![](1_Recovery.assets/image-20240314130644337.png)![](1_Recovery.assets/image-20240314130720673.png)

 

### Walkthrough
> [!example] EECS186 Fa20 Disc09 P2
> ![](1_Recovery.assets/image-20240402094259771.png)![](1_Recovery.assets/image-20240402094314002.png)






## Comparisons
> [!important]
> ![](1_Recovery.assets/image-20240314130736044.png)![](1_Recovery.assets/image-20240314130744159.png)



# Write Ahead Logging
## WAL Protocols
> [!def]
> Having undo logging and redo logging alone is not enough to ensure atomicity and durability.
> - Undo logging only guarantees durability(due to force) but no guarantees on atomicity(due to steal).
> - Redo logging only guarantees atmociticy(due to no-steal) but no gurantees on durability(do to no-force).
> 
> In short, we want to achieve atomicity and durablity for the log records, just like regular data pages.
> 
> So we need a protocol for the undo/redo logging as follows:
> ![](1_Recovery.assets/image-20240314150213919.png)![](1_Recovery.assets/image-20240314150546582.png)




## WAL Implementations
### Update Log Record
> [!def]
> ![](1_Recovery.assets/image-20240314155609429.png)
> - Each log has a an `LSN` , which serves as unique identifer of the log record and it's automatically increasing on each newly created log record.
> 	- This will be flushed to disk since log is flushed to disk.
> 	- Need for tracing.
> - Each log also has an `prevLSN` to help track the log record chain during recovery process.
> 	- Same as above.
> - `flushedLSN` keeps track of the `LSN` of the **last** log record that's flushed to the disk. This helps to spot the last operation before the log and mark the start of undo process or the end of the redo process. 
> - We will store `flushedLSN` at disk, naming it as `masterRecord`.
> 
> ![](1_Recovery.assets/image-20240314155831163.png)


### Compensation Log Record
> [!def]
> ![](1_Recovery.assets/image-20240314162432287.png)



### Page
> [!def]
> Each page in the memory has a `pageLSN`, which stores the `LSN` of the operation that last modified the page.
> - `pageLSN <= flushedLSN` for all pages. This comes from our first rule for WAL(atomicity) - we must flush the corresponding log records before we can flush the data page to disk. A data page is only flushed to disk if the LSN of the last operation to modify it is less than or equal to the flushedLSN. In other words, before page i can be flushed to disk, the log records for all operations that have modified page i must have been flushed to disk.
> - `pageLSN` is stored in buffer pool, and will be flushed to disk. 


### Dirty Page Table - DPT
> [!def]
> ![](1_Recovery.assets/image-20240314151117809.png)
> **Note:**
> - `recLSN` as part of the page, will be together flushed to the disk.
> - Any time when a page is loaded into the memory by the buffer pool manager, the `recLSN` value will be set to `null` in the `DPT`, and will then be set to the `LSN` of the first operation that modified this page.





### Transaction Table - Xact Table
> [!def]
> The transaction table stores information on the active transactions. The transaction table has three fields:
> ![](1_Recovery.assets/image-20240314152134334.png)![](1_Recovery.assets/image-20240314152139125.png)
> **Note on some inequalities:**
> 
> ![](1_Recovery.assets/image-20240314152237266.png)![](1_Recovery.assets/image-20240314152319983.png)



### Summary
> [!summary]
> ![](1_Recovery.assets/image-20240314154309682.png)



## WAL Example
> [!example]
> ![](1_Recovery.assets/image-20240314155730401.png)![](1_Recovery.assets/image-20240314155749230.png)![](1_Recovery.assets/image-20240314155811566.png)![](1_Recovery.assets/image-20240314155907841.png)![](1_Recovery.assets/image-20240314155952678.png)



## Group Commiting Optimization
> [!important]
> ![](1_Recovery.assets/image-20240314160204898.png)



## Logging Scheme
> [!def]
> ![](1_Recovery.assets/image-20240314160333362.png)![](1_Recovery.assets/image-20240314160340679.png)

> [!important] Comparisons
> ![](1_Recovery.assets/image-20240314160423245.png)



# ARIES Recovery Algorithm
> [!overview]
> ![](1_Recovery.assets/image-20240314152522791.png)



## ARIES Normal Operations
### Assumptions
> [!def]
> ![](1_Recovery.assets/image-20240314161712136.png)




### Transaction Starts
> [!def]
> ![](1_Recovery.assets/image-20240314161227099.png)




### Transaction Updates
> [!def]
> ![](1_Recovery.assets/image-20240314161253287.png)


### Page Flushes
> [!def]
> ![](1_Recovery.assets/image-20240314161328839.png)
> After page flush:
> 
> ![](1_Recovery.assets/image-20240314161358041.png)


### Page Fetches
> [!def]
> ![](1_Recovery.assets/image-20240314161434340.png)


### Transaction Commits
> [!def]
> ![](1_Recovery.assets/image-20240314161743831.png)![](1_Recovery.assets/image-20240314161524635.png)![](1_Recovery.assets/image-20240314161533647.png)


### Transaction Aborts
> [!def]
> ![](1_Recovery.assets/image-20240314162534037.png)![](1_Recovery.assets/image-20240314162102156.png)






## Checkpointing
### Motivations
> [!bug] Problem with Undo/Redo
> ![](1_Recovery.assets/image-20240314152416667.png)
> The main problem with **a WAL-based DBMS is that the log file will grow forever.** 
> 
> After a crash, the DBMS has to replay the entire log, which can take a long time if the log file is large. 
> 
> Thus, the DBMS can periodically take a checkpoint where it flushes all buffers out to disk. 
> 
> How often the DBMS should take a checkpoint depends on the application’s performance and downtime requirements. 
> 
> Taking a checkpoint too often causes the DBMS’s runtime performance to degrade. But waiting a long time between checkpoints can potentially be just as bad, as the system’s recovery time after a restart increases.



### Non-Fuzzy Checkpointing
> [!def]
> ![](1_Recovery.assets/image-20240314152926147.png)![](1_Recovery.assets/image-20240314152941442.png)


### Fuzzy Checkpointing
> [!def]
> ![](1_Recovery.assets/image-20240314154017188.png)![](1_Recovery.assets/image-20240314160807829.png)

> [!example] Protocol and Example
> - Any txn that begins but not end before `CKPT` is included in the ATT and DPT. But the ATT and DPT that's actually written to the `END CKPT` log can be any state between `BEGIN CKPT` and `END CKPT`. 
> 	- In this example, `END CKPT1` only write the `C->P22` to the DPT
> 	- The latest one before `END CKPT 1`, which is `A->P11`, is not written to DPT.
> - Any txn that begins and ends before `CKPT` is excluded from the ATT and DPT.
> - Any txn that begins after the `CKPT` is excluded from the ATT and DPT.
> 
> ![](1_Recovery.assets/image-20240314163121992.png)
> **In this example:**
> - `T1` ends before `CKPT1`, so it is not included in ATT and DPT.
> - `T2` begins before `CKPT1` but not ends before `CKPT`, so all of its modifications are reflected in ATT and DPT.
> - `T3` begins after `CKPT1`, so it is not included in ATT and DPT.

 

## Algorithm Procedures
> [!overview]
> ![](1_Recovery.assets/image-20240314162704454.png)![](1_Recovery.assets/image-20240314162751323.png)![](1_Recovery.assets/image-20240314162801046.png)



### Analysis Phase
> [!important]
> ![](1_Recovery.assets/image-20240402104821681.png)![](1_Recovery.assets/image-20240402104844053.png)![](1_Recovery.assets/image-20240314165856204.png)![](1_Recovery.assets/image-20240314165816175.png)
> We start out traversing of logs from the last `BEGIN CKPT`. Since the tables written to the log can be the state of tables at any point between the `BEGIN CKPT` and `END CKPT`. 
> 
> This means we need to start at the `BEGIN CKPT` because we’re not sure if the records after it are actually reflected in the tables that were written to the log.
> 

> [!example] Example from Notes
> ![](1_Recovery.assets/image-20240314170432797.png)![](1_Recovery.assets/image-20240314170441493.png)![](1_Recovery.assets/image-20240314170448896.png)![](1_Recovery.assets/image-20240314170455540.png)![](1_Recovery.assets/image-20240314172540240.png)

> [!example] Example from Fa20 Disc09 P3
> See [CS 186 Discussion 9](CS%20186%20Discussion%209.pdf)
> ![](1_Recovery.assets/image-20240402105229583.png)![](1_Recovery.assets/image-20240402105240098.png)







### Redo Phase
> [!important]
> ![](1_Recovery.assets/image-20240314170522176.png)![](1_Recovery.assets/image-20240314170549157.png)![](1_Recovery.assets/image-20240314170703114.png)

> [!example]
> ![](1_Recovery.assets/image-20240314170722444.png)![](1_Recovery.assets/image-20240314171638105.png)![](1_Recovery.assets/image-20240314171642897.png)
> 

> [!bug] Caveats
> ![](1_Recovery.assets/image-20240314172137338.png)



### Undo Phase
> [!overview] Overview
> ![](1_Recovery.assets/image-20240314171727612.png)

> [!def]
> ![](1_Recovery.assets/image-20240314171838257.png)![](1_Recovery.assets/image-20240314171736993.png)

> [!example]
> ![](1_Recovery.assets/image-20240314171851033.png)![](1_Recovery.assets/image-20240314171905711.png)![](1_Recovery.assets/image-20240314171910798.png)

> [!bug] Caveats
> ![](1_Recovery.assets/image-20240314171939574.png)
> Otherwise, we would be undoing the undone, which is equivalent to do something that we don't want.


### Undo Implementations
> [!algo]
> ![](1_Recovery.assets/image-20240314172213824.png)![](1_Recovery.assets/image-20240314172220085.png)![](1_Recovery.assets/image-20240314172225640.png)



## Caveats
> [!bug] Caveats
> ![](1_Recovery.assets/image-20240314172046032.png)



# Appendix
> [!def]
> ![](1_Recovery.assets/image-20240314172238034.png)

