# Compile C Codes
## Into Object Files
> ![image.png](./X86_Basics.assets/20231023_2318399552.png)



## Into Assembly
> ![image.png](./X86_Basics.assets/20231023_2318407286.png)



## Into Object Code
> ![image.png](./X86_Basics.assets/20231023_2318414278.png)
> `gcc -Og sum.c -o sum`
> ![image.png](./X86_Basics.assets/20231023_2318426627.png)


# Diassemble Object Codes
> ![image.png](./X86_Basics.assets/20231023_2318444690.png)
> 从`Object File`to `Assembly Codes`(Reverse Engineering)
> ![image.png](./X86_Basics.assets/20231023_2318462750.png)



# X86 Integer Registers
> ![image.png](./X86_Basics.assets/20231023_2318479771.png)
> **总结一下:**
> 1. 总共有`16`个`64-bit registers`
> 2. `%r`开始的寄存器最多能够存放`64-bit integer`
> 3. `%e`开头的寄存器最多能够存放`32-bit integer`
> 
![image.png](./X86_Basics.assets/20231023_2318486048.png)
> 在`Old IA32`机器上，只有`8`个`%eax`寄存器。`%ebp`现在也不常用了(base pointer)。
> ![image.png](./X86_Basics.assets/20231023_2318507547.png)![image.png](./X86_Basics.assets/20231023_2318516117.png)![image.png](./X86_Basics.assets/20231023_2318525132.png)


# X86 Operations
## Move Instructions
> ![image.png](./X86_Basics.assets/20231023_2318542347.png)![image.png](./X86_Basics.assets/20231023_2318554638.png)



## Memory Addressing Modes
### Simple Mode
> ![image.png](./X86_Basics.assets/20231023_2318562097.png)


### Complete Mode
> ![image.png](./X86_Basics.assets/20231023_2318576453.png)



### Summary
> ![image.png](./X86_Basics.assets/20231023_2318588418.png)![image.png](./X86_Basics.assets/20231023_2318598769.png)



## Address Computation Instructions
> ![image.png](./X86_Basics.assets/20231023_2318598375.png)



## Arithmetic Instructions
> ![image.png](./X86_Basics.assets/20231023_2319017592.png)![image.png](./X86_Basics.assets/20231023_2319025056.png)![image.png](./X86_Basics.assets/20231023_2319042192.png)


