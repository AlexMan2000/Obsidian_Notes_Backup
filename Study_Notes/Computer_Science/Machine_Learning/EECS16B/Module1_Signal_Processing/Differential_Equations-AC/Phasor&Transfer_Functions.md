# AC Steady State
## AC input
> `AC Input`和`DC Input`最大的不同就是`AC`输入是一个可变函数。



## Exponential Input
> 1. 对于一个微分方程$\frac{dx(t)}{dt}=\lambda x(t)+u(t)\tag{1}$来说，我们可以使用`Integrating Factor`得到:
> 
$x(t)=x_0e^{\lambda t}+\int_0^t u(\tau) e^{\lambda(t-\tau)}d\tau$
> 当$u(t)=ke^{st}(s\neq \lambda)$时，我们有:
> $\begin{aligned}x(t)&=(x_0-\frac{k}{s-\lambda})e^{\lambda t}+\frac{k}{s-\lambda}e^{st}\end{aligned}$
> 当$Re(\lambda)< 0$时(一般的电路都满足这个条件)，第一项在$t\to \infty$时趋近于零，于是$\lim_{t\to\infty}x(t)\approx \frac{k}{s-\lambda}e^{st}=u_0e^{st}$。
> 第一项被称为`Transient Solution`, 第二项是`Steady State Solution`。
> 2. 对于一个微分方程组$\frac{d\vec{x}(t)}{dt}=\mathbf{A} \vec{x}(t)+\vec{u}(t)\tag{2}$来说, 我们假设$\vec{u}(t)=\vec{u}_0e^{st}$, $\vec{u}_0$是与$t$无关的常数向量。
>    1. 我们先进行坐标转换，利用$\vec{x}(t)=\mathbf{V}\vec{z}(t)$得到新坐标下的微分方程组$\frac{d}{dt}\vec{z}(t)=\mathbf{\Lambda}\vec{z}(t)+\mathbf{V}^{-1}\vec{u}(t)$, 其中$\mathbf{V}$是$\mathbf{A}$的特征向量矩阵，对每一行我们有: $\frac{\mathrm{d}}{\mathrm{d} t} z_i(t)=\lambda_i z_i(t)+\left(V^{-1} \vec{u}_0 \mathrm{e}^{s t}\right)_i=\lambda_i z_i(t)+\left(V^{-1} \vec{u}_0 \right)_i\mathrm{e}^{s t}$
>    2. 然后我们利用$(1)$中的结果，得到$\lim_{t\to \infty}z_i(t)=\alpha_ie^{st}$(令$\left(V^{-1} \vec{u}_0 \right)_i=\alpha_i$), 向量化后得到$\lim_{t\to \infty}\vec{z}(t)=\vec{\alpha}e^{st}$。
>    3. 将$\vec{z}(t)$进行坐标转换为原来的坐标，得到$\lim_{t\to \infty}\vec{x}(t)=V\vec{z}(t)=(V\vec{\alpha})e^{st}=\vec{x_0}e^{st}$(如果$s\neq \lambda_i,\forall i$)
> 3. 将$\begin{cases} \vec{u}(t)=\vec{u}_0e^{st}\\ \lim_{t\to \infty}\vec{x}(t)=\vec{x}_0e^{st}\end{cases}$带入$(2)$中得到: $(s\mathbf{I}-\mathbf{A})\vec{x}_0=\vec{u}_0$, 因为$s\neq \lambda_i$, 所以满足$(s\mathbf{I}-\mathbf{A})\vec{y}=\vec{0}$的$\vec{y}$是不存在的，否则存在$\vec{y}$, 使得$\mathbf{A}\vec{y}=s\vec{y}$, 其中$s$是$\mathbf{A}$的特征值，矛盾，所以我们知道$(s\mathbf{I}-\mathbf{A})$的零空间没有非零解，即$(s\mathbf{I}-\mathbf{A})$可逆，所以$\vec{x}_0=(s\mathbf{I}-\mathbf{A})^{-1}\vec{u}_0$。
> 
于是$\lim_{t\to \infty}\vec{x}(t)=\vec{x_0}e^{st}=(s\mathbf{I}-\mathbf{A})^{-1}\vec{u}_0e^{st}$, 验证这个`Steady State Solution`满足$(2)$:
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687488615954-48509aca-9ae5-4565-b05e-b339b3087960.png#averageHue=%23fcfcfb&clientId=ubb32db90-495a-4&from=paste&id=qxgNJ&originHeight=713&originWidth=1758&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=131491&status=done&style=none&taskId=u9034941c-a987-4a86-9af5-3f8a0555e7e&title=)
> **综上所述: **对于$u(t)=\vec{u_0}e^{st}, s\neq \lambda_i$, 我们有$\lim_{t\to \infty}\vec{x}(t)=(s\mathbf{I}-\mathbf{A})^{-1}\vec{u}_0e^{st}$，对于$s\in \mathbb{C}$，有:
> 1. $Re(s)>0$, 则`Steady State Solution`$\vec{x}(t)$explodes to infinity.
> 2. $Re(s)<0$, 则`Steady State Solution`$\vec{x}(t)$decays to zero.
> 3. $Re(s)=0$, 则`Steady State Solution`$\vec{x}(t)$是周期函数, 使用`Euler Formula`可得。

# 
## Sinusoidal Input
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688017756631-7a933cde-7708-4bbb-a71e-623bf087108c.png#averageHue=%23e8e9fd&clientId=ue013ba67-f3b8-4&from=paste&id=u8921e335&originHeight=219&originWidth=973&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=22484&status=done&style=none&taskId=u29f828ef-c4d4-4f2a-8cfa-e25812b92e0&title=)
> 其实`Sinusoidal Input`就可以看成是两个共轭的`Exponential Input`。




### Ex1: Oscillating Current Input⭐⭐⭐
> **EECS16B sp23 disc 01A P2**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685591239603-4364e75f-5522-45fa-96ae-e11af4e6befc.png#averageHue=%23fbfbfb&clientId=ua37d54c7-8842-4&from=paste&id=ubfb489b9&originHeight=732&originWidth=1550&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=96380&status=done&style=none&taskId=ud6e45274-eb77-40e6-bd51-c83066204b4&title=)

**Solution**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685591977999-a42c4c40-5c97-44d8-956b-d77eda2824b0.png#averageHue=%23ffffff&clientId=ua37d54c7-8842-4&from=paste&height=529&id=uf8d0c911&originHeight=827&originWidth=1035&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=105767&status=done&style=none&taskId=u692a2353-215b-4b92-aa9f-b6917d1a38e&title=&width=662.4)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685591981274-7fa84920-1284-41d3-95c5-6d32559b69c7.png#averageHue=%23fefefe&clientId=ua37d54c7-8842-4&from=paste&height=659&id=u2668e1f7&originHeight=1029&originWidth=1075&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=96696&status=done&style=none&taskId=udad59fe6-b13a-4266-be11-2a05e2f239c&title=&width=688)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685591984233-f0610d8c-5c8e-4fb1-a39f-38c84d1c8f9f.png#averageHue=%23fefdfd&clientId=ua37d54c7-8842-4&from=paste&height=648&id=u7bab9929&originHeight=1012&originWidth=1032&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=60876&status=done&style=none&taskId=ub3c0fe55-8201-413a-a8dc-7ef2cda7fdb&title=&width=660.48)

### Ex2: Oscillation Voltage Input
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685592418819-50245aa7-7420-4211-bd39-73d73f09b7d3.png#averageHue=%23fbfbfa&clientId=ub67c7d7d-fbda-4&from=paste&id=u2b01a8f9&originHeight=555&originWidth=1527&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=64599&status=done&style=none&taskId=uba98c2f8-b526-4773-b23e-d775ed88644&title=)

**(a) Set Up Differential Equation**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685592604678-36bddf9d-1abd-410a-b831-d6b65ffba7bf.png#averageHue=%23f8f7f6&clientId=ub67c7d7d-fbda-4&from=paste&height=115&id=u306ff2fc&originHeight=179&originWidth=1641&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=41030&status=done&style=none&taskId=u79d570b5-9216-497a-b7fd-9ae0ce6adcc&title=&width=1050.24)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685592592403-63c80306-3db9-4473-9136-517b26868f37.png#averageHue=%23ffffff&clientId=ub67c7d7d-fbda-4&from=paste&id=u6856784d&originHeight=478&originWidth=1613&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=89537&status=done&style=none&taskId=u96b69bb9-dd03-4ee4-b52b-a07feafc0d4&title=)
**(b) Initial Condition**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685592631149-9e4a583f-4b68-48d7-be74-07069b9e7f2b.png#averageHue=%23fbfafa&clientId=ub67c7d7d-fbda-4&from=paste&id=ua95c0d6b&originHeight=209&originWidth=1699&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=67882&status=done&style=none&taskId=ua95e40cd-1233-4e34-ba7d-16b36b661c3&title=)
**(c) Solve the Voltage - Method 1: Definite Integral**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685594819131-7b35eb4d-9609-4499-980b-0d4508354577.png#averageHue=%23f8f7f6&clientId=ub67c7d7d-fbda-4&from=paste&id=ue101faa0&originHeight=512&originWidth=1666&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=137647&status=done&style=none&taskId=u0e3d674a-8dce-47ab-8329-893ad02bfe1&title=)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685593190138-8a61c6c5-3455-4669-aba8-695038d76e9a.png#averageHue=%23ffffff&clientId=ub67c7d7d-fbda-4&from=paste&height=158&id=u5471e9dc&originHeight=247&originWidth=1668&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=60000&status=done&style=none&taskId=u68b080e9-f340-4f3a-9410-7537fbabe1e&title=&width=1067.52)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685593196459-0ef1e950-ccd2-4c07-87fa-74dc9d18ea6c.png#averageHue=%23ffffff&clientId=ub67c7d7d-fbda-4&from=paste&height=1000&id=u2113620c&originHeight=1562&originWidth=1732&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=335190&status=done&style=none&taskId=u242dc1dc-ca27-4766-8a56-17ac8a0d8d6&title=&width=1108.48)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685593269719-eacbb234-2ea1-475f-81f4-a18ac7d18964.png#averageHue=%23ffffff&clientId=ub67c7d7d-fbda-4&from=paste&height=190&id=u347d154e&originHeight=297&originWidth=1670&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=64078&status=done&style=none&taskId=uffd11491-543b-4c51-874f-89e4410a979&title=&width=1068.8)
**(c) Solve the Voltage - Method 2: Indefinite Integral**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685594945699-9bfe61c0-d840-4c68-aaf6-1b174742b73f.png#averageHue=%23f8f7f6&clientId=ub67c7d7d-fbda-4&from=paste&id=uffe757d5&originHeight=589&originWidth=1750&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=146274&status=done&style=none&taskId=u4def25ba-fa41-45a1-b4ec-db9d15bf619&title=)
**我们有如下的推导步骤:**
$\begin{aligned} v(t)&=A^{-\frac{1}{RC}t}+e^{-\frac{1}{RC}t}\int e^{\frac{1}{RC}t}\frac{1}{RC}V_{in}(t)dt\\&=A^{-200t}+e^{-200t}\int e^{200t}\cdot 200\cdot 2sin(200t)dt\\&=Ae^{-200t}+400e^{-200t}\frac{1}{200^2+200^2}e^{200t}(200sin(200t)-200cos(200t))\\&=Ae^{-200t}+(sin(200t)-cos(200t))\end{aligned}$
$v(0)=1$得到$A=2$
所以$v(t)=2e^{-200t}+(sin(200t)-cos(200t))$
**(d) Solve the Current**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685593890152-254d9e38-bce5-404d-83df-aca19d5486a2.png#averageHue=%23ebe9e7&clientId=ub67c7d7d-fbda-4&from=paste&height=40&id=u5933df4e&originHeight=63&originWidth=1055&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=20879&status=done&style=none&taskId=u0b2f68fc-ed64-4144-9113-e7432cc8d23&title=&width=675.2)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685593886479-7c7afe49-555e-49a3-a464-f3ef836e60af.png#averageHue=%23ffffff&clientId=ub67c7d7d-fbda-4&from=paste&height=284&id=u5634234b&originHeight=444&originWidth=1622&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=105047&status=done&style=none&taskId=ud2d7f870-564a-4d82-a14f-3969a62801e&title=&width=1038.08)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685593894885-90a5b045-e0e6-48e4-af52-79d26fbb701a.png#averageHue=%23ffffff&clientId=ub67c7d7d-fbda-4&from=paste&height=143&id=u89f0992d&originHeight=223&originWidth=1521&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=38658&status=done&style=none&taskId=ua5615a20-04b4-4b4f-bfd6-753b70058b1&title=&width=973.44)


# More on Complex Numbers
## Euler Theorem
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688138084206-0b4f9083-08f3-4c33-9300-61b7335fb7dc.png#averageHue=%23e9eafd&clientId=uf765d120-6674-4&from=paste&id=u7bbdbeed&originHeight=477&originWidth=2148&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=59913&status=done&style=none&taskId=ucbe48397-1757-46ae-95af-407666eb0aa&title=)

## Magnitude-Phase Representation
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688138062974-378e2497-2f96-49dd-9679-0e035a137f70.png#averageHue=%23fbfbfa&clientId=uf765d120-6674-4&from=paste&id=u7e8f54c6&originHeight=1350&originWidth=2219&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=254402&status=done&style=none&taskId=u8da48b6b-89b2-4ccc-a013-52666445803&title=)


# Phasors
## Definition 1: With 1/2
### Concepts
> **From Note 5/6 Fa21: 这个定义和后续的课程衔接更紧密, 我们选择这个定义。**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687506269368-61730ea3-5c91-4ab5-bd4c-3e0897e664a7.png#averageHue=%23f8f7f6&clientId=u85f58887-1a76-4&from=paste&id=g2xkW&originHeight=525&originWidth=1597&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=158694&status=done&style=none&taskId=u447d4da7-7724-440f-be3c-b5d3e65838b&title=)
> 对于一个三角函数$u(t)=Acos(wt+\phi)$来说，我们有如下定义:
> 1. $A$是`Amplitude`
> 2. $w$是`Angular Frequency`, $T=\frac{2\pi}{w}$是`Period`。要转化为`Frequency`我们可以使用$w=2\pi f$或者$f=\frac{w}{2\pi}$。
> 3. $w$的单位是$\frac{rad}{s}$, $f$的单位是$Hz$。
> 4. $\phi$是`Phasor Shift/Lag`, 表示将和$Acos(wt)$的图像向左平移$\frac{\phi}{w}$秒，表示图像比$Acos(wt)$先出现了$\frac{\phi}{w}$秒。
> 
结合`Euler Formula`, 我们有:
>  $\begin{aligned}Acos(wt+\phi)&=A\frac{e^{j(wt+\phi)}+e^{-j(wt+\phi)}}{2}\\&=\frac{Ae^{j\phi}}{2}e^{jwt}+\frac{Ae^{-j\phi}}{2}e^{-jwt}\end{aligned}$
> 其中:
> 1. $\frac{Ae^{j\phi}}{2}e^{jwt}$和$\frac{Ae^{-j\phi}}{2}e^{-jwt}$互为`Complex Conjugate`, 二者之和为`Real Number`。
> 2. $\frac{Ae^{j\phi}}{2}$被称为$jw-phasor$(`Coefficient of the time dependent exponentials`$e^{jwt}$)。$\frac{Ae^{-j\phi}}{2}$没有什么定义，因为知道了$\frac{Ae^{j\phi}}{2}$之后取一个`Complex Conjugate`就是$\frac{Ae^{-j\phi}}{2}$。



### Phasors As Input
> 对于任意的形如上述三角函数的输入$\vec{u}(t)$(假设$\pm jw$不是$\mathbf{A}$的特征值)，微分方程组$\frac{d\vec{x}(t)}{dt}=\mathbf{A} \vec{x}(t)+\vec{u}(t)$可以写成:
> $\frac{d\vec{x}(t)}{dt}=\mathbf{A} \vec{x}(t)+\vec{u_p}(t)+\overline{\vec{u_p}(t)}$
>  我们使用`Superposision Principle`可知:
> 1. 对于$\frac{d\vec{x}(t)}{dt}=\mathbf{A} \vec{x}(t)+\vec{u_p}(t)$, $\vec{x}(t)=(jw\mathbf{I}-\mathbf{A})^{-1}\frac{\mathbf{A}e^{j\phi}}{2}e^{jwt}$
> 2. 对于$\frac{d\vec{x}(t)}{dt}=\mathbf{A} \vec{x}(t)+\overline{\vec{u_p}(t)}$, $\vec{x}(t)=(-jw\mathbf{I}-\mathbf{A})^{-1}\frac{\mathbf{A}e^{-j\phi}}{2}e^{-jwt}=\overline{(jw\mathbf{I}-\mathbf{A})^{-1}\frac{\mathbf{A}e^{j\phi}}{2}e^{jwt}}$
> 
所以$\vec{x}(t)=(jw\mathbf{I}-\mathbf{A})^{-1}\frac{\mathbf{A}e^{j\phi}}{2}e^{jwt}+\overline{(jw\mathbf{I}-\mathbf{A})^{-1}\frac{\mathbf{A}e^{j\phi}}{2}e^{jwt}}$



### Phase Transform
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687490878035-710a2a3d-653f-4c11-bfeb-514aeb879f68.png#averageHue=%23faf9f9&clientId=ubb32db90-495a-4&from=paste&id=u768d5fa5&originHeight=150&originWidth=1656&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=33725&status=done&style=none&taskId=ucee116b7-53b3-4bf9-be88-1bed0a5498f&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687490884425-1446a0b5-6cfa-4b35-9b0a-3a2b8c1a5645.png#averageHue=%23f9f8f7&clientId=ubb32db90-495a-4&from=paste&id=u180cce71&originHeight=111&originWidth=1373&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=29753&status=done&style=none&taskId=u72294fbb-dc5d-45c5-8b67-5a01a26ec1b&title=)
> `Inverse Phasor Transform`($jw$phasor): $u(t)=\widetilde{W}e^{jwt}+\overline{\widetilde{W}}e^{-jwt}$。
> 注意到`Input`的`Magnitude`被先除以了$2$, 所以在后续`Output`的时候需要乘以$2$。



### Phasor KVL&KCL
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687491122312-0c5b533d-e749-4eb2-a16f-25ad36758d32.png#averageHue=%23faf9f8&clientId=ubb32db90-495a-4&from=paste&id=eO2vS&originHeight=588&originWidth=1913&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=150019&status=done&style=none&taskId=uc95ff100-b04f-4aa5-8b93-2313636b481&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687491134236-24e487c4-9c0c-470c-9eb8-ef3fef474c59.png#averageHue=%23f7f5f4&clientId=ubb32db90-495a-4&from=paste&id=DX6Mx&originHeight=514&originWidth=1851&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=161519&status=done&style=none&taskId=u25cc3352-da1f-4e64-ab31-f301de7c50b&title=)



## Definition 2: Without 1/2
> **From Note 5 Sp23: 这个定义更便于计算。**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688138107616-047d8ad2-5286-4904-9748-355c48952fcf.png#averageHue=%23e5e6fa&clientId=uf765d120-6674-4&from=paste&height=285&id=ua9ec1558&originHeight=428&originWidth=2099&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=148337&status=done&style=none&taskId=ue60ccb0e-73ff-466a-8dba-8ba12448c1b&title=&width=1399.3333333333333)

**Proof**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688138122178-1b4dc2b1-3606-4d6e-9911-17dc10c7d2c1.png#averageHue=%23fafaf9&clientId=uf765d120-6674-4&from=paste&id=uaee2c28b&originHeight=593&originWidth=2181&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=131306&status=done&style=none&taskId=u217666f6-118b-44d1-b65b-b179931ff7a&title=)
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688138134443-c4cb5c39-2386-4101-9b95-13fd60027e72.png#averageHue=%236687b9&clientId=uf765d120-6674-4&from=paste&height=249&id=ub3f8e8c9&originHeight=374&originWidth=2159&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=116434&status=done&style=none&taskId=u85b3bb12-20b7-4f9f-9ad3-b2999edbb31&title=&width=1439.3333333333333)

**Example**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688138145218-58e88dec-10df-4c33-b28d-b92507958d7b.png#averageHue=%23f6f5f4&clientId=uf765d120-6674-4&from=paste&id=u0440482f&originHeight=218&originWidth=2162&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=88445&status=done&style=none&taskId=u3bb426c6-b20f-4c49-86b1-5857647c360&title=)


## General Idea⭐⭐⭐⭐⭐
### Superposition Principle
> **Disc04B Sp23 P1**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688140248140-3c1c844a-b6ef-4cc0-a1ac-a6e888790829.png#averageHue=%23f9f8f7&clientId=u7104ee04-0a27-4&from=paste&id=u82a95d58&originHeight=1092&originWidth=1988&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=294096&status=done&style=none&taskId=u766b49ab-ddc8-48b1-acf1-39a7bfc4f54&title=)
> 这里`Phasor`$\widetilde{V_S},\overline{\widetilde{V_S}}$可以看成系数(因为和$t$无关)，$e^{jwt},e^{-jwt}$可以看成输入, 可以用`Superposition Principle`组合起来。
> $v_s(t)=e^{jwt}$作为电压输入进去的时候，系统的`Steady State Solution`$i_1(t)$的形式就应该是$K_1e^{jwt}$
> $v_s(t)=e^{-jwt}$作为电压输入进去的时候，系统的`Steady State Solution`$i_2(t)$的形式就应该是$K_2e^{-jwt}$。
> 然后使用`Superposition`, 当输入为: $v_s(t)=C_1e^{jwt}+C_2e^{-jwt}$(`Sinusoidal Functions`)时，$i(t)=C_1i_1(t)+C_2i_2(t)=C_1K_1e^{jwt}+C_2K_2$, 其中$C_1$和$C_2$共轭，$K_1$和$K_2$共轭。
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688140261088-9319b947-291e-4597-9e3e-b07d4f47026a.png#averageHue=%23fdfdfc&clientId=u7104ee04-0a27-4&from=paste&id=ud8b7cdd0&originHeight=891&originWidth=1833&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=203719&status=done&style=none&taskId=u612986ed-a3c6-4f67-ad47-320a1f4226b&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688184134405-99a8314a-9381-454b-a93d-96f029a17a52.png#averageHue=%23faf8f6&clientId=u3e3127cb-680f-4&from=paste&height=830&id=uf2760a34&originHeight=1245&originWidth=1093&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=354957&status=done&style=none&taskId=ufd39e85e-e84a-4d50-87b6-2459aa66815&title=&width=728.6666666666666)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688184159485-76ee0469-5f81-4f1a-ada6-b38d496ac0f6.png#averageHue=%23fcfbfa&clientId=u3e3127cb-680f-4&from=paste&id=u8ea463ca&originHeight=1043&originWidth=959&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=190804&status=done&style=none&taskId=u07f950e3-a9fd-491f-b543-f8a24e26651&title=)


### Simple Calculation Method
> If the input to the system is a sinusoidal function with frequency $ω$, the currents and voltages throughout the system in steady state will also be sinusoidal functions of the same frequency $ω$.  
> **简单的解题方法就是:**
> - 如果输入是$Acos(w_1t+\phi_1)$, 则输出是$Bcos(w_2t+\phi_2)$, 函数名对应上即可
> - 如果输入是$Asin(w_1t+\phi_1)$, 则输出是$Bsin(w_1 t+\phi_2)$, 函数名对应上即可
> - $\phi_2=\phi_1+\angle H(jw)$
> - $B=|H(jw)|A$
> 
**证明在**`**Transfer Function**`**小节中给出。**


## Warnings about Definitions
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688014810625-dcfb0d33-3e9d-4044-970e-4754ed2f1f4b.png#averageHue=%23fafaf9&clientId=u42f06011-4412-4&from=paste&id=JHNwY&originHeight=454&originWidth=1561&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=94736&status=done&style=none&taskId=u61c21a2c-d729-44ab-86f6-80d28519a21&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688014815201-868c682d-9139-4afc-ba02-2197c32e2101.png#averageHue=%23f3f0ed&clientId=u42f06011-4412-4&from=paste&id=oudw3&originHeight=695&originWidth=1502&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=305840&status=done&style=none&taskId=ua98c8568-203e-486f-82d1-dba00d4907e&title=)



# Phasors and Eigenvalues⭐⭐⭐⭐⭐
> **Hw05 Fa21 P6**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688141021139-f8b0f8d1-3333-4dcd-94bb-aaeaf75d39ff.png#averageHue=%23f4f4f4&clientId=ubd171f42-c62f-4&from=paste&id=u9cb806b3&originHeight=203&originWidth=1524&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=39946&status=done&style=none&taskId=u77a4d9ab-b3d4-4992-b7f2-106e9bac9ca&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688188558836-7010fcc3-c59f-480f-b7a9-167f2aa9ab9b.png#averageHue=%23f2f2f2&clientId=ue2f51580-0128-4&from=paste&id=ub0200597&originHeight=813&originWidth=2592&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=267772&status=done&style=none&taskId=uaa085b20-2ac1-4063-8a24-7e1b2511275&title=)
>  首先我们分析一下本题中的假设，即如果输入为$u(t)=\widetilde{U}e^{jwt}+\overline{\widetilde{U}}e^{-jwt}$, 则输出为$\vec{x}(t)=\overrightarrow{\widetilde{X}} \mathrm{e}^{+\mathrm{j} \omega t}+\overline{\overrightarrow{\widetilde{X}}} \mathrm{e}^{-\mathrm{j} \omega t} .$
> 这个结论在我们的`Exponential Input`小节中有分析过，当时我们的结论是，对于微分方程组$\frac{d}{dt}\vec{x}(t)=A\vec{x}(t)+\vec{u}(t)$, 如果$\vec{u}(t)=\vec{b}u(t)$, 则`Steady State Solution`:$\lim_{t\to\infty}\vec{x}(t)=\vec{x_0}e^{st}=(sI-A)\vec{b}e^{st}$。
> 本题中也是类似的思想，我们将解的形式带入原微分方程可得:
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688191645565-1791138f-0b57-474c-a629-83da361e32f4.png#averageHue=%23ffffff&clientId=ue2f51580-0128-4&from=paste&id=u26af80f2&originHeight=275&originWidth=1391&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=42255&status=done&style=none&taskId=u2226083f-95bc-4876-9041-b1ae5c48c3d&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688191653314-189571bd-f455-471d-aa7d-70a543cf5153.png#averageHue=%23ffffff&clientId=ue2f51580-0128-4&from=paste&id=u6a947525&originHeight=718&originWidth=1506&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=94854&status=done&style=none&taskId=u8f487065-dd15-4f35-9be6-24ffe992fdc&title=)



# Impedance&Reactance
## Capacitor
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687490245678-0c861917-ccb5-436a-88ca-1c06c471f7b9.png#averageHue=%23faf9f9&clientId=ubb32db90-495a-4&from=paste&id=u5743ac44&originHeight=372&originWidth=1348&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=76248&status=done&style=none&taskId=u396a535c-a70e-4b8f-a115-0423f3c9b18&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687490253408-cdfa9a1a-d772-4631-8098-6eb31e64bf1c.png#averageHue=%23fbfaf9&clientId=ubb32db90-495a-4&from=paste&id=ub559e2db&originHeight=1236&originWidth=1396&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=281998&status=done&style=none&taskId=u672155be-aa63-4509-86b5-a0aaf1a4148&title=)



## Resistor
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687490281560-d82247ff-afcf-45c1-a09a-11314f40dc20.png#averageHue=%23fdfcfc&clientId=ubb32db90-495a-4&from=paste&id=uba6d1515&originHeight=492&originWidth=1399&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=63518&status=done&style=none&taskId=u7c4a0c07-daff-45ca-880f-bc4b7539efd&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687490286196-218964ad-1536-416b-a253-1a892ba8d189.png#averageHue=%23fcfcfb&clientId=ubb32db90-495a-4&from=paste&id=u6564f381&originHeight=523&originWidth=1363&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=73028&status=done&style=none&taskId=u3935b5b3-8c9d-4443-842e-11f924fbf6d&title=)



## Inductor
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687490299716-1d525b8e-3964-4052-9227-d824cad6b587.png#averageHue=%23fcfcfb&clientId=ubb32db90-495a-4&from=paste&id=u28c93bea&originHeight=900&originWidth=1356&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=137377&status=done&style=none&taskId=u6a6716ae-e6a7-455b-b17c-189a6efd7f0&title=)



## Impedence&Reactance
> **Impedances that are pure imaginary are also called reactances. 比如电容和电导。**



# Impedence in complex plane
> **HW04 Fa21 P7**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687704228657-30728d2a-c7d8-4c36-b3de-6b61cef375ce.png#averageHue=%23f9f9f8&clientId=ue0a8f307-e14a-4&from=paste&id=ud8bec8cd&originHeight=593&originWidth=1854&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=143075&status=done&style=none&taskId=u08db1b92-0760-4dec-b2cc-adb73819cf9&title=)

**(a) w = 0.5**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687704247263-03e03bac-a7a1-4236-856c-84eb6cd0f4a9.png#averageHue=%23f7f7f7&clientId=ue0a8f307-e14a-4&from=paste&id=QFR1i&originHeight=1210&originWidth=1568&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=367338&status=done&style=none&taskId=ufd691c57-506e-480b-a881-40919b3ba03&title=)
**(b) w = 1**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687704287836-2dd92662-88e3-4371-a280-22de01eda166.png#averageHue=%23e0e0e0&clientId=ue0a8f307-e14a-4&from=paste&id=ue49dd1e9&originHeight=195&originWidth=1519&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=65573&status=done&style=none&taskId=u759d65f8-a775-421d-9778-f29e83f12d7&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687704324483-f3f561fb-730a-4c05-a9a7-57836e3c2e8c.png#averageHue=%23fcfbfb&clientId=ue0a8f307-e14a-4&from=paste&id=u2c86b799&originHeight=994&originWidth=1507&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=274558&status=done&style=none&taskId=u47d151ba-6e9b-48c2-b97d-5fec4a305ed&title=)
**(c) w = 2**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687704343752-d639852e-aa89-4b49-a3f6-9ea466df1f93.png#averageHue=%23f5f5f5&clientId=ue0a8f307-e14a-4&from=paste&id=u4043498b&originHeight=784&originWidth=1519&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=217826&status=done&style=none&taskId=ube3aa740-89de-41fc-91ba-926c9d79c07&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687704349788-60fa3ced-1e31-44a0-bc75-eeffe9b5ca05.png#averageHue=%23fbfbfb&clientId=ue0a8f307-e14a-4&from=paste&id=u564732c0&originHeight=421&originWidth=1448&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=126448&status=done&style=none&taskId=u19b79baf-2273-494d-adb9-df19cf2d91e&title=)
**(d) Natural Frequency**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687704369852-d09805b7-b94b-4e95-bd5e-753e4227d0c9.png#averageHue=%23efefef&clientId=ue0a8f307-e14a-4&from=paste&id=u883fe326&originHeight=435&originWidth=1505&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=110918&status=done&style=none&taskId=udfe4170c-bbb5-4a0c-b035-e4aa6129d55&title=)


# Transfer Function&Gain
> 在`DC`电路中, 我们称$\frac{V_{out}}{V_{in}}$为`Gain`是一个常数。
> , 而在`AC`电路中，我们在`Phasor Domain`中称$\frac{\tilde{V}_{out}}{\tilde{V}_{in}}$为`Transfer Function`，是一个`Complex Function`。
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688185231260-8be1e26e-0603-4215-ae85-9858913138c8.png#averageHue=%23f6f6f6&clientId=u871ebc29-d4cf-4&from=paste&id=JncoL&originHeight=518&originWidth=1438&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=151302&status=done&style=none&taskId=u764f6296-4c3f-4b73-8714-5cdd73e06d6&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687964092842-f6ca8520-82ec-407c-9749-b6c14640a68d.png#averageHue=%23faefee&clientId=u7ddb6d62-689c-4&from=paste&id=XKb0p&originHeight=691&originWidth=1210&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=163668&status=done&style=none&taskId=uada6f0e2-9065-40af-b6bb-f9154ef0cbf&title=)
> `Output Phasor`和`Input Phasor`之间的比值$\frac{\tilde{V_{out}}}{\tilde{V_{in}}}$被定义为$H(jw)$。
> 在`Time Domain`中，我们有:
> $\begin{aligned}V_{out}(t)&=\tilde{V}_{out}e^{jwt}+\overline{\tilde{V}_{out}}e^{-jwt}\\&=|\tilde{V}_{out}|e^{j\angle \tilde{V}_{out}}\cdot e^{jwt}+|\tilde{V}_{out}|e^{-j\angle \tilde{V}_{out} }\cdot e^{-jwt}\\&=|\tilde{V}_{out}|e^{i(wt+\angle \tilde{V}_{out})}+|\tilde{V}_{out}|e^{-i(wt+\angle \tilde{V}_{out})}\\&=2|\tilde{V}_{out}|cos(wt+\angle \tilde{V}_{out}) \end{aligned} \tag{1}$
> 另外我们知道: $\tilde{V}_{out}=H(jw)\tilde{V}_{in}$, 所以根据复数的性质，我们有: 
> $\begin{aligned}|\tilde{V}_{out}|e^{j\angle \tilde{V}_{out}}&=|H(jw)|e^{j\angle H(jw)}|\tilde{V}_{in}|e^{j\angle \tilde{V}_{in}}\\&=|H(jw)||\tilde{V}_{in}|e^{j(\angle H(jw)+\angle \tilde{V}_{in})}\end{aligned}$
> 所以$|\tilde{V}_{out}|=|H(jw)||\tilde{V}_{in}|,$$\angle \tilde{V}_{out}=\angle H(jw)+\angle \tilde{V}_{in}$
> 所以代入$(1)$后我们有$V_{out}(t)=2|H(jw)||\tilde{V}_{in}|cos(wt+\angle \tilde{V}_{in}+\angle H(jw))$
> **下面我们代入真实的输入函数:**
> 当$V_{in}(t)=V_{in}cos(wt+\phi)$时，$\tilde{V}_{in}=\frac{V_{in}e^{j\phi}}{2}$, 即$|\tilde{V}_{in}|=\frac{V_{in}}{2}$, $\angle \tilde{V}_{in}=\phi$, 所以:
> $\begin{aligned} V_{out}(t)&=2|H(jw)||\tilde{V}_{in}|cos(wt+\angle \tilde{V}_{in}+\angle H(jw))\\&=|H(jw)|V_{in}cos(wt+\phi+\angle H(jw))\end{aligned}$
> 1. `Transfer Function`$H(jw)$取决于我们的电路结构，通常是用`Impedance`来求出的。
> 2. `Transfer Function`$H(jw)$改变输入的信号强度(`Magnitude`)，改变输入信号的`Phase`($\angle H(jw)$)。




# Resources
> Note 5/6 Fa21




