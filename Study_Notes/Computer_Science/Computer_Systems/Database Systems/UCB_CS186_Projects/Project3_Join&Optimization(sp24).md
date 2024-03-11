
# Sort and Join Algorithms

## Task 1: Nested Loop Joins

### SNLJ
> [!algo]
> See [SNLJ](../3_DB_Algorithms/2_Iterators&Joins.md#SNLJ)
> ![](2_Iterators&Joins.assets/image-20240220104035399.png)

> [!code]
> ![](Project3_Join&Optimization(sp24).assets/image-20240308224202089.png)
> See https://github.com/AlexMan2000/UCB_CS186/blob/master/sp24/projs-raw-sp24/sp24-rookiedb-main/sp24-rookiedb-main/src/main/java/edu/berkeley/cs186/database/query/join/SNLJOperator.java

> [!tip]
> ![](Project3_Join&Optimization(sp24).assets/SNLJ.gif)


### PNLJ
> [!code]
> ![](2_Iterators&Joins.assets/image-20240220104606589.png)![](Project3_Join&Optimization(sp24).assets/image-20240308224217929.png)

> [!tip]
> ![](Project3_Join&Optimization(sp24).assets/PNLJ.gif)




### BNLJ
> [!def]
> ![](2_Iterators&Joins.assets/image-20240220104628252.png)
> **Note:**
> - Here we need 1 buffer page for inner relation, 1 buffer for output, B - 2 buffer for outer relation. 
> - B-2 = Buffer page size - input frame for S - buffer frame for output

> [!code]
```java
package edu.berkeley.cs186.database.query.join;  
  
import edu.berkeley.cs186.database.TransactionContext;  
import edu.berkeley.cs186.database.common.iterator.BacktrackingIterator;  
import edu.berkeley.cs186.database.query.JoinOperator;  
import edu.berkeley.cs186.database.query.QueryOperator;  
import edu.berkeley.cs186.database.table.Record;  
  
import java.util.Iterator;  
import java.util.NoSuchElementException;  
  
/**  
 * Performs an equijoin between two relations on leftColumnName and * rightColumnName respectively using the Block Nested Loop Join algorithm. */public class BNLJOperator extends JoinOperator {  
    protected int numBuffers;  
  
    public BNLJOperator(QueryOperator leftSource,  
                        QueryOperator rightSource,  
                        String leftColumnName,  
                        String rightColumnName,  
                        TransactionContext transaction) {  
        super(leftSource, materialize(rightSource, transaction),  
                leftColumnName, rightColumnName, transaction, JoinType.BNLJ  
        );  
        this.numBuffers = transaction.getWorkMemSize();  
        this.stats = this.estimateStats();  
    }  
    @Override  
    public Iterator<Record> iterator() {  
        return new BNLJIterator();  
    }  
    @Override  
    public int estimateIOCost() {  
        //This method implements the IO cost estimation of the Block Nested Loop Join  
        int usableBuffers = numBuffers - 2;  
        int numLeftPages = getLeftSource().estimateStats().getNumPages();  
        int numRightPages = getRightSource().estimateIOCost();  
        return ((int) Math.ceil((double) numLeftPages / (double) usableBuffers)) * numRightPages +  
               getLeftSource().estimateIOCost();  
    }  
    /**  
     * A record iterator that executes the logic for a simple nested loop join.     * Look over the implementation in SNLJOperator if you want to get a feel     * for the fetchNextRecord() logic.     */    private class BNLJIterator implements Iterator<Record>{  
        // Iterator over all the records of the left source  
        private Iterator<Record> leftSourceIterator;  
        // Iterator over all the records of the right source  
        private BacktrackingIterator<Record> rightSourceIterator;  
        // Iterator over records in the current block of left pages  
        private BacktrackingIterator<Record> leftBlockIterator;  
        // Iterator over records in the current right page  
        private BacktrackingIterator<Record> rightPageIterator;  
        // The current record from the left relation  
        private Record leftRecord;  
        // The next record to return  
        private Record nextRecord;  
  
        private BNLJIterator() {  
            super();  
            this.leftSourceIterator = getLeftSource().iterator();  
            this.fetchNextLeftBlock();  
  
            this.rightSourceIterator = getRightSource().backtrackingIterator();  
            this.rightSourceIterator.markNext();  
            this.fetchNextRightPage();  
  
            this.nextRecord = null;  
        }  
        /**  
         * Fetch the next block of records from the left source.         * leftBlockIterator should be set to a backtracking iterator over up to         * B-2 pages of records from the left source, and leftRecord should be         * set to the first record in this block.         *         * If there are no more records in the left source, this method should         * do nothing.         *         * You may find QueryOperator#getBlockIterator useful here.         * Make sure you pass in the correct schema to this method.         */        private void fetchNextLeftBlock() {  
            // TODO(proj3_part1): implement  
            if (!leftSourceIterator.hasNext()) return;  
            /*  
                 If leftRecordSource still has records, then do the following  
                 Call QueryOperator#getBlockIterator() to get the iterator that                 iterates through all the records within the blocks.                 - leftSourceIterator: Iterators over all records of left relations, we want to transform it into a block iterator                 - getLeftSource().getSchema() get the column configuration of left source.                 - numBuffers - 2 get the maximum pages in a block to load from the memory.             */            leftBlockIterator = getBlockIterator(leftSourceIterator, getLeftSource().getSchema(), numBuffers - 2);  
            leftBlockIterator.markNext(); // Backtracking needed  
            leftRecord = leftBlockIterator.next();  
        }  
        /**  
         * Fetch the next page of records from the right source.         * rightPageIterator should be set to a backtracking iterator over up to         * one page of records from the right source.         *         * If there are no more records in the right source, this method should         * do nothing.         *         * You may find QueryOperator#getBlockIterator useful here.         * Make sure you pass in the correct schema to this method.         */        private void fetchNextRightPage() {  
            // TODO(proj3_part1): implement  
  
            if (!rightSourceIterator.hasNext()) return;  
  
            // Create a block BacktrackingIterator with block size = 1(one page)  
            rightPageIterator = getBlockIterator(rightSourceIterator, getRightSource().getSchema(), 1);  
            rightPageIterator.markNext(); // Backtracking needed  
        }  
  
        /**  
         * Returns the next record that should be yielded from this join,         * or null if there are no more records to join.         *         * You may find JoinOperator#compare useful here. (You can call compare         * function directly from this file, since BNLJOperator is a subclass         * of JoinOperator).         */        private Record fetchNextRecord() {  
            // TODO(proj3_part1): implement  
            if (leftRecord == null) {  
                // Case 0: Fail fast, if there is no more record, do nothing  
                return null;  
            }  
            while (true) {  
                if (rightPageIterator.hasNext()) {  
                    // Case 1: Still have records in right page, we keep iterating  
                    Record rightRecord = rightPageIterator.next();  
                    // If key matches, return the concatenated record  
                    if (compare(leftRecord, rightRecord) == 0) {  
                        return leftRecord.concat(rightRecord);  
                    }                } else if (leftBlockIterator.hasNext()) {  
                    // Case 2: If we have finished the records in this page but the vertical axis  
                    // still has records, we have to rewind the horizontal axis in the page                    leftRecord = leftBlockIterator.next();  
                    rightPageIterator.reset();  
                } else if (rightSourceIterator.hasNext()){  
                    /*  
                        Case 3: Both leftblock and rightpage has consumed all the records, but the horizontal                        direction has yet end, then we have to rewind on the vertical axis but fetch the                        next page on the horizontal axis.                     */                    fetchNextRightPage();  
                    leftBlockIterator.reset();  
                    leftRecord = leftBlockIterator.next();  
                } else if (leftSourceIterator.hasNext()){  
                    /*  
                       Reached the end of the current block and horizontal axis, have to rewind on both vertical and                       horizontal axis.  
                     */                    fetchNextLeftBlock();  
                    /* Don't forget to reset here since the getBlockIterator() relies on the current  
                        position of the sourceIterator.                    */  
                    rightSourceIterator.reset();  
                    fetchNextRightPage();  
                } else {  
                    return null;  
                }            }        }  
        /**  
         * @return true if this iterator has another record to yield, otherwise  
         * false         */        @Override  
        public boolean hasNext() {  
            if (this.nextRecord == null) this.nextRecord = fetchNextRecord();  
            return this.nextRecord != null;  
        }  
        /**  
         * @return the next record from this iterator  
         * @throws NoSuchElementException if there are no more records to yield  
         */        @Override  
        public Record next() {  
            if (!this.hasNext()) throw new NoSuchElementException();  
            Record nextRecord = this.nextRecord;  
            this.nextRecord = null;  
            return nextRecord;  
        }    }}
```

> [!tip] When B=4, and block size = B -2 = 2, each block contains 2 pages
> ![](Project3_Join&Optimization(sp24).assets/BNLJ.gif)




## Task 2: Hash Joins

### SHJ
> [!concept]
> ![](Project3_Join&Optimization(sp24).assets/image-20240309202821582.png)

```java

```




### GHJ
> [!task]
> ![](Project3_Join&Optimization(sp24).assets/image-20240309203356063.png)


#### Partition
> [!task]
> Partition phase takes in left relations and right relations and partition them using the same hash function.
```java
/**  
 * For every record in the given iterator, hashes the value * at the column we're joining on and adds it to the correct partition in * partitions. * * @param partitions an array of partitions to split the records into  
 * @param records iterable of records we want to partition  
 * @param left true if records are from the left relation, otherwise false  
 * @param pass the current pass (used to pick a hash function)  
 */private void partition(Partition[] partitions, Iterable<Record> records, boolean left, int pass) {  
    // TODO(proj3_part1): implement the partitioning logic  
    // You may find the implementation in SHJOperator.java to be a good  
    // starting point. You can use the static method HashFunc.hashDataBox    // to get a hash value.    for (Record record: records) {  
        DataBox columnValue;  
        if (left) {  
            columnValue = record.getValue(getLeftColumnIndex());  
        } else {  
            columnValue = record.getValue(getRightColumnIndex());  
        }  
        // Hash the column-value(key)  
        int hashValue = HashFunc.hashDataBox(columnValue, pass);  
        int partitionNum = hashValue % partitions.length;  
        if (partitionNum < 0) {  
            partitionNum += partitions.length;  
        }  
        partitions[partitionNum].add(record);  
    }}
```



#### Build and Probe
> [!task]
> Fix the smaller partition(that can fit into the B-2 buffers) as build relation, larger partition as the probe relation. Concat the record according to the common join key.
```java
/**  
 * Runs the buildAndProbe stage on a given partition. Should add any * matching records found during the probing stage to this.joinedRecords. */private void buildAndProbe(Partition leftPartition, Partition rightPartition) {  
    // true if the probe records come from the left partition, false otherwise  
    boolean probeFirst;  
    // We'll build our in memory hash table with these records  
    Iterable<Record> buildRecords;  
    // We'll probe the table with these records  
    Iterable<Record> probeRecords;  
    // The index of the join column for the build records  
    int buildColumnIndex;  
    // The index of the join column for the probe records  
    int probeColumnIndex;  
  
    if (leftPartition.getNumPages() <= this.numBuffers - 2) {  
        buildRecords = leftPartition;  
        buildColumnIndex = getLeftColumnIndex();  
        probeRecords = rightPartition;  
        probeColumnIndex = getRightColumnIndex();  
        probeFirst = false;  
    } else if (rightPartition.getNumPages() <= this.numBuffers - 2) {  
        buildRecords = rightPartition;  
        buildColumnIndex = getRightColumnIndex();  
        probeRecords = leftPartition;  
        probeColumnIndex = getLeftColumnIndex();  
        probeFirst = true;  
    } else {  
        throw new IllegalArgumentException(  
            "Neither the left nor the right records in this partition " +  
            "fit in B-2 pages of memory."  
        );  
    }    // TODO(proj3_part1): implement the building and probing stage  
    // You shouldn't refer to any variable starting with "left" or "right"  
    // here, use the "build" and "probe" variables we set up for you.    // Check out how SHJOperator implements this function if you feel stuck.  
  
    Map<DataBox, List<Record>> hashTable = new HashMap<>();  
  
    // Stage 1: Building  
    for (Record record: buildRecords) {  
        DataBox key = record.getValue(buildColumnIndex);  
        // No such key, create a bucket  
        if (!hashTable.containsKey(key)) {  
            hashTable.put(key, new ArrayList<>());  
        }        // Has such key, add to the existing bucket  
        hashTable.get(key).add(record);  
    }  
    // Stage 2: Staging  
    for (Record probe: probeRecords) {  
        DataBox key = probe.getValue(probeColumnIndex);  
        if (hashTable.containsKey(key)) {  
            List<Record> records = hashTable.get(key);  
            for (Record build: records) {  
                Record grace;  
                // Because we join left and right, the left relation  
                // should appear first in the final record                if (probeFirst) {  
                    grace = probe.concat(build);  
                } else {  
                    grace = build.concat(probe);  
                }                this.joinedRecords.add(grace);  
            }        }    }}
```


#### Trigger Function
> [!task]
> Run the two phase of GHJ algorithm. If none of the left and right partitions is smaller enough to fit into B - 2 buffers, recursively partition on both sides until one of them can fit. Otherwise, execute build and probe immediately on the current left and right partition.
```java
/**  
 * Runs the grace hash join algorithm. Each pass starts by partitioning * leftRecords and rightRecords. If we can run build and probe on a * partition we should immediately do so, otherwise we should apply the * grace hash join algorithm recursively to break up the partitions further. */private void run(Iterable<Record> leftRecords, Iterable<Record> rightRecords, int pass) {  
    assert pass >= 1;  
    if (pass > 5) throw new IllegalStateException("Reached the max number of passes");  
  
    // Create empty partitions  
    Partition[] leftPartitions = createPartitions(true);  
    Partition[] rightPartitions = createPartitions(false);  
  
    // Partition records into left and right  
    this.partition(leftPartitions, leftRecords, true, pass);  
    this.partition(rightPartitions, rightRecords, false, pass);  
  
    for (int i = 0; i < leftPartitions.length; i++) {  
        // TODO(proj3_part1): implement the rest of grace hash join  
        // If you meet the conditions to run the build and probe you should  
        // do so immediately. Otherwise you should make a recursive call.  
        /*          Since leftPartitions and rightparitions are assumed to be of the same length          We can do the following without OUT OF BOUND exception        */        Partition leftPartition = leftPartitions[i];  
        Partition rightPartition = rightPartitions[i];  
        if (leftPartition.getNumPages() <= numBuffers - 2 || rightPartition.getNumPages() <= numBuffers - 2) {  
            buildAndProbe(leftPartition, rightPartition);  
        } else {  
            run(leftPartition, rightPartition, pass + 1);  
        }  
    }}
```



#### SHJ Fails and GHJ Succeeds
> [!task]
> We want to find an input scheme such that SHJ algorithm fails and GHJ succeeds. The key idea is that SHJ only pass once while GHJ has what we call "recursive partitioning", which makes it possible to handle larger partition by breaking it apart until our memory can hold.
```java
/**  
 * This method is called in testBreakSHJButPassGHJ. 
 * 
 * Come up with two lists of records for leftRecords and rightRecords such 
 * that SHJ will error when given those relations, but GHJ will successfully 
 * run. createRecord(int val) takes in an integer value and returns a record * with that value in the column being joined on. 
 * 
 * Hints: Both joins will have access to B=6 buffers and each page can fit 
 * exactly 8 records. 
 * 
 * @return Pair of leftRecords and rightRecords  
 */public static Pair<List<Record>, List<Record>> getBreakSHJInputs() {  
    ArrayList<Record> leftRecords = new ArrayList<>();  
    ArrayList<Record> rightRecords = new ArrayList<>();  
  
    // TODO(proj3_part1): populate leftRecords and rightRecords such that  
    // SHJ breaks when trying to join them but not GHJ  
  
    // When the left records cannot fit in B - 2 buffers, SHJ will error but SHJ will not,  
    // Any big enough number >= 136 is ok for SHJ to error and GHJ will succeed    for (int i = 0; i < 136; i++) {  
        leftRecords.add(createRecord(i));  
        rightRecords.add(createRecord(i));  
    }  
    return new Pair<>(leftRecords, rightRecords);  
}
```
``


## Task 3: External Sort
### sortRun
> [!task]
> ![](Project3_Join&Optimization(sp24).assets/image-20240309212223408.png)

```java
/**  
 * Returns a Run containing records from the input iterator in sorted order. * You're free to use an in memory sort over all the records using one of * Java's built-in sorting methods. * * @return a single sorted run containing all the records from the input  
 * iterator */public Run sortRun(Iterator<Record> records) {  
    // TODO(proj3_part1): implement  
    List<Record> runRecords = new ArrayList<>();  
    for (Record record: runRecords) {  
        runRecords.add(record);  
    }    
    /* Java built-in sort, it only works on Collection
     * However, Iterator is not a subtype of Collection, so we need
     * to transform it to a List(which is a subtype of Collection)
     */
    Collections.sort(runRecords, this.RecordComparator);  
    // Create a new run object
    Run sortedRun = new Run(transaction, this.getSchema());  
    sortedRun.addAll(runRecords);  
    return sortedRun;  
}
```


### mergeSortedRuns
> [!task]
> ![](Project3_Join&Optimization(sp24).assets/image-20240309213613995.png)
> Here to implement the merge sort, we have a very important algorithmic idea using `Priority Queue` data structure:
> 
> Suppose we want to merge sort on `List<List<T>>` where each `List<T>` is assumed to be sorted. Now a very quick algorithm is to let priority queue to decide which data should come next. The pseudocode is shown below:

```java
/*
   Perform merge sort on input
*/
public List<T> mergeSortPQ(List<List<T>> input) {

	/*
	   Step 1: Create pq and output
	*/
	PriorityQueue<Pair<T, Integer>> pq = new PriorityQueue<>(new DataComparator());
	List<T> output = new ArrayList<>();
	/*
	   Step 2: Create a list of tracker
	*/
	List<Iterator<T>> mergeTracker = new ArrayList<>();
	
	for (List<T> list: input) {
		mergeTracker.add(list.iterator());
	}
	// Initialize the priority queue
	for (int i = 0; i < mergeTracker.size(); i++){
		if (mergeTracker.get(i).hasNext()) {
			pq.add(new Pair<>(mergeTracker.get(i).next(), i));
		}
	}

	/*
	  Step 3: Merge Sorting
	*/
	while (!pq.isEmpty()) {
		Pair<T, Integer> currPair = pq.poll();
		T elem = currPair.getFirst();

	
		/*
		    Put the current elem into result list
		*/
		output.add(elem);

		/*
		   Which iterator produces this element, since we need to update its iterating cursor
		*/
		Integer elemIndex = currPair.getSecond();

		
		/*
		 Add the next elem into the pq, let pq decide the order
		*/
		if (mergeTracker.get(elemIndex).hasNext()) {
			pq.add(new Pair<>(mergeTracker.get(elemIndex).next(), elemIndex));
		}
	}
	
	return output;
}




private class DataComparator implements Comparator<T> {

	@Override
	public int compare(T t1, T t2) {
		// Your own definition of order between t1 and t2
		return ...compareTo(...);
	}
}
```

> [!code]
> Back to the question, we adopt similar ideas as follows:
```java
/**  
 * Given a list of sorted runs, returns a new run that is the result of 
 * merging the input runs. You should use a Priority Queue (java.util.PriorityQueue) 
 * to determine which record should be added to the output run * next. 
 * 
 * You are NOT allowed to have more than runs.size() records in your 
 * priority queue at a given moment. It is recommended that your Priority 
 * Queue hold Pair<Record, Integer> objects where a Pair (r, i) is the 
 * Record r with the smallest value you are sorting on currently unmerged 
 * from run i. `i` can be useful to locate which record to add to the queue * next after the smallest element is removed. 
 * 
 * @return a single sorted run obtained by merging the input runs  
 */
 public Run mergeSortedRuns(List<Run> runs) {  
    assert (runs.size() <= this.numBuffers - 1);  
    // TODO(proj3_part1): implement  
  
    List<BacktrackingIterator<Record>> mergeSortTracker = new ArrayList<>();  
    Run outputSortedRun = new Run(transaction, this.getSchema());  
  
    for (Run run: runs) {  
        mergeSortTracker.add(run.iterator());  
    }  
    PriorityQueue<Pair<Record, Integer>> pq = new PriorityQueue<>(new RecordPairComparator());  
  
    /*  
    * Bring in all the head of the backtracking iterator    
    * */    
    
    for (int i = 0; i < mergeSortTracker.size(); i++) {  
        if (mergeSortTracker.get(i).hasNext()) {  
            pq.add(new Pair<>(mergeSortTracker.get(i).next(), i));  
        }    
	}  
    /*  
    * Start merging, which relies on priority queue to decide which
    * records to put in the output sortedRun    
    *    
    * */  
    while (!pq.isEmpty()) {  
        /*  
        * 1. Get the smallest record(w.r.t join key)        * */        Pair<Record, Integer> currPair = pq.poll();  
        Record currRecord = currPair.getFirst();  
  
        /**  
         * 2. Put this record in the output run         */        outputSortedRun.add(currRecord);  
  
        /**  
         * 3. Figure our where this record come from(which run it belongs to)         */        Integer runIndex = currPair.getSecond();  
  
        /**  
         * 4. Update the cursor in this run iterator         */  
        if (mergeSortTracker.get(runIndex).hasNext()) {  
            /**  
             * Put the next record in this run into the priority queue and             * let it decide its priority             */            pq.add(new Pair<>(mergeSortTracker.get(runIndex).next(), runIndex));  
        }    }    return outputSortedRun;  
}
```

### mergePass
> [!task]
> ![](Project3_Join&Optimization(sp24).assets/image-20240309214931581.png)

```java
/**  
 * Given a list of N sorted runs, returns a list of sorted runs that is the 
 * result of merging (numBuffers - 1) of the input runs at a time. If N is 
 * not a perfect multiple of (numBuffers - 1) the last sorted run should be 
 * the result of merging less than (numBuffers - 1) runs. 
 * 
 * @return a list of sorted runs obtained by merging the input runs  
 */public List<Run> mergePass(List<Run> runs) {  
    // TODO(proj3_part1): implement  
    int sizeSortedRun = numBuffers - 1;  
    List<Run> outputRuns = new ArrayList<>();  
  
  
    List<Run> currGroup = new ArrayList<>();  
    Iterator<Run> runIterator = runs.iterator();  
  
    int counter = 0;  
    while (runIterator.hasNext()) {  
        if (counter < sizeSortedRun) {  
            currGroup.add(runIterator.next());  
            counter++;  
        } else {  
            Run currSortedGroup = mergeSortedRuns(currGroup);  
            outputRuns.add(currSortedGroup);  
            currGroup.clear();  
            counter = 0;  
        }    }  
    // The last group, don't forget  
    if (counter != 0) {  
        Run currSortedGroup = mergeSortedRuns(currGroup);  
        outputRuns.add(currSortedGroup);  
        currGroup.clear();  
    }  
    return outputRuns;  
}

```



### sort
> [!task]
> ![](Project3_Join&Optimization(sp24).assets/image-20240309214944531.png)

```java
/**  
 * Does an external merge sort over the records of the source operator. 
 * You may find the getBlockIterator method of the QueryOperator class useful 
 * here to create your initial set of sorted runs. 
 * 
 * @return a single run containing all of the source operator's records in  
 * sorted order. 
 * */
 public Run sort() {  
    // Iterator over the records of the relation we want to sort  
    Iterator<Record> sourceIterator = getSource().iterator();  
  
    // TODO(proj3_part1): implement  
    /*  
        Pass 0: Sort input pages, using all B buffers     
        So maxPages = B     
    */   
         
    List<Run> currPassSorted = new ArrayList<>();  
    // Get pages of records  
    while (sourceIterator.hasNext()) {  
        BacktrackingIterator<Record> blockIterator = getBlockIterator(sourceIterator, this.getSchema(), numBuffers);  
        Run records = sortRun(blockIterator);  
        currPassSorted.add(records);  
    }  
    /*  
    * Pass 2...n: Merge    
    * */    
    while (currPassSorted.size() > 1) {  
        currPassSorted = mergePass(currPassSorted);  
    }  
    return currPassSorted.get(0);  
}
```


## Task 4: Sort Merge Join
> [!task]
> ![](Project3_Join&Optimization(sp24).assets/image-20240309222801200.png)![](2_Iterators&Joins.assets/image-20240220132045580.png)

```java
/**  
 * Returns the next record that should be yielded from this join, 
 * or null if there are no more records to join. 
 * */
 private Record fetchNextRecord() {  
    // TODO(proj3_part1): implement  
    if (leftRecord == null) {  
        return null;  
    }  
    
    /*  
    * Haven't find a match, find until match    
    * 
    * */    
    if (!marked) {  
        marked = true;  
        while (compare(leftRecord, rightRecord) > 0) {  
            rightRecord = rightIterator.next();  
        }        
        while (compare(leftRecord, rightRecord) < 0) {  
            leftRecord = leftIterator.next();  
        }        
	    /**  
	    * Find a match, mark the current rightCursor       
	    * */        
	    rightIterator.markPrev();  
    }  
    
    /*  
    * Still in the match, find until unmatch    
    * */    
    if (compare(leftRecord, rightRecord) == 0) {  
        nextRecord = leftRecord.concat(rightRecord);  
        if (!rightIterator.hasNext()) {  
            marked = false;  
            if (leftIterator.hasNext()) {  
                leftRecord = leftIterator.next();  
            } else {  
                leftRecord = null;  
            }            
            rightIterator.reset();  
        }        
        rightRecord = rightIterator.next();  
    } else {  
        marked = false;  
        if (leftIterator.hasNext()) {  
            leftRecord = leftIterator.next();  
        } else {  
            leftRecord = null;  
        }        
        rightIterator.reset();  
        rightRecord = rightIterator.next();  
        return fetchNextRecord();  
    }    
    return nextRecord;  
}
```





# Query Optimization
## Task 5: Single Table Access Selection



## Task 6: Join Selection



## Task 7: Optimal Plan Selection




