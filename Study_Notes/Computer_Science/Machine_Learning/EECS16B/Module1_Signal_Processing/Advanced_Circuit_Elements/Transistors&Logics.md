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
![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684330719479-3a470cdc-aea5-4718-98a6-d8b225f176f2.png#averageHue=%23fcfafa&clientId=ud3c484e6-5e0d-4&from=paste&id=ua2a9d5bb&originHeight=521&originWidth=1257&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=41065&status=done&style=none&taskId=ufd7f4a94-06a1-41ab-b516-7279093ec50&title=)


## Terminals
> **对于一个**`**Transistors**`**来说，有三个**`**Terminals**`**:**
> 1. `Source Terminal`: 用$S$表示，电压值为$V_S$。
> 2. `Destination Terminal`: 用$D$表示，电压值为$V_D$。
> 3. `Gate Terminal`: 用$G$表示，电压值为$V_G$。$V_G$的电压大小间接决定了`Source`和`Destination Terminal`之间的电路是否连通。
> 4. `Gate Voltage`: $V_{GS}=V_G-V_S$, 也就是说`Gate`处的电压和`Source`处的电压的差值。



# Basic Transistors
## Delayed Behaviors
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684330157219-361a503b-45bd-4bd4-aade-b297b73d4480.png#averageHue=%23f9efec&clientId=ud3c484e6-5e0d-4&from=paste&id=kurvs&originHeight=310&originWidth=1007&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=102500&status=done&style=none&taskId=uae963104-ae40-4cd6-89ce-465c9159691&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684330342037-2df43af0-a721-4b6b-8c3a-11dd87f73429.png#averageHue=%23f6f3ef&clientId=ud3c484e6-5e0d-4&from=paste&id=f704V&originHeight=189&originWidth=1384&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=79346&status=done&style=none&taskId=u78bb0eeb-2a56-43ac-ac40-9a19552cbad&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684330421964-3af5c4bb-6233-43dc-9d4b-42e8793d0211.png#averageHue=%23faebeb&clientId=ud3c484e6-5e0d-4&from=paste&id=m2W1c&originHeight=607&originWidth=977&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=37835&status=done&style=none&taskId=u6b2a28e7-31a4-4b5f-9516-999f1fb318c&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684330479094-d3d62c87-c306-4ce1-9f6a-5a8df18451a0.png#averageHue=%235d566b&clientId=ud3c484e6-5e0d-4&from=paste&id=ixPba&originHeight=297&originWidth=1289&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=98382&status=done&style=none&taskId=u9bee0a96-7a88-4cb1-a320-d9ed9df200a&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684330719479-3a470cdc-aea5-4718-98a6-d8b225f176f2.png#averageHue=%23fcfafa&clientId=ud3c484e6-5e0d-4&from=paste&id=BUo5p&originHeight=521&originWidth=1257&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=41065&status=done&style=none&taskId=ufd7f4a94-06a1-41ab-b516-7279093ec50&title=)
> 为了能够对上述的`Delay`来建模，我们需要引入一种新的`Transistor`模型，称为`Transistor Resistor-Switch Model`。



## NMOS Transistor
> **Verbal Definition:**
> NMOS transistor is:
> 1. **On** if the gate voltage $V_{GS}$ is greater than some small positive threshold $V_{tn}$. 
> 2. **Off** if the gate voltage $V_{GS}$ is less than some small positive threshold $V_{tn}$. 
> 3. This means that an NMOS transistor is on when the gate voltage is sufficiently higher than the source voltage. The threshold voltage tells us how much higher it needs to be.
> 
**Simple Model(所有**`**Switch**`**在达到阈值条件时立刻关闭或者开启):**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684329294947-1440de98-b4e2-425b-b48d-b929faab00ca.png#averageHue=%23fbebea&clientId=ud3c484e6-5e0d-4&from=paste&id=ue245417a&originHeight=540&originWidth=1354&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=101506&status=done&style=none&taskId=u1bf7a180-43da-4ba5-8b42-4cf0a6138b9&title=)
> - 我们一般假设$V_{th}$是一个提前决定的`Positive Constant`。
> - 当$V_{GS} \geq V_{t_n}$时，`Switch is on`。
> - 当$V_{GS} < V_{t_n}$时，`Switch is off`，此时电路是一个`Open Circuit`（No path from gate to source, no path from gate to destination）。
> 
**Real Model: 我们会用一个电容和电阻表示**`**NMOS**`**来模拟**`**Delayed Behavior**`**:**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684331121420-1f3f3ff2-5731-4fcb-91d1-edb5758ca3e1.png#averageHue=%23fceceb&clientId=ud3c484e6-5e0d-4&from=paste&id=KbdPC&originHeight=510&originWidth=988&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=73995&status=done&style=none&taskId=ue01ab9f7-590a-4854-a043-8d9e8029937&title=)



## PMOS Transistor
> **Verbal Definition:**
>  A PMOS transistor is on if the gate voltage $V_{GS}$ is less than a small negative threshold −$|V_{tp}|$. This means that a PMOS transistor is on when the gate voltage is sufficiently lower than the source voltage. The threshold voltage tells us how much lower it needs to be.  
> **Technical Definition:**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684329321158-e2914c2f-0b47-46f0-8c42-6fded1711733.png#averageHue=%23faebea&clientId=ud3c484e6-5e0d-4&from=paste&id=u49b4347c&originHeight=542&originWidth=1349&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=105478&status=done&style=none&taskId=u1abfd215-710c-4af0-a0e7-3c5c21e7433&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684329428406-37bcf2ef-683f-4596-b566-28bfcfbdc5b5.png#averageHue=%23f9f7f6&clientId=ud3c484e6-5e0d-4&from=paste&id=ue89e60b6&originHeight=109&originWidth=1432&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=36020&status=done&style=none&taskId=u8ce17921-3527-4278-8b4f-c1530a556c7&title=)
> **我们定义:**
> 1. $V_{GS}=V_G-V_S$
> 2. $V_{SG}=V_S-V_G$
> 
当`Switch is on`:
> $V_{GS}\leq -|V_{t_p}|$or $V_{SG}\geq|V_{t_p}|$
> 当`Switch is off`:
> $V_{GS}> -|V_{t_p}|$or $V_{SG}< |V_{t_p}|$
> **Real Model: 我们会用一个电容和电阻表示**`**PMOS**`**来模拟**`**Delayed Behavior**`**:**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684331140710-327ec5c6-c93f-4158-affd-f1a318747ecf.png#averageHue=%23f9e8e5&clientId=ud3c484e6-5e0d-4&from=paste&id=nzRN9&originHeight=168&originWidth=989&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=53671&status=done&style=none&taskId=uc1b23df3-e6c3-431d-806c-6f5eb42b50c&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684331153922-11dcf942-a6e3-44ea-9d84-73882569d5e3.png#averageHue=%23fdeeee&clientId=ud3c484e6-5e0d-4&from=paste&id=t9CEa&originHeight=350&originWidth=892&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=22239&status=done&style=none&taskId=u38a476d7-13d5-4c37-9e22-8a3bf650cc6&title=)


## NMOS vs PMOS
> 简单理解:
> `NMOS`:
>  $V_{in}\uparrow$: Closed
>  $V_{in}\downarrow$: Open
> `PMOS`:
>  $V_{in}\uparrow$: Open
>  $V_{in}\downarrow$: Closed


## Charge Puddle Model - Physics
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684843793635-d29e7f57-a6b8-4628-aea4-cce094c5b3c2.png#averageHue=%23ebe7e3&clientId=u19b50310-a067-4&from=paste&id=ucd1dbcf9&originHeight=394&originWidth=1452&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=130067&status=done&style=none&taskId=u8688aa31-90fa-4b67-a7b6-8fe06039eff&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684845363960-be029a75-2ef0-4eab-9798-578d2c9ae547.png#averageHue=%23fefefe&clientId=u19b50310-a067-4&from=paste&id=ucaeccde0&originHeight=553&originWidth=1465&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=148156&status=done&style=none&taskId=u6ed45b89-2150-40b6-9960-00c2a772d46&title=)




# Logic Gates
## NOT GATE - CMOS
### Definition
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684329525208-cc4f84f2-b58d-47c1-acfb-24ffe505854e.png#averageHue=%23fdeded&clientId=ud3c484e6-5e0d-4&from=paste&id=uf0793f90&originHeight=716&originWidth=975&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=63271&status=done&style=none&taskId=ua63456cd-a5e8-48a6-9c27-d791894aba9&title=)
> 🔔在上图中我们有如下的`Notations`:
> - $V_{thn}$表示`NMOS`中的`Threshold`
> - $V_{thp}$表示`PMOS`中的`Threshold`
> - $V_{SS}=0V$表示接地`Terminal` 
> - $V_{dd}$表示最上端的`Terminal`
> 
![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684803128577-61615a18-77ad-400f-a948-73e4645f4011.png#averageHue=%23fefefe&clientId=u19b50310-a067-4&from=paste&height=351&id=u5307cbe0&originHeight=548&originWidth=1400&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=103920&status=done&style=none&taskId=u5814eac7-1ae9-4deb-993c-b24eb0d181a&title=&width=896)
> 🔔我们一般会有以下假设:
> 1. $V_{thn}+|V_{thp}|\geq V_{dd}$时
> 2. $0\leq V_{thn}\leq V_{dd}$
> 3. $0\leq |V_{thp}|\leq V_{dd}$
> 
**当上述三个条件都满足时，当左侧输入**$V_{in}$**时有且仅有一个**`**Transistor**`**的电路会被接通**（Also a Sanity Check, 两个通路不能同时接通）：
> 1. 当输入的电压$V_{in}=0V$(`Logic 0 False`)时，输出的电压$V_{out}=V_{dd}=[0.7V,1.0V]$:
> 
![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684803627237-a9f6ce56-29ad-48d3-8a0b-2bd2a0d61a05.png#averageHue=%23fefefe&clientId=u19b50310-a067-4&from=paste&height=362&id=u67a5bdc5&originHeight=566&originWidth=1413&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=159098&status=done&style=none&taskId=u363cf742-1565-4f1c-ab25-f41e9792e23&title=&width=904.32)
> 2. 当输入的电压$V_{in}=V_{dd}=1V$(`Logic 1，True`)时, 输出的电压是$0V$, 相当于$not~V_{in}$:
> 
![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684804316906-b0a49c49-6677-4248-a2ad-0d589d5895ef.png#averageHue=%23fefefe&clientId=u19b50310-a067-4&from=paste&id=ua6ff42b6&originHeight=652&originWidth=1406&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=178233&status=done&style=none&taskId=ub0b4e2ad-a0ed-4f95-966b-4c77fc451f2&title=)
> **Real Model:**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685614854263-78773ba2-b066-46cc-9bf0-7f491aac5b85.png#averageHue=%23f8f8f7&clientId=u2e64c21c-9930-4&from=paste&id=ue1c85088&originHeight=532&originWidth=951&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=62217&status=done&style=none&taskId=u239ed29d-712e-4a9b-87b3-35dd56b93fa&title=)



### Circuit Analysis Caveats
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685614926888-59e2bb08-8372-49d0-8a98-756cf45edbe3.png#averageHue=%23f5f5f5&clientId=u2e64c21c-9930-4&from=paste&id=ub639bff2&originHeight=708&originWidth=1419&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=179293&status=done&style=none&taskId=ucf4363f1-7c22-4a35-bab9-6a14de02000&title=)
> 如果此时$V_{in}=5V$, 则$V_{GS, P}=V_{in}-V_{DD}=0V$, 所以`PMOS`是`Closed`，而$V_{GS,N}=V_{in}-0V=5V$, 所以`NMOS`是`Open`的。
> 此时要注意我们不需要把两个电容考虑进来，因为这两个电容两端的电压都是不变的，所以电流均为零，可以看成`Open Circuit`。
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685615234913-ec390578-da6a-48a8-ba48-ce05ba616a12.png#averageHue=%23f6f6f6&clientId=u2e64c21c-9930-4&from=paste&height=252&id=ufa264d30&originHeight=1007&originWidth=1495&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=153189&status=done&style=none&taskId=u7d5a49af-ce9e-4749-a2e0-ca2d4917f94&title=&width=374)
> 只需要考虑下面的模型即可:
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685615281485-ad169446-3889-4806-bad9-6562f3cac3d7.png#averageHue=%23f9f9f9&clientId=u2e64c21c-9930-4&from=paste&height=234&id=u7e8869ef&originHeight=365&originWidth=1441&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=62674&status=done&style=none&taskId=ue573bb06-fe86-4bbd-a924-c704ab57687&title=&width=922.24)

 




## Multi-NOT GATE - Ring Oscillator
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684330421964-3af5c4bb-6233-43dc-9d4b-42e8793d0211.png#averageHue=%23faebeb&clientId=ud3c484e6-5e0d-4&from=paste&id=Thusw&originHeight=607&originWidth=977&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=37835&status=done&style=none&taskId=u6b2a28e7-31a4-4b5f-9516-999f1fb318c&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684840325316-b5cd3944-8c83-4eb0-88d0-37e7f1f854f3.png#averageHue=%23fefdfc&clientId=u19b50310-a067-4&from=paste&id=FcnJa&originHeight=775&originWidth=1406&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=161101&status=done&style=none&taskId=udc21500b-e664-4b9c-9c1c-250f5299645&title=)
> **Real Model:**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685539156108-b4e0fcef-905a-4bcb-91fe-1c4f77006ba9.png#averageHue=%23f8f8f7&clientId=u98a90371-fd23-4&from=paste&id=u5788033a&originHeight=863&originWidth=1611&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=106582&status=done&style=none&taskId=ude9c02dd-a958-4899-9710-1943d53fa6b&title=)



## NAND GATE
> **From Discussion 01A Fa21**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685538000807-06525115-0c21-488b-80ba-a704ab8f2500.png#averageHue=%23fbfafa&clientId=ue636e274-5454-4&from=paste&id=u3bce326a&originHeight=1030&originWidth=1558&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=123445&status=done&style=none&taskId=u4faa4e60-c945-4500-9155-08999fe2b8f&title=)

**Proof of Validity**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685538596397-900e6294-be56-4a35-868d-115c0b22af72.png#averageHue=%23f5f4f2&clientId=ue636e274-5454-4&from=paste&id=u56a381d8&originHeight=112&originWidth=1681&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=42156&status=done&style=none&taskId=u01bbfd4a-b10d-45b6-a7c5-5952f366f42&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685538602395-599c628d-09e2-4145-8544-269d91bc3cf8.png#averageHue=%23fefefd&clientId=ue636e274-5454-4&from=paste&id=u2b5af202&originHeight=1134&originWidth=1705&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=462354&status=done&style=none&taskId=u95cdc2be-8f4d-407a-954e-e05b5baaf71&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685538607236-0d99432d-5813-4810-8835-2b6b455d1203.png#averageHue=%23fdfdfd&clientId=ue636e274-5454-4&from=paste&id=u2e05c40d&originHeight=717&originWidth=1645&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=63738&status=done&style=none&taskId=u380e3b65-f29e-436c-ab0b-584e089ca07&title=)



# Cascading Logic
## Example 1 - Low to High
### Circuit Model⭐⭐⭐⭐⭐
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684918791520-e909d37f-5532-4c3b-b9e9-2aa90c57871a.png#averageHue=%23fefdfd&clientId=ub8844205-b80f-4&from=paste&id=Rxnv4&originHeight=760&originWidth=1276&originalType=binary&ratio=1.875&rotation=0&showTitle=false&size=167146&status=done&style=none&taskId=ue09960fd-b1d0-47a9-9a64-b14902bde41&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684919463696-b47df592-3194-40af-8bfc-dd176d216e3a.png#averageHue=%23e4e5ee&clientId=ub8844205-b80f-4&from=paste&id=u60c271c3&originHeight=660&originWidth=1532&originalType=binary&ratio=1.875&rotation=0&showTitle=false&size=711127&status=done&style=none&taskId=u1ab43cd0-7b9d-4c3a-8eb8-786221f93a1&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684934935062-20a2a7ef-5abf-485f-851e-39725f018a73.png#averageHue=%23fdfcfb&clientId=ub8844205-b80f-4&from=paste&id=u44299229&originHeight=664&originWidth=941&originalType=binary&ratio=1.875&rotation=0&showTitle=false&size=154450&status=done&style=none&taskId=u13f50522-2b0e-4fb5-87db-57844db0cda&title=)
> **❔: 为什么**$V_x(0)=V_{DD}$**?**
> 这涉及到电路稳定，因为在$V_{in}=0V$经过很长时间后，电路最终会趋于稳定，此时电路中不应该有电流，所以电容$C_{GP,2},C_{GN,2}$两端的电压均为零，所以$V_x=V_{DD}$。
> 也可以参考`Example 2`中的推导。
> **❔：为什么不需要考虑左侧电容和右侧电阻（为什么只要考虑三个电子元件就能得到目标电压方程）？**
> 因为流经左侧电容和右侧电阻的电流不会对中间的电压计算产生影响。我们的KCL只需要关注三个电子元件即可。
> **几个注意点:**
> 1. 一旦开关闭合，左侧电容就会被`shorted`。
> 2. **第二个**`**CMOS**`**的电阻不需要考虑（计算**$V_{out}$**的时候只需要考虑三个电子元件）**






### Circuit Analysis(Solving Differential Equations)
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685611828530-73ce49a6-5a1d-423f-a6d5-93fdfa44d1bc.png#averageHue=%23fefefe&clientId=u48534cec-a337-4&from=paste&height=996&id=u5b84cc36&originHeight=1557&originWidth=1857&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=224426&status=done&style=none&taskId=uf5c37e28-8e18-4943-8d8b-3afed6e8780&title=&width=1188.48)

**Set Up DE**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685611841861-0ec122cd-e8bb-48b2-94c9-e2c2c56ea4ac.png#averageHue=%23ffffff&clientId=u48534cec-a337-4&from=paste&id=u8a6a4259&originHeight=768&originWidth=1856&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=144730&status=done&style=none&taskId=uf043fbe1-cbe0-44cf-b1ab-00df65afb37&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685611844582-6ea8ff35-7b9a-4dd6-ba33-c6c673f9616f.png#averageHue=%23ffffff&clientId=u48534cec-a337-4&from=paste&id=uf392a09c&originHeight=959&originWidth=1856&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=151424&status=done&style=none&taskId=u6b4fc71d-6ec4-4f96-8e8e-c3ef507f07e&title=)
**Solving DE**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685611883629-0f08d6df-ef3e-48f1-89cd-dfcf3673a18b.png#averageHue=%23fefdfd&clientId=u48534cec-a337-4&from=paste&id=u1df135d7&originHeight=1308&originWidth=1877&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=239402&status=done&style=none&taskId=u40a950bf-a954-4158-a678-f67e9163c87&title=)
**Sketch the Output**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685611899138-c11d136b-6e0d-4232-a5d0-22fb2c0cc0c0.png#averageHue=%23f5f4f3&clientId=u48534cec-a337-4&from=paste&height=246&id=uc71436d6&originHeight=385&originWidth=1889&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=126192&status=done&style=none&taskId=ue153b83c-8a1a-4952-b596-393680f6cb9&title=&width=1208.96)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685611903438-db7032ae-1373-4a6f-a2c4-6cf4af5a17f7.png#averageHue=%23fefefe&clientId=u48534cec-a337-4&from=paste&height=1092&id=u02b3fce6&originHeight=1707&originWidth=1817&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=264198&status=done&style=none&taskId=ub968dc53-d02b-49d9-9bef-343bcd33048&title=&width=1162.88)
**Comparative Analysis - Different Values of RC**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684935601630-9690f1d0-858f-463e-ae5b-3ad7f16b664e.png#averageHue=%23fefefd&clientId=ub8844205-b80f-4&from=paste&id=xmLAA&originHeight=547&originWidth=806&originalType=binary&ratio=1.875&rotation=0&showTitle=false&size=102449&status=done&style=none&taskId=u33ab1092-38e3-413e-ae33-42f6d7a3003&title=)


## Example 2 - High to Low
### Circuit Model
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684939539089-c7636327-562d-48c6-8459-99a140ed7d02.png#averageHue=%23fdfcfc&clientId=ub8844205-b80f-4&from=paste&id=u6ea7d650&originHeight=560&originWidth=801&originalType=binary&ratio=1.875&rotation=0&showTitle=false&size=106537&status=done&style=none&taskId=uce19d644-4249-4bf2-97b2-512b87fccf8&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684939715440-7b9468e0-687e-45a5-a402-91ad3aa84057.png#averageHue=%23f5f6cf&clientId=ub8844205-b80f-4&from=paste&id=u7508ae37&originHeight=503&originWidth=956&originalType=binary&ratio=1.875&rotation=0&showTitle=false&size=471563&status=done&style=none&taskId=ua708023f-c89d-4542-936e-0daaa98e717&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684939824978-14a65a61-3923-408e-bc1e-f03b8f0924d0.png#averageHue=%23f5f796&clientId=ub8844205-b80f-4&from=paste&id=u03650db8&originHeight=419&originWidth=808&originalType=binary&ratio=1.875&rotation=0&showTitle=false&size=106278&status=done&style=none&taskId=u89acc5d3-2b9b-446f-85bd-d3a1b9abfc0&title=)



### Circuit Analysis(Solving Differential Equations)
> `KCL`: $I_1+I_2+I_3=0\quad(1)$
> `Elements`: 
> 1. $V_1=I_1\cdot R_{on, n1}=V_x-V_{dd}$, $I_1=\frac{V_1}{R_{on, n1}}$
> 2. $I_2=C_{G_{n2}}\cdot \frac{dV_2}{dt}$, $V_2=V_x$
> 3. $I_3=C_{G_{p2}}\cdot \frac{dV_3}{dt}$, $V_3=V_x-V_{dd}$
> 
将`Elements`代入$(1)$中有:
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684939858264-901d1409-8f1a-4fec-9415-034f8eb4bc36.png#averageHue=%23edf1f7&clientId=ub8844205-b80f-4&from=paste&height=243&id=ue1752b28&originHeight=456&originWidth=847&originalType=binary&ratio=1.875&rotation=0&showTitle=false&size=96697&status=done&style=none&taskId=u38e7f753-f5fb-4101-8695-a0a61202eb7&title=&width=451.73333333333335)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684939864319-b36007d7-66a7-4582-b425-9f6fe450ae2a.png#averageHue=%23ecf0f7&clientId=ub8844205-b80f-4&from=paste&height=281&id=uec0203ca&originHeight=527&originWidth=851&originalType=binary&ratio=1.875&rotation=0&showTitle=false&size=120516&status=done&style=none&taskId=u52377aef-50be-4066-ba52-e569248ab55&title=&width=453.8666666666667)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684939874762-7af96a94-05d2-4dff-9ac6-ab8a2b8a0d0f.png#averageHue=%23fefef7&clientId=ub8844205-b80f-4&from=paste&height=322&id=u893c345f&originHeight=604&originWidth=859&originalType=binary&ratio=1.875&rotation=0&showTitle=false&size=111640&status=done&style=none&taskId=u81bb66dc-720a-4e4c-be90-006a2763194&title=&width=458.1333333333333)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684939880546-1567421e-5bb2-439e-a12d-84b9063d79eb.png#averageHue=%23fbfca7&clientId=ub8844205-b80f-4&from=paste&height=242&id=u1fc23d72&originHeight=454&originWidth=846&originalType=binary&ratio=1.875&rotation=0&showTitle=false&size=118351&status=done&style=none&taskId=uaae77018-2682-46ba-a883-f8115036c39&title=&width=451.2)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684940325313-84455ac0-d90e-4633-81b7-3cae747aed37.png#averageHue=%23fefdfd&clientId=ub8844205-b80f-4&from=paste&height=280&id=uf199897d&originHeight=525&originWidth=872&originalType=binary&ratio=1.875&rotation=0&showTitle=false&size=97743&status=done&style=none&taskId=u47ff130d-5123-4b8b-8455-66215d1ad56&title=&width=465.06666666666666)




## Equivalent Circuit
> **HW02 Sp23 P4**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687009179981-e3921268-9380-4a02-8a58-bfa89c81fc0a.png#averageHue=%23eeeeee&clientId=u96849afe-afaa-4&from=paste&id=uc36899f3&originHeight=71&originWidth=1468&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=19818&status=done&style=none&taskId=uc088248d-ce91-48f5-ab0b-926251272bd&title=)

**(a) NMOS**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687009208533-5ad00f48-d748-4bba-9bd5-75d8507e600e.png#averageHue=%23fbfbfb&clientId=u96849afe-afaa-4&from=paste&id=u4b97f3be&originHeight=1251&originWidth=1454&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=92958&status=done&style=none&taskId=u97aad8d4-4d50-40e1-8b9c-21fde6ebf8f&title=)
**(b) PMOS**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687009226997-cbe7140c-82ca-4b5f-9e0f-0c33a056f895.png#averageHue=%23f9f9f9&clientId=u96849afe-afaa-4&from=paste&id=u98169629&originHeight=482&originWidth=1424&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=39546&status=done&style=none&taskId=u894287c4-c1ba-4ab4-a53c-d8f18be353c&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687009233439-620315a2-c310-4648-b2e4-2d6476e73641.png#averageHue=%23fafafa&clientId=u96849afe-afaa-4&from=paste&id=u51bebbcf&originHeight=837&originWidth=1593&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=80899&status=done&style=none&taskId=u65664127-96e4-4984-b1ae-b555ef0d954&title=)
**(c) CMOS**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687009296436-d5c5c77e-6049-4f00-a487-debca9d4e515.png#averageHue=%23f9f9f9&clientId=u96849afe-afaa-4&from=paste&id=ubb0f2153&originHeight=471&originWidth=1495&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=35316&status=done&style=none&taskId=u9564124e-b194-4832-a964-1d8a4a95da3&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687009304092-7714935f-ab92-4283-83b3-0ae7bfd8ba8d.png#averageHue=%23fafafa&clientId=u96849afe-afaa-4&from=paste&id=u5f24e187&originHeight=1369&originWidth=1588&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=202033&status=done&style=none&taskId=u2a7997e0-b34c-4bf6-9021-c2fc63b12f4&title=)


## Cascading Circuit
> **HW01 Fa21 P7**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687046161083-31b0b56b-0ad1-404c-b32c-a412e13e853b.png#averageHue=%23faf8f7&clientId=ubfcbc8f1-ed84-4&from=paste&id=u3a8f83b9&originHeight=1243&originWidth=1107&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=288851&status=done&style=none&taskId=ucd3bcb4a-0a63-4794-b421-bfde78d0b32&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687046164852-2370880c-e944-4c76-8651-5f0f26c78332.png#averageHue=%23f8f7f5&clientId=ubfcbc8f1-ed84-4&from=paste&id=u866e87e0&originHeight=153&originWidth=1074&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=40974&status=done&style=none&taskId=uaa5f5d3a-0d47-4f72-b7ef-4d1e2711863&title=)

**(a)**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687047178507-01581df3-7c68-4d3e-ae27-37d3bbea2017.png#averageHue=%23ffffff&clientId=ubfcbc8f1-ed84-4&from=paste&id=ud7e2b2e9&originHeight=138&originWidth=974&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=28852&status=done&style=none&taskId=uf74ad385-4081-4e84-afdd-3b791a90d4d&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687047187478-7494b6f1-3821-46da-9d79-41b56ed474ff.png#averageHue=%23fefefe&clientId=ubfcbc8f1-ed84-4&from=paste&id=u21a56cd1&originHeight=1129&originWidth=873&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=141393&status=done&style=none&taskId=u14b5454e-2867-439c-a37b-48adbc56394&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687047211374-7f67cb98-5ea9-421c-a64a-7b71d3414e6c.png#averageHue=%23ffffff&clientId=ubfcbc8f1-ed84-4&from=paste&id=u94e69ff0&originHeight=210&originWidth=842&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=26765&status=done&style=none&taskId=u3a13a0a9-bc65-412b-890d-815087df3a9&title=)
**(b)**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687047241235-2d615de2-7b03-4689-aec3-4e0ea786a194.png#averageHue=%23fefefe&clientId=ubfcbc8f1-ed84-4&from=paste&id=ua9932651&originHeight=251&originWidth=1009&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=32314&status=done&style=none&taskId=uc81810b2-99b2-4937-b62a-21bb780d0d8&title=)
**(c)**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687047317181-6189d1b7-f27f-4020-bb03-62bac52a1d72.png#averageHue=%23ffffff&clientId=ubfcbc8f1-ed84-4&from=paste&id=u02a77ed4&originHeight=665&originWidth=1021&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=112342&status=done&style=none&taskId=udbfbf152-8932-45f2-a714-9ea94aa4da3&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687047337135-d6621cef-d592-4cdf-b68d-af6333c78f75.png#averageHue=%23fefefe&clientId=ubfcbc8f1-ed84-4&from=paste&id=u9d067f1d&originHeight=558&originWidth=1028&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=32767&status=done&style=none&taskId=u7ebb8fdd-6521-4025-8dc6-df64a3b0bb2&title=)
**(d)**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687047350133-86f13e90-6271-440e-a8a3-797b08740da2.png#averageHue=%23fefefe&clientId=ubfcbc8f1-ed84-4&from=paste&id=ua383fbf1&originHeight=632&originWidth=1014&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=46468&status=done&style=none&taskId=uf0b867aa-a16e-4450-8e43-a38abca3b9d&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687047362422-09fd2ac6-19da-4324-ada6-5d5fe293d274.png#averageHue=%23ffffff&clientId=ubfcbc8f1-ed84-4&from=paste&id=u5e92a770&originHeight=1302&originWidth=1006&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=149126&status=done&style=none&taskId=uecdc6ca4-74e1-4d0f-a6cc-c45da56aa54&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687047371733-e3417ab6-3934-475f-8f38-c2f1766ed757.png#averageHue=%23fefefe&clientId=ubfcbc8f1-ed84-4&from=paste&id=u6ecb4845&originHeight=938&originWidth=1024&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=95555&status=done&style=none&taskId=u211b2d32-aca5-4813-b902-a555eacc4d3&title=)



# Transistors with RC Circuit
> **Disc02A Sp23 P1**
> 之前的`Transistor`模型我们都是假设`Gate`是直接和$V_{in}$相连的，所以$V_{in}$的变化会立即反应到$V_G$上，但是本题中我们移除这一假设，我们探究如果$V_{in}$和`Gate`之间有一个电阻的情况，这其实就是最简单的`RC`电路，如下图所示:
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687926766046-84487196-1835-461a-b327-d55b3e26af44.png#averageHue=%23fafaf9&clientId=uee33ad92-72c0-4&from=paste&id=ua4f7038c&originHeight=784&originWidth=1486&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=127481&status=done&style=none&taskId=u06a39395-37cd-4bde-95e9-c2e8be8044e&title=)
> 我们会探究不同的`NMOS`模型下$V_{out}$的变化情况, 具体有如下四种:
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687926934681-6a632016-25b1-4464-87bb-e9a7beeffb07.png#averageHue=%23faf9f9&clientId=uee33ad92-72c0-4&from=paste&id=u1207ffdd&originHeight=514&originWidth=1696&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=72726&status=done&style=none&taskId=u9e57a758-f555-4b8c-940b-879dc38eff6&title=)



## Model I
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687927002946-daa025f1-9e29-44c7-9663-f53b20abf87e.png#averageHue=%23ffffff&clientId=uee33ad92-72c0-4&from=paste&height=211&id=u5b0f7f25&originHeight=317&originWidth=1539&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=122340&status=done&style=none&taskId=u5f776887-b1a2-4a13-a7e4-deff81fbf25&title=&width=1026)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687927008032-d0e14c39-23ca-4582-81a7-0d8608fa9c94.png#averageHue=%23fefefe&clientId=uee33ad92-72c0-4&from=paste&height=496&id=u72cad10b&originHeight=744&originWidth=1608&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=61457&status=done&style=none&taskId=u0c82e124-5e1d-4614-b863-48a17d8d0ba&title=&width=1072)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687927012998-e0c303f1-9f27-4469-9c04-411a3736bc7d.png#averageHue=%23fbfafa&clientId=uee33ad92-72c0-4&from=paste&height=331&id=uf34e898b&originHeight=496&originWidth=579&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=22514&status=done&style=none&taskId=ub8023197-a879-42ed-a130-a0ed54e8a03&title=&width=386)



## Model II
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687927092285-ef5c7210-c7b9-4aa2-9aa6-10b8e31b99ee.png#averageHue=%23fefefe&clientId=uee33ad92-72c0-4&from=paste&height=681&id=ubba07470&originHeight=1021&originWidth=1504&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=182957&status=done&style=none&taskId=u423ee0da-3116-44be-a7c9-41e644f265c&title=&width=1002.6666666666666)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687927098502-3e543885-4230-4a68-b62e-dc071e977978.png#averageHue=%23fafaf9&clientId=uee33ad92-72c0-4&from=paste&height=333&id=ue00f304a&originHeight=500&originWidth=499&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=21698&status=done&style=none&taskId=u08b1adaa-6209-482f-a5b8-0f20b66fbde&title=&width=332.6666666666667)




## Model III/ IV: RC Circuit
> `Model III`和`Model IV`其实就是最基本的`RC Circuit`, 如下图所示:
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684326254440-7f5d55d7-66a5-4a5a-aa24-c9d8a21faebd.png#averageHue=%23fdfcfc&clientId=ud3c484e6-5e0d-4&from=paste&id=oJN3Q&originHeight=393&originWidth=1228&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=31839&status=done&style=none&taskId=uf88bbe36-aabc-4806-b611-64d3797b05f&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687927415464-11eef046-fc22-44b0-84ac-6efc7e3993d5.png#averageHue=%23ffffff&clientId=uc8a14aeb-ed15-4&from=paste&id=u9d7d611a&originHeight=543&originWidth=1524&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=194478&status=done&style=none&taskId=ue4b3ca1f-de75-4002-944f-cc48f21d76b&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687927422447-a5db5c20-4f4d-4636-9a98-8f33ee72a65b.png#averageHue=%23fefefe&clientId=uc8a14aeb-ed15-4&from=paste&height=525&id=u3fee672f&originHeight=788&originWidth=1614&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=87449&status=done&style=none&taskId=ua41b21a0-18d5-4fd7-bab8-2049ba4b4c6&title=&width=1076)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687927428951-71c1bd04-3814-4d55-9e36-b834b2949309.png#averageHue=%23fafafa&clientId=uc8a14aeb-ed15-4&from=paste&height=333&id=u5d7337d5&originHeight=499&originWidth=1084&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=32115&status=done&style=none&taskId=uc57f291f-8284-4627-abf8-014491f1072&title=&width=722.6666666666666)


