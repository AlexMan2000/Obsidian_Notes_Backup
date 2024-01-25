<a name="E2D90"></a>
# Overview
> ![image.png](Orthonormalization.assets/20230914_1517124483.png)



<a name="gDViI"></a>
# Orthogonality
<a name="ouBZ9"></a>
## Orthogonality of Vectors
> ![image.png](Orthonormalization.assets/20230914_1517143853.png)
> 🔔: 非零正交向量集合中的向量是线性无关的。
> ![image.png](Orthonormalization.assets/20230914_1517151237.png)![image.png](Orthonormalization.assets/20230914_1517173981.png)

**Proof of Theorem 3 - Method 1**假设$S=\{\vec{a}_1,\vec{a}_2,\cdots, \vec{a}_n\}$，其中$\langle \vec{a}_i,\vec{a}_j\rangle=0(i\neq j)$, 且$\langle \vec{a}_i,\vec{a}_i\rangle>0$则我们要证明:<br />$c_1\vec{a}_1+c_2\vec{a}_2+\cdots +c_n\vec{a}_n=0$的系数$c_i$全部为零。<br />我们**利用**`**Inner Product**`和正交性来证明:<br />我们有$\begin{aligned}0&=\langle \vec{a}_i,0\rangle=\langle \vec{a}_i,c_1\vec{a}_1+c_2\vec{a}_2+\cdots +c_n\vec{a}_n\rangle\\&=c_1\langle\vec{a}_i,\vec{a_1}\rangle+c_2\langle\vec{a}_i,\vec{a_2}\rangle+\cdots+c_i\langle \vec{a}_i,\vec{a_i}\rangle+\cdots+c_1\langle\vec{a}_i,\vec{a_n}\rangle\end{aligned}$<br />因为$\langle \vec{a}_i,\vec{a}_i\rangle>0$, 所以$c_1\langle\vec{a}_i,\vec{a_1}\rangle+c_2\langle\vec{a}_i,\vec{a_2}\rangle+\cdots+c_i\langle \vec{a}_i,\vec{a_i}\rangle+\cdots+c_1\langle\vec{a}_i,\vec{a_n}\rangle=c_1\|\vec{a}_i\|=0$<br />所以$c_i=0,~\forall i$, 证毕。
**Proof of Theorem 3 - Method 2**![image.png](Orthonormalization.assets/20230914_1517198123.png)
> ![image.png](Orthonormalization.assets/20230914_1517205131.png)



<a name="dvIhm"></a>
## Orthogonality of Sets
> ![image.png](Orthonormalization.assets/20230914_1517227637.png)![image.png](Orthonormalization.assets/20230914_1517245714.png)
> ⭐: 注意这里$S_1$和$S_2$(都$\in \mathbb{R}^n$)两个子空间彼此正交并不是说$S_1$和$S_2$各自是正交向量的集合，因为子空间中的向量有无限多个，而正交向量集合的条件由`Corollary 4`可知，是不能超过$n$的。
> ![image.png](Orthonormalization.assets/20230914_1517266324.png)![image.png](Orthonormalization.assets/20230914_1517273169.png)

**Proof of Proposition 6**假设$S_1$的基向量为$B_1=\{\vec{a}_1,\vec{a}_2,\cdots, \vec{a}_m\}$, $S_2$的基向量为$B_2=\{\vec{b}_1,\vec{b}_2,\cdots, \vec{b}_n\}$，注意$B_1$和$B_2$各自不一定是由正交向量列构成，则我们有:

1. 如果$B_1$和$B_2$着两个集合互相正交，则$\forall 1\leq i\leq m, 1\leq j\leq n, \langle\vec{a}_i,\vec{b}_j\rangle=0$, 因为$B_1$是$S_1$的基，所以$\forall \vec{u} \in S_1$, $\vec{u}=c_1\vec{a}_1+c_2\vec{a}_2+\cdots+c_m\vec{a}_m$for some coefficients $c_i$'s。同理$\forall \vec{v} \in S_2$, $\vec{v}=d_1\vec{b}_1+d_2\vec{b}_2+\cdots+d_m\vec{b}_m$，所以$\forall \vec{u}\in S_1,\vec{v} \in S_2$我们有：$\begin{aligned}\langle c_1\vec{a}_1+c_2\vec{a}_2+\cdots+c_m\vec{a}_m ,d_1\vec{b}_1+d_2\vec{b}_2+\cdots+d_m\vec{b}_m \rangle&=\sum_{i=1}^m\sum_{j=1}^n c_id_j\langle\vec{a}_i,\vec{b}_j\rangle=0\end{aligned}$，这说明$\forall \vec{u}\in S_1,\vec{v} \in S_2,\langle\vec{u},\vec{v}\rangle=0$，即$S_1$和$S_2$相互正交。
2. 如果$S_1$和$S_2$着两个集合互相正交，$\forall \vec{u}\in S_1,\vec{v} \in S_2,\langle \vec{u},\vec{v}\rangle=0$。同样我们知道
   - $\forall \vec{u} \in S_1$, $\vec{u}=c_1\vec{a}_1+c_2\vec{a}_2+\cdots+c_m\vec{a}_m$
   - $\forall \vec{v} \in S_2$, $\vec{v}=d_1\vec{b}_1+d_2\vec{b}_2+\cdots+d_n\vec{b}_n$

以及$\langle \vec{u},\vec{v}\rangle=0$。所以我们有$\forall c_i,d_j$:$\begin{aligned}\langle c_1\vec{a}_1+c_2\vec{a}_2+\cdots+c_m\vec{a}_m ,d_1\vec{b}_1+d_2\vec{b}_2+\cdots+d_m\vec{b}_m \rangle&=\sum_{i=1}^m\sum_{j=1}^n c_id_j\langle\vec{a}_i,\vec{b}_j\rangle=0\end{aligned}$<br />因为$\forall c_i,d_j, \sum_{i=1}^m\sum_{j=1}^n c_id_j\langle\vec{a}_i,\vec{b}_j\rangle=0$, 所以$\forall i,j,\langle\vec{a}_i,\vec{b}_j\rangle=0$, 这表明$B_1$和$B_2$集合互相正交。 



<a name="mUWbR"></a>
# Orthonormality
<a name="pT0VZ"></a>
## Normalized Vectors
> ![image.png](Orthonormalization.assets/20230914_1517293479.png)



<a name="cVHKT"></a>
## Orthonormal Vectors
> ![image.png](Orthonormalization.assets/20230914_1517318600.png)



<a name="naEGG"></a>
## Orthonormal Set
> ![image.png](Orthonormalization.assets/20230914_1517339975.png)



<a name="dvESF"></a>
## Orthonormal Matrices
<a name="cxI31"></a>
### Definition
> ![image.png](Orthonormalization.assets/20230914_1517357349.png)![image.png](Orthonormalization.assets/20230914_1517377699.png)

**Proof of Theorem 11**![image.png](Orthonormalization.assets/20230914_1517394183.png)

<a name="MBhAu"></a>
### Preserve Length Propoerties
> ![image.png](Orthonormalization.assets/20230914_1517412902.png)![image.png](Orthonormalization.assets/20230914_1517422273.png)

**Proof of Theorem 13**![image.png](Orthonormalization.assets/20230914_1517447991.png)
> ![image.png](Orthonormalization.assets/20230914_1517461380.png)![image.png](Orthonormalization.assets/20230914_1517482088.png)



<a name="Ju59u"></a>
## Unitary Matrices
<a name="zUa5E"></a>
### Definition
> ![image.png](Orthonormalization.assets/20230914_1517508497.png)![image.png](Orthonormalization.assets/20230914_1517524482.png)



<a name="fcVzx"></a>
### Preserve Length Properties
> ![image.png](Orthonormalization.assets/20230914_1517543892.png)



<a name="zMxgy"></a>
# Projections
<a name="nC6W0"></a>
## Definition
> ![image.png](Orthonormalization.assets/20230914_1517561028.png)



<a name="dEhJP"></a>
## Least Squares & Projections
> [!thm]
> ![image.png](Orthonormalization.assets/20230914_1517589561.png)

> [!proof]
> **Proof of Theorem 16**![image.png](Orthonormalization.assets/20230914_1517595429.png)

> [!cor]
> ![image.png](Orthonormalization.assets/20230914_1518018459.png)

> [!proof]
> **Proof of Corollary 17**![image.png](Orthonormalization.assets/20230914_1518033731.png)

> [!thm]
> ![image.png](Orthonormalization.assets/20230914_1518043126.png)

> [!proof]
> **Proof of Theorem 18**我们把$\vec{s}_1, \cdots, \vec{s}_n$放到一个矩阵$M\in \mathbb{R}^{m\times n}$中，这些向量$\vec{s}_i,i\in [1,n]$是互相线性无关的。于是$M$矩阵的形状必须满足$m\geq n$, 然后套用`Corollary 17`即可。<br />重复上述步骤，使用`Theorem 16`即可。



## Orthogonality Principles
> [!important]
> ![image.png](Orthonormalization.assets/20230914_1518067563.png)

> [!proof]
> **Proof of Theorem 19**![image.png](Orthonormalization.assets/20230914_1518083134.png)![image.png](Orthonormalization.assets/20230914_1518094475.png)$\vec{z}\in S, \vec{y}\in S$，根据子空间的性质(向量的线性组合也在子空间内)，所以$\vec{z}-\vec{y}\in S$。<br />因为$(ii)$假设$\vec{y}-\vec{x}$与$S$正交, 所以$\vec{y}-\vec{x}$垂直于$S$中的任何一个向量, 当然也包括$\vec{z}-\vec{y}$, 所以$\langle \vec{z}-\vec{y}, \vec{y}-\vec{x}\rangle=0$。
> **证明中出现的非常重要的想法:**
> 1. 如果我们有$\{\vec{v}_1,\vec{v}_2,\cdots,\vec{v}_n\}$这个`Orthogonal Sets`，则我们可以将这个集合以任意的方式平均分成几个子集，这些子集张成的子空间互相正交。
> 2. 对于任意向量$\vec{x}$和一个子空间$S$, $proj_S(\vec{x})$存在且唯一。令其为$\vec{y}=proj_S(\vec{x})\in S$, 则$\forall z\in S$,$\|\vec{z}-\vec{x}\|>\|\vec{y}-\vec{x}\|$, 也就是投影距离$\vec{x}$的端点最近。



<a name="dsOLx"></a>
# Gram-Schmidt Orthonormalization
## Algorithm
> ![image.png](Orthonormalization.assets/20230914_1518123943.png)



<a name="jynsr"></a>
## Proof of Correctness⭐⭐⭐⭐⭐
> ![image.png](Orthonormalization.assets/20230914_1518141350.png)![image.png](Orthonormalization.assets/20230914_1518161639.png)

**Proof about z's**![image.png](Orthonormalization.assets/20230914_1518187538.png)![image.png](Orthonormalization.assets/20230914_1518202288.png)![image.png](Orthonormalization.assets/20230914_1518229389.png)![image.png](Orthonormalization.assets/20230914_1518247684.png)![image.png](Orthonormalization.assets/20230914_1518267382.png)![image.png](Orthonormalization.assets/20230914_1518285587.png)![image.png](Orthonormalization.assets/20230914_1518303221.png)
**Proof about p's**![image.png](Orthonormalization.assets/20230914_1518329477.png)
**Proof of Theorem 21**![image.png](Orthonormalization.assets/20230914_1518342379.png)![image.png](Orthonormalization.assets/20230914_1518362133.png)

<a name="xbXKb"></a>
## How to Show Span Equivalency
<a name="pNL7R"></a>
### Method 1 - Set Equivalence
> ![image.png](Orthonormalization.assets/20230914_1518389541.png)

 

<a name="VM3G3"></a>
### Method 2 -  Induction
> **HW 10 Sp23 P1**
> ![image.png](Orthonormalization.assets/20230914_1518404995.png)![image.png](Orthonormalization.assets/20230914_1518423012.png)

**Proof Outline**![image.png](Orthonormalization.assets/20230914_1518444775.png)![image.png](Orthonormalization.assets/20230914_1518461559.png)


<a name="yHOOb"></a>
## How to Show Set Orthogonality
> 证明一个集合$\{\vec{v}_1,\vec{v}_2,\cdots, \vec{v}_n\}$中的向量互相正交(`Orthogonal Set`), 我们有两种方法。


<a name="dzl90"></a>
### Method 1 - Arbitrary Vector Pair
> 我们任取两个集合中的向量$\vec{v}_i,\vec{v}_j$, 证明$\vec{v}_i^{\top}\vec{v}_j=0$, 但是证明不具有递归性质。



<a name="TgbmF"></a>
### Method 2 - Induction
> **HW10 Sp23 P1**
> ![image.png](Orthonormalization.assets/20230914_1518484138.png)

**Proof Outline**![image.png](Orthonormalization.assets/20230914_1518503014.png)


<a name="kXuE1"></a>
## Applying the Algorithm
<a name="ZLs2k"></a>
### 标准正交基的存在性
> ![image.png](Orthonormalization.assets/20230914_1518517561.png)



<a name="imcCX"></a>
### 扩展标准正交基
> ![image.png](Orthonormalization.assets/20230914_1518547409.png)![image.png](Orthonormalization.assets/20230914_1518562412.png)

**Example**![image.png](Orthonormalization.assets/20230914_1518581685.png)![image.png](Orthonormalization.assets/20230914_1519004591.png)



<a name="GAkO8"></a>
## Example
> ![image.png](Orthonormalization.assets/20230914_1519035621.png)



<a name="OChZ9"></a>
# QR Decomposition
> ![image.png](Orthonormalization.assets/20230914_1519052342.png)![image.png](Orthonormalization.assets/20230914_1519076853.png)

**Proof of Theorem 25**![image.png](Orthonormalization.assets/20230914_1519082772.png)



<a name="MK68T"></a>
# Resources
> **Note 13 Sp22**
> **Disc09B Sp22**

