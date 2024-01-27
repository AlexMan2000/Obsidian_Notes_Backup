# Second Order DE to Vector DE
## Method
> 对于一个`Second Order DE`$\frac{\mathrm{d}^2 y(t)}{\mathrm{d} t^2}+a \frac{\mathrm{d} y(t)}{\mathrm{d} t}+b y(t)=0$来说, 我们可以：
> 如果我们令 $x_1(t)=y(t), x_2(t)=\frac{\mathrm{a} y(t)}{\mathrm{d} t}$, 则我们有:
> $\begin{aligned}& \frac{\mathrm{d} x_1(t)}{\mathrm{d} t}=\frac{\mathrm{d} y(t)}{\mathrm{d} t}=x_2(t) \\& \frac{\mathrm{d} x_2(t)}{\mathrm{d} t}=\frac{\mathrm{d}^2 y(t)}{\mathrm{d} t^2}=-a \frac{\mathrm{d} y(t)}{\mathrm{d} t}-b y(t)=-a x_2(t)-b x_1(t)\end{aligned}$
> 于是我们可以将`Second Order DE`转化成如下的`Vector DE`:
> $\frac{\mathrm{d}}{\mathrm{d} t} \vec{x}=\frac{\mathrm{d}}{\mathrm{d} t}\left[\begin{array}{l}x_1 \\x_2\end{array}\right]=\left[\begin{array}{cc}0 & 1 \\-b & -a\end{array}\right]\left[\begin{array}{l}x_1 \\x_2\end{array}\right]$


## Example 1: Transformation
### Solving Vector DE
> **HW03 Fa21 P5**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688002497985-aa8a1a6c-d422-4dd2-bad3-595532a99517.png#averageHue=%23f7f5f4&clientId=u87c1740e-ef38-4&from=paste&id=u2e62491a&originHeight=900&originWidth=1396&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=281181&status=done&style=none&taskId=ufc0119e3-b61e-4ebc-bbc1-8ae60d9ee34&title=)

**(a)**$\begin{bmatrix}\frac{dx_1(t)}{dt}\\\frac{dx_2(t)}{dt} \end{bmatrix}=\begin{bmatrix}7&-8\\4&-5 \end{bmatrix}\begin{bmatrix}x_1(t)\\x_2(t) \end{bmatrix}$
我们对$A=\begin{bmatrix} 7&-8\\4&-5\end{bmatrix}$求解特征值：
$(7-\lambda)(-5-\lambda)+32=0$, 所以$\lambda_1=-1,\lambda_2=3$
**(b)**$\lambda_1=-1$, 对应的特征向量是$\begin{bmatrix} 1\\1  \end{bmatrix}$。
$\lambda_2 = 3$，对应的特征向量是$\begin{bmatrix} 2\\1\end{bmatrix}$。
所以`Column Eigenvectors`是$\begin{bmatrix} 1&2\\1&1\end{bmatrix}$。
**(c)**我们只需使用$B=\begin{bmatrix} 1&2\\1&1\end{bmatrix}$作为我们的`New Basis`, 也就是`Eigen Basis`, 此时$D=\begin{bmatrix} -1&0\\0&3\end{bmatrix}$
$\frac{d\vec{z}(t)}{dt}=D\vec{z}(t)$。
**(d)**首先我们需要求出$\vec{z}(0)=B^{-1}\vec{x}(0)=\begin{bmatrix} -1&2\\1&-1\end{bmatrix}\begin{bmatrix} 1\\-1\end{bmatrix}=\begin{bmatrix} -3\\2\end{bmatrix}$
根据一阶线性常系数齐次微分方程，我们有$\vec{z}(t)=\begin{bmatrix} -3e^{-t}\\2e^{3t}\end{bmatrix}$
**(e)**所以$\vec{x}(t)=B\vec{z}(t)=\begin{bmatrix} 1&2\\1&1\end{bmatrix}\begin{bmatrix} -3e^{-t}\\2e^{3t}\end{bmatrix}=\begin{bmatrix}-3e^{-t}+4e^{3t}\\-3e^{-t}+2e^{3t}\end{bmatrix}$

### Converting Second Order to Vector
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688002541248-1a0bf2a0-1b12-44b2-a3a9-816585124562.png#averageHue=%23efefef&clientId=u87c1740e-ef38-4&from=paste&id=u2a9480ce&originHeight=354&originWidth=950&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=103956&status=done&style=none&taskId=u296a0940-2ab9-4c4a-8425-404785c3f27&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688002547021-d1f18084-bca9-42f8-b851-b5e88abb4dfb.png#averageHue=%23efefef&clientId=u87c1740e-ef38-4&from=paste&id=u6f618932&originHeight=501&originWidth=969&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=138345&status=done&style=none&taskId=uf7f02adb-676d-4235-b78c-8aea5ef0d40&title=)
> 注意$(g)$问中的两个特征值必须都是**实数根且不同**才满足上述解的形式。

**(f) Converting from Second Order DE to Vector DE**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688002582875-1a8b342e-354e-424e-93fe-2e3108cc0b56.png#averageHue=%23ffffff&clientId=u87c1740e-ef38-4&from=paste&id=u1d3c9c5d&originHeight=366&originWidth=1106&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=40442&status=done&style=none&taskId=u89287ed0-f387-48f6-b958-4aae4aa3004&title=)
**(g) Solving IVP**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688002601443-137198ed-0670-423f-8227-0301be70509e.png#averageHue=%23ffffff&clientId=u87c1740e-ef38-4&from=paste&id=ueda7639b&originHeight=831&originWidth=1125&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=99103&status=done&style=none&taskId=u2a41d08f-6628-414e-b4e5-5699d84c906&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688002607813-52a802fb-75be-4ed0-9369-b94b17dc534a.png#averageHue=%23ffffff&clientId=u87c1740e-ef38-4&from=paste&id=u550f7183&originHeight=287&originWidth=1122&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=38929&status=done&style=none&taskId=ue9bfa466-bc9f-41c0-a862-3117e8d8d02&title=)


## Example 2: RLC Circuit
> **Hw05 Fa21 P4**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687871064964-a32d8f7c-6a18-4847-91c4-89436dc2a82d.png#averageHue=%23f0f0f0&clientId=u59328758-c2df-4&from=paste&id=xGCIY&originHeight=1159&originWidth=1936&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=263017&status=done&style=none&taskId=u37c36f2d-74a2-49eb-9093-f20f184f2f3&title=)

**Set up Second Order DE**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688013758340-61ba6037-fe51-40a3-8b21-7ed964f61509.png#averageHue=%23fbfbfb&clientId=u0e9441d5-0e78-4&from=paste&id=udc229169&originHeight=466&originWidth=1353&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=59635&status=done&style=none&taskId=u21574ee0-d313-4fb2-9725-669108b6d6b&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688013764608-2bf1a807-ce69-4053-93c6-be06886c1c1b.png#averageHue=%23ffffff&clientId=u0e9441d5-0e78-4&from=paste&id=ub9c919c5&originHeight=335&originWidth=1458&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=33307&status=done&style=none&taskId=u1fc248d1-e98e-4d64-b789-c382522f32a&title=)
注意这里$I_L(t)$是没有办法化成二阶形式的，所以我们的`Damping Analysis`基本针对于由$V_C(t)$构成的二阶常系数微分方程。
**Convert to Vector DE and Solve**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688013843446-005289b9-2f41-4ed5-b5db-ea0f24bed39f.png#averageHue=%23f7f7f7&clientId=u0e9441d5-0e78-4&from=paste&id=u8f8e3589&originHeight=1104&originWidth=894&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=172513&status=done&style=none&taskId=u2f52790b-f26a-402a-9e14-92a610e76bc&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688013852728-111dbdcf-fda5-4c1f-afaa-a35b981594b5.png#averageHue=%23ffffff&clientId=u0e9441d5-0e78-4&from=paste&id=u9d3fff73&originHeight=519&originWidth=949&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=44364&status=done&style=none&taskId=u12eaba40-a5a8-4d8e-a2e8-973c0b6ad7f&title=)
**Solve for Coeffients**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688014012290-54f3b369-3ea1-44fb-8b6d-8dba90259230.png#averageHue=%23f5f5f5&clientId=u0e9441d5-0e78-4&from=paste&id=uc5c1dd4c&originHeight=744&originWidth=874&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=156914&status=done&style=none&taskId=u5f0d90f5-63b8-4780-b35c-e807208d2cb&title=)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688013962469-a428d15e-d504-4ec6-80b5-29558bbc92ac.png#averageHue=%23ffffff&clientId=u0e9441d5-0e78-4&from=paste&id=pw5uE&originHeight=1150&originWidth=1022&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=156528&status=done&style=none&taskId=u9357d79e-bad8-4dc5-8d9f-6fbfb87a2b5&title=)


# Second Order DEs
## Second Order DE Analysis
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687240904357-36431332-0658-47fb-905f-b7c704c5cfbc.png#averageHue=%23f9e8e7&clientId=ude6e3a59-bf7d-4&from=paste&id=u415975b9&originHeight=563&originWidth=1472&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=161093&status=done&style=none&taskId=ue306bfac-0d3d-4458-9e23-8041ed2eff8&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687240914944-d0b8c2c6-30f9-4981-a3e2-f97de9717d5d.png#averageHue=%23e6e6fb&clientId=ude6e3a59-bf7d-4&from=paste&id=u6cf06bd5&originHeight=874&originWidth=1477&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=241572&status=done&style=none&taskId=u950785cb-0aca-48d7-a5d1-af92041b036&title=)
> 🔔注意点:
> 1. $s_1$和$s_2$是$\frac{d^2x(t)}{dt}+2\frac{\zeta}{\tau}\frac{dx(t)}{dt}+\frac{1}{\zeta^2}x(t)=0$的两个根，用$\frac{-b\pm \sqrt{b^2-4ac}}{2a}$求得。
> 2. $K_1$和$K_2$需要通过$\frac{dx(0)}{dt}$和$x(0)$这两个`Initial Conditions`来求出。


## Computing Components
> 一般形式:$\frac{\mathrm{d}^2 x(t)}{\mathrm{d} t^2}+2 \frac{\zeta}{\tau} \frac{\mathrm{d} x(t)}{\mathrm{d} t}+\frac{1}{\tau^2} x(t)=f(t)$/ $\frac{\mathrm{d}^2 x(t)}{\mathrm{d} t^2}+2 \alpha \frac{\mathrm{d} x(t)}{\mathrm{d} t}+w_0^2 x(t)=f(t)$
> `Example RLC Circuit`:$\frac{\mathrm{d}^2 v_C(t)}{\mathrm{d} t^2}+\frac{R}{L} \frac{\mathrm{d} v_C(t)}{\mathrm{d} t}+\frac{1}{L C} v_C(t)=\frac{50}{L C}$
> 我们可以计算一些量:
> 1. $\tau^2=LC$, 即$\tau=\sqrt{LC}$
> 2. $2 \frac{\zeta}{\tau}=\frac{R}{L}$, $\zeta=\frac{R\tau}{2L}=\frac{R\sqrt{LC}}{2L}$, 来判断`Homogeneous Solution`的形式。
> 3. `Eigenvalues/Roots`$s_1:=-\frac{\zeta}{\tau}+\frac{1}{\tau} \sqrt{\zeta^2-1} \text { and } s_2:=-\frac{\zeta}{\tau}-\frac{1}{\tau} \sqrt{\zeta^2-1} \text {. }$`Eigenvalues`是针对`Vector`形式的微分方程组。`Roots`是针对`Second Order DE`的特征方程。
> 4. `Damping Coefficient`: $\alpha = \frac{R}{2L}$
> 5. `Undamped Resonant Frequency`: $w_0=\frac{1}{\sqrt{LC}}=\frac{1}{\tau}$
> 6. `Natural Frequency`: $\omega_n=\sqrt{w_0^2-\alpha^2}$，这个频率是使得我们的特征多项式的解为纯虚数的频率。对于$\frac{\mathrm{d}^2 x(t)}{\mathrm{d} t^2}+2 \alpha \frac{\mathrm{d} x(t)}{\mathrm{d} t}+w_0^2 x(t)=0$来说，如果求根判断   $b^2-4ac<0$，即两根是复数，则$\lambda_{1,2}=\frac{-2\alpha\pm 2j\sqrt{w_0^2-\alpha^2}}{2}=-\alpha\pm j\sqrt{w_0^2-\alpha^2}$ , 此时$j$后面这项称为系统的自然频率，此时是`Underdamped`或者`Undamped Case`(如果$\alpha=0$)。
> 7. `Forcing Function`: $f(t)$



## RLC Circuit Examples
### Example 1: RLC Overdamped⭐⭐⭐
> **HW03 Sp23 P7**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687914315922-62a79b3b-a7df-4d5d-b2c4-55984ecb0457.png#averageHue=%23fbfafa&clientId=uc10953c7-6db6-4&from=paste&height=491&id=u267c4dd2&originHeight=737&originWidth=1489&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=102023&status=done&style=none&taskId=ud26c92f9-e335-4eed-b0f6-811700e42a9&title=&width=992.6666666666666)
> 首先进行电路分析获得微分方程:
> We can apply KVL to the circuit to obtain:
> $\begin{aligned}50 & =v_L(t)+v_R(t)+v_C(t) \\& =L \frac{\mathrm{d} i(t)}{\mathrm{d} t}+i(t) R+v_C(t) \\& =L \frac{\mathrm{d} i(t)}{\mathrm{d} t}+R C \frac{\mathrm{d} v_C(t)}{\mathrm{d} t}+v_C(t)\end{aligned}$
> Now, we have that $L \frac{\mathrm{d} i(t)}{\mathrm{d} t}=L \frac{\mathrm{d}}{\mathrm{d} t}\left(C \frac{\mathrm{d} v_C(t)}{\mathrm{d} t}\right)=L C \frac{\mathrm{d}^2 v_C(t)}{\mathrm{d} t^2}$. Plugging this in, we get
> $\begin{aligned}& L C \frac{\mathrm{d}^2 v_C(t)}{\mathrm{d} t^2}+R C \frac{\mathrm{d} v_C(t)}{\mathrm{d} t}+v_C(t)=50 \\& \frac{\mathrm{d}^2 v_C(t)}{\mathrm{d} t^2}+\frac{R}{L} \frac{\mathrm{d} v_C(t)}{\mathrm{d} t}+\frac{1}{L C} v_C(t)=\frac{50}{L C}\end{aligned}$
> 留意到右侧的输入`Forcing Function`, 我们要求$v_C(t)=v_{C_h}(t)+v_{C_p}(t)$，因为$R\neq 0$, 所以在$t\to \infty$时，`Transient Part`会衰减到零:
> 1. 将电容等效为`Open Circuit`, 并将电导等效为`Wire`, 我们有$v_{C_p}(t)=50V$。
> 2. 计算$\zeta=\frac{R\tau}{2L}=\frac{R\sqrt{LC}}{2L}=2>1$, 所以是`Overdamped Case`, $v_{C_h}(t)=K_1e^{s_1t}+K_2e^{s_2t}$, $s_1:=-\frac{\zeta}{\tau}+\frac{1}{\tau} \sqrt{\zeta^2-1} \text { and } s_2:=-\frac{\zeta}{\tau}-\frac{1}{\tau} \sqrt{\zeta^2-1} \text {. }$可知$s_1=-2679.49$, $s_2=-37320.5$
> 3. 利用初值条件$v_C(0)=0 \text { and }\left.\frac{\mathrm{d} v_{\mathcal{C}}(t)}{\mathrm{d} t}\right|_{t=0}=\frac{i(0)}{C}=0$求解通解: $v_C(t)=v_{C_P}(t)+v_{C_C}(t)=50+K_1 \mathrm{e}^{s_1 t}+K_2 \mathrm{e}^{s_2 t}$
> 
 $\begin{aligned}&v_C(0)=25=50+K_1+K_2\\&\left.\frac{\mathrm{d} v_C(t)}{\mathrm{d} t}\right|_{t=0}=0=s_1 K_1+s_2 K_2\end{aligned}$
> 得到$K_1=-26.93 \text { and } K_2=1.93$和$v_C(t)=50+(-26.93) \mathrm{e}^{-2679.49 t}+(1.93) \mathrm{e}^{-37320.5 t}$



### Example 2: RLC Overdamped⭐⭐⭐
> **Disc03A Sp23 P1**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687963617357-267b40f0-a63f-4595-bf74-5a26aa3fa484.png#averageHue=%23fafaf9&clientId=u6abc82f3-ca5c-4&from=paste&id=ud8d82130&originHeight=736&originWidth=1707&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=102467&status=done&style=none&taskId=uc81ce891-68c3-4a07-9a8a-d4066366450&title=)

**(a) Find Equivalent Circuit**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688008430937-bf50520a-1dae-4898-a709-254a4b6c8810.png#averageHue=%23fdfdfd&clientId=uc912c756-fbb0-4&from=paste&id=u9c112556&originHeight=529&originWidth=992&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=61611&status=done&style=none&taskId=u7d6fe653-d802-4ce5-a8b0-2a6783155c8&title=)
**(b) Set up Differential Equations**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688008465396-06266c7c-e052-4ba5-9497-3f9636f47ec1.png#averageHue=%23fdfdfd&clientId=uc912c756-fbb0-4&from=paste&id=uefed64b8&originHeight=154&originWidth=976&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=26596&status=done&style=none&taskId=ue1e2073a-9a6c-4c76-98be-9da1a6f861e&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688008468777-d00925fc-7fbd-422f-ab4c-0581eedf1274.png#averageHue=%23ffffff&clientId=uc912c756-fbb0-4&from=paste&id=u0e74fff6&originHeight=353&originWidth=999&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=48646&status=done&style=none&taskId=u10a3df94-7780-4bca-abb0-7f80ccccf51&title=)
**(c) Solve the Differential Equations⭐⭐⭐**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688008493855-f0e8c77b-c138-4eea-9c7d-5f2625c73993.png#averageHue=%23fefefe&clientId=uc912c756-fbb0-4&from=paste&id=u0384d110&originHeight=1301&originWidth=1432&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=293147&status=done&style=none&taskId=u90cbec63-dd3b-4707-8abc-3f60fc8010d&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688008585971-b86fe998-5e7f-4019-ae86-71784003c923.png#averageHue=%23ffffff&clientId=uc912c756-fbb0-4&from=paste&id=u779ee827&originHeight=1235&originWidth=1190&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=197889&status=done&style=none&taskId=u82845012-0ebb-45a2-920c-ff47dd1865a&title=)
**(d) Circuit in Steady State**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688008632529-b6977cff-07e5-446c-ac01-eef30f61185b.png#averageHue=%23fbfaf9&clientId=uc912c756-fbb0-4&from=paste&id=uf92d008b&originHeight=130&originWidth=1190&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=40651&status=done&style=none&taskId=u854926ac-1b20-456b-afdf-ae7c4ad6b5c&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688008642625-fbdcc385-cdea-440f-bcef-e7793068e046.png#averageHue=%23fefefe&clientId=uc912c756-fbb0-4&from=paste&id=u212807ce&originHeight=437&originWidth=1171&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=38481&status=done&style=none&taskId=uc3a442d0-3b23-4617-af45-ed618dcd61f&title=)
**(e) Plot the Solution**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688008660755-083841ac-e0f7-4d47-aee8-82fcd872eb3f.png#averageHue=%23fefefe&clientId=uc912c756-fbb0-4&from=paste&id=ud523eebe&originHeight=636&originWidth=1135&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=42268&status=done&style=none&taskId=u2b180310-b7b5-4dee-9eb5-d480f85ce15&title=)


## LC Tank Example
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687242300069-1f530f78-0f46-44ed-abd5-00a27680f2ee.png#averageHue=%23fcfcfc&clientId=ude6e3a59-bf7d-4&from=paste&id=uSf17&originHeight=703&originWidth=1559&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=91449&status=done&style=none&taskId=u3de12030-3294-4428-903f-c937c0abc0d&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687242312289-8e03b051-0b58-4b31-b993-51536e5b226b.png#averageHue=%23fcfbfa&clientId=ude6e3a59-bf7d-4&from=paste&id=zfOM5&originHeight=1243&originWidth=1031&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=281761&status=done&style=none&taskId=uf74cf0b0-9e62-41e5-bf08-28fd41f4db2&title=)


# Resources
> Note 4 from Fa21
> Note 3/4b from Sp23

