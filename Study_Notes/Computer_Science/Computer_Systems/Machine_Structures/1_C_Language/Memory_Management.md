# Addressing and Endianness
## Addresses
> ![image.png](./Memory_Management.assets/20231023_2305565757.png)



## Endianness
> ![image.png](./Memory_Management.assets/20231023_2305583441.png)



### Big Endian
> ![image.png](./Memory_Management.assets/20231023_2305598883.png)![image.png](./Memory_Management.assets/20231023_2306018971.png)



### Little Endian
> ![image.png](./Memory_Management.assets/20231023_2306039936.png)![image.png](./Memory_Management.assets/20231023_2306047123.png)




### Common Mistakes
> ![image.png](./Memory_Management.assets/20231023_2306077180.png)



### Difference between OS
> ![image.png](./Memory_Management.assets/20231023_2306094020.png)![image.png](./Memory_Management.assets/20231023_2306101294.png)



## Code for Endinaness
> ![image.png](./Memory_Management.assets/20231023_2306121077.png)![image.png](./Memory_Management.assets/20231023_2306148766.png)

```c
typedef unsigned char *pointer;
void show_bytes(pointer start, size_t len){
     size_t i;
     for (i = 0; i < len; i++)
     printf(”%p\t0x%.2x\n",start+i, start[i]);
     printf("\n");
} 
```

## Representing Pointers
> ![image.png](./Memory_Management.assets/20231023_2306154998.png)


## Representing Strings
> ![image.png](./Memory_Management.assets/20231023_2306172639.png)
> `**Endianness**`**only takes effect on multi-byte objects.**


### String Storation Exercise
> **Sp23 Disc02**
> ![image.png](./Memory_Management.assets/20231023_2306187520.png)![image.png](./Memory_Management.assets/20231023_2306201564.png)![image.png](./Memory_Management.assets/20231023_2306216675.png)![image.png](./Memory_Management.assets/20231023_2306238915.png)



# C Memory Layout
## Memory Layout/Sectors
> ![image.png](./Memory_Management.assets/20231023_2306241397.png)![image.png](./Memory_Management.assets/20231023_2306269881.png)![image.png](./Memory_Management.assets/20231023_2306286625.png)



## Stack
> ![image.png](./Memory_Management.assets/20231023_2306302381.png)![image.png](./Memory_Management.assets/20231023_2306328403.png)
> 注意，当例程执行结束后，仅仅是`SP`指向的内存地址发生变化(向上缩减)，例程活跃期间的局部变量仍然存在于原来的栈帧中，可以访问到，详见下面的例子:
> ![image.png](./Memory_Management.assets/20231023_2306338920.png)
> 这里第一个`printf`调用时，由`ptr()`函数调用产生的栈帧中的局部变量`y=3`依然能够被`printf`访问到。但是在调用第二次时，调用`printf()` 产生的栈帧会将`y`的位置覆盖掉，无法用指针解引用访问内容。
> ![image.png](./Memory_Management.assets/20231023_2306356021.png)



## Static Data
> ![image.png](./Memory_Management.assets/20231023_2306373103.png)![image.png](./Memory_Management.assets/20231023_2306385398.png)



## Code(Text)
> ![image.png](./Memory_Management.assets/20231023_2306398963.png)![image.png](./Memory_Management.assets/20231023_2306417724.png)



## Heap
> ![image.png](./Memory_Management.assets/20231023_2306435117.png)![image.png](./Memory_Management.assets/20231023_2306442718.png)![image.png](./Memory_Management.assets/20231023_2306447690.png)![image.png](./Memory_Management.assets/20231023_2306462672.png)![image.png](./Memory_Management.assets/20231023_2306485163.png)



## Summary⭐⭐⭐⭐⭐
> ![image.png](./Memory_Management.assets/20231023_2306491607.png)![image.png](./Memory_Management.assets/20231023_2306512526.png)



# Dynamic Memory Allocation
## Heap Management
> ![image.png](./Memory_Management.assets/20231023_2306526508.png)![image.png](./Memory_Management.assets/20231023_2306548360.png)![image.png](./Memory_Management.assets/20231023_2306573320.png)



## Malloc/Calloc/Realloc
### Basics
> ![image.png](./Memory_Management.assets/20231023_2306582351.png)
> 分配`char*`的时候要注意，需要分配`strlen + 1`的长度给`0 terminator`用。
> ![image.png](./Memory_Management.assets/20231023_2307009893.png)![image.png](./Memory_Management.assets/20231023_2307021802.png)![image.png](./Memory_Management.assets/20231023_2307057143.png)



### Tips when using realloc
> The point to note is that **realloc() should only be used for dynamically allocated memory**. If the memory is not dynamically allocated, then behavior is undefined.

```c
#include <stdio.h>
#include <stdlib.h>
int main()
{
int arr[2], i;
int *ptr = arr;
int *ptr_new;
	
arr[0] = 10;
arr[1] = 20;	
	
// incorrect use of new_ptr: undefined behaviour
ptr_new = (int *)realloc(ptr, sizeof(int)*3);
*(ptr_new + 2) = 30;
	
for(i = 0; i < 3; i++)
	printf("%d ", *(ptr_new + i));

getchar();
return 0;
}

```
```c
#include <stdio.h>
#include <stdlib.h>
int main()
{
int *ptr = (int *)malloc(sizeof(int)*2);
int i;
int *ptr_new;
	
*ptr = 10;
*(ptr + 1) = 20;
	
ptr_new = (int *)realloc(ptr, sizeof(int)*3);
*(ptr_new + 2) = 30;
for(i = 0; i < 3; i++)
	printf("%d ", *(ptr_new + i));

getchar();
return 0;
}

```
> **What will realloc do to the old pointer?**
> - Realloc will copy the content of the old pointer.
> - Pointer `a` still point to the same address, but the content is changed.
> - That's because realloc() may first try to increase the size of the block that `a` points to. However, it can instead allocate a new block, copy the data (or as much of the data as will fit) to the new block, and free the old block. You really shouldn't use `a` after calling `b = realloc(a, 200000 * sizeof(int))` since the realloc call may move the block to a new location, leaving a pointing to memory that is no longer allocated. Use `b` instead.




## Free
> ![image.png](./Memory_Management.assets/20231023_2307069959.png)




## Malloc/Free Implementation
> ![image.png](./Memory_Management.assets/20231023_2307087013.png)![image.png](./Memory_Management.assets/20231023_2307096172.png)![image.png](./Memory_Management.assets/20231023_2307111062.png)![image.png](./Memory_Management.assets/20231023_2307139331.png)



# Memory Management Failure
## Using Uninitialized Values
> ![image.png](./Memory_Management.assets/20231023_2307147447.png)



## Using Memory You Don't Own
> ![image.png](./Memory_Management.assets/20231023_2307164140.png)![image.png](./Memory_Management.assets/20231023_2307181005.png)![image.png](./Memory_Management.assets/20231023_2307207600.png)



## Using Memory You Haven's Allocated
> ![image.png](./Memory_Management.assets/20231023_2307217953.png)![image.png](./Memory_Management.assets/20231023_2307264978.png)![image.png](./Memory_Management.assets/20231023_2307272574.png)




## Returning Pointers into Stack
> ![image.png](./Memory_Management.assets/20231023_2307287644.png)
> 这里第一次调用`printf`的时候，由于



## Freeing Invalid Memory
> ![image.png](./Memory_Management.assets/20231023_2307301955.png)



## Memory Leaks
> ![image.png](./Memory_Management.assets/20231023_2307302970.png)![image.png](./Memory_Management.assets/20231023_2307329673.png)



# Linked List Example
## Struct
> ![image.png](./Memory_Management.assets/20231023_2307322670.png)



## Add Node to the Front
> ![image.png](./Memory_Management.assets/20231023_2307344278.png)![image.png](./Memory_Management.assets/20231023_2307366048.png)![image.png](./Memory_Management.assets/20231023_2307378791.png)![image.png](./Memory_Management.assets/20231023_2307383455.png)![image.png](./Memory_Management.assets/20231023_2307409139.png)![image.png](./Memory_Management.assets/20231023_2307412576.png)



## Delete First Node
> ![image.png](./Memory_Management.assets/20231023_2307432393.png)



# Exercises
> **Fa20 Disc02**
> ![image.png](./Memory_Management.assets/20231023_2307446742.png)



## Initialize variables on heap
> ![image.png](./Memory_Management.assets/20231023_2307468302.png)![image.png](./Memory_Management.assets/20231023_2307477147.png)



## Debug Memory  - Buffer Overflow
> ![image.png](./Memory_Management.assets/20231023_2307492992.png)![image.png](./Memory_Management.assets/20231023_2307513261.png)



## Linked List Memory Allocation/Free
> ![image.png](./Memory_Management.assets/20231023_2307521455.png)



### prepend
> ![image.png](./Memory_Management.assets/20231023_2307529326.png)![image.png](./Memory_Management.assets/20231023_2307543955.png)



### free_ll - Recursive
> ![image.png](./Memory_Management.assets/20231023_2307555332.png)![image.png](./Memory_Management.assets/20231023_2307569208.png)![image.png](./Memory_Management.assets/20231023_2307587289.png)
> 注意，第`6`行的步骤不是必须的，仅仅是为了防止我们后续修改这个地址的内容。因为当一个指针的地址被设置为`NULL`后就不具有`write`的功能了。


