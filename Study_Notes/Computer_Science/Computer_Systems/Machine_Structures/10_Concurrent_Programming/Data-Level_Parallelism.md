# Amdahl's Law
> 



# Flynn's Taxonomy
> ![image.png](Data-Level_Parallelism.assets/20231105_1747232396.png)
> ![image.png](Data-Level_Parallelism.assets/20231105_1747267622.png)
> ![image.png](Data-Level_Parallelism.assets/20231105_1747288891.png)
> SIMD 和 MIMD 是目前最常见的并行处理技术。最普遍的并行处理编程风格是SPMD，一个程序在MIMD的所有处理器上运行。通过条件表达式进行跨处理器的执行协调。
> SIMD是专门的硬件单元，用于处理数组计算，常应用于科学计算、机器学习、信号处理和多媒体处理。




# SIMD History
## SISD/SIMD/MIMD/MISD
> ![image.png](Data-Level_Parallelism.assets/20231105_1747304543.png)![image.png](Data-Level_Parallelism.assets/20231105_1747322705.png)![image.png](Data-Level_Parallelism.assets/20231105_1747353509.png)![image.png](Data-Level_Parallelism.assets/20231105_1747374292.png)




## SIMD Evolution
> ![image.png](Data-Level_Parallelism.assets/20231105_1747397933.png)



### MMX
> ![image.png](Data-Level_Parallelism.assets/20231105_1747416116.png)




### SSE
> ![image.png](Data-Level_Parallelism.assets/20231105_1747423153.png)



### AVX
> ![image.png](Data-Level_Parallelism.assets/20231105_1747446654.png)



## SIMD Architecture
### XMM Register in SSE
> 本质上说，`XMM Register`就是一个能够储存位宽为`128bit`的大号寄存器，一共有`16`个。
> ![image.png](Data-Level_Parallelism.assets/20231105_1747464789.png)![image.png](Data-Level_Parallelism.assets/20231105_1747492427.png)
> `Packed`的意思就是我们可以同时处理多个数据段。



### SIMD Register in AVX512
> ![image.png](Data-Level_Parallelism.assets/20231105_1747509247.png)![image.png](Data-Level_Parallelism.assets/20231105_1747523613.png)



### WSL Parameter(lscpu)
> ![image.png](Data-Level_Parallelism.assets/20231105_1747541883.png)



# SIMD Parallel Instructions
## SIMD Array Processing
> ![image.png](Data-Level_Parallelism.assets/20231105_1747567914.png)
> 我们可以发现`SIMD`可以极大程度上的缩减我们循环体执行的次数，每个循环体内做的事情会比`SISD`更多。
> ![image.png](Data-Level_Parallelism.assets/20231105_1747585944.png)



## SIMD Matrix Multiplication
> ![](Data-Level_Parallelism.assets/image-20231105204038302.png)





