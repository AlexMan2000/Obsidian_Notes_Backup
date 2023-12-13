# Operating System Concepts
## Supervisor Mode
> ![image.png](./OS_VM_I_O.assets/20231024_0926072073.png)


## Syscalls
> ![image.png](./OS_VM_I_O.assets/20231024_0926097010.png)



## Interrupts&Exception
> ![image.png](./OS_VM_I_O.assets/20231024_0926119903.png)![image.png](./OS_VM_I_O.assets/20231024_0926125602.png)




## Forking
> ![image.png](./OS_VM_I_O.assets/20231024_0926141146.png)

**Solution**![image.png](./OS_VM_I_O.assets/20231024_0926156305.png)


## Concept Check
> ![image.png](./OS_VM_I_O.assets/20231024_0926175324.png)



# Physical Memory and Storage
## CPU I/O Gap
> ![image.png](./OS_VM_I_O.assets/20231024_0926188843.png)



## Volatile Memory - RAM
> ![image.png](./OS_VM_I_O.assets/20231024_0926207498.png)
> **Two Types:**
> 1. **Static RAM(SRAM): **Used for cache, faster than DRAM
> 2. **Dynamic RAM(DRAM):** Used for main memory/ frame buffers.
> 
![image.png](./OS_VM_I_O.assets/20231024_0926216539.png)


### SRAM(Bistable)
> ![image.png](./OS_VM_I_O.assets/20231024_0926238060.png)![image.png](./OS_VM_I_O.assets/20231024_0926247795.png)![image.png](./OS_VM_I_O.assets/20231024_0926248262.png)
> **SRAM:**
> 1. Store bits as bi-state.
> 2. Stable against disturbance of voltage or power.



### DRAM(Volatile)
> ![image.png](./OS_VM_I_O.assets/20231024_0926251265.png)
> **DRAM:**
> 1. Store bits as charges on the capacitor.
> 2. Vulnerable to disturbance of voltage.




## Non-volatile Memories
> ![image.png](./OS_VM_I_O.assets/20231024_0926254284.png)



### Hard Disk
> ![image.png](./OS_VM_I_O.assets/20231024_0926277542.png)



#### Disk Structure
> ![image.png](./OS_VM_I_O.assets/20231024_0926297129.png)![image.png](./OS_VM_I_O.assets/20231024_0926306824.png)


#### Disk Capacity
> ![image.png](./OS_VM_I_O.assets/20231024_0926303995.png)![image.png](./OS_VM_I_O.assets/20231024_0926322875.png)![image.png](./OS_VM_I_O.assets/20231024_0926324990.png)![image.png](./OS_VM_I_O.assets/20231024_0926337220.png)



#### Seek Time
> ![image.png](./OS_VM_I_O.assets/20231024_0926349971.png)
> 就是`Disk Arm Head`移动到目标`Track`的时间，由`Arm`移动速度和硬盘转速决定。




#### Rotational Latency
> ![image.png](./OS_VM_I_O.assets/20231024_0926355116.png)




#### Transfer Time
> ![image.png](./OS_VM_I_O.assets/20231024_0926385865.png)
> 也就是一个划过某个特定的`Track`上的`Sector`需要多少秒。



 
#### Average Time to Access
> ![image.png](./OS_VM_I_O.assets/20231024_0926399415.png)![image.png](./OS_VM_I_O.assets/20231024_0926428562.png)![image.png](./OS_VM_I_O.assets/20231024_0926446111.png)



#### Logical Disk Block
> ![image.png](./OS_VM_I_O.assets/20231024_0926452427.png)




### 

### SSD
#### Definition
> ![image.png](./OS_VM_I_O.assets/20231024_0926467628.png)![image.png](./OS_VM_I_O.assets/20231024_0926467625.png)


#### Performance Metric
> ![image.png](./OS_VM_I_O.assets/20231024_0926473398.png)![image.png](./OS_VM_I_O.assets/20231024_0926495906.png)


#### Practices - P6.5
> ![image.png](./OS_VM_I_O.assets/20231024_0926498828.png)![image.png](./OS_VM_I_O.assets/20231024_0926513371.png)![image.png](./OS_VM_I_O.assets/20231024_0926523722.png)




### Flash Memory
> ![image.png](./OS_VM_I_O.assets/20231024_0926535735.png)


# Virtual Memory Basics
## Virtual&Physical Memory
> ![image.png](./OS_VM_I_O.assets/20231024_0926574710.png)![image.png](./OS_VM_I_O.assets/20231024_0926584292.png)


## Address Sapces
> ![image.png](./OS_VM_I_O.assets/20231024_0927003848.png)![image.png](./OS_VM_I_O.assets/20231024_0927028374.png)![image.png](./OS_VM_I_O.assets/20231024_0927028392.png)



## Memory Manager
> ![image.png](./OS_VM_I_O.assets/20231024_0927034384.png)




## Paged Memory
> ![image.png](./OS_VM_I_O.assets/20231024_0927043671.png)
> `offset bits`由`page size`决定，上文中`page size`是$4KiB=2^2\times 2^{10}=2^{12}B$, 所以需要`12 bit`来表示。
> ![image.png](./OS_VM_I_O.assets/20231024_0927072349.png)



## Example Computer
> ![image.png](./OS_VM_I_O.assets/20231024_0927084457.png)


## Summary
> [!concept]
> ![](OS_VM_I_O.assets/image-20231212140959467.png)




# VM as Caching - Page Table
## Page Table Structure
> ![image.png](./OS_VM_I_O.assets/20231024_0927109996.png)
> `Page Table`的每一项储存的是`Physical Memory Address`, 比如`0x02033244`(`32 bit memory`)
> ![image.png](./OS_VM_I_O.assets/20231024_0927112463.png)![image.png](./OS_VM_I_O.assets/20231024_0927131315.png)




## Accessing Pages
### Page Hit
> ![image.png](./OS_VM_I_O.assets/20231024_0927149880.png)



### Page Fault
> ![image.png](./OS_VM_I_O.assets/20231024_0927153775.png)![image.png](./OS_VM_I_O.assets/20231024_0927172942.png)![image.png](./OS_VM_I_O.assets/20231024_0927189711.png)



### Protection Fault
> ![image.png](./OS_VM_I_O.assets/20231024_0927203309.png)



### Handling Page Fault
> ![image.png](./OS_VM_I_O.assets/20231024_0927213003.png)![image.png](./OS_VM_I_O.assets/20231024_0927226709.png)![image.png](./OS_VM_I_O.assets/20231024_0927248852.png)![image.png](./OS_VM_I_O.assets/20231024_0927263803.png)



## Allocating Pages
> ![image.png](./OS_VM_I_O.assets/20231024_0927276729.png)



## Page Table Size
> ![image.png](./OS_VM_I_O.assets/20231024_0927282832.png)
> $4\times 2^{20}$**的由来:**
> 1. 首先前文介绍过我们使用`12 bits as offset bits`, `20 bits as VPN bits`。
> 2. 所以`Page Table`会有$2^{20}$个`Entries`，每个`Entry`中储存的是`32 bit Physical address`, 对应的大小是$\frac{32}{8}=4$bytes per entry.
> 3. 所以`Page Table Size`$=4\times 2^{20}B=4-MiB$。
> 
因为每一个进程都享有自己的`Page Table`, 进程数量一多，我们需要在内存中储存的页表数量就越多，所以我们需要有一种设计能够减轻因为进程数量增多导致的页表空间占用过大的问题。
> ![image.png](./OS_VM_I_O.assets/20231024_0927301044.png)



## Hierarchical Page Tables
> ![image.png](./OS_VM_I_O.assets/20231024_0927321301.png)![image.png](./OS_VM_I_O.assets/20231024_0927339175.png)
> 总的来说, `Level i-1 Page Table`points to `Start address of Level i Page Table`, `Level n Page Table`points to the physical memory address.
> ![image.png](./OS_VM_I_O.assets/20231024_0927364858.png)



# VM as Memory Management
## Process Isolation
> ![image.png](./OS_VM_I_O.assets/20231024_0927374177.png)![image.png](./OS_VM_I_O.assets/20231024_0927408868.png)


## Simplifying Linking and Loading
> ![image.png](./OS_VM_I_O.assets/20231024_0927413014.png)![image.png](./OS_VM_I_O.assets/20231024_0927427808.png)![image.png](./OS_VM_I_O.assets/20231024_0927443204.png)



# VM for Memory Protection
## Extended Page Table
> ![image.png](./OS_VM_I_O.assets/20231024_0927454403.png)



# VM Address Translation Procedure
> ![image.png](./OS_VM_I_O.assets/20231024_0927451738.png)![image.png](./OS_VM_I_O.assets/20231024_0927482980.png)



## Address Translation with Page Table
> ![image.png](./OS_VM_I_O.assets/20231024_0927516308.png)



### Page Hit
> ![image.png](./OS_VM_I_O.assets/20231024_0927538627.png)




### Page Fault
> ![image.png](./OS_VM_I_O.assets/20231024_0927545903.png)![image.png](./OS_VM_I_O.assets/20231024_0927554611.png)![image.png](./OS_VM_I_O.assets/20231024_0927574472.png)



## Translation Lookaside Buffers(TLB)
> ![image.png](./OS_VM_I_O.assets/20231024_0927593266.png)



### TLB Structure
> ![image.png](./OS_VM_I_O.assets/20231024_0928005715.png)



### Accessing TLB
> ![image.png](./OS_VM_I_O.assets/20231024_0928024365.png)



### TLB Hit
> ![image.png](./OS_VM_I_O.assets/20231024_0928047298.png)



### TLB Miss
> ![image.png](./OS_VM_I_O.assets/20231024_0928066583.png)![image.png](./OS_VM_I_O.assets/20231024_0928093179.png)

**Possible Reasons - Locality!**![image.png](./OS_VM_I_O.assets/20231024_0928106394.png)


### TLB in RISC-V DataPath
> ![image.png](./OS_VM_I_O.assets/20231024_0928124521.png)![image.png](./OS_VM_I_O.assets/20231024_0928157014.png)![image.png](./OS_VM_I_O.assets/20231024_0928167390.png)



### TLB Initialization
> ![image.png](./OS_VM_I_O.assets/20231024_0928174811.png)![image.png](./OS_VM_I_O.assets/20231024_0928192282.png)



## Full Address Translation Procedure
> ![image.png](./OS_VM_I_O.assets/20231024_0928218289.png)![image.png](./OS_VM_I_O.assets/20231024_0928248275.png)![image.png](./OS_VM_I_O.assets/20231024_0928279629.png)![image.png](./OS_VM_I_O.assets/20231024_0928283012.png)

![](./OS_VM_I_O.assets/20231024_0928307856.png)



# VM Performance Analysis
## Concept Reviews
> ![image.png](./OS_VM_I_O.assets/20231024_0928327156.png)


## AWAT Analysis
> ![image.png](./OS_VM_I_O.assets/20231024_0928342856.png)![image.png](./OS_VM_I_O.assets/20231024_0928354624.png)



# VM Concept Check
## Benefits of Using Virtual Memory
> ![image.png](./OS_VM_I_O.assets/20231024_0928377726.png)



## TLB Access Pattern
> ![image.png](./OS_VM_I_O.assets/20231024_0928382502.png)
> **总结:**
> 1. 首先计算`Page offset`和`VPN bits`。
> 
![image.png](./OS_VM_I_O.assets/20231024_0928403119.png)
> 2. 每次`Read/Write`完之后都需要更新所有的`LRU Bits + 1`
> 3. `Write`操作一般都需要设置`Dirty Bit`为`1`, 因为`TLB`没有和`PTE`同步。

**First Access**![image.png](./OS_VM_I_O.assets/20231024_0928418319.png)
**Second Access - Kick and Create Entry**![image.png](./OS_VM_I_O.assets/20231024_0928427356.png)
**Third Access**![image.png](./OS_VM_I_O.assets/20231024_0928436714.png)
写入`0x20`这一行，需要设置`Dirty bit`为`1`。
**Fourth Access**![image.png](./OS_VM_I_O.assets/20231024_0928447263.png)
**Fifth Access**![image.png](./OS_VM_I_O.assets/20231024_0928467582.png)
**Sixth Access**![image.png](./OS_VM_I_O.assets/20231024_0928485471.png)
**Final TLB and Review**![image.png](./OS_VM_I_O.assets/20231024_0928503333.png)


# I/O Devices
## I/O Polling(轮询)
### Definition
> ![image.png](./OS_VM_I_O.assets/20231024_0928523416.png)![image.png](./OS_VM_I_O.assets/20231024_0928541903.png)![image.png](./OS_VM_I_O.assets/20231024_0928557420.png)
> 使用一个`bit`来标记`I/O`设备是否允许进行`I/O`操作，处理器不断循环查看这个`bit`的值，如果在某个循环内`bit`**被**`**I/O**`**设备设置**为了`1`, 则表明处理器可以对`I/O`设备进行读写操作。
> **一个形象的类比就是: **我在餐厅点餐，我在拿好号之后一直不断的询问服务员好了没，直到得到肯定的回答。



### Cost of Polling
> ![image.png](./OS_VM_I_O.assets/20231024_0928568402.png)



#### Polling Mouse
> ![image.png](./OS_VM_I_O.assets/20231024_0928585391.png)
> 可以看到在一秒钟的时间内，`Polling Mouse`占用的时钟数不是很多。
> 由于鼠标的点击事件实际上在一秒的尺度内不会发生超过`30`次（除非你使用机械臂），我们的轮询次数不需要太多，一秒钟内$30$次就可以。




#### Polling Hard Disk
> ![image.png](./OS_VM_I_O.assets/20231024_0929005776.png)
> 由于硬盘在读取的过程中会不断的产生数据，所以我们需要经常轮询看看有没有新的数据可供读取。
> 假设一秒钟就有$16MB$的新鲜数据产出。此时如果我们一次轮询接收$16B$的数据，则一秒内需要$1\times 10^6$次轮询，这会导致处理器处理其他任务的时间被严重侵占。



## I/O Interrupts(中断)
> ![image.png](./OS_VM_I_O.assets/20231024_0929029402.png)![image.png](./OS_VM_I_O.assets/20231024_0929042243.png)
> 对于那些不经常发送信号数据的设备(比如鼠标和键盘)来说，操作系统一般使用`Interrupts`而不是`Polling`。




## Concept Check
> ![image.png](./OS_VM_I_O.assets/20231024_0929064402.png)



## RISC-V Code Implementations
> ![image.png](./OS_VM_I_O.assets/20231024_0929109621.png)
> 这里`Control Register`的地址是`0x7ffff`, 然后我们使用`lw`获取这个`register`的值，和`1`作比较，如果`register`的值是`0`则结果为`0`此时不能进行`I/O`读写，再次循环。![image.png](./OS_VM_I_O.assets/20231024_0929122423.png)

**Solution**![image.png](./OS_VM_I_O.assets/20231024_0929121482.png)![image.png](./OS_VM_I_O.assets/20231024_0929132080.png)


# Direct Memory Access(DMA)
## Improvements
> ![image.png](./OS_VM_I_O.assets/20231024_0929142367.png)
> `DMA`使得`I/O`设备和内存设备的交互过程不需要中央处理器的直接接入。处理器只需要在一开始把任务交代给`I/O`设备和内存设备，告诉他们处理器最终需要什么样的数据就行。处理器只需要把任务布置下去即可。完成后由`DMA Controller`打断处理器。总的来说，处理器只需要在任务开始和结束两次询问(下图中的`1`和`5`)数据即可，省下不少时间。
> ![image.png](./OS_VM_I_O.assets/20231024_0929152389.png)



## Procedure Logic
> ![image.png](./OS_VM_I_O.assets/20231024_0929173871.png)![image.png](./OS_VM_I_O.assets/20231024_0929194524.png)



## Where to put DMA?
> ![image.png](./OS_VM_I_O.assets/20231024_0929219436.png)
> `Coherency`: 就是数据不一致的问题。因为`Cache`由`Write-Back`和`Write-Through Policy`所以我们不需要担心`Data Coherency`的问题。




# Bus Structure
## Overview
> ![image.png](./OS_VM_I_O.assets/20231024_0929212769.png)




## Main Memory Read
> ![image.png](./OS_VM_I_O.assets/20231024_0929233814.png)![image.png](./OS_VM_I_O.assets/20231024_0929244837.png)![image.png](./OS_VM_I_O.assets/20231024_0929256169.png)



## Main Memory Write
> ![image.png](./OS_VM_I_O.assets/20231024_0929267268.png)![image.png](./OS_VM_I_O.assets/20231024_0929278893.png)![image.png](./OS_VM_I_O.assets/20231024_0929296217.png)



## I/O Bus
> ![image.png](./OS_VM_I_O.assets/20231024_0929302989.png)



## Disk Read
> ![image.png](./OS_VM_I_O.assets/20231024_0929317272.png)![image.png](./OS_VM_I_O.assets/20231024_0929331473.png)![image.png](./OS_VM_I_O.assets/20231024_0929358009.png)


