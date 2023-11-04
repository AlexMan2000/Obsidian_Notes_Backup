[Vector Spaces.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1660655263179-996b6391-6856-4d60-bf1b-708797b19eb2.pdf)
:::success
本章节探究有限维的向量空间，线性代数主要研究的就是有限维的向量空间， 也就是不会研究例如$\bf F^{\infty}$这种无限维空间。$\bf F^n$就是我们要研究的主要空间($n$为正整数)
:::

# 1 线性组合和基
## 1.1 Linear Combination
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1149388504.png)
> 在矩阵视角中，我们常常将这些向量$\bf v_1,v_2,v_3,...,v_m$看成是某个矩阵的列向量, 这些列向量的线性组合构成了$\bf A=\begin{bmatrix} v_1&v_2&v_3&\cdots &v_m\end{bmatrix}$的列空间$\bf col(A)$

> **例如: 我们说**$(17,-4,2)$**是**$(2,1,-3)$**和**$(1,-2,4)$**的线性组合**
> - 在矩阵视角下, 意味着$(17,-4,2)$在矩阵$\bf A=\begin{bmatrix} 2&1\\1&-2\\-3&4\end{bmatrix}$的列空间中。
> - 在线性算子视角下，意味着线性方程组$\begin{cases} 2a+b=17\\a-2b=-4\\-3a+4b=2 \end{cases}$有解。



## 1.2 Span
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1149401134.png)
> 我们使用`Span`符号来表示一组向量的线性组合。数学家也常常使用`Linear Span`来描述和`Span`相同的含义。
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1149413828.png)



## 1.3 Span 的性质**⭐⭐⭐⭐⭐**
### Lemma 1
> ** If **$S\subseteq W$**(**$W$**is a subspace of **$V$**), then **$Span(S)\subseteq W$**。**
> **证明:** 令$|S|=n$(即$S$这个列表$\{\vec{s}_1,\cdots, \vec{s}_n\}$长度为$n$)，则$\forall \vec{s}\in Span(S)$, $\exists \vec{\alpha}\in \mathbf{F}^n,~~s.t.~~\vec{s}=\vec{a}^{\top}\vec{s}_i=\alpha_1\vec{s}_1+\cdots\alpha_n\vec{s}_n$, 因为$\vec{s}_i\in S\subseteq W$, 且$W$是子空间，所以$\alpha_i\vec{s}_i\in W$, 即所以$\vec{s}\in W$, 于是$Span(S)\subseteq W$。


### Lemma 2
> $Span(S)$is a subspace that contains $S$
> 这个结论很容易证明，读者自行证明。



### Lemma 3 - Subset Relationship
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1149417732.png)


### Theorem 2.7 - Version 1
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1149434991.png)

**证明是V的子空间**
1. 首先要证明`Span`张成的空间是一个$V$的子空间

因为对于`Span`张成的空间$S\subset V$, 我们只要证明$S$满足加法和数乘封闭性即可。
**加法封闭性:**
对于$\forall u,v\in S$, 我们有$u=a_1v_1+a_2v_2+\cdots+a_mv_m,v=b_1v_1+b_2v_2+\cdots+b_mv_m$
所以$u+v=a_1v_1+a_2v_2+\cdots+a_mv_m+b_1v_1+b_2v_2+\cdots+b_mv_m=(a_1+b_1)v_1+\cdots+(a_m+b_m)v_m$
因为$a_i,b_i\in \mathbf{F}$, 有$a_i+b_i\in \mathbf{F}$, 于是$(a_1+b_1)v_1+\cdots+(a_m+b_m)v_m \in S$
**数乘封闭性：**
$\forall u\in S$, $cu=c(a_1v_1+a_2v_2+\cdots+a_mv_m)=ca_1v_1+ca_2v_2+\cdots+ca_mv_m$
因为$\forall a_i\in \mathbf{F},ca_i\in \bf F$, 所以$ca_1v_1+ca_2v_2+\cdots+ca_mv_m\in S$
**非空性:**
因为$0=0v_1+v_2+\cdots+0v_m$, 所以$0\in S$
**证明是最小的V的子空间**
1. **先证明**`**Span**`**张成的子空间**$S$**包含了**$S$**中所有的向量(利用加法恒等元)**

因为$v_j=0v_1+0v_2+\cdots+1v_j+\cdots+0v_m$, 所以$S$包含了所有$S$中的向量

2. **再证明**`**Span**`**张成的子空间**$S$**是 所有包含了**$S$**中所有向量的子空间**$T$**中最小的那个子空间。 换句话说，有很多**$V$**的子空间**$\{T_1,T_2,\cdots ,T_n\}$**，他们都包含**$\{v_1,v_2,\cdots,v_m\}$**但是**$span(v_1,v_2,\cdots,v_m)$**代表的子空间**$S$**一定是最小的那个, 也就是**$|S|<|T_i|,\forall i$**, 我们下面来证明这个拗口的结论。**

首先, 对于子空间$T_i\subset V$, 因为他们对加法数乘都封闭，所以$\forall u,v \in T_i,au+bv\in T_i$, 所以$a_1v_1+a_2v_2+\cdots+a_mv_m \in T_i$但是$T_i$还可以继续扩展，因为$T_i$还含有$v_{m+1},\cdots$甚至无限多个向量, 而$S$中包含$m$个向量$a_1v_1+a_2v_2+\cdots+a_mv_m \in S$, 所以$S\subset T_i$, 所以$S$是最小的那个子空间
**图例**![](./Ch2_张成空间，维数和基.assets/20231103_1149442281.png)


### Theorem 2.7 - Version 2
> 这个结论很重要，需要认真对待。另一种表述
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1149458086.png)
> $\operatorname{span}(S) = \bigcap_{W \text { a subspace of } \mathrm{V},~S\subseteq W} W$

**Proof**![image.png](./Ch2_张成空间，维数和基.assets/20231103_1149478304.png)![image.png](./Ch2_张成空间，维数和基.assets/20231103_1149483215.png)



## 1.4 Spans
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1149505140.png)
> 说白了就是$v_1,...,v_m$通过线性组合能够得到$V$中的所有向量。
> 转化成矩阵语言就是$\bf \begin{bmatrix} v_1&v_2&\cdots&v_m\end{bmatrix}x=b$对于所有$\bf b\in V$都有解

> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1149515225.png)



# 2 向量空间
## 2.1 有限维向量空间
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1149523673.png)
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1149542710.png)
> $\mathcal{P}(\bf F)$是定义在$\bf F$上的向量空间，且为$\bf F^F$的子空间, 这里给出证明:

**Proof**> 对于$\mathcal{P}(\mathbf{F})=\{p(z)=a_0+a_1z+a_2z^2+\cdots +a_mz^m|a_i\in \mathbf{F},z\in \mathbf{F},p:\mathbf{F}\to \mathbf{F}\}$
> **先证明其非空性: **
> 取$a_i=0$, 则$p(z)=0\in \mathcal{P}(\mathbf{F})$
> **证明加法封闭性:**
> 任取$u,v\in \mathbf{F}$, $u=a_0+a_1z+a_2z^2+\cdots+a_mz^m,u=b_0+b_1z+b_2z^2+\cdots+b_mz^m$
> $u+v=(a_0+b_0)+(a_1+b_1)z+\cdots+(a_m+b_m)z^m$, 因为$a_i,b_i\in \mathbf{F}, \therefore a_i+b_i \in \mathbf{F}$, $\because z \in \mathbf{F}$ 所以$u+v\in \mathcal{P}(\mathbf{F})$
> **证明数乘封闭性:**
> 证明较为容易，此处省略。



## 2.2 Degree of Polynomial
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1149554226.png)
> 一般而言，如果一个多项式($\bf F\to F$)$p(z)=a_0+a_1z+\cdots+a_mz^m$能够同时被两组系数$a_0,a_1,\cdots,a_m$和$b_1,b_2,\cdots,b_m$表示，则一定有$a_i=b_i$, 即$p(z)=0\in \mathcal{P}(\mathbf{F})$(`additive identity`)。换句话说，一个多项式的系数被唯一的确定。于是就有了下面的定义:
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1149572517.png)
> **此处**$-\infty < m$**, 这里其实就开始渗透同构的概念了，说的就是一个多项式也能够看成一个向量空间，其向量空间的维数等于多项式的**`**最高次数+1**`

:::success
![image.png](./Ch2_张成空间，维数和基.assets/20231103_1149598057.png)
![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150004960.png)
:::

## 2.3 无限维向量空间
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150021307.png)
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150024042.png)
> $\mathcal{P}_m(\mathbf{F})$是有限维的，$\mathcal{P}(\mathbf{F})$是无限维的。





# 3 线性无关性
> 本小节主要讲述线性无关性，是线性算子视角理解线性代数的最核心的部分。

## 3.1 定义
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150039723.png)
> 对于定义中的第一条，从矩阵的视角就是$v_1,v_2,\cdots,v_m$按列组成的矩阵的零空间只有$\{0\}$


## 3.2 推论
> **另外，从这个定义出发我们可以得到如下推论:**
> **Corollary 2.17.1:**
> 如果$v_1,v_2,\cdots,v_m$**线性无关, 那么**$\forall v_j\in span(v_1,v_2,\cdots,v_m),v_j=a_1v_1+a_2v_2+\cdots+a_mv_m$**只有一种线性组合方式。**
> **证明如下：**
> 假设对于$v_j\in span(v_1,v_2,\cdots,v_m),v_j=a_1v_1+a_2v_2+\cdots+a_mv_m=b_1v_1+b_2v_2+\cdots+b_mv_m$
> 我们对后一个等式进行移项操作:
> $(a_1-b_1)v_1+(a_2-b_2)v_2+\cdots+(a_m-b_m)v_m=0$
> 根据我们的定义`2.17`，$a_i=b_i$, 所以只能有唯一的表示方式，这个推论很重要，后续证明会用到。
> 
> **Corollary 2.17.2:**
> **如果从线性无关的向量组**$v_1,v_2,\cdots,v_m$**中移除某些向量，则剩下的向量仍然线性无关。**
> 证明:
> 因为原来的向量线性无关，所以$a_1v_1+a_2v_2+\cdots+a_mv_m=0$当且仅当$a_1=a_2=\cdots =a_m=0$, 去掉任意一个向量后上述等式和成立条件仍然成立，也就是说剩下的向量任然线性无关。



## 3.3 线性无关的例子
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150055748.png)

**(a)****先证明正方向:**
对于$v\in \{v\}$, 如果$\{v\}$中的向量线性无关，则我们说$v$只能被唯一的表示成$v$的线性组合(`**Corollary 2.17**`)，也就是说只存在唯一的$a$使等式$(1-a)v=0$（$v=av$得到）成立, 所以$a=1$, 如果$v=0$，则$a$有无数种选择，与线性无关性矛盾，证毕。
**证明反方向:**
如果$\{v\}$中的向量线性相关，则$v$可以表示成$v$的多种线性组合，也就是$v=av$有无数解，所以$v=0$, 也就是原命题的逆否命题成立，证毕。
**(b)****正方向：**
考虑逆否命题, 如果存在两个向量$u,v$, 使得$u=cv,c\in \mathbf{F}$, 则使得$a(cv)+bv=0$成立的$(a,b)$有无数组, 不符合$u,v$线性无关的定义，所以$u,v$线性相关，逆否命题为真，证毕。
**反方向:**
考虑逆否命题，如果$u,v$线性相关，则$au+bv=0$有非零$(a,b)$数对, 假定$a\neq 0$, 则$u=-\frac{b}{a}v$ , 所以满足$u$是$v$的常熟倍，所以逆否命题成立，证毕。
**(c)**解如下线性方程组$\begin{cases} a=0\\b=0\\c=0\\\end{cases}$, 所以这个齐次方程组只有零解，故上述向量线性无关。
从矩阵视角来看，这个三个列向量组成的矩阵的零空间只有零向量，于是这三个向量线性无关。
**(d)**这个结论很显然，我们就不证明了。


# 4 线性相关性
## 4.1 线性相关的定义
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150077295.png)
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150087303.png)


## 4.2 推论
> **Corollary 2.19.1**
> **如果**$v_1,v_2,\cdots,v_m$**向量列表中的某个向量是其他向量的线性组合，则这个向量列表中的向量线性相关**
> **证明:**
> $v_j=a_1v_1+a_2v_2+\cdots+a_mv_m$, 所以$a_1v_1+\cdots-v_j+\cdots+a_mv_m=0$
> 所以找不到$a_1=a_2=\cdots=a_j=\cdots=a_m=0$成立的情况, 因为$v_j$的系数恒为$1$, 系数不全为零，根据线性相关性的定义，证毕。
> **Corollary 2.19.2**
> **如果向量列表中有零向量，则这个向量列表中的向量线性相关**
> **证明:**
> 简单说一下，零向量前面乘以任何系数都是零向量(向量空间基本性质), 所以肯定存在不全为零的系数使得$a_1v_1+...+a_j\cdot \mathbf{0}+\cdots+a_mv_m=0$成立, 因为$a_j$可以任意取值，系数不全为零，根据线性相关性的定义，证毕。


## 4.3 线性相关性引理
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150101910.png)
> $(b)$**说的是，如果一个向量列表**$v_1,v_2,\cdots,v_m$**是线性相关的， 则任意从中去掉一个向量，剩余的向量仍然能够张成原来的空间**
> 这个引理是为了证明后面的`4.4`中的定理。
> **边界情况:**
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150116664.png)

**Proof of (a)**![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150144796.png)
**Proof of (b)**![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150159239.png)
![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150175750.png)
代入$v_j$后，$u=c_1-\frac{a_1}{a_j}v_1+\cdots+(c_j-\frac{a_{j-1}}{a_j})v_{j-1}+a_{j+1}v_{j+1}+\cdots +a_mv_m$
$u$$\in$$span(v_1,\cdots,v_{j-1},v_{j+1},\cdots v_m)$, 所以删除$j^{th}$之后的向量列表$v_1,\cdots,v_{j-1},v_{j+1},\cdots,v_m$仍然能够张成原来$v_1,v_2,\cdots,v_m$能张成的空间的
 


## 4.4 无关组长度小于张成组长度
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150183906.png)
> 结论挺显然的，我们就不去深究了, 其实就是如果一些向量是线性相关且能张成有限维空间$\bf V$，则去掉一个向量也能张成这个空间。**本质就是**`**Spanning List**`**虽然张成了**$V$**，但不是最短的向量列表, 而**`**Linear Independent List**`**是最短的向量列表。**

**Proof**![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150199719.png)
**Step 1**![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150214291.png)
**Step j**![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150237134.png)
每次在增加了$u$的时候(比如我们刚刚增加了$u_t$的时候)，得到了如下长度为$n+1$的向量列表$u_1,u_2,\cdots,u_t,w_1,w_2,\cdots, w_{n-t},w_{n-t+1}$，此时向量列表长度为$n+1$, 一定是线性相关且能`Span`$\bf V$空间的(引理告诉我们的)，马上下一步我们就要划掉$w_{n-t+1}$, 因为引理告诉我们如果一个向量列表线性相关，则划掉一个不会影响划掉以后剩余向量所能张成的空间的。如果划掉的是$u$中的某一个了，则说明我们划掉前的向量就已经线性无关了，矛盾，所以划掉的永远是$w$中的一个。于是$w$一定比$u$多。


## 4.5 使用4.4的一些例子
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150258621.png)
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150264262.png)


## 4.6 有限维子空间的定义
> 我们给出一个常用命题
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150271344.png)

**Proof**![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150281493.png)


# 5 基
## 基的定义
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150298480.png)![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150309096.png)
> 基就是能够张成$V$空间的线性无关的**向量列表**。

**Examples**![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150326330.png)





## 基的判断条件
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150348085.png)
> **如果一个向量列表想要成为**$V$**的基:**
> - 他必须张成$V$
> - 向量列表中的向量还要**线性无关**。

**Proof（类似于线性无关的定义）**[证明类似于线性无关性](https://www.yuque.com/alexman/so5y8g/atgxkz/edit#rFstW)
![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150367944.png)



## 基的常用性质
### Useful Lemma⭐⭐⭐
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150368659.png)

**Proof**![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150371802.png)![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150391144.png)


### Spanning List 可以缩减为基
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150414654.png)
> 证明思路就是我们先找一组向量能够`Span`这个`Vector Space`, 然后一点一点删除多余的向量最后得到这个`Vector Space`的一组基。
> 这个就对应了`EECS16B`中的`Gram-Schmidt`过程。

**Proof**![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150426277.png)
**Step 1**![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150446691.png)
**Step j**![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150458672.png)

### 有限维向量空间一定有基
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150464991.png)
> **每个有限维空间一定有其张成向量组**, 则根据`5.3`中的定理，这个向量组可以被化简成一组基，所以每个有限维空间一定有其基。

**Proof**![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150473865.png)

### 线性无关组可以扩充成一个基
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150488187.png)
> 一个向量列表中的向量光线性无关还不够，他们必须能够张成$V$, 所以可以被扩充到恰好能张成$V$，扩张过度就会变成线性相关列了。
> 本质就是我先从$\bf V$中找一组线性无关的向量$u_1,\cdots, u_m$，然后找一组$\bf V$的基$w_1,\cdots,w_n$, 把这两个列表合并成一个大列表，$u_1,\cdots, u_m, w_1,\cdots,w_n$, 这个大列表一定能够`Span`$\bf V$, 然后从这个列表中开始删除多余的向量最后得到一组基。

**Proof**![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150517048.png)


## 子空间和直和
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150514299.png)

**Proof**![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150541234.png)

 
# 6 维数
## 维数的定义
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150541859.png)![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150553557.png)![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150558043.png)




## 维数和基的性质
### 同一个向量空间的基长度相同
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150555035.png)![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150563349.png)
> 一个有限维向量空间的基长度一定相等。

**Proof**![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150578945.png)


### 向量列表的长度限制
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150572554.png)
> **证明可以使用下列引理:**
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150579790.png)

**Proof of 1**因为$dim(V)=n$, 所以$V$有一个长度为$n$的`Basis`, 不妨令其为$(v_1,v_2,\cdots,v_n)$, 令$x_1,x_2,\cdots, x_k\in Span(v_1,v_2,\cdots, v_n)$, 根据引理可知如果$x_1,\cdots x_k$是线性无关的，则$k\leq n$。因为否则($k>n$)就是线性相关的了。
**Proof of 2**因为$dim(V)=n$, 所以我们考虑$V$的一组基$v_1,\cdots, v_n$。因为$Span(x_1,\cdots, x_k)=V$,$v_1,v_2,\cdots, v_n\in Span(x_1,\cdots, x_k)$。因为$(v_1,v_2,\cdots, v_n)$线性无关，所以根据引理$n\leq k$。


### 长度正好的向量列表是基⭐⭐⭐
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150572105.png)
> **为了证明这个结论，我们需要先证明下列三个引理:**
> **引理1:**
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150577706.png)![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150574040.png)![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150589098.png)
> **引理2:**
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150589224.png)
> 1. $\forall x\in Span(x_2,\cdots, x_k)$, 我们有$x=\alpha_2x_2+\cdots+\alpha_kx_k=0x_1+\alpha_2x_2+\cdots+\alpha_kx_k\in Span(x_1,\cdots, x_k)$。
> 
所以$Span(x_2,\cdots, x_k)\subseteq Span(x_1,\cdots, x_k)$
> 2. $\forall x\in Span(x_1,\cdots, x_k)$, 我们有$x=\alpha_1x_1+\alpha_2x_2+\cdots+\alpha_kx_k$, 因为$x_1\in Span(x_2,\cdots, _k)$, 所以$x_1=\beta_2x_2+\cdots +\beta_nx_n$, 带入上式得到$x=(\alpha_2+\alpha_1\beta_2)x_2+\cdots+(\alpha_k+\alpha_1\beta_k)x_k\in Span(x_2,\cdots, x_k)\in Span(x_2,\cdots, x_k)$, 于是$Span(x_1,\cdots, x_k)\subseteq Span(x_2,\cdots, x_k)$。
> 
综上，$Span(x_1,\cdots, x_k)= Span(x_2,\cdots, x_k)$
> **引理3:**
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150581129.png)
> 因为$v_1,\cdots, v_k$是线性无关的，所以$\alpha_1v_1+\cdots\alpha_kv_k=0$仅在$\alpha_1=\alpha_2=\cdots=\alpha_k=0$时成立。
> 假设$(v_1,\cdots, v_k,x)$线性相关，则存在使得$\beta_1v_1+\beta_2v_2+\cdots \beta_kv_k+\beta_{k+1}x=0$成立的不全为零（即$(\beta_1,\cdots,\beta_{k+1})\neq \vec{0}$)的系数。
> 如果$\beta_{k+1}\neq 0$, 则$x=\frac{\beta_1}{\beta_{k+1}}v_1+\frac{\beta_2}{\beta_{k+1}}v_2+\cdots+\frac{\beta_k}{\beta_{k+1}}v_k\in Span(v_1,\cdots, v_k)$矛盾。
> 如果$\exists \beta_i\neq 0, i=1,2,\cdots, k$且$\beta_{k+1}=0$, 则$v_i=\frac{\beta_1}{\beta_{i}}v_1+\cdots+\frac{\beta_{i-1}}{\beta_{i}}v_{i-1}+\cdots+\frac{\beta_{i+1}}{\beta_{i}}v_{i+1}+\cdots+\frac{\beta_k}{\beta_{i}}v_k$, 这和$v_i$线性无关矛盾。
> 所以综上，$(v_1,\cdots, v_k,x)$线性无关。

**Proof of 1**![image.png](./Ch2_张成空间，维数和基.assets/20231103_1150598515.png)
![image.png](./Ch2_张成空间，维数和基.assets/20231103_1151001856.png)
**Proof of 2**![image.png](./Ch2_张成空间，维数和基.assets/20231103_1151023257.png)
![image.png](./Ch2_张成空间，维数和基.assets/20231103_1151037656.png)![image.png](./Ch2_张成空间，维数和基.assets/20231103_1151046491.png)



## 维数和子空间
### 子空间的维数(不等/等式关系)
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1151046098.png)![image.png](./Ch2_张成空间，维数和基.assets/20231103_1151055133.png)

**Proof****先证明第一部分：**
我们可以利用`Proposition 3.1`进行证明, 每个不等式使用一次。因为$dim(U)=a$, 所以$U$存在一组基$\{u_1,u_2,\cdots, u_a\}$, 同理$V$存在一组基$\{v_1,v_2,\cdots, v_b\}$。
因为$\forall u_i, u_i\in U\subset V$, 即$u_1,u_2,\cdots, u_a\in V$。因为$u_i$线性无关，所以根据`proposition 3.1`, $a\leq b$, 即$dim(U)\leq dim(V)$。
同理可证明第二个不等式。
**证明第二部分：**
如果$dim(U)=dim(V)$, 说明$dim(U)\leq dim(V)$和$dim(U)\geq dim(V)$同时成立。也就是说$u_1,u_2,\cdots, u_a$即线性无关，又是$V$的`Spanning List`, 于是$\{u_1,\cdots ,u_a\}$也构成$V$的基。因为同一个字空间的基长度相同，所以$a=b$。证毕。

### 不等关系
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1151057612.png)





### 子空间的和的维数(等式关系)
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1151051029.png)

**Proof**![image.png](./Ch2_张成空间，维数和基.assets/20231103_1151065366.png)


## 算例
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1151083099.png)

> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1151087425.png)

**Proof**![image.png](./Ch2_张成空间，维数和基.assets/20231103_1151094301.png)




# 7 总结
## 7.0 前言
> 前两章出现了非常多的定理，推论和引理，我们在此构建一个逻辑链条帮助理解。
> 首先我们针对集合定义了`Field`(域)的概念，**如果一个集合满足加法和数乘封闭性，则这个集合称为**`**Field**`**(复数集合称为**`**Field of Complex Number**`**)**。`Field`具有诸如`Additive Inverse, additive identity, distributive Law`等代数性质。
> 然后我们给了`Field`一个数学记号$\bf F$表示实数域$\mathbb{R}$和复数域$\mathbb{C}$的并集，并以此为基础建立了诸如$\bf F^S,F^n$等不同的高维集合。集合内部的元素较为特殊，有向量有函数，也可以是任何东西，如果这些集合恰巧同时满足了加法和数乘封闭性，则这些集合成为域或者空间。
> 线性代数研究的主体是$\bf F^n$(有限维向量空间)。同样，向量空间需要满足加法和数乘的封闭性。对于一个向量空间，他和`Field`一样，也有`Additive Inverse, Additive Identity`之类的运算性质，这些性质全都是由加法和数乘封闭性推导出来的。
> 之后我们定义了子空间的概念，子空间其实就是一个向量空间的子集，且满足加法数乘封闭性。然后我们开始探究子空间之间的关系, 定义了子空间的和$U+W$以及子空间的直和$U\oplus W$。线性代数的故事便从这里开始。


## 7.1 Sum of subspaces
> 对于$U_1,U_2,...U_m$这$m$个$V$的子空间，子空间的和定义为$U_1+U_2+...+U_m=\{u_1+u_2+...+u_m|u_j\in U_j,j\in \bf F\}$ , 意思就是我从每个子空间中随便拿一个向量出来，把他们加起来，得到的新的向量组成的集合。
> **1.39 Lemma 1 那么一个很自然的想法是，这个集合**$U=U_1+U_2+...+U_m$**是不是一个子空间?**
> 首先$0$向量肯定在$U$里面，因为$u_j$全部取零就行。
> 他满不满足加法封闭呢? 取两个元素$u,v\in U$, 首先$u$可以表示成$u=a_1+a_2+a_3+...+a_m,a_j\in U_j$, $v=b_1+b_2+...+b_m,b_j\in U_j$， 所以$u+v=(a_1+b_1)+(a_2+b_2)+...+(a_m+b_m)$, $a_j+b_j$是否属于$U_j$呢？答案也是肯定的，因为$U_j$本身是子空间满足加法封闭性，所以$a_j+b_j\in U_j$。数乘呢？不说了肯定满足。所以`Directed Sum`是子空间。
> 
> **1.39 Lemma 2 这个新的集合**$U_1+U_2+...+U_m$**一定包含了原来每一个**$U_j$**中的所有元素，为什么呢? **
> 其实我如果只盯着一个集合$U_t$中取非零向量，其他集合都取零向量，那么我取遍$U_t$中的向量的时候，$U_1,U_2,...,U_{t-1},U_{t+1},...,U_m$中都取零向量，得到的集合不就是$U_t$本身吗。对每个集合都这么来，那么这些子空间的和一定会包含原来子空间内的所有向量。
> 
> [**1.39**](https://www.yuque.com/alexman/so5y8g/wal3n1#Vxeyk)** **紧接着我们想$U=U_1+U_2+...+U_m$这个家伙和原来的$U_j$之间存在怎样的关系。根据**1.39 Lemma**我们知道这个集合包含了原来所有$U_j$内的所有向量，那么有没有比这个集合更小的集合能够恰好包含我们原来的所有向量呢？
> 答案就是$U$本身。论证的思路也很简单，我们先要找到所有和$U$一样，能够包含所有$U_j$中的向量的集合$T_i$，然后说明这样的每个$T_i$都必须包含我们的$U$, 这样就能说明$U$是满足条件的最小集合了。
> ![image.png](./Ch2_张成空间，维数和基.assets/20231103_1151122384.png)
> 注意到所有包含$U_1,U_2,...,U_m$的子空间$T_i$必须包含$U_1+U_2+U_3+...+U_m$(这是因为加法封闭性), 于是$U$是最小的那个。
> **对于**`**Directed Sum**`**的一个很好的类比就是集合的并集，包含两个集合**$U_1,U_2$**的所有元素的最小集合就是**$U_1\cup U_2$

** **

## 7.2 Directed Sum
> 接下来我们到了`Directed Sum`的定义:
> `Direct Sum`在`Sum of subspaces`的基础上做了一定的限制，使得我们在从不同的子空间中取元素加和的时候不能像`Sums of subspaces`那样自由散漫了(自由散漫指的是我们可以从$U_j$中任取元素)。
> [**1.40 定义**](https://www.yuque.com/alexman/so5y8g/wal3n1#pJimY)`**Directed Sum**`**的限制在于，我们从不同的子空间中取出的元素之和为任意**$\bf b$**时只有一种取法。**
> **这其实就是线性方程组**$\bf Ax=b$**只有唯一解或者**$\bf Ax=0$**只有零解的条件。其中**$\bf A$**就是将子空间**$U_i$**的基向量取出来按列组成的矩阵，且 **$\bf b$**在**$\bf A$**的列空间中(否则无解了)。**
> 

> [**1.44**](https://www.yuque.com/alexman/so5y8g/wal3n1#FCZA1)** 由这个1.40的性质，我们给出了一个定理，就是和是直和当且仅当**$u_1+u_2+...+u_m=0$**时**$u_1=u_2=...=u_m=0$
> 紧接着我们给出了证明, 证明思路首先当且仅当需要双向证明，然后对于反方向我们有, 
> 就是利用直和的性质，对于$v\in U_1+U_2+...+U_m$来说， $v$只能写成$u_1+u_2+...+u_m$唯一一种表达形式。



## 7.3 Span
> `Span`的概念和`Sum of subspaces`很像：
> 假设我们有一堆向量，那么`Span of these vectors`就是包含这些向量的最小的子空间。比如我们有$(v_1,v_2\cdots,v_n)$这$n$个向量`Spans`了向量空间$V$, 则$v_i$能够表示成$v_1,v_2,\cdots,v_n$的线性组合。因为$(v_1,v_2\cdots,v_n)$包含了所有$v_i$


## 7.4 线性无关性
> [2.17](https://www.yuque.com/alexman/so5y8g/atgxkz/edit#rFstW)说的是使$a_1v_1+a_2v_2+\cdots+a_nv_n=0$的系数组合只有$a_1=a_2=\cdots =a_n=0$
> =>推出任何在$span(v_1,v_2,\cdots,v_n)$中的向量$u=a_1v_1+\cdots+a_nv_n$只有一种系数组合
> =>如果$v_1,\cdots v_n$线性无关，则我随便拿掉一个$v_j$,剩下的向量仍然线性无关。


## 7.5 线性相关性
