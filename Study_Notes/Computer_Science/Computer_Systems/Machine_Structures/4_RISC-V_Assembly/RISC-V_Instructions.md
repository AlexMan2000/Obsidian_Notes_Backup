# Overview
> ![image.png](./RISC-V_Instructions.assets/20231023_2313161519.png)

# 
# Registers
> ![image.png](./RISC-V_Instructions.assets/20231023_2313187323.png)![image.png](./RISC-V_Instructions.assets/20231023_2313203298.png)![image.png](./RISC-V_Instructions.assets/20231023_2313223440.png)![image.png](./RISC-V_Instructions.assets/20231023_2313222143.png)![image.png](./RISC-V_Instructions.assets/20231023_2313242553.png)



# Basic Instruction Types
[lec06.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1694609457998-48cdc036-9188-4471-a6bf-e07d74b15f32.pdf)


## Word Instructions
### Word/Byte Memory Alignment
> ![image.png](./RISC-V_Instructions.assets/20231023_2313263985.png)



### Arithmetic Instructions
> ![image.png](./RISC-V_Instructions.assets/20231023_2313266678.png)![image.png](./RISC-V_Instructions.assets/20231023_2313281950.png)![image.png](./RISC-V_Instructions.assets/20231023_2313297443.png)



### Logical Instructions
> ![image.png](./RISC-V_Instructions.assets/20231023_2313316686.png)![image.png](./RISC-V_Instructions.assets/20231023_2313326503.png)




### Shifting Instructions
> ![image.png](./RISC-V_Instructions.assets/20231023_2313342491.png)![image.png](./RISC-V_Instructions.assets/20231023_2313366324.png)
> **注意:**
> 1. When using immediate, only values 0-31 are practical.
> 2. When using variable, only lowest 5 bits are used (read as unsigned).
> 
这取决于`Instruction Format`带来的限制。

**Example 1**![image.png](./RISC-V_Instructions.assets/20231023_2313373865.png)


### Immediate Instruction
> ![image.png](./RISC-V_Instructions.assets/20231023_2313392062.png)![image.png](./RISC-V_Instructions.assets/20231023_2313409225.png)



### Data Transfer Instructions
#### Data Transfer
> ![image.png](./RISC-V_Instructions.assets/20231023_2313417353.png)![image.png](./RISC-V_Instructions.assets/20231023_2313437356.png)



#### Instructions
> ![image.png](./RISC-V_Instructions.assets/20231023_2313448384.png)![image.png](./RISC-V_Instructions.assets/20231023_2313452453.png)



#### Endianness in RISC-V
> ![image.png](./RISC-V_Instructions.assets/20231023_2313476094.png)



#### Sign Extension in RISC-V
> ![image.png](./RISC-V_Instructions.assets/20231023_2313491240.png)




## Non-word Instructions
> ![image.png](./RISC-V_Instructions.assets/20231023_2313506120.png)

### Byte Instructions
> ![image.png](./RISC-V_Instructions.assets/20231023_2313513619.png)![image.png](./RISC-V_Instructions.assets/20231023_2313523239.png)



### Half-Word Instructions
> ![image.png](./RISC-V_Instructions.assets/20231023_2313539711.png)

**Example 1 - Build lbu with lw**![image.png](./RISC-V_Instructions.assets/20231023_2313547955.png)
**Example 2 - Build sb with sw**![image.png](./RISC-V_Instructions.assets/20231023_2313558108.png)


## Decision Making Instructions -  Control
### Branch Instructions
> ![image.png](./RISC-V_Instructions.assets/20231023_2313552536.png)![image.png](./RISC-V_Instructions.assets/20231023_2313567716.png)![image.png](./RISC-V_Instructions.assets/20231023_2313573639.png)
> 一个问题是: 为什么我们没有`Branch Greater Then`或者`Branch Less Than Or Equal`这两个指令？
> **这里有一个**`**RISC-V**`**的设计哲学，就是说：**
> 1. `Branch Greater Than`可以通过`Branch Less Than`来实现(交换`reg1`和`reg2`的顺序)。
> 2. `Branch Less Than Or Equal`可以通过已有的`Branch Greater Than or Equal`来实现(交换`reg1`和`reg2`的顺序)。
> 
所以我们无需设计额外的两个指令`bgt`和`ble`。



### Compare Instructions
> ![image.png](./RISC-V_Instructions.assets/20231023_2313576664.png)



### If-Else in RISC-V
> ![image.png](./RISC-V_Instructions.assets/20231023_2313599718.png)![image.png](./RISC-V_Instructions.assets/20231023_2314009602.png)



### Loop in RISC-V
> ![image.png](./RISC-V_Instructions.assets/20231023_2314013786.png)



## Program Counter
> ![image.png](./RISC-V_Instructions.assets/20231023_2314034685.png)![image.png](./RISC-V_Instructions.assets/20231023_2314042012.png)



## Summary
> ![image.png](./RISC-V_Instructions.assets/20231023_2314057551.png)




# Pseudoinstructions
> ![image.png](./RISC-V_Instructions.assets/20231023_2314066454.png)![image.png](./RISC-V_Instructions.assets/20231023_2314068637.png)



# Instruction Formats
[lec08.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1694886564141-2960e1df-a8e2-4e4a-884b-9927c6a247ea.pdf)
## Overview
> ![image.png](./RISC-V_Instructions.assets/20231023_2314072549.png)
> **几个注意点:**
> 1. `opcode`用于区分指令的类型(`Instruction Format`)。
> 2. `funct`用于确定具体是哪一个指令，相当于唯一标识。
> 
![image.png](./RISC-V_Instructions.assets/20231023_2314101240.png)



## R-Format(3 regs)
> ![image.png](./RISC-V_Instructions.assets/20231023_2314128433.png)
> 1. 运算指令，比如`add, xor, mul`, 这类型的指令含有三个寄存器，`rs1, rs2, rd`, 代表两个`operand`和一个结果寄存器
> 2. 指令有`6`个`Field`, 其中`7+5+5+3+5+7`，所有长度为`5`的都用于表示寄存器是哪个，因为`RISC-V`有`32`个寄存器，所以我们只需要`5`位就可以表示所有的寄存器。
> 
![image.png](./RISC-V_Instructions.assets/20231023_2314124710.png)
> 3. 每一个`Field`都被当做是`unsigned int`来`evaluate`。
> 
![image.png](./RISC-V_Instructions.assets/20231023_2314137444.png)
> `func7+func3`一共可以表示`1024`种不同的运算指令。



## I-Format(12 bit imm&load, 2 regs)
> `I-Format`主要是那些包括了两个`Registers`和一个`Immediate Field`的指令集。
> ![image.png](./RISC-V_Instructions.assets/20231023_2314156317.png)



### addi...
> ![image.png](./RISC-V_Instructions.assets/20231023_2314162465.png)![image.png](./RISC-V_Instructions.assets/20231023_2314183887.png)



### load
> ![image.png](./RISC-V_Instructions.assets/20231023_2314199292.png)![image.png](./RISC-V_Instructions.assets/20231023_2314219105.png)![image.png](./RISC-V_Instructions.assets/20231023_2314239792.png)



### jalr
> ![image.png](./RISC-V_Instructions.assets/20231023_2314241236.png)![image.png](./RISC-V_Instructions.assets/20231023_2314256930.png)


## S-Format(2 regs, no rd)
> `S-Format`主要用于将寄存器内的值保存到内存地址中。因为这样的指令不需要`rd`(目标寄存器)，所以`rd`段
> ![image.png](./RISC-V_Instructions.assets/20231023_2314265632.png)![image.png](./RISC-V_Instructions.assets/20231023_2314274651.png)
> The sb instruction itself does not perform any sign extension; it merely stores the least significant byte of the source register to the specified memory address.


## SB-Format(branching)
### PC-Relative Addressing
> ![image.png](./RISC-V_Instructions.assets/20231023_2314298836.png)![image.png](./RISC-V_Instructions.assets/20231023_2314306766.png)


### Branch Instructions
> ![image.png](./RISC-V_Instructions.assets/20231023_2314321326.png)![image.png](./RISC-V_Instructions.assets/20231023_2314346493.png)![image.png](./RISC-V_Instructions.assets/20231023_2314353067.png)



### RISC-V SB Format(2 bytes incre)
> ![image.png](./RISC-V_Instructions.assets/20231023_2314367997.png)![image.png](./RISC-V_Instructions.assets/20231023_2314377513.png)



### Branch Example
> ![image.png](./RISC-V_Instructions.assets/20231023_2314377583.png)![image.png](./RISC-V_Instructions.assets/20231023_2314385225.png)



## U-Format(20 bit Imm)
> ![image.png](./RISC-V_Instructions.assets/20231023_2314395317.png)![image.png](./RISC-V_Instructions.assets/20231023_2314413954.png)




### lui+addi Corner Cases⭐⭐⭐⭐⭐
> ![image.png](./RISC-V_Instructions.assets/20231023_2314429047.png)![image.png](./RISC-V_Instructions.assets/20231023_2314434468.png)


### auipc
> ![image.png](./RISC-V_Instructions.assets/20231023_2314446607.png)




## UJ-Format(Jump Anywhere, 1 reg)
> ![image.png](./RISC-V_Instructions.assets/20231023_2314454847.png)![image.png](./RISC-V_Instructions.assets/20231023_2314472445.png)![image.png](./RISC-V_Instructions.assets/20231023_2314488302.png)




# Exercises
> ![image.png](./RISC-V_Instructions.assets/20231023_2314497460.png)![image.png](./RISC-V_Instructions.assets/20231023_2314509338.png)![image.png](./RISC-V_Instructions.assets/20231023_2314515178.png)


   

## C to RISC-V Examples
**Example 1 - while loop**![image.png](./RISC-V_Instructions.assets/20231023_2314529934.png)![image.png](./RISC-V_Instructions.assets/20231023_2314533815.png)![image.png](./RISC-V_Instructions.assets/20231023_2314549308.png)
**Example 2 - do while loop**![image.png](./RISC-V_Instructions.assets/20231023_2314555415.png)![image.png](./RISC-V_Instructions.assets/20231023_2314565591.png)
**Example 3 - More practices Su20 Disc04**![image.png](./RISC-V_Instructions.assets/20231023_2314566354.png)![image.png](./RISC-V_Instructions.assets/20231023_2314579498.png)![image.png](./RISC-V_Instructions.assets/20231023_2314587366.png)


## RISC-V to C Examples
**Example 1 - Su20 Disc04**![image.png](./RISC-V_Instructions.assets/20231023_2315005042.png)
**Example 2 - Su20 Disc04**![image.png](./RISC-V_Instructions.assets/20231023_2315016438.png)![image.png](./RISC-V_Instructions.assets/20231023_2315027542.png)


## RISC-V With Arrays
**Example 1 - Su20 Disc04 P6**![image.png](./RISC-V_Instructions.assets/20231023_2315035096.png)![image.png](./RISC-V_Instructions.assets/20231023_2315056239.png)
> 如果我们要遍历`int[]`则我们有一个常用的办法，就是使用一个临时寄存器`t0`作为`index`, 每个循环增加`1`, 但是因为`int`的长度是`4-byte`, 所以我们需要对`t0`做`t0<<2`(扩大四倍)获得真正的地址值差异。



