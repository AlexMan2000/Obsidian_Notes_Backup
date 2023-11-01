# Convexity of Functions
## Miscellaneous Definitions
### Definition 1: Inequality
> [!def] Definition1 : Jensen's Inequality
> ![](Convex_Functions.assets/image-20231101091313319.png)![](Convex_Functions.assets/image-20231101091321286.png)


### Definition 2: Restricted to a line
> [!def]
   ![image.png](Convex_Functions.assets/20231023_2246109067.png)
> 
> 这个情况说的是，如果一个函数$g(t)$定义为$f$沿着$\forall \vec{v}$的方向的取值，且$g$为凸函数，则$f$为凸函数。几何上来说，如果$f$以$\vec{x}$为起点，如果其向着任意方向定义的函数$g(t)$都是凸函数的话，则$f$为凸函数。
> ![image.png](Convex_Functions.assets/20231023_2246128604.png)


### Defintion 3: First Order Condition
> [!def] First Order Condition
> ![](Convex_Functions.assets/image-20231101091447280.png)
> 在$\mathbb{R}^3$定义域中，这个条件可以想象成函数的图像总是在其定义域中的任意一点的切平面之上。
> **Implications: If **$\nabla f(\vec{x}_*)=0$** and  **$f$**  is convex and differentiable, then **$\vec{x}_*$**  is a global minimum.**
> **Proof:** Since $f$ is convex, then $\forall \vec{y}\in dom(f)$, we have $f(\vec{y})\geq f(\vec{x}_*)+0$, which directly implies that $\vec{x}_*$is the global minimum.

> [!proof]
> ![](Convex_Functions.assets/image-20231101091541333.png)



### Defintion 4: Second Order Condition
> [!def] Second Order Condition
> ![](Convex_Functions.assets/image-20231101091518411.png)![](Convex_Functions.assets/image-20231101095409365.png)

> [!example]
> ![image.png](Convex_Functions.assets/20231023_2246106208.png)![image.png](Convex_Functions.assets/20231023_2246102904.png)



## Extended Value Extensions
### Definition
> [!def]
> 
> ![](Convex_Functions.assets/image-20231101083304682.png)
> 这样的定义方法保证了，如果$f$ 是凸函数，则$\tilde{f}$ 也是凸函数，而且是扩展了定义域之后的凸函数。
> 读者可能会想，为什么我们要在$x\notin dom(f)$的时候取正无穷，本质上是因为如果不取正无穷，$\tilde{f}$ 就不一定能保持凸性了。

> [!important]
> ![](Convex_Functions.assets/image-20231101084605534.png)
> 设想一下，如果我们定义$\tilde{f}(x)=\begin{cases} f(x)& x\in dom(f)\\300&x\notin dom(f)\end{cases}$,  我们很容易找到一个反例使得$f(\theta x+(1-\theta)y)> \theta f(x)+(1-\theta)f(y)$。所以当$x\in dom(f)$时，我们要尽可能取大一点的数，或者说是很大的数，那么正无穷就是首选，因为正无穷加上任何数都还是正无穷。


### Indicator Function 
> [!def]
> ![](Convex_Functions.assets/image-20231101084742813.png)![](Convex_Functions.assets/image-20231101084749028.png)


## Sub/Super-Level Set
> [!def] Definition
> ![image.png](Convex_Functions.assets/20231023_2245513924.png)
> **总结一下:**
> 1. A convex function's sublevel set is convex, and the converse is not true.
> 2. A concave function's superlevel set is convex, and the converse is not true.
> 
![image.png](Convex_Functions.assets/20231023_2245531802.png)




## Epi/Hypo-graph of Functions
> [!def]
> ![image.png](Convex_Functions.assets/20231023_2245548465.png)![image.png](Convex_Functions.assets/20231023_2245568651.png)
> 证明一个函数是否是凸函数的一个重要的方法是证明其`Epigraph`is convex set. 这个性质使得我们能可以在`Convex Function`和`Convex Set`之间互相转化。
> **总的来说:**
> 1. `Convex Function <=> Epigraph is Convex Set`.
> 2. `Concave Function <=>  Hypograph is Convex Set`.

> [!example] Matrix Fractional Function
> ![image.png](Convex_Functions.assets/20231023_2245588951.png)


## Some common convex functions
### Quadratic Functions
> [!important] 
> ![](Convex_Functions.assets/image-20231101095533452.png)
> 二次函数是为数不多的，$\nabla^{2}f(\vec{x})\succ0\iff f~is~stritly~convex$ 的例子。



### Functions on R
> [!example] Examples
> ![image.png](Convex_Functions.assets/20231023_2245592268.png)![image.png](Convex_Functions.assets/20231023_2246006779.png)
> 1. **Exponential: **$(e^{ax})''=a^2e^{ax}\geq 0,\forall x\in dom(f)$
> 2. **Powers:** $(x^a)''=a(a-1)x^{a-2}$, 于是当$a(a-1)\leq 0$时，$(x^a)''\leq 0$-> Concave，否则$(x^a)''\geq 0$-> Convex
> 3. **Powers of absolute value:** 
>    1. 首先注意到，如果$p<0$, 则 $dom(f)$ 不是凸集，当$p=1$时，函数不可微，但是可以使用`Definition 1/2`判断其凸性。当$p=0$时，函数是常值函数，此时函数既是凸函数又是凹函数。当$0<p<1$时，函数既不是凸函数又不是凹函数。
>    2. 当$p\geq 2$时，函数处处二阶可微，所以我们可以用二阶条件判断凸性。
> 	   1. $\forall x>0, (|x|^p)''=p(p-1)x^{p-2}$, when $p> 1$, we have $p(p-1)x^{p-2}\geq 0$
> 	   2. $\forall x<0$, $(|x|^p)''=((-x)^p)^{''}=p(p-1)(-x)^{p-2}$, which is the same as above.
> 	   3. The $x=0$ case is just trivial, since the second derivative is 0.
> 	3. 当$1< p< 2$时，函数在`0`处不是二阶可微的，所以我们只能用一阶条件判断凸性: 我们有$f'(x)=sign(x)|x|^{p-1}$, 这是严格单调递增的，所以$f$是凸函数。
> 
> 4. **Logarithm:** $(logx)''=-\frac{1}{x^2}<0,\forall x\in dom(f)$
> 5. **Negative Entropy:** $(xlogx)''=\frac{1}{x}>0,\forall x\in \mathbb{R}_{+}$or $\forall x\in \mathbb{R}_{++}$



### Functions on R^n
> [!example] Examples
> ![image.png](Convex_Functions.assets/20231023_2246025766.png)![image.png](Convex_Functions.assets/20231023_2246036586.png)
> 1. **Norm:** $\|\theta x+(1-\theta)y\|_p\leq \theta \|x\|_p+(1-\theta) \|y\|_p$ by triangle inequality and homogenity. 这里$p>0$，因为当$p=0$时$\|x\|_0$表示零范数，而零范数不是范数，因为不满足`homogenity`。
> 2. **Max Function: **
>    1. **Prove by Definition:** $\theta \vec{x_i} + (1-\theta)\vec{y_i}\leq \theta \max(\vec{x})+(1-\theta)\max(\vec{y}),\forall i=1,2,\cdots, n$, 所以$\max(\theta \vec{x}+(1-\theta)\vec{y})\leq \theta \max(\vec{x})+(1-\theta)\max(\vec{y})$
>    2. **Prove by Epigragh:  Define **$f(\vec{x})=\max\{f_1(\vec{x}),f_2(\vec{x},\cdots, f_n(\vec{x}))\}$where **$f_i(\vec{x})=x_i$**, then:
> $\begin{aligned}epi(f)&=\{(\vec{x},t)~~|~~\vec{x}\in dom(f),f(\vec{x})\leq t\}\\&=\{(\vec{x},t)~~|~~\vec{x}\in \bigcap_{i=1}^n dom(f_i),f_1(\vec{x}),\cdots, f_n(\vec{x})\leq t\}\\&=\bigcap_{i=1}^n\{(\vec{x},t)~~|~~\vec{x}\in dom(f_i),f_i(\vec{x})\leq t\}\\&=\bigcap_{i=1}^n epi(f_i)\end{aligned}$, since $f_i(\vec{x})$'s are all affine functions, which are guaranteed to be convex, thus we have $epi(f_i)$'s are convex set, and that $epi(f)$is convex.
> 3. **Quadratic Over Linear Function:** 
> ![image.png](Convex_Functions.assets/20231023_2246053673.png)
> The last inequality comes from a very important property of dyad matrix $\vec{u}\vec{v}^{\top}$where if $\vec{u}=\vec{v}$, we have $\vec{v}\vec{v}^{\top}$is convex.
> 4. **Log-Sum-Exp: **
> 	这个函数是一个解析函数，性质较好，同时解析函数就是无穷可导的函数。
> - 当$i\neq j$时，$\frac{\partial ^2f}{\partial x_ix_j}=\frac{-e^{x_i}e^{x_j}}{(e^{x_1}+e^{x_2}+\cdots+e^{x_n})^2}$
> - 当$i= j$时，$\frac{\partial ^2f}{\partial x_i^2}=\frac{-e^{x_i}e^{x_i}+e^{x_i}(e^{x_1}+\cdots+e^{x_n})}{(e^{x_1}+e^{x_2}+\cdots+e^{x_n})^2}$
> ![image.png](Convex_Functions.assets/20231023_2246063791.png)
> 5. **Geometric Mean:**
> ![image.png](Convex_Functions.assets/20231023_2246086478.png)
> 其中，$\begin{aligned}\frac{\partial^2 f(x)}{\partial x_k\partial x_l}&=\frac{1}{n}(\frac{1}{n}-1)(\prod_{i=1}^n x_i)^{\frac{1}{n}-2}(\prod_{j\neq k}x_j)(\prod_{i\neq k,l}x_i)+\frac{1}{n}(\prod_{i=1}^n x_i)^{\frac{1}{n}-1}(\prod_{i\neq k,l}x_i)\\&=\frac{(\prod_{i=1}^nx_i)^{\frac{1}{n}}}{n^2x_kx_l}\end{aligned}$
> 6. **Log-Determinant:**
> ![image.png](Convex_Functions.assets/20231023_2246104253.png)
> **推导中使用到了几个重要的性质：**
> 	1. $det(ABC)=det(A)det(B)det(C)$
> 	2. If $Z\in \mathbf{S}_{++}$, then $Z^{-\frac{1}{2}}$exists.
> 	3. **Eigenshift Rules**: If the eigenvalues for $\mathbf{A}$ are $\sigma_i(\mathbf{A})$ then the eigenvalues for $\mathbf{A}+\lambda I$are $\sigma_i(\mathbf{A})+1$。




# Operations Preserving Convexity
## Affine Mapping
### Affine Function
> [!def]
> 对于$f:\mathbb{R}^n\to \mathbb{R}$来说，我们有$f(\vec{x})=A\vec{x}+\vec{b}$ is convex.
> Proof by ZOC:
> 首先$dom(f)=\mathbb{R}^n$, 这肯定是一个`Convex Set`，其次$\forall\vec{x},\vec{y}\in dom(f),\theta\in [0,1]$, 我们有$f(\theta\vec{x}+(1-\theta)\vec{y})=A(\theta\vec{x}+(1-\theta)\vec{y})=\theta (A\vec{x}+\vec{b})+(1-\theta)(A\vec{y}+\vec{b})=\theta f(\vec{x})+(1-\theta)f(\vec{y})$
> 所以$f$is convex.


### Affine Composition
> [!def]
> ![image.png](Convex_Functions.assets/20231023_2246129018.png)
> **Proof:**
> If f is convex, then $\forall A\vec{x}+\vec{b},A\vec{y}+\vec{b}\in dom(f),\theta \in [0,1]$, we have:
> $\begin{aligned}f(\theta(A\vec{x}+\vec{b})+(1-\theta)f(A\vec{x}+\vec{b}))&\leq \theta f(A\vec{x}+\vec{b})+(1-\theta)f(A\vec{x}+\vec{b})\\f(A(\theta\vec{x}+(1-\theta )\vec{y})+\vec{b})&\leq \theta g(\vec{x})+(1-\theta)g(\vec{y})\\g(\theta\vec{x}+(1-\theta)\vec{y})&\leq \theta g(\vec{x})+(1-\theta)g(\vec{y})\end{aligned}$
> Moreover, since $f$is convex, then $dom(f)$is convex by definition, so $dom(g)$is convex by easy calculation，which together shows that $g$is convex.
> If g is convex, then $\forall \vec{x},\vec{y}\in dom(g),\theta\in [0,1]$, we have:
> $\begin{aligned}g(\theta\vec{x}+(1-\theta)\vec{y})&\leq \theta g(\vec{x})+(1-\theta)g(\vec{y})\\f(A(\theta \vec{x}+(1-\theta)\vec{y})+\vec{b})&\leq \theta f(A\vec{x}+\vec{b})+(1-\theta)f(A\vec{y}+\vec{b})\\f(\theta(A\vec{x}+\vec{b})+(1-\theta)(A\vec{y}+\vec{b}))&\leq\theta f(A\vec{x}+\vec{b})+(1-\theta)f(A\vec{y}+\vec{b})\end{aligned}$
> which shows that $f$is convex.
> Moreover, since $g$is convex, then $dom(g)$is convex by definition, so $dom(f)$is convex by easy calculation，which together shows that $g$is convex.


## Non-negative Weighted Sum
### Finite Sum
> [!important]
> ![](Convex_Functions.assets/image-20231101114414046.png)![image.png](Convex_Functions.assets/20231023_2246121329.png)![image.png](Convex_Functions.assets/20231023_2246132323.png)

> [!example] 
> 假设$f_i:\mathbb{R}^{n\to}\mathbb{R}, i=1,2,\cdots, m$为凸，$\vec{a}\in \mathbb{R}^{n}, \vec{b}\in\mathbb{R}$, 且$g(\vec{x})=\vec{a}^{\top}\begin{bmatrix}f_1(\vec{x})&\cdots&f_n(\vec{x}) \end{bmatrix}+\vec{b}$, 问: $g(\vec{x})$是否是凸函数。
> 由上述定义可知，由于我们不知道$\vec{a}$中元素的非负性，所以答案是否定的。


### Infinite Sum - Integral
> [!important]
> ![](Convex_Functions.assets/image-20231101114432188.png)



## Pointwise Maximum
### Fundations
> ![](Convex_Functions.assets/image-20231101120344693.png)
> Alternative Proof: Proof by Epigraph
> ![image.png](Convex_Functions.assets/20231023_2246167709.png)



### Piecewise Linear Function
> As an extension to point-wise maximum
> ![image.png](Convex_Functions.assets/20231023_2246179087.png)![image.png](Convex_Functions.assets/20231023_2246184725.png)



### NN Weighted Sum of r largest components
> [!important]
> ![image.png](Convex_Functions.assets/20231023_2246206555.png)![image.png](Convex_Functions.assets/20231023_2246223596.png)
> **对于**$(a)$**来说:**
> 
> ![](Convex_Functions.assets/image-20231101121136772.png)![](Convex_Functions.assets/image-20231101121151361.png)
> **对于**$(b)$**来说:**
> 
> ![](Convex_Functions.assets/image-20231101121205701.png)



## Pointwise Supremum
### Definition
> [!def]
> ![](Convex_Functions.assets/image-20231101122046683.png)


### Maximum Eigenvalue
> [!example]
> ![](Convex_Functions.assets/image-20231101123141856.png)
> 注意到这里 $\vec{y}^{\top}X\vec{y}$ 是一个关于 $X$ 的线性函数，因为$\vec{y}^{\top}X\vec{y}=\sum_{i=1}^{n}X_{ii}y_i^2+\sum_{i,j,i\neq j}y_iy_jX_{ij}$，而线性函数一定是凸函数。




## Composition of functions
> ![image.png](Convex_Functions.assets/20231023_2246227216.png)![image.png](Convex_Functions.assets/20231023_2246243355.png)

**Proofs**

