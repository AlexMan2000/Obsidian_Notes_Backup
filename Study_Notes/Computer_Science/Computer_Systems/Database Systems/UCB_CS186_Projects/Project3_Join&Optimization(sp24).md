
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
> [!task]
> ![](Project3_Join&Optimization(sp24).assets/image-20240313111439741.png)
> For a column to be eligible for index scan, it has to satisfy the following:
> 1. There is index built on that column.
> 2. The selection operator on that column should not be `NOT_EQUAL`
> 
> Suppose we have a relation $R(a,b,c)$ and we are doing a index scan on column b with selection predicate b >= 4 AND a < 5, then:
> 1. The indexscan operator spits out records with b >= 4 one by one on-the-fly.
> 2. For each record produced by indexscan operator, apply SelectOperator with predicate a < 5 to the record. If the predicate returns true, keep it, otherwise drop it.
> 3. The I/O cost of SelectorOperator is defined to be the same as the source Operator that produces the records.
> 

> [!code]
```java
// Task 5: Single Table Access Selection

    /**
     * Gets all select predicates for which there exists an index on the column
     * referenced in that predicate for the given table and where the predicate
     * operator can be used in an index scan.
     *
     * @return a list of indices of eligible selection predicates in
     * this.selectPredicates
     */
    private List<Integer> getEligibleIndexColumns(String table) {
        List<Integer> result = new ArrayList<>();
        for (int i = 0; i < this.selectPredicates.size(); i++) {
            SelectPredicate p = this.selectPredicates.get(i);
            // ignore if the selection predicate is for a different table
            if (!p.tableName.equals(table)) continue;
            boolean indexExists = this.transaction.indexExists(table, p.column);
            // indexScan not supported for != predicate
            boolean canScan = p.operator != PredicateOperator.NOT_EQUALS;
            if (indexExists && canScan) result.add(i);
        }
        return result;
    }

    /**
     * Applies all eligible select predicates to a given source, except for the
     * predicate at index except. The purpose of except is because there might
     * be one select predicate that was already used for an index scan, so
     * there's no point applying it again. A select predicate is represented as
     * an element in this.selectPredicates. `except` corresponds to the index
     * of the predicate in that list.
     *
     * @param source a source operator to apply the selections to
     * @param except the index of a selection to skip. You can use the value -1
     *               if you don't want to skip anything.
     * @return a new query operator after select predicates have been applied
     */
    private QueryOperator addEligibleSelections(QueryOperator source, int except) {
        for (int i = 0; i < this.selectPredicates.size(); i++) {
            if (i == except) continue;
            SelectPredicate curr = this.selectPredicates.get(i);
            try {
                String colName = source.getSchema().matchFieldName(curr.tableName + "." + curr.column);
                source = new SelectOperator(
                        source, colName, curr.operator, curr.value
                );
            } catch (RuntimeException err) {
                /* do nothing */
            }
        }
        return source;
    }

    /**
     * Finds the lowest cost QueryOperator that accesses the given table. First
     * determine the cost of a sequential scan for the given table. Then for
     * every index that can be used on that table, determine the cost of an
     * index scan. Keep track of the minimum cost operation and push down
     * eligible select predicates.
     *
     * If an index scan was chosen, exclude the redundant select predicate when
     * pushing down selects. This method will be called during the first pass of
     * the search algorithm to determine the most efficient way to access each
     * table.
     *
     * @return a QueryOperator that has the lowest cost of scanning the given
     * table which is either a SequentialScanOperator or an IndexScanOperator
     * nested within any possible pushed down select operators. Ties for the
     * minimum cost operator can be broken arbitrarily.
     */
    public QueryOperator minCostSingleAccess(String table) {
        QueryOperator minOp = new SequentialScanOperator(this.transaction, table);

        // TODO(proj3_part2): implement
        // Even if the full scan will always cost <num_of_pages> I/Os to run, we have to apply selection
        // operator to it in order to pass the test.
        minOp = addEligibleSelections(minOp, -1);
        int bestIOCost = minOp.estimateIOCost();
        int currIOCost;

        // Get the index of the column that has index built on it and the select operator on that column
        // is not !=
        List<Integer> tableIndices = getEligibleIndexColumns(table);

        /* For each column with index built on it, calculate the I/O costs of performing indexScan
        *  If there is selection operator that's pushed down on that column, ignore it since index scan
        *  is using that selection operator, we don't want to count for its I/Os twice(one for selection, one for indexScan)
        * */
        for (Integer index: tableIndices) {
            // Get the select predicate for current index scan, we want to exclude this select predicate
            SelectPredicate sp = this.selectPredicates.get(index);
            QueryOperator indexScanOp = new IndexScanOperator(this.transaction,
                    table,
                    sp.column,
                    sp.operator,
                    sp.value);
            indexScanOp = addEligibleSelections(indexScanOp, index);
            currIOCost = indexScanOp.estimateIOCost();
            if (currIOCost < bestIOCost) {
                bestIOCost = currIOCost;
                minOp = indexScanOp;
            }
        }

        return minOp;
    }
```
> [!code] Test Output
> ![](Project3_Join&Optimization(sp24).assets/image-20240313113458161.png)





## Task 6: Join Selection
> [!task]
> ![](Project3_Join&Optimization(sp24).assets/image-20240313113522480.png)![](3_Query_Optimization.assets/image-20240223164110532.png)
> For pass 1....n, the function takes in the optimal results from pass i-1 and spit out the optimal result at pass i.
> 
> For example, `prevMap` could be:
> `{{A,B}: SMJ, {A,C}: SNLJ, {B,C}: BNLJ, {B,T}: GHJ, {A,T}: SNLJ}`
> 
> And `result` could be:
> `{{A,B,T}: PNLJ, {A,B,C}: INLJ, {B,C,T}: SMJ, {A,B,T}: SNLJ, {A,C,T}: SNLJ}`

> [!code]
```java
// Task 6: Join Selection //////////////////////////////////////////////////

    /**
     * Given a join predicate between left and right operators, finds the lowest
     * cost join operator out of join types in JoinOperator.JoinType. By default
     * only considers SNLJ and BNLJ to prevent dependencies on GHJ, Sort and SMJ.
     *
     * Reminder: Your implementation does not need to consider cartesian products
     * and does not need to keep track of interesting orders.
     *
     * @return lowest cost join QueryOperator between the input operators
     */
    private QueryOperator minCostJoinType(QueryOperator leftOp,
                                          QueryOperator rightOp,
                                          String leftColumn,
                                          String rightColumn) {
        QueryOperator bestOperator = null;
        int minimumCost = Integer.MAX_VALUE;
        List<QueryOperator> allJoins = new ArrayList<>();
        allJoins.add(new SNLJOperator(leftOp, rightOp, leftColumn, rightColumn, this.transaction));
        allJoins.add(new BNLJOperator(leftOp, rightOp, leftColumn, rightColumn, this.transaction));
        for (QueryOperator join : allJoins) {
            int joinCost = join.estimateIOCost();
            if (joinCost < minimumCost) {
                bestOperator = join;
                minimumCost = joinCost;
            }
        }
        return bestOperator;
    }

    /**
     * Iterate through all table sets in the previous pass of the search. For
     * each table set, check each join predicate to see if there is a valid join
     * with a new table. If so, find the minimum cost join. Return a map from
     * each set of table names being joined to its lowest cost join operator.
     *
     * Join predicates are stored as elements of `this.joinPredicates`.
     *
     * @param prevMap  maps a set of tables to a query operator over the set of
     *                 tables. Each set should have pass number - 1 elements.
     * @param pass1Map each set contains exactly one table maps to a single
     *                 table access (scan) query operator.
     * @return a mapping of table names to a join QueryOperator. The number of
     * elements in each set of table names should be equal to the pass number.
     */
    public Map<Set<String>, QueryOperator> minCostJoins(
            Map<Set<String>, QueryOperator> prevMap,
            Map<Set<String>, QueryOperator> pass1Map) {
        Map<Set<String>, QueryOperator> result = new HashMap<>();
        // TODO(proj3_part2): implement
        // We provide a basic description of the logic you have to implement:
        // For each set of tables in prevMap
        //   For each join predicate listed in this.joinPredicates
        //      Get the left side and the right side of the predicate (table name and column)
        //
        //      Case 1: The set contains left table but not right, use pass1Map
        //              to fetch an operator to access the rightTable
        //      Case 2: The set contains right table but not left, use pass1Map
        //              to fetch an operator to access the leftTable.
        //      Case 3: Otherwise, skip this join predicate and continue the loop.
        //
        //      Using the operator from Case 1 or 2, use minCostJoinType to
        //      calculate the cheapest join with the new table (the one you
        //      fetched an operator for from pass1Map) and the previously joined
        //      tables. Then, update the result map if needed.
        for (Map.Entry<Set<String>, QueryOperator> pair: prevMap.entrySet()) {
            // { A,B } SNLJ  {B, C} SMJ  {A, C} BNLJ, {B,T} SNLJ, .... all are optimal plans
            Set<String> tablePairSet = pair.getKey();
            QueryOperator leftOp = pair.getValue();
            for (JoinPredicate jp: this.joinPredicates) {
                String leftTable = jp.leftTable;
                String leftColumn = jp.leftColumn;
                String rightTable = jp.rightTable;
                String rightColumn = jp.rightColumn;

                QueryOperator rightOp;
                QueryOperator minCostOp;
                Set<String> probeKey= new HashSet<>();
                Set<String> resultKey = new HashSet<>(tablePairSet);

                if (!tablePairSet.contains(leftTable) && tablePairSet.contains(rightTable)) {
                    probeKey.add(leftTable);
                    rightOp = pass1Map.get(probeKey);
                    /*
                        Be careful with the order here, suppose the join predicate is
                            JOIN ON A.aid = B.bid
                            - leftTable = A
                            - rightTable = B
                        But the current set is {B,C}, then B is in the set but A is not.
                        So we want to join B and A where {B,C} is leftOp and A is rightOp

                        B has rightColumn, but has to be on the left, so we pass in rightColumn first.
                     */
                    minCostOp = minCostJoinType(leftOp, rightOp, rightColumn, leftColumn);
                    resultKey.add(leftTable);
                } else if (tablePairSet.contains(leftTable) && !tablePairSet.contains(rightTable)){
                    probeKey.add(rightTable);
                    rightOp = pass1Map.get(probeKey);
                    minCostOp = minCostJoinType(leftOp, rightOp, leftColumn, rightColumn);
                    resultKey.add(rightTable);
                } else {
                    /*
                        3. If both exists, then this join must have been evaluated
                        and optimized in previous pass, don't have to evaluate it again, skip
                        4. If neither exists, then skip.
                     */
                    continue;
                }

                int minCost = minCostOp.estimateIOCost();
                if (result.containsKey(resultKey)) {
                    if (minCost < result.get(resultKey).estimateIOCost()) {
                        result.put(resultKey, minCostOp);
                    }
                } else {
                    result.put(resultKey, minCostOp);
                }
            }
        }

        // {A,B,C} SMJ, {A,B,T} SNLJ ... all optimal plans
        return result;
    }
```
> [!test] Test Output
> ![](Project3_Join&Optimization(sp24).assets/image-20240313132102608.png)



## Task 7: Optimal Plan Selection
> [!task]
> ![](Project3_Join&Optimization(sp24).assets/image-20240313131550582.png)

> [!code]
```java
// Task 7: Optimal Plan Selection //////////////////////////////////////////

    /**
     * Finds the lowest cost QueryOperator in the given mapping. A mapping is
     * generated on each pass of the search algorithm, and relates a set of tables
     * to the lowest cost QueryOperator accessing those tables.
     *
     * @return a QueryOperator in the given mapping
     */
    private QueryOperator minCostOperator(Map<Set<String>, QueryOperator> map) {
        if (map.size() == 0) throw new IllegalArgumentException(
                "Can't find min cost operator over empty map"
        );
        QueryOperator minOp = null;
        int minCost = Integer.MAX_VALUE;
        for (Set<String> tables : map.keySet()) {
            QueryOperator currOp = map.get(tables);
            int currCost = currOp.estimateIOCost();
            if (currCost < minCost) {
                minOp = currOp;
                minCost = currCost;
            }
        }
        return minOp;
    }

    /**
     * Generates an optimized QueryPlan based on the System R cost-based query
     * optimizer.
     *
     * @return an iterator of records that is the result of this query
     */
    public Iterator<Record> execute() {
        this.transaction.setAliasMap(this.aliases);
        // TODO(proj3_part2): implement
        // Pass 1: For each table, find the lowest cost QueryOperator to access
        // the table. Construct a mapping of each table name to its lowest cost
        // operator.
        int joinSize = tableNames.size();
        Map<Set<String>, QueryOperator> pass1Map = new HashMap<>();
        Map<Set<String>, QueryOperator> prevMap = pass1Map;
        for (String tableName: tableNames) {
            QueryOperator minCostOp = minCostSingleAccess(tableName);
            Set<String> mapKey = new HashSet<>();
            mapKey.add(tableName);
            pass1Map.put(mapKey, minCostOp);
        }
        // Pass i: On each pass, use the results from the previous pass to find
        // the lowest cost joins with each table from pass 1. Repeat until all
        // tables have been joined.
        int currSize = 1;
        while (currSize < joinSize) {
            prevMap = minCostJoins(prevMap, pass1Map);
            currSize++;
        }

        // Set the final operator to the lowest cost operator from the last
        // pass, add group by, project, sort and limit operators, and return an
        // iterator over the final operator.

        this.finalOperator = minCostOperator(prevMap);
        this.addGroupBy();
        this.addProject();
        this.addSort();
        this.addLimit();

        return this.finalOperator.iterator();
    }
```
> [!test] Test Output
> ![](Project3_Join&Optimization(sp24).assets/image-20240313143459459.png)








