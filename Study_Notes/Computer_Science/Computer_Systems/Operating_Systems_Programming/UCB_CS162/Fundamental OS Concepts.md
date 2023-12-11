# Concept 1: Thread of Control
> [!important]
> ![](Fundamental%20OS%20Concepts.assets/image-20231205164545188.png)

## Illusion of Multiple Processors
> [!def]
> ![](Fundamental%20OS%20Concepts.assets/image-20231205164630676.png)![](Fundamental%20OS%20Concepts.assets/image-20231205164646533.png)


## Thread Control Block
> [!concept]
> ![](Fundamental%20OS%20Concepts.assets/image-20231205175754744.png)



# Concept 2: Address Space
> [!concept]
> ![](Fundamental%20OS%20Concepts.assets/image-20231205180123495.png)![](Fundamental%20OS%20Concepts.assets/image-20231205180313828.png)



## Simple Protection: Base and Bound(B&B)
> [!concept] Limit the stretch of memory
> ![](Fundamental%20OS%20Concepts.assets/image-20231206223717315.png)
> In this first method, we will have two registers, base and bound, that limits the memory span of the process.
> 
> ![](Fundamental%20OS%20Concepts.assets/image-20231206223924002.png)
> When the program is loaded into the memory, it will be relocated by the operating system. Here the program counter is moving around the actual physical memory. The above method is called hardware base and bound.
> In the following second method, which is called software base and bound, apply address translation with base and bound. Here the program counter is still moving across the virtual memory space.
> 
> ![](Fundamental%20OS%20Concepts.assets/image-20231206224200473.png)


## x86 segments and stacks
> [!important]
> ![](Fundamental%20OS%20Concepts.assets/image-20231206225111992.png)
> `CS`: Register that points to the start of Code Section 
> `SS`: Register that points to the start of Static Data Section
> `EIP`: Register that points to the current instruction that's being executed.
> `ESP`: Register that points to the current data segment that's being accessed. 


## Address Space Translation
> [!concept]
> ![](Fundamental%20OS%20Concepts.assets/image-20231206225314297.png)![](Fundamental%20OS%20Concepts.assets/image-20231206225325095.png)![](Fundamental%20OS%20Concepts.assets/image-20231206225334688.png)



# Concept 3: Process
## Definition
> [!concept]
> ![](Fundamental%20OS%20Concepts.assets/image-20231206225619441.png)![](Fundamental%20OS%20Concepts.assets/image-20231206230848609.png)![](Fundamental%20OS%20Concepts.assets/image-20231206230905327.png)






## Single and Multithreaded Processes
> [!important]
> ![](Fundamental%20OS%20Concepts.assets/image-20231206225818695.png)
> - All threads share a common heap.
> - Each thread has its own stack, which it can quickly add and remove items from. This makes stack based memory fast, but if you use too much stack memory, as occurs in infinite recursion, you will get a stack overflow.
> - Every thread has a separate stack, but it is not necessarily 'private'. Other threads are usually allowed to access it.
> - Since all threads share the same heap, access to the allocator/deallocator must be synchronized. There are various methods and libraries for avoiding [allocator contention](https://stackoverflow.com/questions/470683/memory-allocation-deallocation-bottleneck).
> - Some languages allow you to create private pools of memory, or individual heaps, which you can assign to a single thread.


## Process and Isolation
> [!concept]
> ![](Fundamental%20OS%20Concepts.assets/image-20231206230234819.png)





# Concept 4: Dual Mode Operation
> [!concept]
> ![](Fundamental%20OS%20Concepts.assets/image-20231206231210104.png)![](Fundamental%20OS%20Concepts.assets/image-20231206231458556.png)








