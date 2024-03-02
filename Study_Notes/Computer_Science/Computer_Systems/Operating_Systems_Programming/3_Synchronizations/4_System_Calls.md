# System Calls
> [!concept]
> ![](System_Calls.assets/image-20231229110648752.png)




# System Calling Conventions
> [!concept]
> ![](System_Calls.assets/image-20231229111304102.png)![](System_Calls.assets/image-20231229111323839.png)![](System_Calls.assets/image-20231229111418387.png)
> - The user function call and return protocol, however, does little to encapsulate and privatize the memory used by a function. 
> - Consider, for instance, the execution of **loadFiles** as per the diagram below. Because **loadFiles**'s stack frame is directly below that of its caller, it can use pointer arithmetic to advance beyond its frame and examine—or even update— the stack frame above it. 
> - After **loadFiles** returns, **main** could use pointer arithmetic to descend into the ghost of **loadFiles**'s stack frame and access data **loadFiles** never intended to expose. Because incrementing stack pointer doesn't wipe out the data in the frame.
> - Functions are supposed to be modular, but the function call and return protocol's support for modularity and privacy is pretty soft.
> 
> ![](System_Calls.assets/image-20231229111932850.png)
> - The relevant opcode is placed in **%rax**. Each system call has its own opcode (e.g. 0 for **read**, 1 for **write**, 2 for **open**, 3 for **close**, 4 for **stat**, and so forth). 
> - The system call arguments—there are at most 6—are evaluated and placed in **%rdi, %rsi, %rdx, %r10, %r8,** and **%r9**. ==Note the fourth parameter is %r10, not %rcx==. **Note that by design, there are no system calls with more than six input parameters.**
> - The system issues a software interrupt (otherwise known as a trap) by executing **syscall,** which prompts an interrupt **handler** to execute in superuser mode. 
> - The interrupt handler builds a frame in the kernel stack, executes the relevant code, places any return value in %rax, and then executes iretq to return from the interrupt handler, revert from superuser mode, and execute the instruction following the syscall.
> - If **%rax** is negative, **errno** is set to abs(**%rax**) and **%rax** is updated to contain a ­**-1**. If **%rax** is nonnegative, it's left as is. The value in is **%rax** then extracted by the caller as any return value would be.


## Two Stacks Per Process
> [!important]
> ![](4_System_Calls.assets/image-20240229160520352.png)![](4_System_Calls.assets/image-20240229160531478.png)



## Mode Transfer
> [!important]
> First, we provide some background on the x86 architecture. The x86 is segmented, so 
> 1. Pointers come in two parts:
> 	1. A **segment**, a region of memory such as code, data, or stack.
> 	2. An **offset within that segment**. The current user-level instruction is a combination of the code segment (cs register) plus the instruction pointer (eip register). Likewise, the current stack position is the combination of the stack segment (ss) and the stack pointer within the stack segment (esp). 
> 	3. For example, to represent a pointer(address), we write `SS:ESP` for stack pointer, and `CS:EIP` for instruction pointer.
> 2. The **current privilege level** is stored as the **low-order bits of the cs register** rather than in the processor status word (eflags register). 
> 3. The **eflags register** has condition codes that are modified as a by-product of executing instructions; the eflags register also has other flags that control the processor’s behavior, such as whether interrupts are masked or not.


### Before System Call
> [!concept]
> ![](4_System_Calls.assets/image-20240229161245588.png)



### Prologue of Syscall Handler
> [!concept]
> When a processor exception or system call trap occurs, the hardware carefully saves a small amount of the interrupted thread state:
> ![](4_System_Calls.assets/image-20240229161507405.png)![](4_System_Calls.assets/image-20240229161617905.png)
> 
> The handler must first save the rest of the interrupted process’s state — it needs to save the other registers before it changes them! The handler pushes the rest of the registers, including the current stack pointer, onto the stack using the x86 pushad instruction.
> ![](4_System_Calls.assets/image-20240229161805669.png)
> The handler must then save the rest of the interrupted process’s state — it needs to save the other registers before it changes them! The handler pushes the rest of the registers, including the current stack pointer, onto the stack using the x86 pushad instruction.
> 
> Once the handler has saved the interrupted thread’s state to the stack, it can use the registers as it pleases, and it can push additional items onto the stack. So, the handler can now do whatever work it needs to do.


### After System Call
> [!concept]
> ![](4_System_Calls.assets/image-20240229162218359.png)







## Syscall Handler
> [!def]
>![](4_System_Calls.assets/image-20240229155246755.png) 
> **How does the syscall handler protect the kernel from corrupt or malicious user code?**
> 
> When executing a syscall, the user program specifies an index instead of the direct address of the handler, meaning the user program cannot directly execute in kernel mode. 
> 
> The **arguments will be <font color="#d83931">validated</font>** by the handler to make sure the user is not intending a malicious attack. Moreover, the handler will **<font color="#d83931">copy over the arguments instead of using them</font>** from the user stack directly. 
> 
> This is necessary because the user program could change the arguments after the handler performs initial checks for malicious purposes (i.e. https://en.wikipedia.org/wiki/Time-of-check_to_time-of-use ). 
> 
> After the syscall finishes, the results are **copied back** in to user memory. The user process is not allowed to access the results stored in kernel memory for security reasons.




