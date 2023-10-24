# R-Format Instructions
## add instruction
> ![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315055075.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315067824.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315085444.png)




## sub instruction
> ![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315099468.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315114766.png)



## ALUSel
> ![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315134855.png)




# I-Format Instructions
## addi instruction
> ![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315156822.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315168407.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315176139.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315182744.png)



## ImmSel
> ![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315196631.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315235609.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315242675.png)




# Load&Store Instructions
## load instruction
> ![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315255690.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315274629.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315284456.png)



## store instruction
> ![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315302295.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315302147.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315318681.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315321267.png)




# Branch Instructions
## Add Branches
> ![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315346460.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315358390.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315372973.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315396666.png)



## Branch Comparators
> ![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315408239.png)



## Immediates Encoding
> ![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315419151.png)



# Jump Instructions
## Jalr Instructions
> ![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315425966.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315449276.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315442470.png)



## J Instructions
> ![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315461910.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315471972.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315491850.png)



# U-Type Instructions
> ![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315505552.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315508952.png)



## Lui
> ![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315528638.png)



## Auipc
> ![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315548914.png)




# Complete Datapath
## Graph
> ![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315559780.png)


## Control Signal Exercises
> ![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315574457.png)
> **总结一下不同**`**Control Bits**`**对应的意义:**
> 1. 首先`ASel`选择的是`rs1/PC`, `BSel`选择的是`rs2/imm`。`0`表示选择`register`, `1`表示`PC/imm`。
> 2. ** **`PCSel`表示我们是要将`PC`在指令执行完毕后更新为`PC+4`还是`PC+jump`。`1`表示`PC+jump`, `0`表示`PC+4`。
> 3. `ImmSel`表示我们要如何来解读`instruction`中表示`imm`的字段，可选的`Signal`有`R/I/S/SB/UJ`
> 4. `ALUSel`表示我们要进行何种代数运算，常见的有`add/or/sub`
> 5. `MemRW`表示我们是否要对内存进行读写，`0`代表`read`, `1`代表`write`
> 6. `RegWEn`表示我们是否要对`rd`进行写回操作，`1`代表指令中存在`rd`即需要写回，`0`代表指令中不存在`rd`不需要写回。
> 7. `WBSel`表示选择写回的数据类型是什么，上表中，`0`表示数据是`PC+imm`, `1`表示数据是`ALU`计算的结果，`2`表示数据是`PC+4`(一般是`jal`需要的)。



# Clocking Methodology
## Concept
> ![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315593276.png)







## Exercises
> ![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2315599105.png)![image.png](./RISC-V_Single-Cycle_Datapath.assets/20231023_2316008453.png)



