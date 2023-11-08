# Overview
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934514170.png)


# Stability
## Definitions
### Boundedness
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934518545.png)
> - $\vec{z}_d:\mathbb{N}\to \mathbb{R}^k$的含义是: 我们通过`Indexing`操作(指定一个$i\in \mathbb{N}$)，得到的是在时间步$i$时的状态向量$\vec{z}_d[i]\in\mathbb{R}^k$
> - $\vec{z}_c:\mathbb{N}\to \mathbb{R}^k$的含义是: 我们通过`Indexing`操作(指定一个正的时间$t\in \mathbb{R_+}$)，得到的是在时刻$t$的状态向量$\vec{z}_c(t)\in\mathbb{R}^k$
> - $R_d$和$R_c$都是与时间无关的有限常数。
> - $\vec{z_d},\vec{z}_c$是有界的意思是说他们的`Norm`在所有的时间上都是有界的。换句话说，我们沿着`Discrete LTI/Continuous LTI Model`的`State Trajectory`($i\in [0, n]$, t$\in [0,t]$)走的话, 每一个时刻对应的`State`向量的`Norm`都得是有界的。
> - 对于实数向量来说，向量的模长就是每个向量元素的平方和。对于复数向量来说，向量的模长就是每个向量元素的模长的平方和。



### BIBO Stability
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934519319.png)


## Why we need Stability?
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934518683.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934515327.png)



# Asymptotic Stability
## Math Tools
### General Triangle Inequality
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934516306.png)



### Boundedness of Vector Sequences and Functions
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934518040.png)

> [!proof]
> **Proof of Lemma 17 Discrete Case**
> **<font color="#ff0000">(i):</font>** **$(\implies)$如果$\vec{u}_d$是有界的，则根据定义，$\|\vec{u}_d[i]\|\leq R_u,\forall i$, 即$\forall i,\exists R_u~s.t.~~\|\vec{u}_d[i]\|=\sqrt{|u_{d,1}[i]|^2+|u_{d,2}[i]|^2+\cdots+|u_{d,n}[i]|^2}\leq R_u$
> 所以$|u_{d,1}[i]|^2+|u_{d,2}[i]|^2+\cdots+|u_{d,n}[i]|^2\leq R_u^2$, 对于$u_{d,j}[i]$来说，假设$\exists j, s.t. \forall M\in \mathbb{R},|u_{d,j}[i]|>M$(即无界)，则$|u_{d,1}[i]|^2+|u_{d,2}[i]|^2+\cdots+|u_{d,n}[i]|^2\leq R_u^2$,不成立，所以$u_{d,j}[i]$is bounded for all i.
> $(\Longleftarrow)$如果$u_k$是有界的，则$\exists R_{u,i}\in \mathbb{R}, s.t. |u_k[i]|\leq R_{u,k},\forall k\in \{1,2,\cdots, m\},\forall i$。则$|u_{d,1}[i]|^2+|u_{d,2}[i]|^2+\cdots+|u_{d,n}[i]|^2\leq \sum_{k}R_{u,k}^2$, 即$\|\vec{u}[i]\|\leq \sum_{k}R_{u,k}^2$所以$\vec{u}$有界。
> <font color="#ff0000">(ii): </font>$(\implies)$如果$\vec{u}$是有界的，则根据$(i)$, $u_k$是有界的，令其为$R_k$, 即$|u_k[i]|\leq R_k,\forall i$。因为$C\vec{u}$有界等价于$(C\vec{u})_{k,:}$有界。而$(C\vec{u}[i])_{k,:}=C_{k,:}\vec{u}[i]=\sum_{j=1}^kc_{kj}u_{j[i]}\leq \sum_{j=1}^kc_{kj}R_{k}$, 证毕。
> $(\Longleftarrow)$如果$C\vec{u}$有界，则$(C\vec{u})_{k,:}$有界, 则利用$(i)$中的逻辑即可。
> **Proof of Lemma 17 Continuous Case**将上述证明中所有的求和符号都改成积分符号即可。



### Upper Triangularization
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934512442.png)



## Discrete Time Model
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934513631.png)



### Scalar Case
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934518407.png)

> [!proof]
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934527126.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934526538.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934525077.png)
> 上述证明中，当$|a|<1$, 如果$x[0]=0$, 则我们选择$u[k]=0,\forall k$即可让`System Unstable`, 但是如果$x[0]\neq 0$的取值, 则使得系统`unstable`的$u[i]$的构造需要变化一下，详见下面的例子:
> **Disc06B**
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934525133.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934523789.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934525468.png)





### Diagonalizable Matrix Case
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934523922.png)

> [!proof]
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934527652.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934527047.png)
🔔: $\vec{e}_j$表示只有第$j$项元素为$1$, 其余所有项元素为$0$的向量。


### Non-Diagonalizable Matrix Case
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934522088.png)

**Proof**![image.png](./Stability_Feedback_Control.assets/20230722_0934536704.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934535679.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934537328.png)
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934535270.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934531879.png)





### Stable Region
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934539978.png)


## Continuous Time Model
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934537785.png)

**Proof **![image.png](./Stability_Feedback_Control.assets/20230722_0934535693.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934537392.png)


### Scalar Case
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934544725.png)

**Proof**![image.png](./Stability_Feedback_Control.assets/20230722_0934548723.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934546119.png)

### Diagonalizable Matrix Case
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934545562.png)

**Proof**![image.png](./Stability_Feedback_Control.assets/20230722_0934541783.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934544886.png)

### Non-Diagonalizable Matrix Case
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934542460.png)

**Proof**![image.png](./Stability_Feedback_Control.assets/20230722_0934547966.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934546798.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934555278.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934559009.png)


### Stable Region
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934559568.png)



## Proof Idea
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934553214.png)


# Marginal Stability - Diagonalizable
## Definition
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934552282.png)


## Discrete Time Model
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934559897.png)

**Proof**![image.png](./Stability_Feedback_Control.assets/20230722_0934557745.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934557145.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934557290.png)
> 换句话说，就是如果$|\lambda_i|<1,\forall i$, 那么无论什么`Input`，模型永远是`Stable`的。但是如果$\lambda_k=1, k\in \mathbb{N}$, 则我们必须保证$(V^{-1}B)_{k,:}$也就是$V^{-1}B$的第$k$行是零向量, 那么模型才是稳定的，否则第$k$行的`Scalar Result`就是$z_k[i]=\lambda_k^iz_k[0]+\sum_{j=0}^{i-1}\lambda_k^{j}(V^{-1}B)_{k,:}\vec{u}[i-k-1]$, 此时我们取模得到:
> $\begin{aligned}|z_k[i]|&=|\lambda_k^iz_k[0]+\sum_{j=0}^{i-1}\lambda_k^{j}(V^{-1}B)_{k,:}\vec{u}[i-k-1]|\\&=|z_k[0]+\sum_{j=0}^{i-1}(V^{-1}B)_{k,:}\vec{u}[i-k-1]|\end{aligned}$
> 而$\lim_{i\to \infty} |z_k[i]| = \lim_{i\to \infty}|z_k[0]+\sum_{j=0}^{i-1}(V^{-1}B)_{k,:}\vec{u}[i-k-1]|$显然不是`Bounded`的。


## Continuous Time Model
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934564457.png)

**Proof**![image.png](./Stability_Feedback_Control.assets/20230722_0934563400.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934564108.png)



# Stability Sanity Check
## Discrete Time Model
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934564637.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934568391.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934565570.png)

**Example**![image.png](./Stability_Feedback_Control.assets/20230722_0934566275.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934565809.png)


## Continous Time Model
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934562134.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934577482.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934578915.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934576382.png)

**Example**![image.png](./Stability_Feedback_Control.assets/20230722_0934579452.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934576210.png)





# Feedback Control
## Open/Closed Loop System
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934577781.png)


## Discrete Time Case
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934575494.png)
> $F\vec{x}[i]$代表的就是$\vec{f}(\vec{x}[i])$，一个向量函数。
> $F$的形状是由$\vec{x}[i]$的维数和$\vec{u}[i]$的维数共同决定的。
> 假设我们的模型是$\vec{x}[i+1]=\begin{bmatrix} 1&1\\0&2\end{bmatrix}\vec{x}[i]+\begin{bmatrix} 0\\1\end{bmatrix}u[i]$, 此时$A=\begin{bmatrix} 1&1\\0&2\end{bmatrix}$, $B=\begin{bmatrix} 0\\1\end{bmatrix}$, $u[i]\in \mathbb{R}^1$, $\vec{x}[i]\in \mathbb{R}^2$, 所以$F\in \mathbb{R}^{1\times 2}=\begin{bmatrix} f_1&f_2\end{bmatrix}$。

**Proof**![image.png](./Stability_Feedback_Control.assets/20230722_0934576906.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934578216.png)
> 一般而言，我们会令$\vec{u}_{OL}[i]=\vec{0}$。


## Continuous Time Case
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934587518.png)
> 其中$F=B^{-1}(A_{CL}-A)$, 如果$B^{-1}$存在的话。

**Proof**![image.png](./Stability_Feedback_Control.assets/20230722_0934588085.png)一般而言，我们会令$\vec{u}_{OL}[i]=\vec{0}$。


## Choice of F
### Input with Noise
> **Disc07A Sp22 P1**
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934585624.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934581947.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934587876.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934586813.png)




### Eigenvalues' Choice
> **Disc07B P1 Sp22**
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934588369.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934588465.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934582281.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934588607.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934598198.png)



## Summary
> 对于一个离散系统$\vec{x}[i+1]=A\vec{x}[i]+B\vec{u}[i]$或者连续系统$\frac{d}{dt}\vec{x}(t)=A\vec{x}(t)+B\vec{u}(t)$来说，如果$A$有一些特征值$\lambda_k$(包括上三角化得到的)不满足`Stable`的条件，则我们可以对$\vec{u}[i]$做`Feedback Control`, 令$\vec{u}[i]=F\vec{x}[i]$, 此时我们可以得到一个新的系统:
> $\vec{x}[i+1]=(A+BF)\vec{x}[i]$或者$\frac{d}{dt}\vec{x}(t)=(A+BF)\vec{x}(t)$
> 令$A_{CL}=A+BF$, 我们定义了一个新的状态转移矩阵，我们期望通过改变$F$这个矩阵使得$A_{CL}$的特征值能够使得我们的系统稳定。
> 但是在某些情况下我们无论如何也无法找到这样的$F$,
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934598903.png)




# Stablizing the Model
## Algorithm
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934594883.png)![image.png](./Stability_Feedback_Control.assets/20230722_0934596904.png)



## Example
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934592832.png)



# Circuit Examples(Disc06B)
> **Disc06B Sp22**
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934598697.png)

**Solution**![image.png](./Stability_Feedback_Control.assets/20230722_0934597393.png)
> ![image.png](./Stability_Feedback_Control.assets/20230722_0934592291.png)

**(i) Derive Differential Equations**![image.png](./Stability_Feedback_Control.assets/20230722_0935006331.png)
**(ii) Solving Differential Equations**![image.png](./Stability_Feedback_Control.assets/20230722_0935009907.png)
**(iii) Stability Control**![image.png](./Stability_Feedback_Control.assets/20230722_0935002633.png)![image.png](./Stability_Feedback_Control.assets/20230722_0935006519.png)
> ![image.png](./Stability_Feedback_Control.assets/20230722_0935009539.png)

**Choice of Input Sequence**![image.png](./Stability_Feedback_Control.assets/20230722_0935004024.png)


# Resources
> **Note 11 Sp22**
> **Disc06B/07A Sp22**

