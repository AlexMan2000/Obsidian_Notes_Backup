# Buffer Pool Manager
## Organization
> [!important]
> ![](Buffer_Management.assets/image-20240514110707784.png)


## Page Table
> [!def]
> ![](Buffer_Management.assets/image-20240514110727225.png)



## Locks&Latches
> [!important]
> When some trasaction asks the bufferpool manager to load some data into the buffer pool(i.e. asking for records)
> ![](Buffer_Management.assets/image-20240514111313910.png)



## Page Allocation Policy
> [!def]
> ![](Buffer_Management.assets/image-20240514112120160.png)






## Buffer Manager
> [!def]
> ![](Buffer_Management.assets/image-20240209161413726.png)![](Buffer_Management.assets/image-20240209161420509.png)![](Buffer_Management.assets/image-20240209161549538.png)





# Traditional Page Replacement Policy
## Why Software Level?
> [!motiv]
> ![](Buffer_Management.assets/image-20240209165350460.png)
> Remember when something is embedded to the hardware level, it generally cannot change in the future. And software level DBMS can have more flexibility.


## LRU Counting Policy
### Algorithm
> [!concept]
> ![](Buffer_Management.assets/f26f072a667b5f9538613811e657cc03_MD5.jpeg)
> We can implement the eviction priority using a priority queue(based on heap). Everytime it pops from the queue the frameID with the smallest `last used`.


### Examples
> [!example] Fa23 Disc04 P1 Unpinned Random Access Pattern
> ![](Buffer_Management.assets/image-20240209162923557.png)
> The x-axis is the timeline. (\*) denotes cache hit event and y-axis represent the buffer-ids.

> [!example] Fa23 Disc04 P1 Pinned Random Access Pattern
> ![](Buffer_Management.assets/image-20240209164838484.png)![](Buffer_Management.assets/image-20240209164843808.png)

> [!example] Longer Sequence of Accessment W.O. Pinning
> ![](Buffer_Management.assets/image-20240209171951464.png)![](Buffer_Management.assets/image-20240209172145247.png)![](Buffer_Management.assets/image-20240209172316942.png)










### Implementations
#### Java Implementation - DLL
> [!code]
```java
public class LRUEvictionPolicy implements EvictionPolicy {  
    private Tag listHead;  
    private Tag listTail;  
  
    // Doubly-linked list between frames, in order of least to most  
    // recently used.    private class Tag {  
        Tag prev = null;  
        Tag next = null;  
        BufferFrame cur = null;  
  
        @Override  
        public String toString() {  
            String sprev = (prev == null || prev.cur == null) ? "null" : prev.cur.toString();  
            String snext = (next == null || next.cur == null) ? "null" : next.cur.toString();  
            String scur = cur == null ? "null" : cur.toString();  
            return scur + " (prev=" + sprev + ", next=" + snext + ")";  
        }    }  
    public LRUEvictionPolicy() {  
        this.listHead = new Tag();  
        this.listTail = new Tag();  
        this.listHead.next = this.listTail;  
        this.listTail.prev = this.listHead;  
    }  
    /**  
     * Called to initiaize a new buffer frame.     * @param frame new frame to be initialized  
     */    @Override  
    public void init(BufferFrame frame) {  
        Tag frameTag = new Tag();  
        frameTag.next = listTail;  
        frameTag.prev = listTail.prev;  
        listTail.prev = frameTag;  
        frameTag.prev.next = frameTag;  
        frameTag.cur = frame;  
        frame.tag = frameTag;  
    }  
    /**  
     * Called when a frame is hit.     * @param frame Frame object that is being read from/written to  
     */    @Override  
    public void hit(BufferFrame frame) {  
        Tag frameTag = (Tag) frame.tag;  
        frameTag.prev.next = frameTag.next;  
        frameTag.next.prev = frameTag.prev;  
        frameTag.next = this.listTail;  
        frameTag.prev = this.listTail.prev;  
        this.listTail.prev.next = frameTag;  
        this.listTail.prev = frameTag;  
    }  
    /**  
     * Called when a frame needs to be evicted.     * @param frames Array of all frames (same length every call)  
     * @return index of frame to be evicted  
     * @throws IllegalStateException if everything is pinned  
     */    @Override  
    public BufferFrame evict(BufferFrame[] frames) {  
        Tag frameTag = this.listHead.next;  
        while (frameTag.cur != null && frameTag.cur.isPinned()) {  
            frameTag = frameTag.next;  
        }        if (frameTag.cur == null) {  
            throw new IllegalStateException("cannot evict anything - everything pinned");  
        }        return frameTag.cur;  
    }  
    /**  
     * Called when a frame is removed, either because it     * was returned from a call to evict, or because of other constraints     * (e.g. if the page is deleted on disk).     * @param frame frame being removed  
     */    @Override  
    public void cleanup(BufferFrame frame) {  
        Tag frameTag = (Tag) frame.tag;  
        frameTag.prev.next = frameTag.next;  
        frameTag.next.prev = frameTag.prev;  
        frameTag.prev = frameTag.next = frameTag;  
    }}
```



#### C++ Implementation



## LRU Clock Policy
### Why Clock Policy?
> [!important]
> ![](Buffer_Management.assets/image-20240209165223724.png)![](Buffer_Management.assets/image-20240209165242937.png)


### Algorithm
> [!algo]
> ![](Buffer_Management.assets/image-20240209161753170.png)![](Buffer_Management.assets/image-20240209161921826.png)![](Buffer_Management.assets/image-20240209161929257.png)
> **Note:**
> - When the buffer pool is not full, no replacement policy will be triggered. In this case, the clock hand is nowhere to find.
> - When the buffer pool is full, the clock hand will be set to the first unpinned page in the buffer pool.
> - We don't move the pointer when there is a page hit, we will start the clock hand iteration at this position.(not the next one).

> [!example] Hit Event Without Pinning Event
> See [CS 186 Discussion 4](CS%20186%20Discussion%204.pdf)
> ![](Buffer_Management.assets/image-20240209164214220.png)![](Buffer_Management.assets/image-20240209164218564.png)
> Here the second chance bit is the same as reference bit.

> [!example] With Pinned Event
> ![](Buffer_Management.assets/image-20240209161938290.png)![](Buffer_Management.assets/image-20240209161944359.png)![](Buffer_Management.assets/image-20240209162049866.png)![](Buffer_Management.assets/image-20240209162055609.png)![](Buffer_Management.assets/image-20240209162101917.png)




## MRU Policy
### Algorithm
> [!def]
> Just a little modification of LRU where we evict the page by the most recently used time frame.


### Examples
> [!example] Disc04 P1 MRU Random Access Pattern
> ![](Buffer_Management.assets/image-20240209163225659.png)

> [!example] Fa23 Disc04 P1 MRU Pinned Random Access Pattern
> ![](Buffer_Management.assets/image-20240209165011040.png)![](Buffer_Management.assets/image-20240209165016269.png)

> [!example] Longer Sequence of Accessment W.O. Pinning
> ![](Buffer_Management.assets/image-20240209172536705.png)![](Buffer_Management.assets/image-20240209172541724.png)![](Buffer_Management.assets/image-20240209172527736.png)



## Random Access Performance
> [!important]
> ![](Buffer_Management.assets/image-20240209162452708.png)


> [!example] Disc04 P1 LRU Random Access Pattern
> ![](Buffer_Management.assets/image-20240209162923557.png)
> The x-axis is the timeline. (\*) denotes cache hit event. 

> [!example] Disc04 P1 MRU Random Access Pattern
> ![](Buffer_Management.assets/image-20240209163225659.png)




## Sequantial Scanning Performance
### LRU - Sequantial Flooding
> [!important]
> ![](Buffer_Management.assets/image-20240209162153568.png)![](Buffer_Management.assets/image-20240209162158019.png)
> Is like cache miss if we keep loading conclicting blocks in.


### MRU - Good at Sequential Requests
> [!important]
> ![](Buffer_Management.assets/image-20240209162209299.png)![](Buffer_Management.assets/image-20240209162245985.png)



# Better Page Eviction Policies
## LRU - K
> [!important]
> ![](Buffer_Management.assets/image-20240514121956352.png)![](Buffer_Management.assets/image-20240514133422288.png)



## Localization
> [!important]
> ![](Buffer_Management.assets/image-20240514134502136.png)


## Priority Hints
> [!important]
> ![](Buffer_Management.assets/image-20240514140539694.png)
> For autoincrement key(with index on it) like this, we know pages that stores larger key are more important.




# Buffer Pool Optimization
## Multiple Buffer Pools
> [!important]
> ![](Buffer_Management.assets/image-20240514112212163.png)
> - Each pool can be managed independently, with its own set of resources and management strategies.
> - **Latch contention** occurs when multiple threads or processes attempt to acquire a latch at the same time, leading to delays and decreased performance as each thread waits for access.
> - **How Partitioning Helps**: By dividing memory into multiple pools, the likelihood that two processes will need to access the same memory region simultaneously is reduced. Each process accesses its designated memory pool, thereby reducing the competition or "contention" for latches. This can significantly decrease waiting times and increase throughput.
> 
> ![](Buffer_Management.assets/image-20240514112400434.png)![](Buffer_Management.assets/image-20240514112408425.png)



## Pre-Fetching
> [!def]
> ![](Buffer_Management.assets/image-20240514112906896.png)
> 1. **Identifying Access Pattern:** If sequential scan, pre-fetch the next few consecutive pages so that the SQL executor won't have to wait for data to be ready. If index scan, pre-fetch the next childNode in the index tree.
> 2. **Preactive Loading:** Based on these predictions, the buffer pool manager preloads the anticipated data pages from the disk into the buffer pool. This is done in a way that does not disrupt the current performance but instead utilizes idle I/O capacity or prioritizes prefetching to maximize efficiency.
> 3. **Optimizing Resource Use:** By loading data pages before they are needed, the system can **reduce I/O wait times** when the actual query is executed.
> 
> ![](Buffer_Management.assets/image-20240514113809663.png)
> When Q1 is asking for index-page 1, the buffer pool manager already predicts that the next pages to load are index-page3 and index-page5.



## Scan Sharing
> [!def]
> ![](Buffer_Management.assets/image-20240514113939755.png)![](Buffer_Management.assets/image-20240514114441345.png)![](Buffer_Management.assets/image-20240514114654554.png)



## Buffer Pool ByPass
> [!def]
> ![](Buffer_Management.assets/image-20240514114957388.png)











