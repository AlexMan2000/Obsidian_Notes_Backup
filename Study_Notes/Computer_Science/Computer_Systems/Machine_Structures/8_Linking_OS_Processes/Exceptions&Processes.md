# Exceptions
## Definition
> [!Definition]
> An exception is an `abrupt change in the control flow in response to some change in the processor’s state`.
> ![](Exceptions&Processes.assets/image-20231024152705741.png)
> 

## Exception Table
> [!info]
> **Each type of possible exception** in a system is assigned a *unique nonnegative integer exception number*. Some of these numbers are assigned by the designers of the processor. Other numbers are assigned by the designers of the operating system kernel (the memory-resident part of the operating system). 
> Examples of the former includes:
> - Divide by zero, 
> - Page faults, 
> - Memory access violations, 
> - Break- points,
> - Arithmetic overflows. 
> 
> Examples of the latter include:
> - System calls.
> - Signals from external I/O devices.
> 
> 下面的`Exception Table`在电脑开机时由操作系统设置并初始化，表中的每一项都是`Exception Handler`的地址。
>
> ![](Exceptions&Processes.assets/image-20231024152849399.png)
> 在程序运行时，如果`Processor`检测到其`Processor State`发生改变了，即某些事件发生了，则他会先决定这个`Exception Number k`, 然后结合`Exception Table`的`Base Register`(表格的起始地址)求出我们具体要调用的那一个`Exception Handler`的地址，然后跳转进入内核态。



# Classes of Exceptions
> [!info]
> ![](Exceptions&Processes.assets/image-20231024154608382.png)
> Exception 和 Procedure Call 的逻辑很类似，都是调用一个例程，但是有一些重要的区别:
> - 在调用异常之前的准备工作，比如将返回地址压入栈内存中，是一致的。只是取决于异常的类别，在异常程序执行完毕后，我们有可能返回到当前指令（比如`Fault`）, 也有可能返回到下一条指令，比如`Traps, I/O Interrupts`等。也有可能永远不返回而直接停止程序。但是`Procedure Call`永远会返回到下一条指令。
> - 处理器会往栈上放入一些额外的数据以保证我们从`Exception Handler`返回到用户程序时候顺利地从之前中断的地方开始继续执行指令。
> - `Exception Handler`全程运行在内核态。


## Asychronous Exceptions
> [!Definition]
> `Asychronous` 意味着`Exception`的触发不是由处理器显式地执行某条指令导致的。换句话说，是`I/O`设备读取数据完毕并告知`CPU`的时候改变`Processor State(Interrupt Pin)`而触发。最常见的`Asychronous Exception`就是`Interrupts`。下图中展示了`Interrupt`的全过程:
> - 在当前指令$I_{curr}$ 执行的过程中，`Interrupt Pin`被某个`I/O` 设备设置成了`1` (高电压)。
> - 当前指令执行完毕之后，处理器注意到自己的`Processor State`被修改了，于是知道有事件被触发了，于是从`System Bus`上读取到`Exception Number`并查表调用对应的`Exception Handler`进入内核态。
> - 执行完后返回到$I_{next}$ 继续执行剩下的指令，就好像`Interrupt`从外发生过一样。
>
> ![](Exceptions&Processes.assets/image-20231024155042029.png)
> ![](Exceptions&Processes.assets/image-20231024155412189.png)


## Synchronous Exceptions
> [!Definition]
> ![](Exceptions&Processes.assets/image-20231024155845334.png)



### Traps
> [!info]
> User programs often need to `request services from the kernel` such as:
> 1. Reading a file (**fread**)
> 2. Creating a new process (**fork**)
> 3. Loading a new program (**execve**) 
> 4. Terminating the current process (**exit**). 
> 
> To allow controlled access to such kernel services, processors provide a special `syscall n` instruction that user programs can execute when they want to request service n. Executing the syscall instruction causes a trap to an exception handler that decodes the argument and calls the appropriate kernel routine. 
> ![](Exceptions&Processes.assets/image-20231024160111021.png)

> [!Attention]
> From a programmer’s perspective, a system call is identical to a regular function call. However, their implementations are quite different. 
> - Regular functions run in `user mode`, which restricts the types of instructions they can execute, and they access the same stack as the calling function. 
> - A system [call](CALL.md) runs in `kernel mode`, which allows it to execute privileged instructions and access a stack defined in the kernel. 







### Faults
> [!info]
> Faults result from `error conditions that a handler might be able to correct`. When a fault occurs, the processor transfers control to the fault handler. 
> - If the handler can correct the error condition, it returns control to the faulting instruction, `re-executing` it. 
> - Otherwise, the handler returns to an abort routine in the kernel that `terminates the application program` that caused the fault. 
> 
> ![](Exceptions&Processes.assets/image-20231024164357716.png)



### Aborts
> [!info]
> Aborts result from `unrecoverable fatal errors`, typically hardware errors such as parity errors that occur when DRAM or SRAM bits are corrupted. 
> Abort handlers `never return control to the application program`.




# Exceptions in Linux X86-64 
## Linux Faults/Aborts
> ![](Exceptions&Processes.assets/image-20231024171337871.png)![](Exceptions&Processes.assets/image-20231024171351796.png)![](Exceptions&Processes.assets/image-20231024171357550.png)




## Linux System Calls
> ![](Exceptions&Processes.assets/image-20231024171258828.png)![](Exceptions&Processes.assets/image-20231024171317581.png)



# Process
## Overview
> [!Definition]
> ![](Exceptions&Processes.assets/image-20231024171753323.png)


## Logic Control Flow
> A



## Concurrent/Parallel Flow
> ![](Exceptions&Processes.assets/image-20231024185728801.png)![](Exceptions&Processes.assets/image-20231024190020373.png)




