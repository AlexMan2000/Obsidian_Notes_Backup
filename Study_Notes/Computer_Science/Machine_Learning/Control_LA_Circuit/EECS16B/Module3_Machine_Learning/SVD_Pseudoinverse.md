
# Overview
> ![image.png](SVD_Pseudoinverse.assets/20230914_1513499887.png)



<a name="qtVmA"></a>
# Minimum Energy Control
<a name="ZONsS"></a>
## Definition
> ![image.png](SVD_Pseudoinverse.assets/20230914_1513517615.png)![image.png](SVD_Pseudoinverse.assets/20230914_1513531032.png)



<a name="tY8B8"></a>
## Minimizing Formulation(Disc10A)
> 对于一个系统$x[i+1]=ax[i]+bu[i]~~(a>0,b>0)$来说:
> $x[l]=\begin{bmatrix} b&ab&a^2b&\cdots&a^{l-1}b\end{bmatrix}\begin{bmatrix} u[l-1]\\u[l-2]\\u[l-3]\\\vdots\\u[0]\end{bmatrix}=\langle\vec{v},\vec{u}\rangle$
> 其中$u[i]$是我们可以认为控制的输入，$\vec{v}$是参数向量，是系统内置的。
> 我们想要通过控制输入使得系统在第$l$个时间步达到$m$, 即$x[l]=m$，同时想要这个输入的`Energy`(用`L2 Norm`表示)最小。
> 则我们的最优化目标是：
> $\argmin_{\vec{u}}\|\vec{u}\|^2\\s.t.~~\langle\vec{u},\vec{v}\rangle=m$
> 求解此类最优化的方法有两种, 一种是使用多元微分中的拉格朗日乘子法，另一种是使用柯西不等式。


<a name="kD3D2"></a>
### Lagrange Method
> 将$\|\vec{u}\|^2$看成是由$l$个变量组成的多元函数，令$f(\vec{u})=\|\vec{u}\|^2=\vec{u}^{\top}\vec{u}$, 约束为$g(\vec{x})=\langle\vec{u},\vec{v}\rangle=m$, 其中$f$和$g$都是$R^m\to R$的函数。
> 则我们使用乘子法得到零界点必须满足的方程组:
> $\begin{cases}\frac{d}{d\vec{u}}f(\vec{u})=\lambda \frac{d}{d\vec{u}}g(\vec{u}) \\g(\vec{u})=m\end{cases}$
> 化简可得:
> $\begin{cases}2\vec{u}=\lambda \vec{v}~~~~~~~~~~~~~~~~(1)\\\langle\vec{u},\vec{v}\rangle=m~~~~~~~~~~~~(2)\end{cases}$
> 发现$\vec{x}$和$\vec{v}$同向，将$(1)$带入$(2)$消去$\vec{x}$得:
> $\langle\vec{u},\vec{v}\rangle=\langle\frac{\lambda}{2}\vec{v},\vec{v}\rangle=\frac{\lambda}{2}\|\vec{v}\|^2=m$
> 因为$\vec{v}$已知，于是$\lambda=\frac{2m}{\|\vec{v}\|^2}$, 然后可以解得:
>  $\vec{u}=\frac{m}{\|\vec{v}\|^2}\vec{v}$
> 然后我们还需要求二阶导来判断这个是最小值还是最大值:
> $\frac{d^2}{d\vec{u}^2}f(\vec{u})=2>0$
> 所以函数$f(\vec{x})$在定义域上都是`Convex`的，所以这个零界点是全局最小值。

 

<a name="dYsrh"></a>
### Cauchy Schwarz
> 柯西不等式说的是$\langle \vec{u},\vec{v}\rangle\leq \|\vec{u}\|\cdot\|\vec{v}\|$, 因为$\vec{v}$是常值向量，于是如果我们要最小化$\|\vec{u}\|$等价于最小化$\|\vec{u}\|\cdot\|\vec{v}\|$, 而这个不等式在$\vec{u}=\lambda \vec{v}$时取到（读者可以自行验证）。
> 因为$\langle \vec{u},\vec{v}\rangle=m$, 所以$\langle \lambda \vec{v},\vec{v}\rangle=\lambda\|\vec{v}\|^2=m$, 于是$\lambda = \frac{m}{\|v\|^2}$，也就是说$\vec{x}=\frac{m}{\|\vec{v}\|^2}\vec{v}$, 和上面一样。



<a name="j3544"></a>
### *Generalize to Matrix 
> 



<a name="wRIfT"></a>
### *Concrete Example
> 对于$x[i+1]=1.0 x[i]+0.7 u[i]$来说，我们有$a=1, b=0.7$:
> $\vec{v}=\begin{bmatrix} b&ab&a^2b&\cdots&a^{l-1}b\end{bmatrix}$



<a name="cA04m"></a>
# Proof of Rank-Nullity Theorem⭐⭐⭐⭐⭐
> ![image.png](SVD_Pseudoinverse.assets/20230914_1513551577.png)

**Proof**![image.png](SVD_Pseudoinverse.assets/20230914_1513583002.png)


<a name="E1BTp"></a>
# SVD - Algebraic Properties
<a name="Mmqs5"></a>
## Important Lemma
> [!lemma]
> ![image.png](SVD_Pseudoinverse.assets/20230914_1514004989.png)


## A^TA and AA^T
### Eigenvalues
```ad-proof
![image.png](./SVD_Pseudoinverse.assets/20230914_1514024217.png)
> ⭐: 如果$A$是实数矩阵，则$A^TA$和$AA^T$的特征值相等(但是零特征值可能不等，视$A^TA$和$AA^T$的形状而定)，且都为**非负实数**，$\lambda=\frac{\|A\vec{v}\|^2}{\|\vec{v}\|^2}$。
```
>[!proof]
>**Proof of Proposition 4**![image.png](SVD_Pseudoinverse.assets/20230914_1514049418.png)![image.png](SVD_Pseudoinverse.assets/20230914_1514068199.png)
> ![image.png](SVD_Pseudoinverse.assets/20230914_1514089412.png)


### Null Spaces
> [!important]
> 1. $Null(A^{\top}A)=Null(A)$
>$\forall v\in Null(A)$, $A\vec{v}=\vec{0}$, 则$A^TA\vec{v}=\vec{0}$，则$\vec{v}\in Null(A^{\top}A)$, 所以$Null(A)\subseteq Null(A^{\top}A)$。
> $\forall v\in Null(A^{\top}A)$, $A^{\top}A\vec{v}=\vec{0}$, 则$\vec{v}^{\top}A^{\top}A\vec{v}=0$，则$(A\vec{v})^{\top}(A\vec{v})=\|A\vec{v}\|^2=0$, 根据`Norm`的性质，$A\vec{v}=\vec{0}$, 即$\vec{v}\in Null(A)$, 所以$Null(A^{\top}A)\subseteq Null(A)$。
> 2. $Null(AA^{\top})=Null(A^{\top})$
> 
将上述证明中的$A$替换成$A^{\top}$即可。


### Column Spaces
> 1. $Col(AA^{\top})=Col(A)$:
> 
因为$AA^{\top}$的本质是$A$的线性组合，所以$Col(AA^{\top})\subseteq Col(A)$。
> 因为$Null(AA^{\top})=Null(A)$, 所以根据`Rank-Nullity Theorem`我们有$n - dim(Col(AA^{\top}))=n-dim(Col(A))$, 于是$dim(Col(A))=dim(Col(AA^{\top}))$, 于是根据`Lemma`我们有$Col(AA^{\top})=Col(A)$。
> 2. $Col(A^{\top}A)=Col(A^{\top})$:
> 
将上述过程中的$A$替换成$A^{\top}$即可。



<a name="n8jBO"></a>
## Full SVD
> ![image.png](SVD_Pseudoinverse.assets/20230914_1514107632.png)
> **有一些衍生的性质:**
> 1. 因为$Col(A)\perp Null(A^T)$, 所以$Col(U_r)\perp Col(U_{m-r})$。
> 2. 因为$Col(A^T)\perp Null(A)$, 所以$Col(V_r)\perp Col(V_{n-r})$。
> 3. $dim(Col(U_r))+dim(Col(U_{m-r}))=m$
> 4. $dim(Col(V_r))+dim(Col(V_{n-r}))=n$
> 5. $U_r$ form a basis for the columnspace of $A$.
> 6. $U_{m-r}$ form a basis for the nullspace of $A^T$.
> 7. The first $r$ columns of $U$, which come from the column space of $A$, are guaranteed to be orthogonal to the last $m-r$ columns of $U$, which are from the null space of $A^T$.
> 8. The first $r$ columns of $V$ form a basis for the column space of $A^T$.
> 9. The last $n-r$ columns of the $V$ matrix form a basis for the nullspace of $A$ (they form a basis because they are $n-r$ linearly independent vectors from a $n-r$-dimensional subspace)
> 10. The first $r$ columns of $V$, which come from the column space of $A^T$, are guaranteed to be orthogonal to the last $n-r$ columns of $V$, which are from the null space of $A$.
> 11. 性质$(v)-(viii)$使用`Outer Product Form`证明最方便。
> 
![image.png](SVD_Pseudoinverse.assets/20230914_1514123964.png)![image.png](SVD_Pseudoinverse.assets/20230914_1514148664.png)![image.png](SVD_Pseudoinverse.assets/20230914_1514155035.png)



<a name="MeJdS"></a>
## Compact SVD
> ![image.png](SVD_Pseudoinverse.assets/20230914_1514187023.png)![image.png](SVD_Pseudoinverse.assets/20230914_1514207835.png)



<a name="EMRdQ"></a>
## Outer Product Form
> ![image.png](SVD_Pseudoinverse.assets/20230914_1514222894.png)![image.png](SVD_Pseudoinverse.assets/20230914_1514245686.png)![image.png](SVD_Pseudoinverse.assets/20230914_1514269808.png)![image.png](SVD_Pseudoinverse.assets/20230914_1514281770.png)



<a name="m67Ju"></a>
## Orthogonal SVD
> ![image.png](SVD_Pseudoinverse.assets/20230914_1514302739.png)![image.png](SVD_Pseudoinverse.assets/20230914_1514322810.png)



<a name="ySMOt"></a>
## Existence Theorem
> ![image.png](SVD_Pseudoinverse.assets/20230914_1514345112.png)![image.png](SVD_Pseudoinverse.assets/20230914_1514366285.png)
> 之所以我们可以使用$U=EXTENDBASIS(U_r,R^m)$的方法是因为$U_{m-r}$的结果对$A$不构成影响。

**Proof of Theorem 6⭐⭐⭐⭐⭐**![image.png](SVD_Pseudoinverse.assets/20230914_1514382081.png)![image.png](SVD_Pseudoinverse.assets/20230914_1514407258.png)![image.png](SVD_Pseudoinverse.assets/20230914_1514426551.png)![image.png](SVD_Pseudoinverse.assets/20230914_1514453412.png)![image.png](SVD_Pseudoinverse.assets/20230914_1514471653.png)![image.png](SVD_Pseudoinverse.assets/20230914_1514505027.png)![image.png](SVD_Pseudoinverse.assets/20230914_1514526018.png)![image.png](SVD_Pseudoinverse.assets/20230914_1514541370.png)![image.png](SVD_Pseudoinverse.assets/20230914_1514565052.png)![image.png](SVD_Pseudoinverse.assets/20230914_1514578879.png)![image.png](SVD_Pseudoinverse.assets/20230914_1514592207.png)
> ![image.png](SVD_Pseudoinverse.assets/20230914_1515019191.png)![image.png](SVD_Pseudoinverse.assets/20230914_1515036938.png)
> 或者先$\text{DIAGONALIZE}(AA^T)$, 得到$U$和$\Lambda$, 然后通过$\vec{v}_i=\frac{A^T \vec{u}_i}{\sqrt{\lambda_i}}$构造$V$, 选取参数数量较小的计算。


## Uniqueness Theorem
> ![image.png](SVD_Pseudoinverse.assets/20230914_1515053703.png)![image.png](SVD_Pseudoinverse.assets/20230914_1515073811.png)![image.png](SVD_Pseudoinverse.assets/20230914_1515102139.png)![image.png](SVD_Pseudoinverse.assets/20230914_1515123111.png)



<a name="ezkna"></a>
## Construction from Existing SVD
<a name="sDy1m"></a>
### Creating from Transpose
> ![image.png](SVD_Pseudoinverse.assets/20230914_1515143147.png)



<a name="Mm2Ry"></a>
### Compact SVD => Full SVD
> 观察`Compact SVD`的形式:
> $A=U_r \Sigma_r V_r^{\top}=\left[\begin{array}{ll}U_r & U_{m-r}\end{array}\right]\left[\begin{array}{cc}\Sigma_r & 0_{r \times(n-r)} \\0_{(m-r) \times r} & 0_{(m-r) \times(n-r)}\end{array}\right]\left[\begin{array}{c}V_r^{\top} \\V_{n-r}^{\top}\end{array}\right]$
> 其中:
> 1. 如果$m-r>0$则: $\mathcal{N}(AA^{\top})\neq \{0\}$, 则我们需要通过求解$AA^{\top}$的零空间中的基向量得到$U_{m-r}$
> 2. 如果$n-r>0$则: $\mathcal{N}(A^{\top}A)\neq \{0\}$, 则我们需要通过求解$A^{\top}A$的零空间中的基向量得到$V_{n-r}$

**Example**![image.png](SVD_Pseudoinverse.assets/20230914_1515168126.png)


<a name="KBuie"></a>
### Full SVD => Compact SVD
> 观察`Full SVD`的形式
> $A=U \Sigma V^{\top}=\left[\begin{array}{ll}U_r & U_{m-r}\end{array}\right]\left[\begin{array}{cc}\Sigma_r & 0_{r \times(n-r)} \\0_{(m-r) \times r} & 0_{(m-r) \times(n-r)}\end{array}\right]\left[\begin{array}{c}V_r^{\top} \\V_{n-r}^{\top}\end{array}\right]$
> 提取出$A=U_r \Sigma_r V_r^{\top}$即可。

**Example**![image.png](SVD_Pseudoinverse.assets/20230914_1515183426.png)![image.png](SVD_Pseudoinverse.assets/20230914_1515199813.png)


## Useful Techniques
> [!important]
> Suppose $A\in \mathbb{R}^{m\times n}$.
> - When $A$ is full column rank, where $m>n$ and $rank(A)=n$, we have $A=U\begin{bmatrix} \Sigma_1\\0\end{bmatrix}V^{\top}$
> - When $A$ is full row rank, where $m<n$ and $rank(A)=m$, we have $A=U\begin{bmatrix} \Sigma_1&0\end{bmatrix}V^{\top}$


<a name="saySj"></a>
# Vector Space Miscellaneous
<a name="dswpA"></a>
## Vector Decomposition
> ![image.png](SVD_Pseudoinverse.assets/20230914_1515214283.png)



<a name="aqWql"></a>
## Vector Space Properties
> 对于一个矩阵$A\in \mathbb{R}^{m\times n}$且$Rank(A)=r\leq min(m,n)$, 我们有:
> 1. $Col(A^{\top})\perp Null(A)$(行空间正交于零空间) 。
> 2. $Col(A)\perp Null(A^{\top})$(列空间正交于左零空间)。
> 3. $dim(Col(A^T))=Rank(A)=dim(Col(A))=r$**行秩列秩相同**。
> 4. $dim(Null(A))=n-Rank(A)=n-dim(Col(A))=n-r$(**Rank Nullity Theorem**)
> 5. $dim(Null(A))+dim(Col(A^{\top}))=n$且$Col(A^{\top})\perp Null(A)$
>    1. 这说明没有向量同时处于两个空间中。如果有的话，假设为$\vec{v}$, 则根据$Col(A^{\top})\perp Null(A)$的定义，$\forall \vec{u}\in Col(A^{\top}), \vec{v}\in Null(A)$, $\langle \vec{u},\vec{v}\rangle=0$, 因为$\vec{v}\in Col(A)^{\top}, \vec{v}\in Null(A)$, 则$\langle \vec{v},\vec{v}\rangle=0$, 即$\vec{v}=\vec{0}$。
>    2. 对于任意向量$\vec{l}\in \mathbb{R}^n$来说，一般而言他由两部分构成。假设现在我们有一个子空间$S$, 则$\vec{l}=proj_S(\vec{l})+\vec{e}$, 其中$\vec{e}\perp proj_S(\vec{l})$。第一部分为在$S$上的投影，第二部分为正交于投影的部分。将$\vec{e}$所在的子空间定义为$T$且$S\perp T$, $dim(S)+dim(T)=n$。令$\vec{e}=proj_{T}(\vec{l})$, 则$\vec{l}=proj_S(\vec{l})+proj_{T}(\vec{l})$。
>    3. 我们有$Col(A^{\top})\perp Null(A)$, 所以对于任意$\vec{l}\in \mathbb{R}^n$，我们可以将其分别投影到$Col(A^{\top})$和$Null(A)$上。如果$\vec{l}\perp Col(A^{\top})$, 这说明$\vec{l}\notin Col(A^T)$，也就是$proj_{Col(A^T)}\vec{l}=\vec{0}$，那么$proj_{Null(A)}\vec{l}=\vec{l}-proj_{Col(A)}\vec{l}=\vec{l}-\vec{0}=\vec{l}$，投影为自身，所以$\vec{l}\in Null(A)$。
> 6. 推广到多个子空间$A_1,A_2,\cdots, A_n$, 这些子空间彼此正交且$\sum_{i=1}^n dim(A_i)=n$, 则对于任意的向量$\vec{v}\in \mathbb{R}^n$, 我们可以将其写成$\vec{v}=\sum_{i=1}^n proj_{A_i}(\vec{v})$, 如果$\vec{v}\perp A_i$, 则$\vec{v}\in S$, $S$为除了$A_i$以外的所有子空间长成的子空间之和(在线性代数线性算子中有更多介绍)。

 



<a name="mblDe"></a>
# SVD -  Geometric Properties
> ![image.png](SVD_Pseudoinverse.assets/20230914_1515237848.png)![image.png](SVD_Pseudoinverse.assets/20230914_1515252016.png)



<a name="po5OU"></a>
# SVD - Speed Up Least Square
> **Disc09B Sp22**


<a name="REVlx"></a>
## Normal Equation Method
> ![image.png](SVD_Pseudoinverse.assets/20230914_1515277145.png)



<a name="lfo6b"></a>
## SVD Method
> ![image.png](SVD_Pseudoinverse.assets/20230914_1515291358.png)![image.png](SVD_Pseudoinverse.assets/20230914_1515307585.png)![image.png](SVD_Pseudoinverse.assets/20230914_1515332269.png)![image.png](SVD_Pseudoinverse.assets/20230914_1515344392.png)



<a name="rqRco"></a>
# Moore-Penrose Pseudoiniverse
<a name="lw9FL"></a>
## Pseudoinverse Definition
> [!def]
> ![](SVD_Pseudoinverse.assets/20230914_1515365295.png)![](SVD_Pseudoinverse.assets/20230914_1515382241.png)




<a name="Tlj0A"></a>
## Left/Right Inverses
> [!important]
> 1. 当$A\in \mathbb{R}^{m\times n}$列满秩时，即$r=Rank(A)=n\leq m$时:
>    1. $A^{\dagger}A=(V_r\Sigma_r^{-1} U_r^{\top})(U_r\Sigma_r V_r^{\top})=V_rV_r^{\top}=V_nV_n^{\top}=I_n$
>    2. $A^{\dagger}=(A^{\top}A)^{-1}A^{\top}$**(Left Inverse)**
> **推导:** $\begin{aligned}(A^{\top}A)^{-1}A^{\top}&=(V_r\Sigma_r^{\top}\Sigma_r V_r^{\top})^{-1}(U_r\Sigma_r V_r^{\top})^{\top}\\&=V_r(\Sigma_r^{\top}\Sigma_r)^{-1}V_r^{\top}V_r\Sigma_r^{\top}U_r^{\top}\\&=V_r(\Sigma_r^{\top}\Sigma_r)^{-1}\Sigma_r^{\top}U_r^{\top}\\&=V_r\Sigma_r^{-2}\Sigma_rU_r^{\top}\\&=V_r\Sigma_r^{-1}U_r^{\top}\\&=A^{\dagger}\end{aligned}$($V_r^{\top}=V_r^{-1}$, 因为$V_r=V_n$, 为方阵)
>    3. $\Sigma^{\dagger}=(\Sigma^{\top}\Sigma)^{-1}\Sigma^{\top}$
> **推导:** $\begin{aligned}(A^{\top}A)^{-1}A^{\top}&=(V\Sigma^{\top}\Sigma V^{\top})^{-1}(U\Sigma V^{\top})^{\top}\\A^{\dagger}&=V(\Sigma^{\top}\Sigma)^{-1}V^{\top}V\Sigma^{\top}U^{\top}\\&=V(\Sigma^{\top}\Sigma)^{-1}\Sigma^{\top}U^{\top}\\&=V(\Sigma^{\top}\Sigma)^{-1}\Sigma^{\top}U^{\top}\\&=V\Sigma^{\dagger}U^{\top}\end{aligned}$
>    4. 所有`Left Inverse`可以表示为$A^{li}=A^{\dagger}+Q^{\top}$, 其中$A^{\top}Q=0$($Q$列向量$\in Null(A^{\top})$)
> 2. 当$A\in \mathbb{R}^{m\times n}$行满秩时，即$r=Rank(A)=m\leq n$时:
>    1. $AA^{\dagger}=(U_r\Sigma_r V_r^{\top})(V_r\Sigma_r^{-1} U_r^{\top})=U_rU_r^{\top}=U_mU_m^{\top}=I_m$
>    2. $A^{\dagger}=A^{\top}(AA^{\top})^{-1}$**(Right Inverse)**
> **推导:** $\begin{aligned}A^{\top}(AA^{\top})^{-1}&=(U_r\Sigma_r V_r^{\top})^{\top}(U_r\Sigma_r\Sigma_r^{\top} U_r^{\top})^{-1}\\&=V_r\Sigma_r^{\top}U_r^{\top}U_r(\Sigma_r\Sigma_r^{\top})^{-1}U_r^{\top}\\&=V_r\Sigma_r^{\top}(\Sigma_r\Sigma_r^{\top})^{-1}U_r^{\top}\\&=V_r\Sigma_r\Sigma_r^{-2}U_r^{\top}\\&=V_r\Sigma_r^{-1}U_r^{\top}\\&=A^{\dagger}\end{aligned}$($U_r^{\top}=U_r^{-1}$, 因为$U_r=U_m$, 为方阵)
>    3. $\Sigma^{\dagger}=\Sigma^{\top}(\Sigma\Sigma^{\top})^{-1}$
> **推导:** $\begin{aligned}A^{\top}(AA^{\top})^{-1}&=(U\Sigma V^{\top})^{\top}(U\Sigma\Sigma^{\top} U^{\top})^{-1}\\A^{\dagger}&=V\Sigma^{\top}U^{\top}U(\Sigma\Sigma^{\top})^{-1}U^{\top}\\&=V\Sigma^{\top}(\Sigma\Sigma^{\top})^{-1}U^{\top}\\&=V\Sigma^{\dagger}U^{\top}\end{aligned}$
>    4. 所有`Left Inverse`可以表示为$A^{ri}=A^{\dagger}+Q$, 其中$AQ=0$($Q$列向量$\in Null(A)$)



<a name="rFSjc"></a>
## Misellaneous Properties
> [!property]
> ![](SVD_Pseudoinverse.assets/20230914_1515409235.png)
> **还有一些常用性质, 假设**$A\in \mathbb{R}^{m\times n}$**:**
> 1. $\Sigma\in \mathbb{R}^{m \times n}$, $\Sigma^{\dagger}\in \mathbb{R}^{n\times m}$
> 2. 如果$A$列满秩，则$\Sigma^{\dagger}_{n\times m}=(\Sigma^{\top}\Sigma)^{-1}_{n\times n}\Sigma^{\top}_{n\times m}$。推导如上文。
> 3. 如果$A$行满秩，则$\Sigma^{\dagger}_{n\times m}=\Sigma^{\top}_{n\times m}(\Sigma \Sigma^{\top})^{-1}_{m\times m}$。推导如上文。

> [!proof]
> **Proofs**(i): **如果$A$可逆，则$AA^{-1}=I$, $A=U_r\Sigma_r V_r^{\top}$, 所以$A^{-1}=(U_r\Sigma_r V_r^{\top})^{-1}=V_r\Sigma_r^{-1}U_r^{\top}=A^{\dagger}$<br />**(ii): **$(A^{\dagger})^{\dagger}=(V_r\Sigma_r^{-1}U_r^{\top})^{\dagger}$, 令$\widetilde{U}_r=V_r,\widetilde{V}_r=U_r,\widetilde{\Sigma}_r=\Sigma_r^{-1}$, 即$(\widetilde{U}_r\widetilde{\Sigma}_r\widetilde{V}_r^{\top})^{\dagger}=\widetilde{V}_r\widetilde{\Sigma}_r^{-1}\widetilde{U}_r^{\top}=U_r\Sigma_r V_r^{\top}=A$, 证毕。<br />**(iii):** $(A^{\top})^{\dagger}=(V_r\Sigma_r U_r^{\top})^{\dagger}$, 令$\widetilde{U}_r=V_r,\widetilde{V}_r=U_r,\widetilde{\Sigma}_r=\Sigma_r$, 即$(\widetilde{U}_r\widetilde{\Sigma}_r\widetilde{V}_r^{\top})^{\dagger}=\widetilde{V}_r\widetilde{\Sigma}_r^{-1}\widetilde{U}_r^{\top}=U_r\Sigma_r^{-1} V_r^{\top}=(V_r\Sigma_r^{-1}U_r^{\top})^{\top}=(A^{\dagger})^{\top}$<br />**(iv): **$(\alpha A)^{\dagger}=( U_r\alpha\Sigma_r V_r^{\top})^{\dagger}=V_r(\alpha\Sigma_r)^{\dagger}U_r^{\top}=V_r\alpha^{-1}\Sigma^{\dagger}U_r^{\top}=\alpha^{-1}A^{\dagger}$<br />**(v): **$AA^{\dagger}A=(U_r\Sigma_r V_r^{\top})(U_r\Sigma_r V_r^{\top})^{\dagger}(U_r\Sigma_r V_r^{\top})=(U_r\Sigma_r V_r^{\top})(V_r\Sigma_r^{-1}U_r)(U_r\Sigma_r V_r^{\top})=U_r\Sigma_r V_r^{\top}=A$<br />**(vi):**$A^{\dagger}AA^{\dagger}=(U_r\Sigma_r V_r^{\top})^{\dagger}(U_r\Sigma_r V_r^{\top})(U_r\Sigma_r V_r^{\top})^{\dagger}=(V_r\Sigma_r^{-1}U_r)(U_r\Sigma_r V_r^{\top})(V_r\Sigma_r^{-1}U_r^{\top})=V_r\Sigma_r U_r^{\top}=A^{\dagger}$<br />**(vii) 和 (viii) 见上文推导。**



## Orthogonal Projectors
> [!important]
> 我们知道对于一个$d$维子空间$S$来说，存在一个`Basis`$\{\vec{b}_1,\vec{b}_2,\cdots, \vec{b}_d\}$, $\vec{b}_i\in \mathbb{R}^n$。
> 令$B=[\vec{b}_1,\vec{b}_2,\cdots, \vec{b}_d]\in \mathbb{R}^{n\times d}$，则对于任意向量$\vec{x}\in \mathbb{R}^n$来说，$proj_S(\vec{x})=B(B^{\top}B)^{-1}B^{\top}\vec{x}$
> 当$B$的各列为单位正交向量时，$B^{\top}B=I_d$, 即$proj_S(\vec{x})=BB^{\top}\vec{x}$。
> **对于一个矩阵**$A\in \mathbb{R}^{m\times n}$**来说，我们定义其四个空间的**`Orthogonal Projectors`**为:**
> 1. $P_{\mathcal{R}(A)}=AA^{\dagger}$
> - 对于$\mathcal{R}(A)$来说，我们知道$\mathcal{R}(U_r)=\mathcal{R}(A)$, 且$U_r\in \mathbb{R}^{m\times r}$为$\mathcal{R}(A)$的一组正交基。根据上面的描述，$\forall \vec{x}\in \mathbb{R}^m$来说，$proj_{\mathcal{R}(A)}(\vec{x})=U_rU_r^{\top}\vec{x}=AA^{\dagger}\vec{x}$。
> - 如果$A$为列满秩，则$P_{\mathcal{R}(A)}=AA^{\dagger}=A(A^{\top}A)^{-1}A^{\top}$
> 2. $P_{\mathcal{N}(A^{\top})}=I_m-AA^{\dagger}$
> - 对于$\mathcal{N}(A^{\top})$来说，我们知道$\mathcal{R}(U_{m-r})=\mathcal{N}(A^{\top})$, 且$U_{m-r}\in \mathbb{R}^{m\times (m-r)}$为$\mathcal{N}(A^{\top})$的一组正交基。根据上面的描述，$\forall \vec{x}\in \mathbb{R}^m$来说，$proj_{\mathcal{N}(A^{\top})}(\vec{x})=U_{m-r}U_{m-r}^{\top}\vec{x}=(I_m-U_rU_r^{\top})\vec{x}=(I_m-AA^{\dagger})\vec{x}$。
> - 如果$A$为列满秩，则$P_{\mathcal{N}(A^{\top})}=I_m-AA^{\dagger}=I_m-A(A^{\top}A)^{-1}A^{\top}$
> 3. $P_{\mathcal{R}(A^{\top})}=A^{\dagger }A$
> - 对于$\mathcal{R}(A^{\top})$来说，我们知道$\mathcal{R}(V_r)=\mathcal{R}(A^{\top})$, 且$V_r\in \mathbb{R}^{n\times r}$的各列为$\mathcal{R}(A^{\top})$的一组正交基。根据上面的描述，$\forall \vec{x}\in \mathbb{R}^n$来说，$proj_{\mathcal{R}(A)}(\vec{x})=V_rV_r^{\top}\vec{x}=A^{\dagger}A\vec{x}$。
> - 如果$A$为行满秩，则$P_{\mathcal{R}(A^{\top})}=A^{\dagger}A=A^{\top}(AA^{\top})^{-1}A$
> 4. $P_{\mathcal{N}(A)}=I_n-A^{\dagger }A$
> - 对于$\mathcal{N}(A)$来说，我们知道$\mathcal{R}(V_{n-r})=\mathcal{N}(A)$, 且$V_{n-r}\in \mathbb{R}^{m\times r}$的各列为$\mathcal{N}(A)$的一组正交基。根据上面的描述，$\forall \vec{x}\in \mathbb{R}^n$来说，$proj_{\mathcal{R}(A)}(\vec{x})=V_{n-r}V_{n-r}^{\top}\vec{x}=(I_n-V_rV_r^{\top})\vec{x}=(I_n-A^{\dagger}A)\vec{x}$
> - 如果$A$为行满秩，则$P_{\mathcal{N}(A)}=I_n-A^{\dagger}A\vec{x}=I_n-A^{\top}(AA^{\top})^{-1}A$



<a name="FqLGO"></a>
## Pseudoinverse&Least Square
> [!thm]
> ![image.png](SVD_Pseudoinverse.assets/20230914_1515427659.png)
> 这里阐述了$A$不是列满秩时的最小二乘问题，当$A$不是列满秩时，我们有多个最小二乘解。
> `Side Notes`**:**
> 1. $proj_{Col(A)}(\vec{b})$是唯一的，且**当**$A$**的列满秩时**，$proj_{Col(A)}(\vec{b})=A(A^TA)^{-1}A^T\vec{b}$ ，此时我们求解$A\vec{z}=proj_{Col(A)}(\vec{b})=A(A^TA)^{-1}A^T\vec{b}$(两边同乘$(A^TA)^{-1}A^T$), 可以得到$\vec{z}=(A^TA)^{-1}A^T\vec{b}$唯一存在。 
> 2. **当**$A$**不是列满秩时**，$A\vec{z}=proj_{Col(A)}(\vec{b})$的解$\vec{z}$就不唯一了。
> 3. $\vec{x}^{*}\in Col(A^{\top})$，因为$\vec{x}^*=A^{\dagger}\vec{y}=\sum_{i=1}^r \sigma_i\vec{v}_i\vec{u}_i^{\top}\vec{y}\in Col(V_r)=Col(A^{\top})$。
> 4. $\vec{x}^*\perp Null(A)$，因为$Col(A^{\top})\perp Null(A)$, 所以$\forall \vec{x}\in Col(A^{\top})$, $\vec{x}\perp Null(A)$。
> 5. $S=A^{\dagger}\vec{b}+Null(A)=\{A^{\dagger}\vec{b}+\vec{z}|\vec{z}\in Null(A)\}$。

> [!proof] **Proof of Theorem 20 - Method 1**
> ![image.png](SVD_Pseudoinverse.assets/20230914_1515446571.png)<br />![image.png](SVD_Pseudoinverse.assets/20230914_1515469953.png)![image.png](SVD_Pseudoinverse.assets/20230914_1515497828.png)![image.png](SVD_Pseudoinverse.assets/20230914_1515513395.png)
**Proof of Theorem 20 - Method 2 Clearer Version （EECS127 HW03）**![image.png](SVD_Pseudoinverse.assets/20230914_1515533336.png)![image.png](SVD_Pseudoinverse.assets/20230914_1515551704.png)![image.png](SVD_Pseudoinverse.assets/20230914_1515572855.png)
> **上面的证明中有一个重要技巧:**
> 1. 假设$\vec{x}_0=\vec{x}-proj_{Null(A)}\vec{x}$, 则$\vec{x}_0$和$Null(A)$正交。几何上来看，$\vec{x}_0$其实就是$Null(A)$的`Error Vector`，所以垂直。
> 2. $\vec{y}=proj_{Null(A)}\vec{x}$实际上就是一个在$Null(A)$中的向量，满足$A\vec{y}=\vec{0}$。
> 3. 要证明一个向量$\vec{x}$和一个子空间$S$不正交，只需要从$S$中任取一个向量$\vec{y}$, 证明$\langle \vec{x},\vec{y}\rangle\neq 0$即可。
> 
![image.png](SVD_Pseudoinverse.assets/20230914_1515598943.png)
> - `Corollary 21`说的是: 对于列满秩矩阵来来说，$\|A\vec{x}-\vec{b}\|$的最小值仅在$\vec{x}=A^+\vec{b}$时取到。
> - `Corollary 22`说的是: 对于行满秩的矩阵来说，满足$A\vec{x}=\vec{b}$的解中最小`Norm`的是$\vec{x}=A^+\vec{b}$。


# Examples
<a name="ikrpE"></a>
## Example 1: Construction
> ![image.png](SVD_Pseudoinverse.assets/20230914_1516014044.png)



<a name="XDm5D"></a>
## Example 2: Infinite SVDs
> ![image.png](SVD_Pseudoinverse.assets/20230914_1516035562.png)



<a name="UPZkF"></a>
## Example 3: Shifted Eigenvalues
> **EECS127 disc_03 P2**
> ![image.png](SVD_Pseudoinverse.assets/20230914_1516054350.png)![image.png](SVD_Pseudoinverse.assets/20230914_1516077924.png)![image.png](SVD_Pseudoinverse.assets/20230914_1516091907.png)![image.png](SVD_Pseudoinverse.assets/20230914_1516116436.png)



<a name="K8mUn"></a>
## Example 4: Discretization
> ![image.png](SVD_Pseudoinverse.assets/20230914_1516137245.png)
> **其中我们分析一下**$(53)$**和**$(54)$**的由来:**
> 1. 首先是$(54)$, 我们有$\int_{i\Delta}^t  \frac{dv(t)}{dt}dt = \int_{i\Delta}^t \frac{1}{RM}u_d[i]dt$, 于是$v(t)-v(i\Delta)=\frac{1}{RM}u_d[i]t\big|_{i\Delta}^t=\frac{1}{RM}(t-i\Delta)u_d[i]$, 即$v(t)=v(i\Delta)+(t-i\Delta)\frac{1}{RM}u_d[i]=v_d[i]+(t-i\Delta)\frac{1}{RM}u_d[i]$($t\in [i\Delta,(i+1)\Delta]$)
> 2. 将$(54)$的结果带入$(51)$得到$\frac{dp(t)}{dt}=v(i\Delta)+(t-i\Delta)\frac{1}{RM}u_d[i]$, 两别取积分得到$\begin{aligned}\int_{i\Delta}^t\frac{dp(t)}{dt}dt&=\int_{i\Delta}^{t}v_d[i]+(\tau-i\Delta)\frac{1}{RM}u_d[i]d\tau\\p(t)-p(i\Delta)&=(t-i\Delta)v_d[i]+\int_{i\Delta}^{t}(\tau-i\Delta)\frac{1}{RM}u_d[i]d(\tau-i\Delta)\\p(t)-p_d[i]&=(t-i\Delta)v_d[i]+\int_{0}^{t-i\Delta}u\frac{1}{RM}u_d[i]du\\p(t)&=p_d[i]+(t-i\Delta)v_d[i]+\frac{1}{2}(t-i\Delta)^2\frac{1}{RM}u_d[i]\end{aligned}$($t\in [i\Delta,(i+1)\Delta]$)
> 
![image.png](SVD_Pseudoinverse.assets/20230914_1516151707.png)![image.png](SVD_Pseudoinverse.assets/20230914_1516175790.png)![image.png](SVD_Pseudoinverse.assets/20230914_1516192006.png)



<a name="FwQxR"></a>
# Resources
> **Note 16 Sp22**
> **Disc09B/10A/10B/11A Sp22**
> **Lecture Note 19 ~ 22**
> **Sp23 HW12**

