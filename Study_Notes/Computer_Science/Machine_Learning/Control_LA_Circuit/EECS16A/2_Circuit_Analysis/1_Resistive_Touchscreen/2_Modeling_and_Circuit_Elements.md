
# Voltage Divider
## Definition
> ![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059259383.png)
> 本质上`Voltage Divider`会将电压按照电阻值按比例分配。下面进行详细分析。



## Circuit Analysis Algorithm
### Step 1 Pick Reference Node
> ![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059267713.png)
> 首先我们需要选择一个参照物节点，比如`ground`来测量电压。


### Step 2 Nodes Set by Voltage Sources
> ![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059264754.png)![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059264274.png)
> 本质上是找到通过`Voltage Source`就能确定电压的那些节点。


### Step 3 Remaining Nodes
> ![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059265423.png)
> 标出那些不能通过`Voltage Sources`直接确定的节点。



### Step 4 Label Voltages&Currents
> ![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059264714.png)



### Step 5 KCL
> ![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059269395.png)


### Step 6 Ohm's Law
> ![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059266829.png)![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059264744.png)


### Step 7 Back Substitution
> ![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059267013.png)


### Step 8 Solving the Equations
> ![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059274293.png)


### Summary
> ![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059278765.png)![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059278164.png)
> `Voltage Divider`最有用的地方在于我们可以用他来构造出任何我们想要的电压节点。



# Resistive Touch Screen
## Introduction
> ![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059279809.png)![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059272942.png)![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059284803.png)
> **How can we measure this physical quantity using an electrical circuit? **
> Next we will introduce some of the physics of circuit components so that we can **convert this physical structure into an electrical model**. Once we have that model, we can connect additional components around it to build a complete circuit which we can then analyze (using the procedure developed in the previous note). 




## Physics of Circuits
### Charge
> ![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059288940.png)




### Current
> ![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059282390.png)![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059289017.png)
> 注意是`Net amount`(正电荷 - 负电荷的总量)


### Voltage
> 电压被定义为将单位电荷$dQ$ 在两点之间移动所需的能量$dE$, 记为$V$, 计算公式为 $\frac{dE}{dQ}=V$。![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059285956.png)





### Resistance
#### Definition
> ![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059281059.png)


#### Ohm's Law
> ![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059293725.png)



## Modeling a Resistor
> ![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059294864.png)![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059293398.png)![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059297074.png)



## 1-D Touchscreen's Modeling
### Physical Model
> ![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059299627.png)



### Circuit Model
> ![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059295433.png)![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059303552.png)![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059307446.png)


### Model Analysis 
> ![image.png](2_Modeling_and_Circuit_Elements.assets/20230302_1059307679.png)


# Resources
[Note12](Typed_notes_pdf/Note12.pdf)
[Written_Notes12](Typed_notes_pdf/Written_Notes12.pdf)
