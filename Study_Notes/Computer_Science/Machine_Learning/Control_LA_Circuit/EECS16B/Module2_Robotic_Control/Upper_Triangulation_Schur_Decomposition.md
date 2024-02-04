# Overview
> ![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519105590.png)



<a name="yM9BZ"></a>
# Non-diagonalizable Matrix
> ![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519137737.png)![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519154275.png)




<a name="IdLBI"></a>
# Upper Triangular Matrices
<a name="LRkNH"></a>
## Upper Triangular Matrix
> ![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519177567.png)


<a name="fK3Wp"></a>
## Eigenvalues of Upper Triangular Matrices
> ![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519184566.png)

**Proof of Theorem 5**![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519207170.png)


<a name="Oypvo"></a>
## Characteristic Equations
> ![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519224462.png)



<a name="HF7bu"></a>
## Solving Upper Triangular System
> ![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519233152.png)![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519267924.png)




<a name="SlepR"></a>
# Schur Decomposition(舒尔分解)
<a name="Gi1Gq"></a>
## Existence of Eigen-pairs
> ![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519289394.png)


<a name="Pdw3T"></a>
## Existence of Real Schur Decomposition
> ![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519294366.png)![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519316157.png)

**Proof of Theorem 9 and Proof of Correctness for the Algorithm 10**![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519334139.png)![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519366835.png)![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519373172.png)![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519394130.png)![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519413921.png)![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519438237.png)


<a name="P0MlD"></a>
## Existence of Complex Schur Decomposition
> ![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519452422.png)![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519472336.png)![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519512439.png)

**Proof**
1. Base Case: 当$n=1$时，$T=A, U=[1],U^*=[1]$成立。
2. 假设$A\in \mathbb{C}^{n\times n}$有$n$个特征值(可能有相同的)$\lambda_1,\cdots, \lambda_n$。

因为特征对$(\lambda_1, \vec{q_1})$一定存在，所以令$Q=\begin{bmatrix} \vec{q}_1&\widetilde{Q}\end{bmatrix}\in \mathbb{C}^{n\times n}$(对$\vec{q}_1$使用`Gram-Schmidt`扩展到$\mathbb{C}^n$), 则我们有: <br />$\begin{aligned}Q^{*} A Q & =\left[\begin{array}{c}\vec{q}^{*} \\\widetilde{Q}^{*}\end{array}\right] A\left[\begin{array}{ll}\vec{q} & \widetilde{Q}\end{array}\right] \\& =\left[\begin{array}{ll}\vec{q}^{*} A \vec{q} & \vec{q}^{*} A \widetilde{Q} \\\widetilde{Q}^{*} A \vec{q} & \widetilde{Q}^{*} A \widetilde{Q}\end{array}\right] \\& =\left[\begin{array}{ll}\lambda_1 \vec{q}^{*} \vec{q} & \vec{q}^{*} A \widetilde{Q} \\\lambda_1 \widetilde{Q}^{*} \vec{q} & \widetilde{Q}^{*} A \widetilde{Q}\end{array}\right] .\end{aligned}$


<a name="voi73"></a>
## Upper Trigularization Procedures
[dis09A_sol.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1689503871740-e1e0fbcf-1de5-4792-b3c1-328eb349bf93.pdf)

<a name="GmZq3"></a>
### Key Ideas
> ![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519539759.png)![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519554975.png)![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519565124.png)




<a name="Vuchx"></a>
### Recursive Approach
> **Disc09A Sp22**
> ![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1519585585.png)



<a name="FNlZ0"></a>
### Iterative Approach
> ![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520005146.png)



<a name="W7gZr"></a>
### Example 1
> **HW09 Fa21**
> ![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520022606.png)
> 方法就是，我们可以先通过`Upper Trigularization Procedures`找到矩阵$U$，然后利用$U^TAU=T$找到上三角矩阵。
> 1. 找到矩阵$U$, 我们可以使用递归的方法，得到$U=\begin{bmatrix} \vec{v}_1&R_{3\times 2}\vec{v}_2&R_{3\times 2}\vec{v}_3\end{bmatrix}$
> 2. 使用$U^TAU=T$找到$T$。



<a name="VlRev"></a>
### Example 2
> **HW10 Sp23 P2**
> ![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520041713.png)

**Procedures**![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520061742.png)![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520078373.png)


<a name="t0uX7"></a>
## Solving Differential Equations
> **HW10 Sp23 P4**
> ![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520091279.png)

**When two eigenvalues coincide**![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520115724.png)
**When we don't have enough eigenvectors**![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520133920.png)
**Find Upper Triangular Matrix**![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520152777.png)![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520168106.png)![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520181786.png)![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520202383.png)![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520224896.png)
**Solve the Differential Equations**![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520237272.png)![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520257351.png)

<a name="IS13V"></a>
# Spectral Theorem
## For Real Matrices
> [!thm]
> ![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520274318.png)
> 其中$$V=\begin{bmatrix}  \vec{v}_1&\vec{v}_2&\cdots&\vec{v}_n\end{bmatrix}$$且$\vec{v}_{i}$是$A$的$i-th$ eigenvectors. 
> 本质上，我们可以通过舒尔分解来构建谱分解。

> [!proof]
> **Proof of Theorem 11 - Using Schur Decomposition**![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520299961.png)![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520318677.png)![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520321991.png)
**Proof of Theorem 11 - Using Induction - HW11 Sp23 P1**
**Simple proof of real eigenvalues**![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520347413.png)

<a name="jJmFu"></a>
## For Hermitian Matrices
> ![image.png](Upper_Triangulation_Schur_Decomposition.assets/20230914_1520361803.png)

**Poor of Theorem 11 - Hermitian Matrices**





# Resources
> **Note 15 Sp22**
> **Disc09A Sp22**

