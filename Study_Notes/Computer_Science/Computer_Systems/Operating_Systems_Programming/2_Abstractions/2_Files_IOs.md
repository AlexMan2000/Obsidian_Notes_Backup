Also see [System_Level_IO](../../Machine_Structures/8_Linking_OS_Processes/System_Level_IO.md)
# I/O and Storage Layers
## File System Abstraction
> [!def]
> ![](2_Files_IOs.assets/image-20240229171219347.png)




## CWD
> [!def]
> ![](2_Files_IOs.assets/image-20240229171225014.png)




## Layered Design
> [!concept]
> ![](2_Files_IOs.assets/image-20240229171243454.png)








## Life Cycle of I/O Request
> [!important]
> ![](2_Files_IOs.assets/image-20240403125210668.png)





# C High-Level File API
> [!def]
> ![](2_Files_IOs.assets/image-20240229171357642.png)![](2_Files_IOs.assets/image-20240229171416742.png)



## Char-by-Char I/O
> [!concept]
> ![](2_Files_IOs.assets/image-20240229171447122.png)


## Block-by-Block I/O
> [!concept]
> ![](2_Files_IOs.assets/image-20240229171507969.png)![](2_Files_IOs.assets/image-20240229171524136.png)



## Summary
> [!summary]
> ![](2_Files_IOs.assets/image-20240403123726541.png)![](2_Files_IOs.assets/image-20240403123733051.png)





# C Low-Level File I/O
> [!concept]
> ![](2_Files_IOs.assets/image-20240229171559114.png)
> We don't want the user program somehow use that pointer to directly access the kernel memory address. No way to access something that you are not supposed to. Kernel immediately check the number that you put in the argument register.
> 
> 


## File Descriptors
> [!concept]
> Also see [File_System_Design from Stanford CS110](../6_Filesystem/Unix_V6_File_Systems/File_System_Design.md)
> ![](2_Files_IOs.assets/image-20240229172756710.png)




## Low-Level File API
> [!def]
> ![](2_Files_IOs.assets/image-20240229173213518.png)
> Reading Less refers to short count problem, details see [Short Counts](../../Machine_Structures/8_Linking_OS_Processes/System_Level_IO.md#Short%20Counts)
> 
> ![](2_Files_IOs.assets/image-20240229173742103.png)
> 

> [!example] CS162 Fa20 Disc02 P2.2
> ![](2_Files_IOs.assets/image-20240406144504484.png)




## POSIX Design Pattern
> [!def]
> ![](2_Files_IOs.assets/image-20240229173917964.png)![](2_Files_IOs.assets/image-20240229173924452.png)
> More details see 




## Summary
> [!summary]
> ![](2_Files_IOs.assets/image-20240403123639795.png)![](2_Files_IOs.assets/image-20240403123658776.png)




## Exercises
### lseek
> [!example] CS162 Fa20 Disc02 p2
> ![](2_Files_IOs.assets/image-20240406144243042.png)![](2_Files_IOs.assets/image-20240406144248388.png)




### dup
> [!example] CS162 Fa20 Disc02 P2
> ![](2_Files_IOs.assets/image-20240406144549688.png)![](2_Files_IOs.assets/image-20240406144554880.png)



