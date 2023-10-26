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



## Physical Control Flow
> [!info]
> - `Physical Control Flow` refers to the actual sequence in which instructions are executed by the hardware, especially in modern processors. 这些指令集可能来自多个`Processes`，互相交错。
> - Due to optimizations like **pipelining, out-of-order execution, and branch prediction**, the physical order in which instructions are executed can differ significantly from the logical order. 
> - These optimizations are done to improve the **throughput and performance** of the processor. For instance, while waiting for data from memory (which can be relatively slow), a modern CPU might execute other independent instructions that come later in the logical sequence.
> - <span style="background:#fff88f">The CPU ensures that, despite the changes in the order of execution, the final outcomes (values in memory and registers) are as if the instructions were executed in the logical order.</span>


## Logic Control Flow
> [!def]
> `Logic Flow`是针对某个`Process`而言的，可以理解成逻辑上畅通的一段代码翻译成的指令集。
> ![](Exceptions&Processes.assets/image-20231025100933917.png)
> 上图中的`Logic Control Flow`就是每个`Process`各自的指令集按照时间轴方向排列的结果。将这些短小的黑线平移到一起后就组成了`Physical Control Flow`，也就是`CPU` 实际上的指令执行顺序。
> 上图中还反映出了一个现象，就是`CPU`总是会在不同的`Process`之间来回快速切换，一会儿执行`Process A`的`Logic Flow`, 一会执行`Process B`的`Logic Flow`， 但是`CPU`会保证最终多个`Process`的运行结果和`CPU`只顺序执行一个`Process`的结果完全一致。



## Concurrent/Parallel Flow
> [!def]
> ![](Exceptions&Processes.assets/image-20231024185728801.png)![](Exceptions&Processes.assets/image-20231024190020373.png)
> - `Concurrency`是并发的意思，表示处理器来回切换任务，宏观上看好像是在同时进行很多任务一样。也成为`Multitasking`。
> - `Parallelism`是并行的意思，表示有多个处理器在同时进行任务，是真正的多任务处理。

> [!example]
> ![](Exceptions&Processes.assets/image-20231026102226550.png)
> 判断两个进程是否并发运行，只需要观察他们的`Logic Control Flow`是否有重叠，上图中:
> 1. A和B有重叠，并发运行
> 2. B和C有重叠，并发运行
> 3. A和C无重叠，顺序执行


## User and Kernel Mode
> [!def]
> Processors typically provide this capability with a `mode bit` in some `control register` that characterizes the privileges that the process currently enjoys. 
> - **When the mode bit is set**, the process is running in kernel mode (sometimes called supervisor mode). A process running in kernel mode can execute any instruction in the instruction set and access any memory location in the system.
> - **When the mode bit is not set**, the process is running in user mode. A process in user mode is not allowed to execute privileged instructions that do things such as halt the processor, change the mode bit, or initiate an I/O operation. Nor is it allowed to directly reference code or data in the kernel area of the address space. Any such attempt results in a fatal protection fault. User programs must instead access kernel code and data indirectly via the system call interface. 
> - **A process running application code is initially in user mode**. The only way for the process to change from user mode to kernel mode is via an exception such as an interrupt, a fault, or a trapping system call. 
> - **When the exception occurs**, and control passes to the exception handler, the processor changes the mode from user mode to kernel mode. `The handler runs in kernel mode`. When it returns to the application code, the processor changes the mode from kernel mode back to user mode.

> [!example]
> - Linux provides a clever mechanism, called the /proc filesystem, that allows user mode processes to access the contents of kernel data structures. 
> - The /proc filesystem exports the contents of many kernel data structures as a hierarchy of text files that can be read by user programs. 
> - For example, you can use the /proc filesys- tem to find out general system attributes such as CPU type (/proc/cpuinfo), or the memory segments used by a particular process (/proc/process-id/maps). The 2.6 version of the Linux kernel introduced a /sys filesystem, which exports addi- tional low-level information about system buses and devices.


## Private Address Space
> [!def]
> 对于每一个进程来说，他们都有自己的私有地址范围`0x00000000~0xffffffff`, 有自己的栈内存，堆内存，`Code`区，`Data`区，以及各种寄存器。但是注意，这些私有地址和寄存器看起来是`Exclusive Access`, 实际上是由操作系统调度完成，为每个进程分配内存和寄存器。让进程感觉自己坐拥着所有程序执行所需的内存和处理器资源。
> 下图展示了这一点。
> ![](Exceptions&Processes.assets/image-20231026102942972.png)



## Context Switches
> [!def]
> ![](Exceptions&Processes.assets/image-20231026110039145.png)
> 在`Context Switching` 的过程中，`Process A`的所有用于确定程序运行状态(确保程序能从中断的位置继续执行)的资源都会被保存起来，包括内存资源，寄存器上的值。然后`Processor`进入`Kernel Mode`进行`Context Switching from Process A to Process B`，切换好之后`Processor`进入用户模式执行`Process B`。



# Process Control
> 本章节非常重要，涉及到进程控制的诸多概念。

## Obtaining Process ID
```ad-code
在操作系统中，每个进程都有自己的独一无二的`ID`, 称为`Processor ID`(PID)，我们可以通过`getpid()`获取调用这个函数的进程，通过`getppid()`获取调用这个进程的进程，也就是父进程。
```
```c 
#include <sys/types.h> 
#include <unistd.h> 
pid_t getpid(void); 
pid_t getppid(void);
```

