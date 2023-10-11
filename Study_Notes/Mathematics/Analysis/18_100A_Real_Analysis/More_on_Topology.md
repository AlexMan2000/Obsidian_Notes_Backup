# 1 Limit/Cluster Point(极限点)
## Definition
> 我们回顾一下`Neighbourhood`的概念: 对于$x\in \mathbb{R}$来说，$x$的$\epsilon-Neighborhood$是$U_{\epsilon}(x)=(x-\epsilon,x+\epsilon)$
> **而**`**Limit Point**`**的定义如下：**
> `Limit Point`是对于一个集合而言的，假设我们有一个集合$A\subset \mathbb{R}$, 则如果$\forall \epsilon>0, U_{\epsilon}(x)\cap A\backslash\{x\}\neq \emptyset$（$\forall \epsilon>0, U_{\epsilon}(x)\cap A$中至少有一个不同于$x$的元素）,  则$x$是$A$的一个`Limit Point`。
> **注意:**
> `**Limit Point**`**不一定要在**$A$**中**。我们可以考虑下面的数列$\{\frac{1}{n}\}_{i=1}^{\infty}$组成的集合$A=\{1,\frac{1}{2},\cdots ,\frac{1}{n}\}, n\to \infty$, 并证明$0$是这个数列的一个`Limit Point`。
> **证明:**
> 根据`Archemedian Property`, 我们知道$\forall \epsilon>0,\exist M_0\in \mathbb{N}, ~~s.t.~~ M_0\epsilon>1$, 即$\epsilon>\frac{1}{M_0}$, 同时因为$M_0>0$, 所以$\exist M_0\in \mathbb{N},~~s.t.~~0<\frac{1}{M_0}<\epsilon$, 即$\frac{1}{M_0}\in (0-\epsilon,0+\epsilon)=U_{\epsilon}(0)$。同时因为$\frac{1}{M_0}\in A$, 所以$U_{\epsilon}(0)\cap A\backslash \{0\}\neq \emptyset$, 所以$0$是$A$的一个`Limit Point`,且$0\notin A$。

**Examples****给定**$A=[1,3]\subset \mathbb{R}$

1. ** 问: **$2$**是否是一个**$A$**的**`**Limit Point**`**?**

$\forall \epsilon>0$, 我们可以分类讨论得到: $U_{\epsilon}(x)\cap A=\begin{cases}(2-\epsilon,2+\epsilon)&\epsilon\leq 1\\ [1,3]&\epsilon >1 \end{cases}$

   - 当$\epsilon\leq 1$时，$\exists 2+\frac{\epsilon}{2}\in (2-\epsilon,2+\epsilon)$且$2+\frac{\epsilon}{2}\neq 2$
   - 当$\epsilon> 1$时，$\exists t\in (2-\epsilon,2+\epsilon)$且$t\neq 2$
2. **问: **$1$**是否是一个**$A$**的**`**Limit Point**`**?**

$\forall \epsilon>0$, 我们可以分类讨论得到: $U_{\epsilon}(x)\cap A=\begin{cases}[1,1+\epsilon)&\epsilon\leq 2\\ [1,3]&\epsilon >2 \end{cases}$

   - 当$\epsilon\leq 2$时，$\exists 1+\frac{\epsilon}{2}\in [1,1+\epsilon)$且$1+\frac{\epsilon}{2}\neq 1$
   - 当$\epsilon> 2$时，$\exists t\in [1,3]$且$t\neq 2$

 

## Theorems
> 如果$x$是集合$A$的一个`Limit Point` $\iff$  **存在**一个数列(数列的元素全部来自于集合$A$, 即$\{a_n\}_{i=1}^n \subset A$), 满足$\lim_{n\to \infty} a_n=x$且$a_n\neq x, \forall n\in \mathbb{N}$。

**Proof**
1. ($\Longrightarrow$)

因为$x$是集合$A$的一个极限点，所以$\forall \epsilon>0, (x-\epsilon,x+\epsilon)\cap A\backslash \{x\}\neq \emptyset$, 换句话说，$\forall n\geq N, x\neq a_n\in (x-\frac{1}{n},x+\frac{1}{n})$, 而根据`Archimedian Property`我们知道, $\forall \epsilon>0, \exists N\in \mathbb{N}, ~~s.t.~~ N\epsilon>1$, 即$N>\frac{1}{\epsilon}$, 即$\frac{1}{N}<\frac{1}{\epsilon}$, 而$n\geq N$, 所以$\frac{1}{n}\leq \frac{1}{N}$，所以$a_n\in(x-\frac{1}{n},x+\frac{1}{n})\subset (x-\frac{1}{N},x+\frac{1}{N})\subset (x-\epsilon,x+\epsilon)$
所以综上，我们知道$\forall n\geq N, a_n\in (x-\epsilon, x+\epsilon)$, 于是$\lim_{n \to \infty}a_n=x$

2. ($\Longleftarrow$)

这个方向证明比较容易，因为首先$\lim_{n\to \infty} a_n=x$且$a_n\neq x, \forall n \in\mathbb{N}$所以$\forall \epsilon>0, \exists M_0\in \mathbb{N}, ~~s.t.~~\forall n\geq M_0, |a_n-x|<\epsilon$, 即$\exists a_n\in U_{\epsilon}(x)$。因为$\{a_n\}_{n=1}^{\infty}\subset A$且$a_n\neq x,\forall n\in \mathbb{N}$, 于是换句话说$U_{\epsilon}(x)\cap A\backslash\{x\}\neq\emptyset$, 证毕。

# 2 Isolated Point（孤立点）
## Definition
> **Definition:**
> An isolated point $x\in A$is a non-limit point of $A$。写的详细一点就是:
> $x\in \mathbb{R}$is an isolated point of $A$if $\exists \epsilon>0, U_{\epsilon}(x)\cap A\backslash\{x\}=\emptyset$,  因为$x\in A$, 所以这句话等价于$U_{\epsilon}(x)\cap A=\{x\}$。
> 而`Isolated Point`的定义就是`Limit Point`的`Negative Definition`。
> **注意点:**
> Isolated Point 一定在我们要研究的集合中

**Example****命题: 对于**$A=\{1,\frac{1}{2},\cdots\}$**集合来说，**$\forall n\in\mathbb{N}, \frac{1}{n}$**是**$A$**的孤立点。**
**证明: **$\forall n\in \mathbb{N}, \exists0<\epsilon<\frac{1}{n(n+1)}, s.t.~~U_{\epsilon}(\frac{1}{n(n+1)})=(\frac{1}{n}-\frac{1}{n(n+1)},\frac{1}{n}+\frac{1}{n(n+1)})\subset (\frac{1}{n+1},\frac{1}{n-1})$且因为$U_{\epsilon}(\frac{1}{n(n+1)})\cap A=\{\frac{1}{n}\}$**, 所以证毕。**

# 3 Closed Sets
## Point Definition
> 我们知道一个集合是`Closed Set`可以通过证明其补集是`Open Set`来验证。但是这种利用补集来证明的方式不是很`Self-contained`, 于是我们在下面给出一个不用依赖于补集就能判断`Closed Set`的方法。
> **定理:**
> $A\subset \mathbb{R}$is said to be closed if it contains **all of its limit points. **
> **说人话就是：**
> 如果$x$是$A$的一个`Limit Point`, 则$x$必定属于$A$, 我们也常常使用这个定义来证明集合是`Close`的

**Proof (Easy)**欲证明$A$是`Closed Set`, 则我们只要证明$A^c$是`Open Set`即可，现在假设$x\in A^c$, 所以$x\notin A$, 则因为$A$包括了自身所有的`Cluster Point`，所以$x\in A$意味着$x$不是$A$的`Cluster Point`所以$\exists \epsilon>0, ~~s.t.~~U_{\epsilon}(x)\cap A\backslash \{x\}= \emptyset$, 这等价于$U_{\epsilon}(x)\subset A^c$, 这意味着$A^c$是`Open set`, 即$A$是`Closed set`。
**Examples(Medium)****Claim: **$A=[b,c]$**is closed**
**想要证明这个结论，我们只要证明下面两个命题:**

1. $A$中的所有点都是$A$的`Limit Points`
2. 所有不属于$A$的点都不是$A$的`Limit Point`(因为一个集合的`Limit Point`可能不在集合内)

**我们先证明第一个命题:**
我们从`Limit Point`的角度来证明这个结论。我们分三类情况讨论:

   1. 证明$x=b$is limit point

$\forall \epsilon>0, U_{\epsilon}(b)\cap A=\begin{cases} [b,b+\epsilon)&\epsilon\leq c-b\\ [b,c]&e>c-b\end{cases}\backslash\{x\}\neq \emptyset$, 所以$b$是$A$的limit point.

   2. 证明$\forall x\in [b,c], x$is limit point 

$\forall \epsilon>0, U_{\epsilon}(x)\cap A=\begin{cases} (x-\epsilon,x+\epsilon)&0<\epsilon\leq min\{x-b,c-x\}\\ [b,x+\epsilon)~~or~~(x-\epsilon,c]&min\{x-b,c-x\}<\epsilon\leq max\{x-b,c-x\}\\ [b,c]&\epsilon> max\{x-b,c-x\}\end{cases}\backslash\{x\}$不为空, 所以$e$是$A$limit points.

   3. 证明$x=c$is limit point

$\forall \epsilon>0, U_{\epsilon}(c)\cap A=\begin{cases} (c-\epsilon,c)&\epsilon\leq c-b\\ [b,c]&\epsilon>c-b\end{cases}\backslash\{x\}\neq \emptyset$, 所以$c$是$A$的limit point.
综上，所有$A$中的点都是$A$的`Limit Points`，证毕。
**然后我们证明第二个命题:**

   1. $x<b$, $\exists 0<\epsilon<b-x$，不妨取$\epsilon=\frac{b-x}{2}$, 此时$U_{\epsilon}(x)=(x-\frac{b-x}{2},x+\frac{b-x}{2})\subset (x-\frac{b-x}{2},b)\cap A\backslash \{x\}=\emptyset$，所以$x$不是`Limit Point`
   2. $x>c$同理。

综上，证毕，所有$x\notin [b,c]$不是$[b,c]$的`Limit Point`
综上，我们证明了$[b,c]$是`Closed Set`。


## Theorem
> 下面我们证明为什么我们可以通过补集的开闭性来判断原集合的开闭性，这就要用到`Limit Point`的性质。
> 假设$A\subset \mathbb{R}$, 则:
> 1. $A$is open $\iff$$A^c$is closed.
> 2. $A$is closed $\iff$$A^c$is open.

**Proof of 1(Medium)**($\Longrightarrow$)
假设$A$是`Open`的，则$\forall x\in A,\exists \epsilon>0,~~s.t.~~(x-\epsilon,x+\epsilon)\subset A$, 也就是$U_{\epsilon}(x)\subset A$。现在我们要证明$\forall x$that is the limit point of $A^c$，$x\in A^c$。
**证明:**
因为$x$是$A^c$的`Limit Point`， 则$\forall \epsilon>0, U_{\epsilon}(x)\cap A^c\backslash\{x\}\neq \empty$, 也就是说$\exists y\in U_{\epsilon}(x)\cap A^c\backslash\{x\}$, 即$y\in U_{\epsilon}(x)\backslash \{x\}$and $y\in A^c$, 即$y\notin A$, 而这说明$U_{\epsilon}(x)\backslash\{x\}$中含有一个不属于$A$的元素。这直接表明$\forall \epsilon>0,U_{\epsilon}(x)\subsetneq A$。而如果此时$x\in A$, 则$\forall x\in A,\exists \epsilon>0,U_{\epsilon}(x)\subset A$，所以矛盾，于是$x\notin A$, 于是$x\in A^c$, 所以证毕。
($\Longleftarrow$)
假设$A^c$是`Closed Set`, 我们要证明如果$x\in A$, 则$\exists \epsilon>0, U_{\epsilon}(x)\subset A$(即$A$is open). 
**证明:**
对于$\forall x\in A$, 有$x\notin A^c$, 即$x$不是$A^c$的`Limit Point`, 所以$\forall x\in A$, 我们有:$\exists \epsilon>0, ~~s.t.~~U_{\epsilon}(x)\cap A^c\backslash\{x\}=\empty$。 这表明$U_{\epsilon}(x)\subset A$，即$A$是`Open`的。


# 4 Closure of a set
## Definition
> Suppose $A\subset \mathbb{R}$and $L=\{x\in \mathbb{R}|x~~is~~a ~~limit~~ point~~ of ~~A\}$, then the closure of $A$is $\bar{A}=A\cup L$。


## Theorem
> $\bar{A}$is the smallest closed set containing $A$。这也很容易理解，因为我们知道`Limit Point`有可能在集合$A$以外，而$L$恰好就捕捉到了所有的$A$的`Limit Point`, 而$A\cup L$就具有了`Closed Set`的性质，唯一值得我们关注的就是这个最小性。即，为什么$\bar{A}=A\cup L$ 就是最小的包括$A$的`Closed Set`? 下面我们将给出证明:

**Proof（Very Hard）**
1. 首先我们证明$L$是`Closed Set`(Hard)

根据定义，假设$x$是$L$的一个`Limit Point`, 所以$\forall \epsilon>0, \exists x\neq y\in U_{\frac{\epsilon}{2}}(x)\cap L$, 这意味着$y\in L$, 因为$L$集合内包含的元素都是$A$的`Limit Point`, 所以$y$是集合$A$的`Limit Point`。在此根据定义，我们知道$\exists y\neq z\in U_{\frac{\epsilon}{2}}(y)\cap A$, 也就是说$z$是$A$的`Limit Point`, 同时$z\in A$。
根据三角不等式: $|x-z|\leq |x-y+y-z| \leq |x-y|+|y-z|<\frac{\epsilon}{2}+\frac{\epsilon}{2}=\epsilon$
于是$z\in U_{\epsilon}(x)\cap A$。然后我们只要证明$x\neq z$就可以使得$x$是$A$的`Limit Point`, 然后根据 集合$L$的定义可知$x\in L$, 于是因为对于所有是$L$的`Limit Point`的$x$， 我们有$x\in L$, 所以$L$是`Closed`的。
下面我们证明为什么$x\neq z$: 因为$|y-z|<min(\frac{\epsilon}{2},|x-y|)$

2. 证明$\bar{A}$是`Closed Set`(Easy)

假设$x$是$\bar{A}$的一个`Limit Point`, 则$\forall \epsilon>0, \exists x\neq y\in U_{\epsilon}(x)\cap \bar{A}$
$\exists x\neq y\in U_{\epsilon}(x)\cap(A\cup L)$, $\exists x\neq y\in (U_{\epsilon}(x)\cap A)\cup (U_{\epsilon}(x)\cap L)$
Case 1: $x\neq y\in U_{\epsilon}(x)\cap A$
则$x$是$A$的`Limit Point`, 即$x\in L$, 所以$x\in \bar{A}$
Case 2: $x\neq y\in U_{\epsilon}(x)\cap L$
则$x\in L$, 所以$x\in \bar{A}$

3. 证明$\bar{A}$是`The Smallest`

假设 $B\subset \mathbb{R}$使得$\begin{cases} B~~is~~closed\\A\subset B\end{cases}$, 并且想要证明$\bar{A} \subset B$
假设$x\in \bar{A}$, 则因为$\bar{A}=A\cup L$, 所以:
Case 1: $x\in A$, 则$A\in B$
Case 2: $x\in L$, 则$x$是$A$的`Limit Point`, 于是$\forall \epsilon>0, \exists x\neq y,~~s.t.~~U_{\epsilon}(x)\cap A\subset U_{\epsilon}(x)\cap B$, 于是$x$是$B$的`Limit Point`，因为$B$是`Closed`, 所以$x\in B$, 于是$\forall x\in \bar{A}, x\in B$, 于是$\bar{A} \subset B$, 证毕。


# 5 Compact Set
## Definition
> We say $K\subset \mathbb{R}$is compact if for all sequences $\{a_n\}_{n=1}^{\infty}\subset K$, there is a subsequence $\{a_{n_k}\}_{k=1}^{\infty}, ~~s.t.~~\lim_{n\to \infty}a_{n_k}=L\in K$。
> 说人话就是: 如果$K$是`Compact Set`, 则对于$K$中的每个数列，都存在一个子数列收敛与$K$中的某个元素。




## Theorem
> $K \in \mathbb{R}$is compact $\iff$it is closed and bounded.

**Proof**

