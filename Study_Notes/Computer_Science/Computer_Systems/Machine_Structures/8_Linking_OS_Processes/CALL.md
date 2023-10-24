# Overview
> ![image.png](CALL.assets/20231024_1008082106.png)![image.png](CALL.assets/20231024_1008108370.png)



# Compiler
> ![image.png](CALL.assets/20231024_1008127043.png)![image.png](CALL.assets/20231024_1008128346.png)



# Assembler
## Overview
> ![image.png](CALL.assets/20231024_1008136771.png)![image.png](CALL.assets/20231024_1008131710.png)


## Object File Format
> ![image.png](CALL.assets/20231024_1008163673.png)



## Directives(Split up Files)
> ![image.png](CALL.assets/20231024_1008193620.png)![image.png](CALL.assets/20231024_1008215387.png)



## Two-Pass(Translation)
### Procedures
> ![image.png](CALL.assets/20231024_1008239310.png)![image.png](CALL.assets/20231024_1008241830.png)![image.png](CALL.assets/20231024_1008264269.png)![image.png](CALL.assets/20231024_1008297280.png)![image.png](CALL.assets/20231024_1008313198.png)



## Solving Relative References
### Symbol Table
> ![image.png](CALL.assets/20231024_1008331548.png)
> 告诉别的`files`我有什么。



### Relocation Table
> ![image.png](CALL.assets/20231024_1008359102.png)
> 告知`Linker`我需要什么的地址。



# Linker
## Overview
> ![image.png](CALL.assets/20231024_1008368083.png)![image.png](CALL.assets/20231024_1008389106.png)![image.png](CALL.assets/20231024_1008405526.png)



## Important File Concepts
### Three Kinds of Object Files
> ![image.png](CALL.assets/20231024_1008422834.png)



### Three Kinds of Symbols
> ![image.png](CALL.assets/20231024_1008441822.png)![image.png](CALL.assets/20231024_1008467957.png)


### Three Types of Addressing
> ![image.png](CALL.assets/20231024_1008488941.png)![image.png](CALL.assets/20231024_1008516289.png)
> `**1.4**`**的意思是: 在**`**Linker**`**进行**`**Link**`**操作之后：**
> 1. `Absolute Adressing`比如`jal ra func`的`func`就直接是一个地址了，也就是我们直接知道了要跳转到哪里， 运行时就是这个地址。
> 2. `Relative Addressing`比如`bne x0, x1, -24`(这就是`Assembler`给的结果)，但是`Linker`不管这个。换句话说，运行时，上述指令被分配了一个地址，但仅仅凭借这个`instruction`和地址我们是不知道要跳转到哪里的，必须在运行时通过计算`PC-24`得到跳转地址。
> 
![image.png](CALL.assets/20231024_1008544619.png)




### ELF Format
> ![image.png](CALL.assets/20231024_1008552445.png)![image.png](CALL.assets/20231024_1008585980.png)![image.png](CALL.assets/20231024_1009007847.png)




## What Linkers Do?
> ![image.png](CALL.assets/20231024_1009049528.png)![image.png](CALL.assets/20231024_1009067377.png)



### Step 1: Symbol Resolution
> ![image.png](CALL.assets/20231024_1009083272.png)


#### Linker's Symbol Rules
> ![image.png](CALL.assets/20231024_1009091460.png)![image.png](CALL.assets/20231024_1009119198.png)



#### Linker's Puzzle
> ![image.png](CALL.assets/20231024_1009125347.png)


#### Golden Rules on Global Symbols
> ![image.png](CALL.assets/20231024_1009141090.png)



### Step 2: Relocation
> ![image.png](CALL.assets/20231024_1009153395.png)


## Solving Absolute References
> ![image.png](CALL.assets/20231024_1009173432.png)![image.png](CALL.assets/20231024_1009184325.png)







# Loader
> ![image.png](CALL.assets/20231024_1009209919.png)



# Integrated Example
## Example 1 - Lecture Slides
> ![image.png](CALL.assets/20231024_1009212421.png)![image.png](CALL.assets/20231024_1009244718.png)![image.png](CALL.assets/20231024_1009263315.png)![image.png](CALL.assets/20231024_1009281218.png)



## Example 2 - Two Tables
> ![image.png](CALL.assets/20231024_1009308190.png)![image.png](CALL.assets/20231024_1009317224.png)![image.png](CALL.assets/20231024_1009335732.png)




### First Pass
> ![image.png](CALL.assets/20231024_1009357085.png)
> `0x00061C28`表示就是我们的`Relative Addressing`/`j loop`。
> ![image.png](CALL.assets/20231024_1009377616.png)



###   Second Pass
> ![image.png](CALL.assets/20231024_1009407567.png)![image.png](CALL.assets/20231024_1009437343.png)
> 剩下的`????`就需要交由`Linker`来完成`relocation table`的填充。
> ![image.png](CALL.assets/20231024_1009452625.png)



## Example 3 - RISC-V Addressing
> ![image.png](CALL.assets/20231024_1009477500.png)![image.png](CALL.assets/20231024_1009493087.png)![image.png](CALL.assets/20231024_1009513330.png)![image.png](CALL.assets/20231024_1009533971.png)









