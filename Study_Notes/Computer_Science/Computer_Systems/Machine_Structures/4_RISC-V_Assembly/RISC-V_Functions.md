# Function Calling Procedure
> ![image.png](./RISC-V_Functions.assets/20231023_2312435262.png)




# 1&5: Put Function Parameter
> ![image.png](./RISC-V_Functions.assets/20231023_2312434818.png)![image.png](./RISC-V_Functions.assets/20231023_2312441700.png)



# 2&6: Transfer Control
## Registers&Instructions
> ![image.png](./RISC-V_Functions.assets/20231023_2312462069.png)![image.png](./RISC-V_Functions.assets/20231023_2312474572.png)![image.png](./RISC-V_Functions.assets/20231023_2312499234.png)![image.png](./RISC-V_Functions.assets/20231023_2312508860.png)


## J-Pseudo-Instruction
> ![image.png](./RISC-V_Functions.assets/20231023_2312525608.png)

**Concept Check**![image.png](./RISC-V_Functions.assets/20231023_2312521695.png)![image.png](./RISC-V_Functions.assets/20231023_2312541666.png)


# 3: Local Storage for Variables
> ![image.png](./RISC-V_Functions.assets/20231023_2312565748.png)



# 4: Calling Convention
## Caller&Callee Convention
> ![image.png](./RISC-V_Functions.assets/20231023_2312575459.png)![image.png](./RISC-V_Functions.assets/20231023_2312591422.png)




## Register Convention
> ![image.png](./RISC-V_Functions.assets/20231023_2312595976.png)![image.png](./RISC-V_Functions.assets/20231023_2313001001.png)
> 如果一个函数同时作为`caller/callee`则它需要同时`save callee-saved registers`和`caller-saved registers`。
> ![image.png](./RISC-V_Functions.assets/20231023_2313014558.png)



## Concept Check
> ![image.png](./RISC-V_Functions.assets/20231023_2313034763.png)![image.png](./RISC-V_Functions.assets/20231023_2313056778.png)![image.png](./RISC-V_Functions.assets/20231023_2313052590.png)




# How to Save Registers
## Methodology
> ![image.png](./RISC-V_Functions.assets/20231023_2313075293.png)![image.png](./RISC-V_Functions.assets/20231023_2313076573.png)![image.png](./RISC-V_Functions.assets/20231023_2313098993.png)




## Structure of a Function
> ![image.png](./RISC-V_Functions.assets/20231023_2313103911.png)

 
## Example
> ![image.png](./RISC-V_Functions.assets/20231023_2313121157.png)


 


# Practice and Summary
## Writing RISC-V Functions
> ![image.png](./RISC-V_Functions.assets/20231023_2313144777.png)
> **逻辑是:**
> 1. 如果我们在`Function Body`中用到了任何`Saved Registers`, 上例中`sumSquare`作为`main`的`callee`用到了`s0`和`s1`(saved registers)，那么我们作为`Callee`需要在`prologue`中将其保存到`Stack`上。
> 2. `sumSquare()`执行时作为`caller`调用了`square()`, 需要保存`caller saved registers`。
> 3. 任何`Function`的`Prologue`中都必须有`sw ra, 0(sp)`当且仅当这个`Function`后续要调用其他函数。



## Translating Functions
> ![image.png](./RISC-V_Functions.assets/20231023_2313142032.png)


