# Instruction Timing
> ![image.png](./Pipelining.assets/20231023_2310082695.png)![image.png](./Pipelining.assets/20231023_2310106462.png)



# Speed Efficiency of A Program
> ![image.png](./Pipelining.assets/20231023_2310126890.png)


## Instructions/Program
> ![image.png](./Pipelining.assets/20231023_2310131092.png)



## Cycles/Instruction(CPI)
> ![image.png](./Pipelining.assets/20231023_2310159938.png)



## Time/Cycle
> ![image.png](./Pipelining.assets/20231023_2310169815.png)



## Speed Tradeoff
> ![image.png](./Pipelining.assets/20231023_2310179049.png)
> **我们来计算一下:**
> 1. Processor A: $1\times 10^6\times 2.5\times \frac{1}{2.5\times 10^9}=1000s$
> 2. Processor B: $1.5\times 10^6\times 1\times \frac{1}{2\times 10^9}=750s$




# Energy Efficiency of A Program
## Energy Per Task
> ![image.png](./Pipelining.assets/20231023_2310198925.png)![image.png](./Pipelining.assets/20231023_2310214910.png)



## Energy "Iron Law"
> ![image.png](./Pipelining.assets/20231023_2310238647.png)



# Pipelining
## Basics - Latency&Throughput
> ![image.png](./Pipelining.assets/20231023_2310255227.png)![image.png](./Pipelining.assets/20231023_2310269167.png)
> **Latency: **The time to finish one instruction.
> **Throughput: **Number of instructions that can be processed(not finished) at the same time.
> ![image.png](./Pipelining.assets/20231023_2310284708.png)



## RISC-V Pipelining
### Sequential
> ![image.png](./Pipelining.assets/20231023_2310304772.png)



### Pipelined
> ![image.png](./Pipelining.assets/20231023_2310303078.png)![image.png](./Pipelining.assets/20231023_2310322831.png)![image.png](./Pipelining.assets/20231023_2310341279.png)![image.png](./Pipelining.assets/20231023_2310357720.png)




### Summary
> - **Pipelining doesn't help latency of single task, it helps throughput of entire workload**
> - Multiple tasks operating simultaneously using different resources
> - Potential speedup = Number of pipe stages
> - Time to "fill" pipeline and time to "drain" it reduces speedup: 2.3X v. 4X in this example
> - **Pipeline rate limited by the slowest pipeline stage**
> - **Unbalanced lengths of pipe stages reduce speedup**
> 
![image.png](./Pipelining.assets/20231023_2310371793.png)![image.png](./Pipelining.assets/20231023_2310382761.png)




## RISC-V Pipelined Datapath
> ![image.png](./Pipelining.assets/20231023_2310407079.png)![image.png](./Pipelining.assets/20231023_2310424738.png)![image.png](./Pipelining.assets/20231023_2310445823.png)



## RISC-V Pipelined Control
> ![image.png](./Pipelining.assets/20231023_2310465998.png)



# RISC-V Pipelining Hazards
> ![image.png](./Pipelining.assets/20231023_2310475096.png)


## Structural Hazard
> ![image.png](./Pipelining.assets/20231023_2310491592.png)![image.png](./Pipelining.assets/20231023_2310502615.png)![image.png](./Pipelining.assets/20231023_2310526563.png)![image.png](./Pipelining.assets/20231023_2310547748.png)![image.png](./Pipelining.assets/20231023_2310568934.png)



### RegFile Structural Hazards
> ![image.png](./Pipelining.assets/20231023_2310589714.png)



### Memory Access
> ![image.png](./Pipelining.assets/20231023_2311003854.png)



## Data Hazard
### Register Access - ID and WB
> ![image.png](./Pipelining.assets/20231023_2311022698.png)![image.png](./Pipelining.assets/20231023_2311042795.png)



### ALU Result -  EX & EX
> ![image.png](./Pipelining.assets/20231023_2311064005.png)


#### Solution 1: Stalling
> ![image.png](./Pipelining.assets/20231023_2311082662.png)![image.png](./Pipelining.assets/20231023_2311108454.png)![image.png](./Pipelining.assets/20231023_2311111230.png)



#### Solution 2: Forwarding
> ![image.png](./Pipelining.assets/20231023_2311138574.png)![image.png](./Pipelining.assets/20231023_2311159771.png)![image.png](./Pipelining.assets/20231023_2311164688.png)![image.png](./Pipelining.assets/20231023_2311182647.png)



### Load Data Hazard - WB & EX
> ![image.png](./Pipelining.assets/20231023_2311203566.png)![image.png](./Pipelining.assets/20231023_2311227800.png)![image.png](./Pipelining.assets/20231023_2311238307.png)



#### Solution 1: Stall Pipeline
> ![image.png](./Pipelining.assets/20231023_2311245783.png)![image.png](./Pipelining.assets/20231023_2311264731.png)



#### Solution 2: Code Rescheduling
> ![image.png](./Pipelining.assets/20231023_2311272052.png)



### Detecting Data Hazards
> ![image.png](./Pipelining.assets/20231023_2311294805.png)



### Exercises - Disc08 Su20
#### Forwarding
> ![image.png](./Pipelining.assets/20231023_2311305166.png)

**Solution**![image.png](./Pipelining.assets/20231023_2311325925.png)
> ![image.png](./Pipelining.assets/20231023_2311333658.png)

**Solution**![image.png](./Pipelining.assets/20231023_2311346723.png)


#### Stalls
> ![image.png](./Pipelining.assets/20231023_2311354360.png)![image.png](./Pipelining.assets/20231023_2311361191.png)![image.png](./Pipelining.assets/20231023_2311387770.png)![image.png](./Pipelining.assets/20231023_2311409860.png)![image.png](./Pipelining.assets/20231023_2311404452.png)![image.png](./Pipelining.assets/20231023_2311412605.png)


### Exam Practices - MT2 Su20
> ![image.png](./Pipelining.assets/20231023_2311427686.png)![image.png](./Pipelining.assets/20231023_2311438797.png)![image.png](./Pipelining.assets/20231023_2311441718.png)![image.png](./Pipelining.assets/20231023_2311455158.png)![image.png](./Pipelining.assets/20231023_2311473208.png)![image.png](./Pipelining.assets/20231023_2311472270.png)


## Control Hazard
> ![image.png](./Pipelining.assets/20231023_2311482953.png)![image.png](./Pipelining.assets/20231023_2311492491.png)![image.png](./Pipelining.assets/20231023_2311513390.png)



### Solution 1: Kill Instructions After Branch
> ![image.png](./Pipelining.assets/20231023_2311526427.png)![image.png](./Pipelining.assets/20231023_2311543574.png)



### Solution 2: Branch Prediction
> ![image.png](./Pipelining.assets/20231023_2311568677.png)![image.png](./Pipelining.assets/20231023_2311574288.png)




### Exercises - Disc08 Su20
> ![image.png](./Pipelining.assets/20231023_2311589756.png)![image.png](./Pipelining.assets/20231023_2312006072.png)



## Complicated Exercises
> ![image.png](./Pipelining.assets/20231023_2312012996.png)![image.png](./Pipelining.assets/20231023_2312026408.png)



# Superscalar Processors
> ![image.png](./Pipelining.assets/20231023_2312039063.png)![image.png](./Pipelining.assets/20231023_2312034430.png)![image.png](./Pipelining.assets/20231023_2312058068.png)



# Pipelineing Registers
> ![image.png](./Pipelining.assets/20231023_2312056431.png)![image.png](./Pipelining.assets/20231023_2312079449.png)![image.png](./Pipelining.assets/20231023_2312088414.png)![image.png](./Pipelining.assets/20231023_2312127462.png)



## How to Insert Pipeline Registers
> ![image.png](./Pipelining.assets/20231023_2312142017.png)![image.png](./Pipelining.assets/20231023_2312154650.png)![image.png](./Pipelining.assets/20231023_2312175629.png)![image.png](./Pipelining.assets/20231023_2312185623.png)



## Diminishing Returns on Deep Pipelining
### Definition
> ![image.png](./Pipelining.assets/20231023_2312196069.png)![image.png](./Pipelining.assets/20231023_2312214926.png)



### Numerical Example
> ![image.png](./Pipelining.assets/20231023_2312227207.png)![image.png](./Pipelining.assets/20231023_2312229428.png)![image.png](./Pipelining.assets/20231023_2312231675.png)![image.png](./Pipelining.assets/20231023_2312245244.png)
> 注意这里的一些单位转换，$1s=10^{12}ps$, $1GI = 10^{9}I$。







# Performance Analysis
## Single Cycle Datapath
> ![image.png](./Pipelining.assets/20231023_2312267250.png)
> **Disc08 Sp23 P3**
> ![image.png](./Pipelining.assets/20231023_2312275254.png)![image.png](./Pipelining.assets/20231023_2312299102.png)
> ![image.png](./Pipelining.assets/20231023_2312313660.png)



## Pipelined Datapath - MT2 Su20
### Critical Path
> ![image.png](./Pipelining.assets/20231023_2312322962.png)![image.png](./Pipelining.assets/20231023_2312347168.png)![image.png](./Pipelining.assets/20231023_2312355552.png)![image.png](./Pipelining.assets/20231023_2312379808.png)![image.png](./Pipelining.assets/20231023_2312377088.png)



### Max Clock Frequency
> ![image.png](./Pipelining.assets/20231023_2312389512.png)![image.png](./Pipelining.assets/20231023_2312391783.png)![image.png](./Pipelining.assets/20231023_2312418705.png)

