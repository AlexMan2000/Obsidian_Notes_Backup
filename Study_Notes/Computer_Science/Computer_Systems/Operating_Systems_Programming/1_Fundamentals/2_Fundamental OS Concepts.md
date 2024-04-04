# Concept 1: Thread of Control
> [!important]
> ![](2_Fundamental%20OS%20Concepts.assets/image-20231205164545188.png)

## Illusion of Multiple Processors
> [!def]
> ![](2_Fundamental%20OS%20Concepts.assets/image-20231205164630676.png)![](2_Fundamental%20OS%20Concepts.assets/image-20231205164646533.png)


## Thread Control Block
> [!concept]
> ![](2_Fundamental%20OS%20Concepts.assets/image-20231205175754744.png)



# Concept 2: Address Space
> [!concept]
> ![](2_Fundamental%20OS%20Concepts.assets/image-20231205180123495.png)![](2_Fundamental%20OS%20Concepts.assets/image-20231205180313828.png)



## Simple Protection: Base and Bound(B&B)
> [!concept] Limit the stretch of memory
> ![](2_Fundamental%20OS%20Concepts.assets/image-20231206223717315.png)
> In this first method, we will have two registers, base and bound, that limits the memory span of the process.
> 
> ![](2_Fundamental%20OS%20Concepts.assets/image-20231206223924002.png)
> When the program is loaded into the memory, it will be relocated by the operating system. Here the program counter is moving around the actual physical memory. The above method is called hardware base and bound.
> In the following second method, which is called software base and bound, apply address translation with base and bound. Here the program counter is still moving across the virtual memory space.
> 
> ![](2_Fundamental%20OS%20Concepts.assets/image-20231206224200473.png)


## x86 segments and stacks
> [!important]
> ![](2_Fundamental%20OS%20Concepts.assets/image-20231206225111992.png)
> `CS`: Register that points to the start of Code Section 
> `SS`: Register that points to the start of Static Data Section
> `EIP`: Register that points to the current instruction that's being executed.
> `ESP`: Register that points to the current data segment that's being accessed. 


## Address Space Translation
> [!concept]
> ![](2_Fundamental%20OS%20Concepts.assets/image-20231206225314297.png)![](2_Fundamental%20OS%20Concepts.assets/image-20231206225325095.png)![](2_Fundamental%20OS%20Concepts.assets/image-20231206225334688.png)
> **Remarks:**
> 1.  **What is the importance of address translation?**
> 	- Address translation is necessary for the idea of **virtual memory** which provides an **isolation abstraction.** 
> 	- This **gives the illusion that each process is the sole user of the address space.** 
> 	- It also provides **protection between different processes** since virtual addresses will not translate to the same physical address, preventing processes from accessing and potentially corrupting each other’s memory.
> 2. 



# Concept 3: Process
## Definition
> [!concept]
> A process is an execution environment with restricted rights. 
> 
> Each process has its own address space and resources such as code, global data, and files. 
> 
> Processes are protected from each other due to differing address spaces. If a bug were to corrupt a process, it would generally avoid compromising the entire system due to the protections from the address space.
> ![](2_Fundamental%20OS%20Concepts.assets/image-20231206225619441.png)![](2_Fundamental%20OS%20Concepts.assets/image-20231206230848609.png)![](2_Fundamental%20OS%20Concepts.assets/image-20231206230905327.png)![](2_Fundamental%20OS%20Concepts.assets/image-20240404170502562.png)








## Single and Multithreaded Processes
> [!important]
> ![](2_Fundamental%20OS%20Concepts.assets/image-20231206225818695.png)
> - All threads share a common heap.
> - Each thread has its own stack, which it can quickly add and remove items from. This makes stack based memory fast, but if you use too much stack memory, as occurs in infinite recursion, you will get a stack overflow.
> - Every thread has a separate stack, but it is not necessarily 'private'. Other threads are usually allowed to access it.
> - Since all threads share the same heap, access to the allocator/deallocator must be synchronized. There are various methods and libraries for avoiding [allocator contention](https://stackoverflow.com/questions/470683/memory-allocation-deallocation-bottleneck).
> - Some languages allow you to create private pools of memory, or individual heaps, which you can assign to a single thread.


## Process and Isolation
> [!concept]
> ![](2_Fundamental%20OS%20Concepts.assets/image-20231206230234819.png)







# Concept 4: Dual Mode Operation
## Kernel and User Mode
> [!concept]
> The underlying hardware that the OS interfaces with provides at least two modes: kernel and user. 
> 
> - **Kernel mode**, also known as **supervisor** or **privileged mode**, has the most privileges, meaning the kernel itself and other parts of the OS operate in this mode. 
> - **User mode** prohibits certain operations. This is where programs are normally executed. The restricted access is important in user mode to make sure processes running in user mode cannot maliciously corrupt another process.
> 
> ![](2_Fundamental%20OS%20Concepts.assets/image-20231206231210104.png)![](2_Fundamental%20OS%20Concepts.assets/image-20231206231458556.png)




## Mode Switching
> [!def]
> There are three main ways the system switches from a user mode to kernel mode (mode transfer). 
> - When processes request a system service, this is known as a **system call** (syscall). While similar to a function call, syscalls occur ”outside” the process, meaning it is executed in the kernel mode. Therefore, syscalls encompass functionality that requires the privileges or abstractions of being in the kernel mode. 
> - **Interrupts**, sometimes referred to as hardware interrupts, are external asynchronous events (e.g. timer, I/O) that trigger a mode switch (from user mode to kernel mode). 
> - **Traps**, also known as **exceptions** or software interrupts, are internal synchronous events (e.g. segmentation fault, divide by zero) that trigger a mode switch.
> 
> All three types of mode transfers are **unprogrammed control transfers**. Instead of the process specifying the specific address like in a regular function call, the process specifies an index into the **interrupt vector table (IVT)**, which is a table that contains the address and properties of each interrupt handler. The ”interrupt” in IVT is used as a general term that’s not just limited to the interrupts mentioned in the previous paragraph. 
> 
> The location of the IVT is stored in a designated processor register.
> ![](2_Fundamental%20OS%20Concepts.assets/image-20240404170653125.png)![](2_Fundamental%20OS%20Concepts.assets/image-20240404170659064.png)




## Calling Convention
> [!quiz] 
> **Similar to what’s done in the prologue at calling convention, what needs to happen before a mode transfer occurs?**
> 
> The processor’s state (e.g. registers) need to be saved in the thread control block (TCB) because the kernel may overwrite the registers when it executes its own code.


## Linux /dev/kmem file
> [!quiz]
> ![](2_Fundamental%20OS%20Concepts.assets/image-20240229163029614.png)



## Kernel Stack
> [!def]
> ![](2_Fundamental%20OS%20Concepts.assets/image-20240404170801333.png)



