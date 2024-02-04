# Transistors
[note0A.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1685522029074-030fcd08-59bf-44d8-9339-7658a323a4f7.pdf)
[note1.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1685522029161-7d9f92aa-a383-4132-9359-0b9f14be5967.pdf)
[lecture1B.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1685522215637-052c8740-3802-45a2-97db-c9cd2e751244.pdf)
[lecture2.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1685522215721-9d55e9a6-7459-4f44-8fc5-e31c612a485c.pdf)
[lecture3.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1685522215714-3babaf48-22c8-4992-b08a-6f780890a4de.pdf)
## Introduction
> We can understand computers as a set of blocks that perform digital logic operations, one after the another. You might be familiar with logic in the form of `AND` and `OR` operations in `if` statements while programming. 
> - **Logic gates** are circuits that behave in a manner compatible with those logical operations. For this, high voltages are traditionally used to represent a logical `1` or `TRUE` and low voltages are traditionally used to represent a logical `0` or `FALSE`. These logical gate circuits are constructed out of physical devices called transistors.  
> - **An inverter** takes a boolean input and outputs the logical inverse: a `0` (low) maps to a `1` (high) and a `1` (high) maps to a `0` (low).  
> - **The speed of computers** is related to how quickly logical blocks can change their state and thus perform logic (for example, how quickly an inverter can output a `0` after its input changes to a `1`). 
> 
![image.png](Transistors&Logics.assets/10f9862a408b7e9ebfa6c0d158a561a9_MD5.png)


## Terminals
> **对于一个**`**Transistors**`**来说，有三个**`**Terminals**`**:**
> 1. `Source Terminal`: 用$S$表示，电压值为$V_S$。
> 2. `Destination Terminal`: 用$D$表示，电压值为$V_D$。
> 3. `Gate Terminal`: 用$G$表示，电压值为$V_G$。$V_G$的电压大小间接决定了`Source`和`Destination Terminal`之间的电路是否连通。
> 4. `Gate Voltage`: $V_{GS}=V_G-V_S$, 也就是说`Gate`处的电压和`Source`处的电压的差值。



# Basic Transistors
## Delayed Behaviors
> ![image.png](Transistors&Logics.assets/ddf2fb6bf3d1cea267c5731e3e0d2c85_MD5.png)
> 为了能够对上述的`Delay`来建模，我们需要引入一种新的`Transistor`模型，称为`Transistor Resistor-Switch Model`。



## NMOS Transistor
> **Verbal Definition:**
> NMOS transistor is:
> 1. **On** if the gate voltage $V_{GS}$ is greater than some small positive threshold $V_{tn}$. 
> 2. **Off** if the gate voltage $V_{GS}$ is less than some small positive threshold $V_{tn}$. 
> 3. This means that an NMOS transistor is on when the gate voltage is sufficiently higher than the source voltage. The threshold voltage tells us how much higher it needs to be.
> 
**Simple Model(所有**`**Switch**`**在达到阈值条件时立刻关闭或者开启):**
> ![image.png](Transistors&Logics.assets/2c4f4e7710b533d3b78ff9fec24ffada_MD5.png)
> - 我们一般假设$V_{th}$是一个提前决定的`Positive Constant`。
> - 当$V_{GS} \geq V_{t_n}$时，`Switch is on`。
> - 当$V_{GS} < V_{t_n}$时，`Switch is off`，此时电路是一个`Open Circuit`（No path from gate to source, no path from gate to destination）。
> 
**Real Model: 我们会用一个电容和电阻表示**`**NMOS**`**来模拟**`**Delayed Behavior**`**:**
> ![image.png](Transistors&Logics.assets/be62c60e781ce297870c5cc7e798e640_MD5.png)



## PMOS Transistor
> **Verbal Definition:**
>  A PMOS transistor is on if the gate voltage $V_{GS}$ is less than a small negative threshold −$|V_{tp}|$. This means that a PMOS transistor is on when the gate voltage is sufficiently lower than the source voltage. The threshold voltage tells us how much lower it needs to be.  
> **Technical Definition:**
> ![image.png](Transistors&Logics.assets/095173f6d832844b24c76a73b35ff01f_MD5.png)
> **我们定义:**
> 1. $V_{GS}=V_G-V_S$
> 2. $V_{SG}=V_S-V_G$
> 
当`Switch is on`:
> $V_{GS}\leq -|V_{t_p}|$or $V_{SG}\geq|V_{t_p}|$
> 当`Switch is off`:
> $V_{GS}> -|V_{t_p}|$or $V_{SG}< |V_{t_p}|$
> **Real Model: 我们会用一个电容和电阻表示**`**PMOS**`**来模拟**`**Delayed Behavior**`**:**
> ![image.png](Transistors&Logics.assets/48eb3f63fefbe3427384846d74c753b2_MD5.png)


## NMOS vs PMOS
> 简单理解:
> `NMOS`:
>  $V_{in}\uparrow$: Closed
>  $V_{in}\downarrow$: Open
> `PMOS`:
>  $V_{in}\uparrow$: Open
>  $V_{in}\downarrow$: Closed


## Charge Puddle Model - Physics
> ![image.png](Transistors&Logics.assets/e2ddce5edb73566f5d5cc6d722067d76_MD5.png)




# Logic Gates
## NOT GATE - CMOS
### Definition
> ![image.png](Transistors&Logics.assets/89fb66ad9b3167e32d0e30bbfa5b680a_MD5.png)
> 🔔在上图中我们有如下的`Notations`:
> - $V_{thn}$表示`NMOS`中的`Threshold`
> - $V_{thp}$表示`PMOS`中的`Threshold`
> - $V_{SS}=0V$表示接地`Terminal` 
> - $V_{dd}$表示最上端的`Terminal`
> 
![image.png](Transistors&Logics.assets/a0eb11d9b300be3aa9e11467b7c2e6ec_MD5.png)
> 🔔我们一般会有以下假设:
> 1. $V_{thn}+|V_{thp}|\geq V_{dd}$时
> 2. $0\leq V_{thn}\leq V_{dd}$
> 3. $0\leq |V_{thp}|\leq V_{dd}$
> 
**当上述三个条件都满足时，当左侧输入**$V_{in}$**时有且仅有一个**`**Transistor**`**的电路会被接通**（Also a Sanity Check, 两个通路不能同时接通）：
> 1. 当输入的电压$V_{in}=0V$(`Logic 0 False`)时，输出的电压$V_{out}=V_{dd}=[0.7V,1.0V]$:
> 
![image.png](Transistors&Logics.assets/d946b10d826034aa08a68cbd390bc325_MD5.png)
> 2. 当输入的电压$V_{in}=V_{dd}=1V$(`Logic 1，True`)时, 输出的电压是$0V$, 相当于$not~V_{in}$:
> 
![image.png](Transistors&Logics.assets/ced72f91a72bbc58a1cbc1496b446cd5_MD5.png)
> **Real Model:**
> ![image.png](Transistors&Logics.assets/e4893a436e75e1f1e4e277895dec2f91_MD5.png)



### Circuit Analysis Caveats
> ![image.png](Transistors&Logics.assets/24d3fe89bf367f256a460701a0f43a21_MD5.png)
> 如果此时$V_{in}=5V$, 则$V_{GS, P}=V_{in}-V_{DD}=0V$, 所以`PMOS`是`Closed`，而$V_{GS,N}=V_{in}-0V=5V$, 所以`NMOS`是`Open`的。
> 此时要注意我们不需要把两个电容考虑进来，因为这两个电容两端的电压都是不变的，所以电流均为零，可以看成`Open Circuit`。
> ![image.png](Transistors&Logics.assets/bea2e91a396ae45e25a9dea884aecc9c_MD5.png)
> 只需要考虑下面的模型即可:
> ![image.png](Transistors&Logics.assets/13f4c90ad729a53270a7d333ba094708_MD5.png)

 




## Multi-NOT GATE - Ring Oscillator
> ![image.png](Transistors&Logics.assets/85ac0a49a466e3c38fdaec820d937422_MD5.png)
> **Real Model:**
> ![image.png](Transistors&Logics.assets/d5024211e50ea0eccf2246a494aaef52_MD5.png)



## NAND GATE
> **From Discussion 01A Fa21**
> ![image.png](Transistors&Logics.assets/1c86ca720f24a5f7739c808295202260_MD5.png)

**Proof of Validity**![image.png](Transistors&Logics.assets/15da8132d945fc4ecb0b1c01c06f3ccf_MD5.png)



# Cascading Logic
## Example 1 - Low to High
### Circuit Model⭐⭐⭐⭐⭐
> ![image.png](Transistors&Logics.assets/ae87ea03bdd9157f0d16db3b9ea00d50_MD5.png)
> **❔: 为什么**$V_x(0)=V_{DD}$**?**
> 这涉及到电路稳定，因为在$V_{in}=0V$经过很长时间后，电路最终会趋于稳定，此时电路中不应该有电流，所以电容$C_{GP,2},C_{GN,2}$两端的电压均为零，所以$V_x=V_{DD}$。
> 也可以参考`Example 2`中的推导。
> **❔：为什么不需要考虑左侧电容和右侧电阻（为什么只要考虑三个电子元件就能得到目标电压方程）？**
> 因为流经左侧电容和右侧电阻的电流不会对中间的电压计算产生影响。我们的KCL只需要关注三个电子元件即可。
> **几个注意点:**
> 1. 一旦开关闭合，左侧电容就会被`shorted`。
> 2. **第二个**`**CMOS**`**的电阻不需要考虑（计算**$V_{out}$**的时候只需要考虑三个电子元件）**






### Circuit Analysis(Solving Differential Equations)
> ![image.png](Transistors&Logics.assets/083065adfd62c3335045d2e8d74b2936_MD5.png)

**Set Up DE**![image.png](Transistors&Logics.assets/eadd63fb6cd8f4371248b61d0d702493_MD5.png)
**Solving DE**![image.png](Transistors&Logics.assets/89253a6f01f8edec4aeb3a0581e290f9_MD5.png)
**Sketch the Output**![image.png](Transistors&Logics.assets/56419acbd05e66956d0a1c64ea35940b_MD5.png)
**Comparative Analysis - Different Values of RC**![image.png](Transistors&Logics.assets/719c62ebfe10c85fc413f42f0f8c88e1_MD5.png)


## Example 2 - High to Low
### Circuit Model
> ![image.png](Transistors&Logics.assets/ce2b22c5675afb4006de53ef5ff5bcba_MD5.png)



### Circuit Analysis(Solving Differential Equations)
> `KCL`: $I_1+I_2+I_3=0\quad(1)$
> `Elements`: 
> 1. $V_1=I_1\cdot R_{on, n1}=V_x-V_{dd}$, $I_1=\frac{V_1}{R_{on, n1}}$
> 2. $I_2=C_{G_{n2}}\cdot \frac{dV_2}{dt}$, $V_2=V_x$
> 3. $I_3=C_{G_{p2}}\cdot \frac{dV_3}{dt}$, $V_3=V_x-V_{dd}$
> 
将`Elements`代入$(1)$中有:
> ![image.png](Transistors&Logics.assets/b5f30bdbba0b184be95d09dc7f1df7f8_MD5.png)




## Equivalent Circuit
> **HW02 Sp23 P4**
> ![image.png](Transistors&Logics.assets/1012aae1201f0909fef2e5e90f683d3e_MD5.png)

**(a) NMOS**![image.png](Transistors&Logics.assets/a9a834e84383aea46936e9896b332b99_MD5.png)
**(b) PMOS**![image.png](Transistors&Logics.assets/e8fba6d0d98f212770e7e50ea05f5d06_MD5.png)
**(c) CMOS**![image.png](Transistors&Logics.assets/de7907449f5e34419a05e0bc9a1107eb_MD5.png)


## Cascading Circuit
> **HW01 Fa21 P7**
> ![image.png](Transistors&Logics.assets/aab49386c0d2cfea1aa5162b1cb6b26f_MD5.png)

**(a)**![image.png](Transistors&Logics.assets/e63d3546efcb90fca05359b0c4c2c5b6_MD5.png)
**(b)**![image.png](Transistors&Logics.assets/35f89ebf8753f8753ed48f9625f7d836_MD5.png)
**(c)**![image.png](Transistors&Logics.assets/d39cca270332e22f771e74969e569cc8_MD5.png)
**(d)**![image.png](Transistors&Logics.assets/9bdbedcb854fc5006553bdde21f71137_MD5.png)



# Transistors with RC Circuit
> **Disc02A Sp23 P1**
> 之前的`Transistor`模型我们都是假设`Gate`是直接和$V_{in}$相连的，所以$V_{in}$的变化会立即反应到$V_G$上，但是本题中我们移除这一假设，我们探究如果$V_{in}$和`Gate`之间有一个电阻的情况，这其实就是最简单的`RC`电路，如下图所示:
> ![image.png](Transistors&Logics.assets/0290bad4d4e33c70059dae8693831a54_MD5.png)
> 我们会探究不同的`NMOS`模型下$V_{out}$的变化情况, 具体有如下四种:
> ![image.png](Transistors&Logics.assets/a0f7128667eda01927df4b2b8d2ef7ad_MD5.png)



## Model I
> ![image.png](Transistors&Logics.assets/76a25d26b8ce5123c29dedccb14fa7e0_MD5.png)



## Model II
> ![image.png](Transistors&Logics.assets/6559afd4b0b85549b52ace5152cca49f_MD5.png)




## Model III/ IV: RC Circuit
> `Model III`和`Model IV`其实就是最基本的`RC Circuit`, 如下图所示:
> ![image.png](Transistors&Logics.assets/cdf53595434795695f68f70b586060d6_MD5.png)


