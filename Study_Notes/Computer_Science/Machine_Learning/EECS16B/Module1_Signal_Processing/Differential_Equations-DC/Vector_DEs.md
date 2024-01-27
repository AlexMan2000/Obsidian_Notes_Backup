# Vector DEs Basics
## RCRC Circuit
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685796458591-ad339a44-b09c-49a9-96a6-30bab2617593.png#averageHue=%23fbfbfb&clientId=u991821ae-921c-4&from=paste&id=udd8aa669&originHeight=361&originWidth=1086&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=27846&status=done&style=none&taskId=uc6405083-b403-4440-862d-af70676fbd6&title=)
> 下面的系统一般称为`RCRC Circuit`, 也是最常见的二维系统。


### Steady State
> 对于这个系统，稳定状态指的是两个电容两端的电压都不发生变化，即$\frac{dV_{C_1}(t)}{dt}=\frac{dV_{C_2}(t)}{dt}=0$, 即$I_{C_1}=I_{C_2}=0$。同时如果我们对`Node 1`和`Node 2`使用`KCL`的话，我们会得到$I_2=0$, $I_1-I_2=0$, 即$I_1=0$。所以$I_1=I_2=0$。这就意味着电流流过电阻$R_1$和$R_2$时没有电势下降，也就是说$V_{C_1}=V_{C_2}=V_{in}$。
> **所以综上所述：**
> - 如果$V_{in}=0V$且经过了足够长的时间使得系统达到了稳定状态，则$V_{C_1}=V_{C_2}=0V$。
> - 如果$V_{in}=1V$且经过了足够长的时间使得系统达到了稳定状态，则$V_{C_1}=V_{C_2}=1V$。
> 
**简单记忆法，对于**`**RCRC**`**电路来说，**$V_{C_1}$**和**$V_{C_2}$**的稳定状态下的电压值和**$V_{in}$**的电压值一致。**


### Transient State
> 对于这个系统，`Transient State`指的是，输入$V_{in}$发生变化后$V_{C_1}$和$V_{C_2}$以及$I_{C_1}$和$I_{C_2}$相应的变化情况。假设$t<=0$时，$V_{in}=1V$，$t>0$时$V_{in}=0V$, 则假设$t<\infty$, 即电路尚未达到稳定状态，则我们对电路使用`Circuit Analysis`可得:
> $\begin{aligned} I_1&=I_{C_1}+I_{C_2}\\V_{in}(t)-I_1R_1&=V_{C_1}(t)\\V_{C_1}(t)-I_{C_2}R_2&=V_2(t)\end{aligned}$
> 根据电容性质我们有:
> $\begin{aligned}I_{C_1}&=\frac{dV_{C_1}(t)}{dt}C_1\\I_{C_2}&=\frac{dV_{C_2(t)}}{dt}C_2\end{aligned}$
> 最终我们可以得到:
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685798009572-6cf26dd0-3b94-4366-9cd1-3c589384bc53.png#averageHue=%23fcfbfa&clientId=u991821ae-921c-4&from=paste&height=120&id=u2f05bd0b&originHeight=187&originWidth=966&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=29059&status=done&style=none&taskId=u0184dbf1-9bf1-4b69-b1c8-4902da02c3e&title=&width=618.24)


### Vector Differential Equations
> 我们可以把上述二维微分方程写成向量形式, 我们定义$\vec{x}(t)=\begin{bmatrix} V_1(t) \\V_2(t)\end{bmatrix}$: 
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685798070874-4d6d0d5b-0b94-4088-93fc-6c998588f0cb.png#averageHue=%23fcfbfa&clientId=u991821ae-921c-4&from=paste&id=u535e5758&originHeight=163&originWidth=850&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=15819&status=done&style=none&taskId=u40ab358c-1c93-458d-8746-e9e3fce283a&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685801037463-ea78c5e9-b097-43b1-91a6-73009f86d34e.png#averageHue=%23fcfbfb&clientId=u991821ae-921c-4&from=paste&id=u8bf7bad5&originHeight=245&originWidth=864&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=24135&status=done&style=none&taskId=u85153a9f-71a4-402d-bf6f-5dd4ff4ac70&title=)



### General Case
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685801105904-fef6465e-91d3-49da-a5af-007a2d255c34.png#averageHue=%23fcfbfa&clientId=u991821ae-921c-4&from=paste&id=udcb6e2d4&originHeight=157&originWidth=1238&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=24563&status=done&style=none&taskId=u278b30d0-9470-4f14-b0e8-d22a3f52a55&title=)
> 当输入电压$V_{in}=0V$时，$\vec{b}=\vec{0}$, 因为没有额外的电压输入系统。



## LC Tank
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687242334463-1ff59e76-e17f-44fc-bb70-46eb8d5acf32.png#averageHue=%23fcfbfb&clientId=ude6e3a59-bf7d-4&from=paste&height=310&id=u7d582d20&originHeight=465&originWidth=1361&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=58424&status=done&style=none&taskId=u9b99ad24-8c75-4d13-8f3f-c40c8de5176&title=&width=907.3333333333334)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687242346865-165533ff-61a1-417a-9e17-6075cd53bbf9.png#averageHue=%23fdfdfc&clientId=ude6e3a59-bf7d-4&from=paste&height=663&id=u4964ff1d&originHeight=995&originWidth=1403&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=111310&status=done&style=none&taskId=ube8d4cbe-9717-4757-8517-38a76c43e24&title=&width=935.3333333333334)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687242355493-ef27f4e0-e07f-41b0-bd49-94ac90e6a2e7.png#averageHue=%23fcfcfb&clientId=ude6e3a59-bf7d-4&from=paste&height=489&id=u58811f59&originHeight=733&originWidth=1374&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=98338&status=done&style=none&taskId=u1b87725a-c2ab-478e-837b-455327a1870&title=&width=916)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687242364740-ea751cbc-1eff-48c8-9055-38685e8df8bb.png#averageHue=%23fcfbfa&clientId=ude6e3a59-bf7d-4&from=paste&height=478&id=u4f18f042&originHeight=717&originWidth=1343&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=117753&status=done&style=none&taskId=u8ce3fadb-09ac-482c-b345-0ab7aa0aab7&title=&width=895.3333333333334)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687242369596-f477c758-bd1c-4a9f-8038-fab2ee1152d6.png#averageHue=%23fbfaf9&clientId=ude6e3a59-bf7d-4&from=paste&height=121&id=u2a0570f1&originHeight=181&originWidth=1333&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=37890&status=done&style=none&taskId=u22392b23-1749-4633-949a-6f359837f6f&title=&width=888.6666666666666)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687242373737-688f6888-e6e7-4b77-849b-b7712f6634fe.png#averageHue=%23fcfcfb&clientId=ude6e3a59-bf7d-4&from=paste&height=338&id=u8c613e47&originHeight=507&originWidth=1299&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=78999&status=done&style=none&taskId=ua8637597-0548-472e-9222-1c807203763&title=&width=866)

**Current**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687242411589-f4271f18-240d-4aa4-9b6a-c24d0b26e68f.png#averageHue=%23fcfbfb&clientId=ude6e3a59-bf7d-4&from=paste&height=657&id=u9fb1dde2&originHeight=985&originWidth=1374&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=207004&status=done&style=none&taskId=u910a6051-d52b-4d42-b398-d543baa6f6e&title=&width=916)
**Energy Stored**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687242453693-82a553a5-c845-467b-9d98-a241635beefb.png#averageHue=%23fbfafa&clientId=ude6e3a59-bf7d-4&from=paste&id=uea602bfd&originHeight=1113&originWidth=1327&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=244728&status=done&style=none&taskId=u8a090c5f-1f7b-477d-8d2d-5146d3ecaa6&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687242444383-ef8e9889-39f2-4d63-9608-4cfc7e980d28.png#averageHue=%23fbf8f8&clientId=ude6e3a59-bf7d-4&from=paste&id=ua1a26dc6&originHeight=966&originWidth=1399&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=289940&status=done&style=none&taskId=u7f5daa8f-b78a-4424-ad22-e5dbe8610ba&title=)


## RLC Circuit - Damping Analysis
### Circuit Damping Analysis
> **HW04 Fa21 P2~P6**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687684542382-e64fa70d-d0fc-4603-a5c2-0662b25c5386.png#averageHue=%23f9f9f9&clientId=u4ab3cf95-f1bd-4&from=paste&id=u42ecf8f7&originHeight=676&originWidth=1766&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=98337&status=done&style=none&taskId=udad3ecfe-7821-4d4f-abf3-41d9defca14&title=)
> 首先我们对电路进行`State Space`分析:
> 1. 电路中有电容和电导，分别对应状态量$V_C$和$V_L$, 电阻状态
> 2. 电路中有电压源，是一个`Independent Source`。
> 
假设状态向量是$\vec{x}(t)=\begin{bmatrix}I_L(t) \\V_C(t)\end{bmatrix}$, 我们的目标就是求出一个形如$\frac{d\vec{x}(t)}{dt}=\mathbf{A}\vec{x}(t)+\mathbf{B}\vec{b_s}$的微分方程组
> 1. **首先我们进行电路分析:**
>    1. 对于电容的状态$V_C(t)$来说，我们有$\begin{aligned}I_C(t) & =C \frac{\mathrm{d}}{\mathrm{d} t} V_C(t)=I_L(t) \\\frac{\mathrm{d}}{\mathrm{d} t} V_C(t) & =\frac{1}{C} I_L(t) .\end{aligned}$ 。
>    2. 对于电导的状态$I_L(t)$来说，我们有$V_C(t)+R I_L(t)+L \frac{\mathrm{d}}{\mathrm{d} t} I_L(t)=V_s=0$。
> 
于是整理之后可得:
> $\left[\begin{array}{l}\frac{\mathrm{d}}{\mathrm{d} t} x_1(t) \\\frac{\mathrm{d}}{\mathrm{d} t} x_2(t)\end{array}\right]=\left[\begin{array}{cc}-\frac{R}{L} & -\frac{1}{L} \\\frac{1}{C} & 0\end{array}\right]\left[\begin{array}{l}x_1(t) \\x_2(t)\end{array}\right]$
> 其中$\mathbf{A} = \begin{bmatrix} -\frac{R}{L}&-\frac{1}{L}\\\frac{1}{C}&0\end{bmatrix}$, $\mathbf{B}=\mathbf{0}$。
> 2. **然后我们计算矩阵**$\mathbf{A}$**的特征值和特征向量:**
>    1. **特征方程**是:$\begin{aligned}\operatorname{det}(A-\lambda I) & =\operatorname{det}\left(\left[\begin{array}{cc}-\frac{R}{L}-\lambda & -\frac{1}{L} \\\frac{1}{C} & -\lambda\end{array}\right]\right) \\& =-\lambda\left(-\frac{R}{L}-\lambda\right)+\frac{1}{L C} \\& =\lambda^2+\frac{R}{L} \lambda+\frac{1}{L C}=0 \end{aligned}$
>    2. **特征值**是: $\lambda=-\frac{1}{2} \frac{R}{L} \pm \frac{1}{2} \sqrt{\left(\frac{R}{L}\right)^2-\frac{4}{L C}}$
>    3. **特征向量**相对难求一些, 但是我们可以观察$\mathbf{A}$的形式，留意到矩阵$\mathbf{A}_{22}=0$这表明我们的特征向量的第一项不为零，即特征向量形如$\begin{bmatrix}1\\y \end{bmatrix}$。
> 
如果第一项是零，则$\mathbf{A}\vec{v_{\lambda}}=\mathbf{A}\begin{bmatrix}0\\y\end{bmatrix}=\begin{bmatrix}  -\frac{y}{L}\\0\end{bmatrix}\neq \lambda \begin{bmatrix} 0\\y\end{bmatrix}$，矛盾。
> 因为$\lambda \neq 0$，所以我们通过求解$\begin{bmatrix} -\frac{R}{L}&-\frac{1}{L}\\\frac{1}{C}&0\end{bmatrix}\begin{bmatrix} 1\\y\end{bmatrix}=\lambda\begin{bmatrix} 1\\y\end{bmatrix}$的第二个方程就可以得到$y = \frac{1}{\lambda C}$, 即特征向量是$\begin{bmatrix} 1\\\frac{1}{\lambda_1 C}\end{bmatrix}$和$\begin{bmatrix} 1\\\frac{1}{\lambda_2 C}\end{bmatrix}$。
>    4. `**Eigenbasis**`就是: $V=\begin{bmatrix} 1&1\\\frac{1}{\lambda_1 C}&\frac{1}{\lambda_2 C}\end{bmatrix}$, 如果$\lambda$是虚数，则$\overline{\lambda_1}=\lambda_2$。$V^{-1}=\frac{\lambda_1 \lambda_2 C}{\lambda_1-\lambda_2}\left[\begin{array}{cc}\frac{1}{\lambda_2 C} & -1 \\-\frac{1}{\lambda_1 C} & 1\end{array}\right]=\left[\begin{array}{cc}\frac{\lambda_1}{\lambda_1-\lambda_2} & -\frac{\lambda_1 \lambda_2 C}{\lambda_1-\lambda_2} \\-\frac{\lambda_2}{\lambda_1-\lambda_2} & \frac{\lambda_1 \lambda_2 C}{\lambda_1-\lambda_2}\end{array}\right]$，我们可以留意到，这个矩阵的按行相加可以得到一个`Real-Valued Vector`, 这表明矩阵的第一行和第二行元素是`Complex Conjugate`，我们可以验证一下:
> 
$\left[\begin{array}{cc}\frac{\lambda_1}{\lambda_1-\lambda_2} & -\frac{\lambda_1 \lambda_2 C}{\lambda_1-\lambda_2} \\-\frac{\lambda_2}{\lambda_1-\lambda_2} & \frac{\lambda_1 \lambda_2 C}{\lambda_1-\lambda_2}\end{array}\right]\begin{bmatrix} x\\y\end{bmatrix}=\begin{bmatrix} \frac{\lambda_1}{\lambda_1-\lambda_2}x-\frac{\lambda_1 \lambda_2 C}{\lambda_1-\lambda_2}y\\-\frac{\lambda_2}{\lambda_1-\lambda_2}x+\frac{\lambda_1 \lambda_2 C}{\lambda_1-\lambda_2}y\end{bmatrix}$，假设$x,y$均为实数。
> 则我们对第一行取共轭，$\overline{ \frac{\lambda_1}{\lambda_1-\lambda_2}x-\frac{\lambda_1 \lambda_2 C}{\lambda_1-\lambda_2}y}=\frac{\overline{\lambda_1}}{\overline{\lambda_1}-\overline{\lambda_2}}x-\frac{\overline{\lambda_1}\times \overline{\lambda_2}C}{\overline{\lambda_1}-\overline{\lambda_2}}y=\frac{\lambda_2}{\lambda_2-\lambda_1}x-\frac{\lambda_1\lambda_2C}{\lambda_2-\lambda_1}y$和第二行一样。
> 3. **根据**$R,L,C$**的相对大小关系电路会有四种状态:**
>    1. `Overdamped`: 此时对应特征值为不相等的实数，即$(\frac{R}{L})^2-\frac{4}{LC}>0$, 即$R>2 \sqrt{\frac{L}{C}}$。
>    2. `Undamped`: 此时对应特征值只有虚数部分，即$R=0$, 且$(\frac{R}{L})^2-\frac{4}{LC}<0$。
>    3. `Underdamped`: 此时对应特征值实部和虚部均不是零，即$R\neq 0$, 且$(\frac{R}{L})^2-\frac{4}{LC}<0$
>    4. `Critically Damped`: 此时对应$(\frac{R}{L})^2-\frac{4}{LC}=0$, 即$R=2\sqrt{\frac{L}{C}}$。
> 4. 解的形式，对于一个微分方程组$\frac{d \vec{x}(t)}{dt}=\mathbf{A}\vec{x}(t)$来说，我们对$\mathbf{A}_{2\times 2}$求特征值:
>    1. $\lambda_1\neq \lambda_2$且均为实数，对应`Overdamped Case`, 微分方程的解为$x_{1,2}(t)=K_1e^{\lambda_1 t} + K_2e^{\lambda_2 t}$
>    2. $\lambda_1\neq \lambda_2$且均为纯虚数，对应`Undamped Case`, 微分方程的解为$x_{1,2}(t)=Acos(\lambda t-\phi)$
>    3. $\lambda_1\neq \lambda_2$且均为虚数(实部和虚部均不为零)，对应`Underdamped Case`, 微分方程的解为$x_{1,2}(t)=K_1e^{Re(\lambda_1) t}cos(Im(\lambda_1)t) + K_2e^{Re(\lambda_2) t}sin(Im(\lambda_2)t)$
>    4. $\lambda_1=\lambda_2=\lambda$对应`Critically Damped Case`, $x_{1,2}(t)=(K_1+K_2t)e^{\lambda t}$。
> 
下面我们逐个探究:

 

### Overdamped(Distinct Real)
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687687798647-400c4566-c4ab-4a88-ab84-6d17fc48e2fd.png#averageHue=%23f8f8f8&clientId=u1de99591-f141-4&from=paste&id=u1e1de7db&originHeight=534&originWidth=1450&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=55976&status=done&style=none&taskId=u1d120e3b-3d99-4b9b-ada2-0f0789dcc41&title=)
> $\lambda_1=-1.0 \times 10^5, \quad \lambda_2=-4.0 \times 10^7$
> $I_L(t)=-0.001 \mathrm{e}^{-\left(1.0 \times 10^5\right) t}+0.001 \mathrm{e}^{-\left(4.0 \times 10^7\right) t}$
> $V_C(t)=\mathrm{e}^{-\left(1.0 \times 10^5\right) t}-0.0025 \mathrm{e}^{-\left(4.0 \times 10^7\right) t}$
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687689876100-1cef423f-a40a-4a10-a534-de20b513bd61.png#averageHue=%23f8f8f8&clientId=u1de99591-f141-4&from=paste&id=u7d008e4f&originHeight=676&originWidth=1297&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=264819&status=done&style=none&taskId=u90d6e816-007b-4986-b15e-433c4499583&title=)
> 表现为图像无震荡。

**Derivations**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687999949717-ebc394e6-330c-4df6-be55-18fe42911c5a.png#averageHue=%23ffffff&clientId=ue36a78cd-8cf6-4&from=paste&id=u5035d4ab&originHeight=708&originWidth=1426&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=75470&status=done&style=none&taskId=uf6e88ae1-749a-4f1f-b5d6-13f18d0550e&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687999962757-f994b119-e497-4c7e-83e8-cf34563b57d2.png#averageHue=%23ffffff&clientId=ue36a78cd-8cf6-4&from=paste&id=u3114c878&originHeight=265&originWidth=1456&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=29720&status=done&style=none&taskId=u32717d1b-8793-49e5-8f30-c5584fda9d9&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687999977228-015dd8d8-6ea8-4fdf-9649-381acc9d5a5c.png#averageHue=%23ffffff&clientId=ue36a78cd-8cf6-4&from=paste&id=ue4a23389&originHeight=1034&originWidth=1550&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=94897&status=done&style=none&taskId=u827370ca-ce10-4a41-91fd-9c046d77d66&title=)

### Undamped(Two Imaginary)
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687689963791-66de80f6-026c-44c8-ad9a-733de480af13.png#averageHue=%23f6f6f6&clientId=u1de99591-f141-4&from=paste&id=u588e786c&originHeight=595&originWidth=1500&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=76334&status=done&style=none&taskId=ud5cc6317-e48b-443f-9a69-a18809cdb80&title=)
> $\lambda= \pm \mathrm{j} \sqrt{\frac{1}{L C}}= \pm \mathrm{j} \sqrt{\frac{1}{250 \times 10^{-15}}}= \pm \mathrm{j}\left(2 \times 10^6\right) \Longrightarrow \lambda_1=\mathrm{j}\left(2 \times 10^6\right), \quad \lambda_2=-\mathrm{j}\left(2 \times 10^6\right)$
> $I_L(t)=\mathrm{j}(0.01) \mathrm{e}^{+\mathrm{j}\left(2 \times 10^6\right) t}-\mathrm{j}(0.01) \mathrm{e}^{-\mathrm{j}\left(2 \times 10^6\right) t}=-0.02 \sin \left(\left(2 \times 10^6\right) t\right)$
> $V_C(t)=0.5 \mathrm{e}^{+\mathrm{j}\left(2 \times 10^6\right) t}+0.5 \mathrm{e}^{-\mathrm{j}\left(2 \times 10^6\right) t}=\cos \left(\left(2 \times 10^6\right) t\right)$
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687689892857-31502f3f-5304-4532-adb6-9d9399a6a5dd.png#averageHue=%23f8f3f3&clientId=u1de99591-f141-4&from=paste&height=478&id=u39b622d8&originHeight=717&originWidth=1312&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=428878&status=done&style=none&taskId=u7acdb410-13d2-4bec-ad70-c0e758de93b&title=&width=874.6666666666666)
> 图像震荡且振幅不衰减。

**Full Derivations**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687999846930-6cc4eccb-45a8-4ec4-adad-2889d2a14169.png#averageHue=%23ffffff&clientId=ue36a78cd-8cf6-4&from=paste&id=u7c1e98b1&originHeight=704&originWidth=1459&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=68797&status=done&style=none&taskId=u237d2c7d-1041-49b9-b139-7b4c945bd5e&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687999923841-b48b631a-24c7-4eca-81df-07b7c499598f.png#averageHue=%23ffffff&clientId=ue36a78cd-8cf6-4&from=paste&id=u38313d79&originHeight=1204&originWidth=1518&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=128344&status=done&style=none&taskId=ubc909aa4-7134-45c3-9a60-0873c9a1550&title=)


### Underdamped(Two Complex)
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687690154542-23ff571e-9eaa-4218-85b2-00abababa26f.png#averageHue=%23f6f6f6&clientId=u1de99591-f141-4&from=paste&id=uf5508d86&originHeight=572&originWidth=1507&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=72727&status=done&style=none&taskId=uad0f8d84-3ecb-4291-978f-c117fc232e7&title=)
> $\begin{aligned}& \lambda_1=-0.02 \times 10^6+\mathrm{j}\left(2 \times 10^6\right)\\& \lambda_2=-0.02 \times 10^6-\mathrm{j}\left(2 \times 10^6\right)\end{aligned}$
> $\begin{aligned}I_L(t) & =\mathrm{j}(0.01) \mathrm{e}^{\left(-0.02 \times 10^6+\mathrm{j}\left(2 \times 10^6\right)\right) t}-\mathrm{j}(0.01) \mathrm{e}^{\left(-0.02 \times 10^6-\mathrm{j}\left(2 \times 10^6\right)\right) t} \\& =\mathrm{j}(0.01) \mathrm{e}^{-\left(0.02 \times 10^6\right) t} \mathrm{e}^{\mathrm{j}\left(2 \times 10^6\right) t}-\mathrm{j}(0.01) \mathrm{e}^{-\left(0.02 \times 10^6\right) t} \mathrm{e}^{-\mathrm{j}\left(2 \times 10^6\right) t} \\& =\mathrm{e}^{-\left(0.02 \times 10^6\right) t}\left(\mathrm{j}(0.01) \mathrm{e}^{\mathrm{j}\left(2 \times 10^6\right) t}-\mathrm{j}(0.01) \mathrm{e}^{-\mathrm{j}\left(2 \times 10^6\right) t}\right) \\& =-0.02 \mathrm{e}^{-\left(0.02 \times 10^6\right) t} \sin \left(\left(2 \times 10^6\right) t\right)\end{aligned}$ 
> $\begin{aligned}V_C(t) & =(0.5-\mathrm{j}(0.005)) \mathrm{e}^{\left(-0.02 \times 10^6+\mathrm{j}\left(2 \times 10^6\right)\right) t}+(0.5+\mathrm{j}(0.005)) \mathrm{e}^{\left(-0.02 \times 10^6-\mathrm{j}\left(2 \times 10^6\right)\right) t} \\& =(0.5-\mathrm{j}(0.005)) \mathrm{e}^{-\left(0.02 \times 10^6\right) t} \mathrm{e}^{\mathrm{j}\left(2 \times 10^6\right) t}+(0.5+\mathrm{j}(0.005)) \mathrm{e}^{-\left(0.02 \times 10^6\right) t} \mathrm{e}^{-\mathrm{j}\left(2 \times 10^6\right) t} \\& =\mathrm{e}^{-\left(0.02 \times 10^6\right) t}\left((0.5-\mathrm{j}(0.005)) \mathrm{e}^{\mathrm{j}\left(2 \times 10^6\right) t}+(0.5+\mathrm{j}(0.005)) \mathrm{e}^{-\mathrm{j}\left(2 \times 10^6\right) t}\right) \\& =\mathrm{e}^{-\left(0.02 \times 10^6\right) t} \cos \left(\left(2 \times 10^6\right) t\right)+0.01 \cdot \mathrm{e}^{-\left(0.02 \times 10^6\right) t} \sin \left(\left(2 \times 10^6\right) t\right) \end{aligned}$
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687690163843-3a4908be-7634-444a-96f0-49ee124d90d0.png#averageHue=%23f8f5f4&clientId=u1de99591-f141-4&from=paste&id=u8c687bf4&originHeight=664&originWidth=1404&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=396645&status=done&style=none&taskId=ub8a635db-32b6-40b2-bac6-8cc726dfd24&title=)
> 表现为图像一边震荡一边衰减。

**Full Derivations**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688000144380-226b15bf-bc65-4082-a6f9-461af6fa8004.png#averageHue=%23ffffff&clientId=ue36a78cd-8cf6-4&from=paste&id=u255a671c&originHeight=565&originWidth=1416&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=55013&status=done&style=none&taskId=u1d621da0-4860-415a-991a-43a1e09c0b1&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688000156326-a937837a-2c77-4399-b1a9-baee59bbb854.png#averageHue=%23ffffff&clientId=ue36a78cd-8cf6-4&from=paste&id=ua240c30e&originHeight=303&originWidth=1446&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=31172&status=done&style=none&taskId=ufc36bbe5-197a-4ad7-89b3-7747fad0447&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688000163431-87df0f55-3fe9-42d0-b844-3231c340522a.png#averageHue=%23ffffff&clientId=ue36a78cd-8cf6-4&from=paste&id=u857078bf&originHeight=1158&originWidth=1487&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=185153&status=done&style=none&taskId=u9465ce51-c34f-466c-a89a-ccc73cd95ee&title=)

### Critically Damped(相等实根)**⭐⭐⭐⭐⭐**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687691748236-a27c2400-7e2b-4aab-9bdd-775ba9b1abc0.png#averageHue=%23f5f5f5&clientId=u1de99591-f141-4&from=paste&id=ue76bbfa6&originHeight=841&originWidth=2053&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=122653&status=done&style=none&taskId=u777466ac-4053-49f0-9c1b-6cfbcd311bf&title=)

**(a) Figure Out R**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687702978960-3e4cf2f6-3af4-44be-a5bc-fa0557321dce.png#averageHue=%23fcfcfc&clientId=uc73823fb-1b0c-4&from=paste&id=u930949d6&originHeight=396&originWidth=1265&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=47978&status=done&style=none&taskId=u76ca63a2-e58f-44af-94db-062f5f4a050&title=)
**(b) Deprecated Eigenspace**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687703022652-ed3c8808-7c87-4730-8408-67e3f69aad02.png#averageHue=%23f7f7f7&clientId=uc73823fb-1b0c-4&from=paste&id=u18ee1992&originHeight=608&originWidth=1240&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=100638&status=done&style=none&taskId=ua5122ebf-9dd2-465f-8f30-31caf9d8cdb&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687703031210-71cb286a-1bfd-4865-bbe1-a76e98874157.png#averageHue=%23ffffff&clientId=uc73823fb-1b0c-4&from=paste&id=uaf313716&originHeight=164&originWidth=1215&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=26309&status=done&style=none&taskId=u7f5b61bc-e53f-4bdf-a702-b969abe2c29&title=)
**(c) Complement the Eigenspace⭐⭐⭐**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687703061465-e83090b6-87e9-426e-99d7-515690f8a8b7.png#averageHue=%23f9f9f9&clientId=uc73823fb-1b0c-4&from=paste&id=uce27ee0b&originHeight=857&originWidth=1256&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=125868&status=done&style=none&taskId=u034ac9c3-ec36-42c6-9d4f-4152e1cc31f&title=)
**(d) Solve x_2(t) tilde**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687703086356-9404fd9c-20a0-45c9-88d8-d35f50c51a65.png#averageHue=%23f2f2f2&clientId=uc73823fb-1b0c-4&from=paste&id=u67a6be20&originHeight=522&originWidth=1259&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=107247&status=done&style=none&taskId=uf5d33df0-80ff-4e9e-bfc0-b793c701de2&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687703095801-5748831d-cc52-4f98-afa5-0ba75ba71a8a.png#averageHue=%23ffffff&clientId=uc73823fb-1b0c-4&from=paste&id=u158adb78&originHeight=248&originWidth=1188&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=27658&status=done&style=none&taskId=u7c9c5d7d-36b6-4039-9dd0-0d9f3e70328&title=)
**(e) Establish DE for x_1(t) tilde**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687703144787-7dbb0e1a-c300-414d-a066-d3016fccb877.png#averageHue=%23f4f4f4&clientId=uc73823fb-1b0c-4&from=paste&height=421&id=u3bea1392&originHeight=631&originWidth=1276&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=149834&status=done&style=none&taskId=uf5db758f-88a4-4964-8d6f-fc0e7fccb4f&title=&width=850.6666666666666)
**(f) Solve x_1(t) tilde - Integrating Factor**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687703184144-8f1385cf-e694-4ef2-8734-34c38cd79fcc.png#averageHue=%23fcfcfc&clientId=uc73823fb-1b0c-4&from=paste&id=uf0acd378&originHeight=781&originWidth=1227&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=105612&status=done&style=none&taskId=ubc480039-8918-4876-b46c-467898cbe17&title=)
**(g) Solve x_1(t) and x_2(t)**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687703209835-98bcad38-b758-41d3-9926-f4c995fc2447.png#averageHue=%23f9f9f9&clientId=uc73823fb-1b0c-4&from=paste&id=u7a8fe0a4&originHeight=579&originWidth=1258&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=91681&status=done&style=none&taskId=u72c35c11-280d-450d-a326-2da40db813c&title=)
**(h) Graph**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687703238612-926a6d53-4eec-4bf7-9b00-c40c5af2e3f0.png#averageHue=%23f7f7f7&clientId=uc73823fb-1b0c-4&from=paste&id=u653979ca&originHeight=921&originWidth=1302&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=302427&status=done&style=none&taskId=ubf5edbcf-35b5-4c59-bfc4-4916809c05f&title=)
**(i) How to choose complement eiganvectors - Upper Trigularization⭐⭐⭐⭐⭐**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687703269923-429f75fd-8caa-4c22-9ccd-ce78c61ab655.png#averageHue=%23f2f2f2&clientId=uc73823fb-1b0c-4&from=paste&height=49&id=u77b4b764&originHeight=74&originWidth=1277&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=15045&status=done&style=none&taskId=ub0b37e96-eba0-4a14-b8b6-e4a24b1339a&title=&width=851.3333333333334)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687703289275-a935c724-50bc-4e79-b7f0-671813160f49.png#averageHue=%23fafafa&clientId=uc73823fb-1b0c-4&from=paste&id=u42d05841&originHeight=1310&originWidth=1069&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=194285&status=done&style=none&taskId=u67b48a97-c31a-423e-9aff-013e6414bc3&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687703296218-6d453093-32dc-4042-943a-7b81cb11116f.png#averageHue=%23ffffff&clientId=uc73823fb-1b0c-4&from=paste&id=u9fc6b8fc&originHeight=270&originWidth=1000&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=61665&status=done&style=none&taskId=u5a4e0eb6-33d9-4d2b-a256-f59adeffcb3&title=)
> **HW05 Fa21 P6**
> 对于微分方程组$\frac{d}{dt}\vec{x}(t)=A\vec{x}(t)+\vec{b}u(t)$来说:
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688181686370-a630414b-a0f2-4b1f-89be-f652473ec5f2.png#averageHue=%23fbfbfb&clientId=u484b6f0e-4286-4&from=paste&id=u6bac5f35&originHeight=1115&originWidth=1345&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=311307&status=done&style=none&taskId=uaff1f85a-2ae7-4932-b6a9-8302f3f13e5&title=)


# Solving Vector DEs 
## Change of Basis
### Idea
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686216728997-a9004af6-627b-47da-96f3-e84b4024bc1c.png#averageHue=%23f9f8f7&clientId=u349f0d23-e19a-4&from=paste&id=u0d5c60e9&originHeight=1807&originWidth=1600&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=379089&status=done&style=none&taskId=ufeeac97c-492e-4487-9b74-de94d4abb1c&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687922841155-d44f252e-133a-4305-8bc0-a49e935e0b59.png#averageHue=%23fcfbfb&clientId=u355830bf-9b92-4&from=paste&id=udd64b42c&originHeight=398&originWidth=1705&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=79540&status=done&style=none&taskId=u61f37254-12d5-4f9f-a444-a9173082f27&title=)


### Example
> **HW03 Fa21 P3 Tracking Terry**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687269728412-a7ec9b56-d9c3-417a-a10c-19bf22695942.png#averageHue=%23f9f7f5&clientId=u0328a585-7e84-4&from=paste&id=JlWc4&originHeight=1069&originWidth=1214&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=297505&status=done&style=none&taskId=ucbda2408-ea8e-42ec-94bf-0ac300e3bc8&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687270825082-85e91d18-2701-46a5-9b4d-88969aa90505.png#averageHue=%23fbfbfb&clientId=u0328a585-7e84-4&from=paste&height=301&id=QaePG&originHeight=452&originWidth=703&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=14031&status=done&style=none&taskId=ue5b2d43f-8edd-428e-a684-26f68470ff3&title=&width=468.6666666666667)

**(a)**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687270039295-1ebc7728-3e5d-46c6-a8d3-4b057452cd84.png#averageHue=%23ffffff&clientId=u0328a585-7e84-4&from=paste&id=dgJhM&originHeight=131&originWidth=1387&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=44799&status=done&style=none&taskId=u11682dd0-be69-4d7d-b53f-58e3b82bbd0&title=)
**(b)**本质上我们要求解这样一个线性方程组: $\begin{bmatrix} x_1&x_2\\x_3&x_4\end{bmatrix}\begin{bmatrix}2\\3 \end{bmatrix} =\begin{bmatrix} 4\\2\end{bmatrix}$, 所以我们有四个未知量，但是只有两个方程，所以不存在唯一的解。
**(c)**本质上我们可以将以$V$和$P$作为`Basis`的向量转换到`Standard Basis`中，也就是说我们有: $V\vec{x}_v=P\vec{x}_p$, 所以$\vec{x}_p=P^{-1}V\vec{x}_v$, $P=\begin{bmatrix} 1&0\\4&1\end{bmatrix}$, $P^{-1}=\begin{bmatrix} 1&0\\-4&1\end{bmatrix}$, 所以$P^{-1}V=\begin{bmatrix} 1&0\\-4&1\end{bmatrix} \begin{bmatrix} 1&0\\1&2\end{bmatrix}=\begin{bmatrix}1&0\\-3&2\end{bmatrix}$, 所以$T=\begin{bmatrix}1&0\\-3&2\end{bmatrix}$。
**(d)**我们要求的是使得$P\vec{x}_p=\vec{x}$和$V\vec{x}_v=\vec{x}$的$\vec{x}_p$和$\vec{x}_v$。
所以$\vec{x}_p=P^{-1}\vec{x}=\begin{bmatrix} 1&0\\-4&1\end{bmatrix}\begin{bmatrix}1\\3 \end{bmatrix}=\begin{bmatrix} 1\\-1\end{bmatrix}$, $\vec{x}_v=V^{-1}\vec{x}=\begin{bmatrix} 1&0\\-\frac{1}{2}&\frac{1}{2}\end{bmatrix}\begin{bmatrix}1\\3 \end{bmatrix}=\begin{bmatrix} 1\\1\end{bmatrix}$
![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687744563874-13c6ca0d-f69b-4654-a039-5e844e871e02.png#averageHue=%23fcfcfc&clientId=ucf4951c4-f4a0-4&from=paste&id=Np9qg&originHeight=919&originWidth=1422&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=42059&status=done&style=none&taskId=u6521460e-428b-4024-92e3-b7dc6ce1c07&title=)


## Scalar Vector DE without Input
> 对于一个**齐次微分方程组**$\begin{cases} \frac{dx_1(t)}{dt}=ax_1(t)+bx_2(t)\\\frac{dx_2(t)}{dt}=cx_1(t)+dx_2(t)\end{cases}$, 我们可以将其写成向量形式，$\begin{bmatrix} \frac{dx_1(t)}{dt}\\\frac{dx_2(t)}{dt}\end{bmatrix}=\begin{bmatrix}a&b\\c&d \end{bmatrix}\begin{bmatrix} x_1(t)\\x_2(t)\end{bmatrix}$, 也就是$\frac{d}{dt}\vec{x}(t)=\mathbf{A}\vec{x}(t)$。
> 如果矩阵$\mathbf{A}$是一个对角阵，即$b=c=0$, 则此时我们会得到$\begin{bmatrix} \frac{dx_1(t)}{dt}\\\frac{dx_2(t)}{dt}\end{bmatrix}=\begin{bmatrix} ax_1(t)\\dx_2(t)\end{bmatrix}$, 此时就是两个齐次常数微分方程，直接分别求解即可。
> 如果矩阵$\mathbf{A}$不是对角阵，则我们一般会对矩阵$\mathbf{A}$进行对角化操作(几何重数等于代数重数的时候)，得到$\mathbf{A=V\Lambda V^{-1}}$($\mathbf{\Lambda=V^{-1}AV}$), 此时$\mathbf{V}$是矩阵$\mathbf{A}$的`Eigenbasis`
> 1. **方法一: **我们会令$\vec{y}(t)=\mathbf{V}^{-1}\vec{x}(t)$，这样的话因为我们有$\mathbf{V^{-1}}d\vec{x}(t)=\mathbf{V^{-1}}\mathbf{A}\vec{x}(t)=\mathbf{\mathbf{V^{-1}}V\Lambda V^{-1}}\vec{x}(t)=\mathbf{\Lambda}\vec{y}(t)$, 即$d\vec{y}(t)=\mathbf{\Lambda}\vec{y}(t)$，其中$\mathbf{\Lambda}$为对角矩阵，对角线上的值为矩阵$\mathbf{A}$的`Eigenvalues`。有了对角阵我们就可以很快求出微分方程组的解$\vec{y}(t)$, 然后通过$\vec{x}(t)=\mathbf{V}\vec{y}(t)$就可以得到原微分方程组的解。
> 2. **方法二:** 我们有$\mathbf{V}$的列作为`New Basis`, 有$\vec{x}(t)=\mathbf{V}\vec{y}(t)$, 此时$d\mathbf{V}\vec{y}(t)=\mathbf{AV}\vec{y}(t)$, 然后左右两边同乘以$\mathbf{V^{-1}}$得到$d\mathbf{V^{-1}V}\vec{y}(t)=\mathbf{V^{-1}AV}\vec{y}(t)$，也就是$d\vec{y}(t)=\mathbf{\Lambda} \vec{y}(t)$。
> 
两种方法的本质就是利用$\vec{x}(t)=\mathbf{V}\vec{y}(t)$和$d\vec{y}(t)=\mathbf{\Lambda} \vec{y}(t)$来转化坐标系从而更快求解微分方程组。


## Scalar Vector DE with Input
### Second Order Version
> 对于一个**非齐次常系数微分方程组**$\begin{cases} \frac{dx_1(t)}{dt}=ax_1(t)+bx_2(t)+u_1\\\frac{dx_2(t)}{dt}=cx_1(t)+dx_2(t)+u_2\end{cases}$($u_1$和$u_2$为常数), 我们可以将其写成向量形式，$\begin{bmatrix} \frac{dx_1(t)}{dt}\\\frac{dx_2(t)}{dt}\end{bmatrix}=\begin{bmatrix}a&b\\c&d \end{bmatrix}\begin{bmatrix} x_1(t)\\x_2(t)\end{bmatrix}+\begin{bmatrix} u_1\\u_2\end{bmatrix}$, 也就是$\frac{d\vec{x}(t)}{dt}=\mathbf{A}\vec{x}(t)+\vec{u}$。
> - 如果矩阵$\mathbf{A}$是一个对角阵，即$b=c=0$, 则此时我们会得到$\begin{bmatrix} \frac{dx_1(t)}{dt}\\\frac{dx_2(t)}{dt}\end{bmatrix}=\begin{bmatrix} ax_1(t)+u_1\\dx_2(t)+u_2\end{bmatrix}$, 此时就是两个非齐次常系数微分方程，直接分别求解即可。
> - 如果矩阵$\mathbf{A}$不是对角阵，则和齐次微分方程组的情况一样，我们将$\vec{y}(t)=\mathbf{V}^{-1}\vec{x}(t)$和$\mathbf{A=V\Lambda V^{-1}}$代入微分方程，可以得到:$\frac{d\mathbf{V}^{-1}\vec{x}(t)}{dt}=\mathbf{V^{-1}A(V}\vec{y}(t))+\mathbf{V}^{-1}\vec{u}$, 且$\frac{d\vec{y}(t)}{dt}=\mathbf{\Lambda}\vec{y}(t)+\mathbf{V^{-1}}\vec{u}$。
> 
然后解得$\vec{y}(t)$并利用$\vec{x}(t)=\mathbf{V}\vec{y}(t)$得到原来的微分方程组的解。


### Higher Order Version
> **HW04 Sp23 P3**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687872777181-a7ddb5d2-52c3-46cc-a023-5a13fe528609.png#averageHue=%23fcfbfa&clientId=ufd0bf38b-fa9c-4&from=paste&id=QzWCG&originHeight=1270&originWidth=1076&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=262888&status=done&style=none&taskId=u25105199-fb92-4545-9755-5f249d9fd53&title=)

**(a) EigenBasis Solution**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687874139287-657868b9-63a1-413b-9d2b-9fe77430e9cd.png#averageHue=%23ffffff&clientId=u4e7e5175-4a75-4&from=paste&id=RBRsY&originHeight=338&originWidth=1000&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=55167&status=done&style=none&taskId=u39ce1673-e7c3-4d34-92d8-ea6964ee8dd&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687874152143-9fa00b54-6454-4b3f-9d52-d2bc17a61e29.png#averageHue=%23ffffff&clientId=u4e7e5175-4a75-4&from=paste&id=KJ7Nk&originHeight=660&originWidth=1021&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=81637&status=done&style=none&taskId=udf171d21-6fbd-4222-bc0c-296a16b2a06&title=)
**(b) Extension to General Matrix**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687874698744-e4896553-d25d-401e-af9a-a32eaefc08c7.png#averageHue=%23ffffff&clientId=u4e7e5175-4a75-4&from=paste&id=gaXRU&originHeight=718&originWidth=1471&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=126737&status=done&style=none&taskId=u33adc1b1-1d36-45e5-a7e4-e4d10113ecc&title=)


## Summary
> 对于一个微分方程组$\frac{d\vec{x}(t)}{dt}=\mathbf{A}\vec{x}(t)+\mathbf{B}\vec{u}(t)$来说, 我们可以转换一下坐标系，通过对矩阵$\mathbf{A}$求特征值和特征向量。然后将特征向量按列组成一个新的基矩阵$\mathbf{V}$满足$\vec{x}(t)=\mathbf{V}\vec{y}(t)$。
> 然后等式两侧同乘以$\mathbf{V}^{-1}$, 得到$\frac{d\vec{y}(t)}{dt}=\mathbf{V^{-1}AV}\vec{y}(t)+\mathbf{V^{-1}B}\vec{u}(t)=\mathbf{\Lambda}\vec{y}(t)+\mathbf{V^{-1}B}\vec{u}(t)$。
> 其中$\mathbf{\Lambda}$是对角矩阵，$\vec{y}(t)$的初值条件$\vec{y}(0)$可以通过$\mathbf{V^{-1}}\vec{x}(0)$得到。




## RCRC Circuit Example
> **Fall 2021 Disc03B Problem 1 非齐次微分方程组**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686219038124-ba9e63b1-3e2a-438e-b7c9-7dc35a9476b7.png#averageHue=%23fbfbfa&clientId=u349f0d23-e19a-4&from=paste&id=ua30bfd89&originHeight=410&originWidth=1308&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=39774&status=done&style=none&taskId=ub5d4cce1-733c-4e15-bd69-d610a184f53&title=)


### Write the Differential Equation - 齐次
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686220115456-291ce106-d5d9-4060-a5cc-0ce5ef82051c.png#averageHue=%23efedeb&clientId=u349f0d23-e19a-4&from=paste&id=u6a05f042&originHeight=135&originWidth=1635&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=53207&status=done&style=none&taskId=u20e635da-ae23-4c43-a00b-c799e97db60&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686219091559-2aa7e448-04e2-4893-9691-8f563bd9ca16.png#averageHue=%23fefefe&clientId=u349f0d23-e19a-4&from=paste&id=u8d7dcdb7&originHeight=376&originWidth=1314&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=53647&status=done&style=none&taskId=u426ac3b8-7d9c-41e6-a2a2-6dcc2671c39&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686219096056-66e71f3f-9ac7-4756-ad85-39746a51ba1c.png#averageHue=%23fefefe&clientId=u349f0d23-e19a-4&from=paste&id=uce19b857&originHeight=872&originWidth=1333&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=138817&status=done&style=none&taskId=u83a9189e-7311-4324-b87a-6397bbb1864&title=)
> 🔔: 对于一个电容的微分方程来说，如果我们要建立微分方程$\frac{dV_{C_i}(t)}{dt}=\frac{I_i(t)}{C}$，最快的方法就是将$I_i(t)$表示成$V_{C_1}(t)$和$V_{C_2}(t)$以及$R_1$和$R_2$的组合, 其中$i\in \{1,2\}$。

**Graph**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686730379984-a9c3c85a-cc7a-4af2-b869-caff827e5b7a.png#averageHue=%23fcfcfb&clientId=u7b2fd1b3-9535-4&from=paste&id=u2fffe696&originHeight=718&originWidth=1261&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=69100&status=done&style=none&taskId=u4eee2f50-11bb-40c5-9c29-f7c304d9659&title=)


### Solving the Differential Equation - 非齐次
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686219998189-f7e50fed-4bea-43b0-9f44-4aca3cfd06f1.png#averageHue=%23fdfdfc&clientId=u349f0d23-e19a-4&from=paste&id=u4197263b&originHeight=1479&originWidth=1701&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=320708&status=done&style=none&taskId=ud6ed0de1-422e-49ef-9c0d-a9539576cc7&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686220101378-46977e31-9923-4925-a46c-caceb8c06d91.png#averageHue=%23fefefe&clientId=u349f0d23-e19a-4&from=paste&id=u50102a5e&originHeight=1618&originWidth=1812&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=237251&status=done&style=none&taskId=u8dc2ac66-1410-41ed-8af1-d1844ca389d&title=)

**Graph**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686730399943-d9f2616f-f9be-493b-aa53-41f10c3eba8e.png#averageHue=%23fcfbfb&clientId=u7b2fd1b3-9535-4&from=paste&id=u72bba7f5&originHeight=749&originWidth=1215&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=68630&status=done&style=none&taskId=ud0b8345a-8145-40e1-a3da-5514c5293b2&title=)



# Uniqueness For Diagonalized Solutions
> **Hw05 Fa21 P9(Modified)**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688221861597-1487d94d-5855-45ad-a614-a3bf872d00b5.png#averageHue=%23ebebeb&clientId=u72651bcd-861a-4&from=paste&id=u753cbc61&originHeight=752&originWidth=1480&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=205375&status=done&style=none&taskId=u840cb8fc-2dc3-4066-b01d-c1ed84e9033&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688221877963-7e875eb1-1336-4685-b061-520a03dc32f0.png#averageHue=%23e5e5e5&clientId=u72651bcd-861a-4&from=paste&id=u90ce3140&originHeight=309&originWidth=1429&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=126839&status=done&style=none&taskId=ud0381f84-cd0d-4694-9e66-71606938488&title=)

**(a) Change of Basis**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688221893543-207a8da5-30dd-4a94-86d0-53dc00bd0500.png#averageHue=%23ffffff&clientId=u72651bcd-861a-4&from=paste&id=ub8fcdb46&originHeight=1229&originWidth=1406&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=207092&status=done&style=none&taskId=uf5bddae3-aa2f-4ae2-a4ba-8178bcbb811&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688221901015-cb0e24db-4047-48b8-98ad-42c8a6659e8f.png#averageHue=%23ffffff&clientId=u72651bcd-861a-4&from=paste&id=u69640159&originHeight=627&originWidth=1391&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=101258&status=done&style=none&taskId=u7e8dafe8-aadf-4e83-8325-a8e2074ea6d&title=)
**(b) Proof for Uniqueness**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688222677278-2aa395d3-3d55-41ec-bf4e-277640a766fd.png#averageHue=%23ffffff&clientId=u72651bcd-861a-4&from=paste&id=u6c2bc33f&originHeight=1092&originWidth=1361&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=298436&status=done&style=none&taskId=u68b9a8af-46ee-4a81-ad96-3d871fdf7f7&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688222684568-fa21fde6-0c1a-42f7-bd07-0ce022a715d5.png#averageHue=%23f7f7f7&clientId=u72651bcd-861a-4&from=paste&id=u465bdc6d&originHeight=350&originWidth=1398&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=91922&status=done&style=none&taskId=u803b3f27-f540-439e-9013-8d581051776&title=)


# Math Tips
## Real-Valued Matrix⭐⭐⭐⭐⭐
> 矩阵$A$  的每一项都是实数且初值条件$\vec{x}_0$ 也都是实数, 则微分方程组 $\frac{\mathrm{d}}{\mathrm{d} t} \vec{x}=A \vec{x}$ ，$\vec{x}(0)=\vec{x}_0$的解也是实数, 无论 $A$的特征值是实数，纯虚数还是复数。
> 如果一个矩阵 $A \in \mathbb{R}^{n \times n}$ 有复数根, 那么这些复数根总是会以共轭对的形式出现。另外这些复数特征值对应的特征向量也是以共轭对的形式出现的。
> 回顾一下我们在`Damping Analysis`中的推导，假设我们的特征值是$\lambda_1,\lambda_2$且$\overline{\lambda_1}=\lambda_2$（共轭对），则特征向量矩阵按列为$V=\begin{bmatrix} 1&1\\\frac{1}{\lambda_1 C}&\frac{1}{\lambda_2 C}\end{bmatrix}$, 注意到$V$的第一列和第二列互为共轭向量。
> 令$\vec{x}(t)=V\widetilde{\vec{x}(t)}$, 则$\widetilde{\vec{x}(t)}=V^{-1}\vec{x}(t)$, 此时我们有$\Lambda = V^{-1}AV=\begin{bmatrix} \lambda_1&0\\0&\lambda_2\end{bmatrix}$,$\frac{d}{dt}\widetilde{\vec{x}(t)}=\Lambda \widetilde{\vec{x}(t)}$，即$\frac{d}{dt}\widetilde{\vec{x}(t)}=\begin{bmatrix} \lambda_1&0\\0&\lambda_2\end{bmatrix} \widetilde{\vec{x}(t)}$, 所以$\widetilde{\vec{x}(t)}=\begin{bmatrix}\widetilde{x_1(t)}\\\widetilde{x_2(t)} \end{bmatrix}=\begin{bmatrix}\widetilde{x_1(0)}e^{\lambda_1 t}\\\widetilde{x_2(0)}e^{\lambda_2 t} \end{bmatrix}$。
> 然后对于初值条件来说，我们有$\widetilde{\vec{x}(0)}=V^{-1}\vec{x}(0)=\frac{\lambda_1 \lambda_2 C}{\lambda_1-\lambda_2}\left[\begin{array}{cc}\frac{1}{\lambda_2 C} & -1 \\-\frac{1}{\lambda_1 C} & 1\end{array}\right]\vec{x}(0)=
\left[\begin{array}{cc}\frac{\lambda_1}{\lambda_1-\lambda_2} & -\frac{\lambda_1 \lambda_2 C}{\lambda_1-\lambda_2} \\-\frac{\lambda_2}{\lambda_1-\lambda_2} & \frac{\lambda_1 \lambda_2 C}{\lambda_1-\lambda_2}\end{array}\right]\vec{x}(0)$，如果初值条件为实数向量，则$\widetilde{x_1(0)}$和$\widetilde{x_2(0)}$互为共轭。所以$\widetilde{x_1(0)}e^{\lambda_1 t}$和$\widetilde{x_2(0)}e^{\lambda_2 t}$互为共轭，即$\widetilde{x_1(t)}$和$\widetilde{x_2(t)}$互为共轭。
> 因为$\vec{x}(t)=V\widetilde{\vec{x}(t)}=\begin{bmatrix} 1&1\\\frac{1}{\lambda_1 C}&\frac{1}{\lambda_2 C}\end{bmatrix}\begin{bmatrix}\widetilde{x_1(t)}\\\widetilde{x_2(t)} \end{bmatrix}$, 所以$x_1(t)$和$x_2(t)$均为共轭复数之和，于是$\vec{x}(t)$为实数向量。
> After all, the quantities that we observe in the world are always purely real, so we would expect that the solutions to our models would also be real-valued.



## Matrix Exponentials
> **HW03 Fa21 P4**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687271259482-520daaec-2c74-4dee-a418-36cf07bb69cb.png#averageHue=%23f9f7f6&clientId=u0328a585-7e84-4&from=paste&id=WILxP&originHeight=969&originWidth=1059&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=275759&status=done&style=none&taskId=u1bb90409-1139-459f-970f-369c47fae53&title=)

**(a)**根据特征向量的定义，我们有$A\vec{v_1}=\lambda \vec{v_1}\cdots,A\vec{v_n}=\lambda \vec{v_n}$, 将$\vec{v_i}$按列组成矩阵$V$我们有$AV= V\Lambda$
**(b)**因为$\vec{v_1},\cdots, \vec{v_n}$是线性无关的，所以$a_1\vec{v_1}+\cdots+a_n\vec{v_n}=\vec{0}$只有$a_1=a_2=\cdots=a_n=0$的解，也就是说如果$V=\begin{bmatrix} \vec{v_1}&\cdots&\vec{v_n}\end{bmatrix}$，则$V\vec{a}=\vec{0}$只有零解，也就是$V$的零空间只有$\{\vec{0}\}$, 所以$V$可逆。
因为$AV=V\Lambda$, 所以$A=V\Lambda V^{-1}$。
**(c)**$\Lambda=V^{-1}AV$。
**(d)**因为$A=UDU^{-1}$, 所以$U$可逆(因为能够表示成$U^{-1}$)，所以$AU=UD$, 令$U=\begin{bmatrix} \vec{u_1}&\vec{u_2}\cdots&\vec{u_n}\end{bmatrix}$ , $D=\begin{bmatrix} \lambda_1&\cdots&0\\\vdots&\ddots&\vdots\\0&\cdots&\lambda_n\end{bmatrix}$, 所以我们有$A\vec{u_i}=\lambda_i\vec{u_i}$，所以$\vec{u_i}$就是`Eigenvectors`。$D$的对角线上的元素就是`Eigenvalues`。
**(e)**因为$A\vec{v_i}=\lambda_i\vec{v_i}$, 所以$A^k\vec{v_i}=\lambda_i^k\vec{v_i}$, 于是$A^k$的特征值是$\lambda_i^k$, 特征向量是$\vec{v_i}$。
所以$A^kV=VD^k$, 即$A^k=VD^kV^{-1}$, 所以$A^k$是`Diagonalizable`的。


## Diagonalizability&Invertibility
> 1. **Every square matrix that can be diagonalizable is invertible. False.**
> 
![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688185488134-b55273fa-6af7-4082-9e36-d543f797bbda.png#averageHue=%23f6f6f6&clientId=u02d56598-df23-4&from=paste&id=udb305df1&originHeight=460&originWidth=1318&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=121365&status=done&style=none&taskId=u56f19039-c1ff-428b-9419-92d7f7ae0ed&title=)
> 2. **Every square matricx that is invertible, can be diagonalized. False.**
> 
![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688185499777-ec86ce32-34fd-4e13-9ffd-74d21e17e081.png#averageHue=%23f4f4f4&clientId=u02d56598-df23-4&from=paste&id=ucceede7f&originHeight=532&originWidth=1320&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=170555&status=done&style=none&taskId=u40ef9902-3bbd-41d6-b6f8-f7f107653cd&title=)




## 

## 

# Resources
> Note 3 Fa21/Note 4 from Sp23
> Disc2B/3A/3B from Fa21
> Hw03 Fa21

