# Heap Allocator
## Motivation: What is heap allocator
> [!motiv] Motivation
> ![](Heap%20Management.assets/image-20231212102026136.png)![](Heap%20Management.assets/image-20231212102106877.png)![](Heap%20Management.assets/image-20231212102126739.png)![](Heap%20Management.assets/image-20231212102156757.png)![](Heap%20Management.assets/image-20231212102217247.png)


## Requirements
> [!important]
> A heap allocator must:
> 1. Handle arbitrary request sequences of allocations and frees 
> 2. Keep track of what memory has been allocated and what memory is free 
> 3. Decide which memory to use when fulfilling an allocation request 
> 4. Respond to requests as quickly as possible 
> 5. Return addresses that are 8-byte-aligned (must be multiples of 8).
> 
> **Notes on alignment:**
> 
> ![](Heap%20Management.assets/image-20231212103534816.png)![](Heap%20Management.assets/image-20231212103546054.png)


## Goals
> [!important]
> 1. ==Maximizing throughput==. Given some sequence of n allocate and free requests $R_0 , R_1 , . . . , R_k , . . . , R_{n−1}$, we would like to maximize an allocator’s throughput, which is defined as the number of requests that it completes per unit time. For example, if an allocator completes 500 allocate requests and 500 free requests in 1 second, then its throughput is 1,000 operations per second. In general, we can maximize throughput by minimizing the average time to satisfy allocate and free requests. 
> 2. ==Maximize utilization==, or how efficiently we make use of the limited heap memory to satisfy requests.
> 
> These are seemingly conflicting goals – i.e., it may take longer to better plan out heap memory use for each request. 
> 
> Heap allocators must strike the right balance between the two.


# Fragmentation
## Internal Fragmentation
> [!concept]
> Internal fragmentation occurs **when an allocated block is larger than the payload.**
> 
> This might happen for a number of reasons. 
> - For example, the implementation of an allocator might impose a minimum size on allocated blocks that is greater than some requested payload. 
> - Or, as we saw in Figure 9.34(b), the allocator might increase the block size in order to satisfy alignment constraints.
> 
> Internal fragmentation is straightforward to quantify. It is simply the sum of the differences between the sizes of the allocated blocks and their payloads. Thus, at any point in time, the amount of internal fragmentation depends only on the pattern of previous requests and the allocator implementation.
> ![](Heap%20Management.assets/image-20231212104029400.png)


## External Fragmentation
> [!concept]
> External fragmentation occurs when:
> 1. **There is enough aggregate free memory** to satisfy an allocate request
> 2. But **no single free block is large enough to handle the request**. For example, if the request in Figure 9.34(e) were for eight words rather than two words, then the request could not be satisfied without requesting additional virtual memory from the kernel, even though there are eight free words remaining in the heap. The problem arises because these eight words are spread over two free blocks.
> 
> ![](Heap%20Management.assets/image-20231212104436726.png)


# Deal with Utilization and Throughput
## Attempt 1: Shifted Blocks
> [!bug] Shifting Allocated Blocks
> ![](Heap%20Management.assets/image-20231212104646459.png)![](Heap%20Management.assets/image-20231212104650426.png)![](Heap%20Management.assets/image-20231212104659337.png)



## Attempt 2: Bump Allocator
> [!bug] Only Consider for Throughput, Not Utilization
> ![](Heap%20Management.assets/image-20231212105220173.png)![](Heap%20Management.assets/image-20231212105429375.png)![](Heap%20Management.assets/image-20231212105444911.png)


## Design Considerations
> [!important]
> ![](Heap%20Management.assets/image-20231212110158049.png)





# Implicit Free Lists
## Block Header Design
> [!success] Implementation Details
> In implicits free list, we keep track of the allocated blocks, which implicitly tell the location of these free blocks.
> ![](Heap%20Management.assets/image-20231212110315819.png)
> **Notes:**
> 
> - If we impose a double word alignment constraint,then the block size is always a multiple of 8 and the 3 low-order bits of the block size are always zero. 
> - Thus, we need to store only the 29 high-order bits of the block size, freeing the remaining 3 bits to encode other information. 
> - For example, if we have an allocated block of 24 bytes, then we for the least significant bit of the higher 29 bit, we only have to store $\frac{24}{8}=3$ in decimal and thus $0b11$ in binary, this gives $0b0...0011001$ and it evaluates to $0x19$ for the header block in heximal.
> - Note in the above header design we have impose a minimum block size on the allocator, which is 4(for header) + 4(for payload)= 8 bytes
> - Whether we store the block size as just payload size or header + payload depends on the implementer, both are ok but differs in ways of traversing the list.
> 
> ![](Heap%20Management.assets/image-20231212113424414.png)
> The following example uses a 8-byte header instead of a 4-byte one, but the idea is the same. Note that in this case we impose a minimum block size on the allocator, which is 8(for header) + 8(for payload) = 16 bytes.
> 
> ![](Heap%20Management.assets/image-20231212113615847.png)
> One good thing about using 8-byte header is that in 64-bit machine we are required to return a 64 bit address from the `malloc/calloc` function, an 8-byte header just makes alignment easier.
> 
> ![](Heap%20Management.assets/image-20231212114419246.png)
> ![](Heap%20Management.assets/image-20231212114544460.png)


> [!example] Calculating header size
> ![](Heap%20Management.assets/image-20231212112335884.png)


## Choose Free Blocks
> [!overview]
> ![](Heap%20Management.assets/image-20231212113718985.png)


### First Fit
> [!example]
> ![](Heap%20Management.assets/image-20231212115149250.png)![](Heap%20Management.assets/image-20231212115027510.png)
> **Here we have several bitwise operations:**
> - `*p & 1` extracts the bit that indicates whether this block has been allocated.
> - `*p & -2` extracts the current block size and `p + *p & -2` moves the pointer to the start of the next block.
> 


### Next Fit
> [!example]
> ![](Heap%20Management.assets/image-20231212115201025.png)


### Best Fit
> [!example]
> ![](Heap%20Management.assets/image-20231212115212590.png)![](Heap%20Management.assets/image-20231212115120724.png)



## Splitting Free Blocks
> [!concept]
> ![](Heap%20Management.assets/image-20231212120432716.png)
> **Notes on the implementations:**
> - `len` here means the number of 4-byte word in a block(including the header word). 
> 	- If the `len` is even , then it has a factor 2, then multiplying it with 4(word size) would give a block size of multiple of 8.
> 	- If the `len` is odd, then it doesn't have factor 2, then multiplying it with 4(word size) wouldn't meet the double-word alignment requirement of the allocator.
> - `*p & -2` mask the lowest bit(indicating allocated or not) to get the size of current block that `p` is pointing to.
> - `newsize | 1` just set the current block to be in the state of allocated.
> - `p + newsize` calculate the starter of the splitting point caused by allocating a block whose size is smaller then the original free block.
> 
> What about edge cases where the block to be allocated is the last free block where after allocating when we want to set the header of the second splitted the free block, if the remaining memory is less than required(for example 8), how are we going to properly end the linked, as shown below:
> ![](Heap%20Management.assets/image-20231212143024978.png)
> We want to allocate `16 bytes` on the heap, so we traverse the implicit list(with first fit policy) and find the virtual address `0x40` where the allocated header says that we have 24 bytes free bytes available, then we apply the splitting policy above, where we calculate the newsize and oldsize and move the pointer ahead. Now at `*(p + newsize) = oldsize - newsize` step, we may have an issue, as shown below:
> 
> ![](Heap%20Management.assets/image-20231212142908400.png)
> 
> What if the we don't have enough bytes ahead starting from `0x58`. For example we only have 4-bytes ahead (`0x58 ~ 0x5B`), but the pointer on the 64-bit machine can access 8 bytes upon dereferencing, which means segment fault. If this is the case, then we could use the following strategy:
> ![](Heap%20Management.assets/image-20231212143647372.png)
> Otherwise, we could just create a pseudo free block as follows:
> 
> ![](Heap%20Management.assets/image-20231212143513602.png)






## Freeing the Blocks
### Clear the Allocated Flag Only
> [!bug] Buggy Attempt: Only Clear the Allocated Flag
> ![](Heap%20Management.assets/image-20231212143811052.png)
> **Notes:**
> - Here the gray color represents allocated blocks and white color denotes free blocks.
> - The mistake happens because when we free the allocated block(in green) without coalescing with the contiguous free block, we will misrepresent the free block size and the allocator may not be able to accurately calculate the free memory size.
> - For example, **from the heap allocator point of view, a contiguous 4-byte free block and 2-byte free block is not equivalent to a single 6-byte free block** where the latter is more capable of being splitted and have greater chance of being the next allocated one(since it has enough free space).




### Clear Flags and Coalescing Free Blocks
> [!success]
> ![](Heap%20Management.assets/image-20231212145949829.png)



### Bidirectional Coalescing
> [!concept]
> 




# Explicit Free Lists