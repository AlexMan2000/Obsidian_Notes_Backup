# Task 1: Argument Passing
> See https://www.youtube.com/watch?v=RbsE0EQ9_dY

## Overview
> [!task]
> ![](Project1_Userprogram.assets/image-20240517134642520.png)![](Project1_Userprogram.assets/image-20240517134558371.png)



## Functions to modify
> [!important]
> ![](Project1_Userprogram.assets/image-20240517134612569.png)



## Tokenizing
> [!important]
> Function provided by `stdlib.c`
> ![](Project1_Userprogram.assets/image-20240517144939986.png)



## Interruption Frame
> [!important]
> ![](Project1_Userprogram.assets/image-20240517145033003.png)![](Project1_Userprogram.assets/image-20240517145047384.png)
> The above is the virtual address space of the operating system.
> - If we are in user space, when we call `int N`, the operating system will push the user program's registers' values onto interrupt frame and set the `esp` to be the top of the kernel stack. **In short, it saves all the registers onto the interrupt frame and suspend the user space execution.**
> - If we are in kernel space, to trap into the user space, we have to initialize a interrupt frame to save the kernel register values and also when we call `iret`, the operating system will set the `esp` to be the top of the user stack. **In short, it resumes user space execution**
> - The operating system will initialize a new interrupt frame for each newly created thread. Once created, it serves as register saving purposes to hold everything the user program need to resume execution.




### Get into the kernel
> [!important]
> ![](Project1_Userprogram.assets/image-20240517150249767.png)![](Project1_Userprogram.assets/image-20240517150411175.png)



### Get out of Kernel
> [!important]
> ![](Project1_Userprogram.assets/image-20240517150601047.png)![](Project1_Userprogram.assets/image-20240517151719458.png)





## Function Calling Convention
> [!important]
> ![](Project1_Userprogram.assets/image-20240517161834952.png)![](Project1_Userprogram.assets/image-20240517172601284.png)![](Project1_Userprogram.assets/image-20240517173955944.png)
> Since each time we start a new kernel thread to to execute a program, 




## Code Implementations





# Task 2: Syscall

