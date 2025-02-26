# Strong Convexity&Lipschitz-Smooth
## Taylor Theorem
### Precise Statement
> [!important]
> ![](../3_Convex_Optimization/Convex_Functions.assets/image-20231108121240259.png)

### Remainder Formula
> [!important] Mean-Value Formulation
> ![](../3_Convex_Optimization/Convex_Functions.assets/image-20231108121316293.png)

> [!important] Integral Formulation
> ![](../3_Convex_Optimization/Convex_Functions.assets/image-20231108121340381.png)


### Vectorized Theorem
> [!thm]
> ![](../3_Convex_Optimization/Convex_Functions.assets/image-20231104220400332.png)
> 其中积分可以理解为`Residuals`

> [!proof]
> ![](../3_Convex_Optimization/Convex_Functions.assets/image-20231104220519742.png)
> **Notes:**
> 1. 上面$(8.1.4)$的推导
> 2. $g''(t)=(\vec{y}-\vec{x})^{\top}\nabla f(\vec{x}+t(\vec{y}-\vec{x}))(\vec{y}-\vec{x})$ is by applying the multivariate chain rule to the function composition $m(\vec{g}(\vec{h}(t)))$ where $m(\vec{r}) = (\vec{y}-\vec{x})^{\top}\vec{r}$, $\vec{g}(\vec{q})=\nabla f(\vec{q})$ and $\vec{h}(t)=\vec{x}+t(\vec{y}-\vec{x})$

 

## Lipschitz Smoothness
> [!important] 
> 注意这个概念和`Lipschitz Continuity`不一样:
> ![](../3_Convex_Optimization/Convex_Functions.assets/image-20231108112104019.png)


#### Definition
> [!def]
> ![](../3_Convex_Optimization/Convex_Functions.assets/image-20231108104402589.png)

#### Important Lemmas  
> [!lemma]
> ![](../3_Convex_Optimization/Convex_Functions.assets/image-20231108104439094.png)![](../3_Convex_Optimization/Convex_Functions.assets/image-20231108104447726.png)![](../3_Convex_Optimization/Convex_Functions.assets/image-20231108111629862.png)

> [!proof] Proof 12.1.1
> ![](../3_Convex_Optimization/Convex_Functions.assets/image-20231108124517995.png)

> [!proof] Proof 12.1.2
> ![](../3_Convex_Optimization/Convex_Functions.assets/image-20231108111333971.png)

> [!proof] Proof 12.1.3
> The first part follows from the first order condition of a convex function.
> The second part:
> - The first inequality follows from 
> - The second inequality follows from lemma 12.1.2 by applying it twice with $f(\vec{x})\leq f(\vec{y})+...$ and $f(\vec{y})\leq f(\vec{x})+...$ and add them up or we can use cauchy inequality for vectors.

> [!proof] Proof 8.1.7
> By lemma 12.1.2 we have:
> ![](../3_Convex_Optimization/Convex_Functions.assets/image-20231108111707483.png)


### Gradient Bound 
> [!thm]
> ![](Gradient_Descent.assets/image-20231213205719519.png)

> [!proof]
> ![](Gradient_Descent.assets/image-20231213222730914.png)



## mu-Strongly Convexity
### Definition 1: Jensen's Inequality
> [!def]
> ![](../3_Convex_Optimization/Convex_Functions.assets/image-20231104212358864.png)

> [!property] Strongly Convex -> Unique Minimizer
> ![](../3_Convex_Optimization/Convex_Functions.assets/image-20231105130951888.png)![](../3_Convex_Optimization/Convex_Functions.assets/image-20231105131006471.png)

> [!property] Convexity -> Local Minimum = Globally Minimum
> ![](../3_Convex_Optimization/Convex_Functions.assets/image-20231105131613001.png)




### Definition 2: First-Order Condition
> [!def]
> ![](../3_Convex_Optimization/Convex_Functions.assets/image-20231104222956395.png)![](../3_Convex_Optimization/Convex_Functions.assets/image-20231108102725005.png)![](../3_Convex_Optimization/Convex_Functions.assets/image-20231104222540926.png)
> **Remarks:**
> - 其中$\frac{\mu}{2}\|\vec{y}-\vec{x}\|^2=\frac{1}{2}(\vec{y}-\vec{x})^{\top}\begin{bmatrix} \mu&0&\cdots&0\\0&\mu&\cdots&0\\\vdots&0&\ddots&\vdots\\0&0&\cdots&\mu\end{bmatrix}(\vec{y}-\vec{x})$, 而我们知道$f(\vec{x})+\langle\nabla f(\vec{x}), \vec{y}-\vec{x}\rangle+\frac{\mu\|\vec{y}-\vec{x}\|^2}{2}$是一个`Quadratic Function`, 所以本质上如果对于可微函数$f$来说，我们能够找到一个`Quadratic Lower Bound Like this`, 那么这个函数是$\mu$-strongly convex的。 
> - 和`Taylor Theorem`做一个对比: `Taylor Theorem`的目的是找到一个最接近原函数的下界$\begin{aligned} f(\vec{y}) \approx f(\vec{x})+\nabla^{\top}(\vec{x}) \cdot(\vec{y}-\vec{x})+\frac{1}{2}(\vec{y}-\vec{x})^{\top} \nabla^2 f(\vec{x})(\vec{y}-\vec{x})\end{aligned}$, 而$\mu$-strongly convex 只需要存在这样一个下界即可。
> - 另外，`Taylor Theorem`中的$\nabla f(\vec{x})$在不同的$\vec{x}$下的值是不一样的，所以在不同的$\vec{x}$下这个`Quadratic Term`是会随$\vec{x}$的位置变化的，而`mu-strongly convex`的这个下界实际上是给海森矩阵规定了一个下界，使得`Hessian Matrix`在所有$\vec{x}$处都是这个下界。
> 

> [!proof] Proof 8.1.5 
> ![](Gradient_Descent.assets/image-20231214230430859.png)![](Gradient_Descent.assets/image-20231214230441623.png)

> [!proof] Proof 8.1.7
> Just apply theorem 8.1.5 on $g(x)=f(x)-\mu\frac{\|x\|^2}{2}$.


### Gradient Bound
> [!thm]
> ![](Gradient_Descent.assets/image-20231214230843591.png)

> [!proof] Proof 8.1.5 and 8.1.6
> ![](../3_Convex_Optimization/Convex_Functions.assets/image-20231104222551310.png)![](Gradient_Descent.assets/image-20231214234100846.png)
> Note that the gradient of $\nabla f(\vec{x})^{\top}(\vec{x}-\vec{y})+\frac{\mu}{2}\|\vec{x}-\vec{y}\|_2^2$ is $\nabla f(\vec{x})\cdot I+\frac{\mu}{2}\cdot I\cdot 2(\vec{y}-\vec{x})$, setting it to zero and we get $\vec{y}=\vec{x}-\frac{\nabla f(\vec{x})}{\mu}$, fitting it back to the objective function and we get the desired result.





## Important Properties
###  mu-strongly => strongly
> [!property] Property: $\mu$-strongly convex=>strongly(strictly) convex
> $\forall\vec{x},\vec{y}\in dom(f),\theta\in [0,1]$, we have by definition of $\mu$-strongly convex that:
> $$\begin{align}f(\theta\vec{x}+(1-\theta)\vec{y})-\frac{\mu}{2}\|\theta\vec{x}+(1-\theta)\vec{y}\|^2\\\leq\theta(f(\vec{x})-\frac{\mu}{2}\|\vec{x}\|^2)+(1-\theta)(f(\vec{y})-\frac{\mu}{2}\|\vec{y}\|^2)\end{align}$$
> Then we rearrange the terms and could get the following:
> $$\begin{align}f(\theta\vec{x}+(1-\theta)\vec{y})&\leq \theta f(\vec{x})+(1-\theta)f(\vec{y})-\frac{\mu}{2}(\theta\|\vec{x}\|^2+(1-\theta)\|\vec{y}\|^2)\\&+\frac{\mu}{2}\|\theta\vec{x}+(1-\theta)\vec{y}\|^2\\&<\theta f(\vec{x})+(1-\theta)f(\vec{y})-\frac{\mu}{2}(\theta\|\vec{x}\|^2+(1-\theta)\|\vec{y}\|^2)\\&+\frac{\mu}{2}(\theta^2\|\vec{x}\|^2+\theta(1-\theta)(\|\vec{x}\|^2+\|\vec{y}\|^2)+(1-\theta)^2\|\vec{y}\|^2)\\&=\theta f(\vec{x})+(1-\theta)f(\vec{y})\end{align}$$ 
> where:
>$$\|\vec{x}\|^2+\|\vec{y}\|^2>2\langle\vec{x}, \vec{y}\rangle \text { for } \vec{x} \neq \vec{y} .$$

> [!corollary] Corollary: $g(\vec{x})$ is convex implies $g(\vec{x})+\mu\frac{\|\vec{x}\|^2}{2}$ is strongly convex
> $$\begin{aligned}g(\theta \vec{x}+(1-\theta) \vec{y})+\frac{\mu \| \theta \vec{x}+(1-\theta)\|^2}{2} & \leq \theta g(\vec{x})+(1-\theta) g(\vec{y})+\frac{\mu}{2}\left(\theta^2\|\vec{x}\|^2+2 \theta(1-\theta)\langle\vec{x}, \vec{y}\rangle+(1-\theta)^2\|\vec{y}\|^2\right) \\& \left.<\theta g(\vec{x})+(1-\theta) g(\vec{y})+\frac{\mu}{2}\left[\theta^2\|\vec{x}\|^2+\theta(1-\theta)\left(\| \vec{x}\left\|^2+\right\| \vec{y} \|^2\right)+(1-\theta)^2\right] \| \vec{y} \|^2\right] \\& =\theta g(\vec{x})+(1-\theta) g(\vec{y})+\frac{\mu}{2}\left[\theta \| \vec{x}\left\|^2+(1-\theta)\right\| \vec{y} \|^2\right] \\& =\theta\left(g(\vec{x})+\frac{\mu}{2}\|\vec{x}\|^2\right)+(1-\theta)\left[g(\vec{y})+\frac{\mu}{2}\|\vec{y}\|^2\right] .\end{aligned}$$


### Quadratic Bounds - For Strong Convexity&Lipschitz Smooth
#### Quadratic Lower Bound
> [!important]
> 本章节主要介绍$\mu$-strongly convex 的一个重要性质。我们知道对于一个凸函数来说，他的下界是其一阶泰勒估计。而$\mu$-strongly convex function的一个重要性质是: 他的下界是一个二次函数, 二次函数的系数由$\mu$决定。
> ![](../3_Convex_Optimization/Convex_Functions.assets/image-20231108104059403.png)![](../3_Convex_Optimization/Convex_Functions.assets/image-20231213210046191.png)





#### Quadratic Upper Bound
> [!important]
> 对于一个$\mu$-strongly且$M$-Lipschitz Smooth的函数来说，其有二阶上界。
> ![](../3_Convex_Optimization/Convex_Functions.assets/image-20231108124744800.png)![](../3_Convex_Optimization/Convex_Functions.assets/image-20231108124750721.png)


#### Bounds on Hessian
> [!corollary] Corollary -  L2 Norm Case
> ![](../3_Convex_Optimization/Convex_Functions.assets/image-20231108125028666.png)
> This implies that $\mu<L$ generally.

> [!proof] Proof of the first inequality
> Since $f$ is $\mu$-strongly convex, we have:$$\langle\nabla f(\vec{x})-\nabla f(\vec{y}), \vec{x}-\vec{y}\rangle \geqslant \mu\|\vec{x}-\vec{y}\|_2^2$$Letting $\vec{y}=\vec{x}+\alpha \vec{h}$ where $\alpha$ is small, then:$$\begin{aligned}\left\langle\nabla f(\vec{x})-\nabla f(\vec{x}+\alpha \cdot \vec{h}), \vec{x}-(\vec{x}+\alpha \cdot \vec{h}) \big\rangle \geqslant \mu\|\vec{x}-(\vec{x}+\alpha \cdot \vec{h})\|_2^2\right. \\\left\langle\nabla f(\vec{x})-\nabla f(\vec{x}+\alpha \vec{h}),-\alpha \cdot \vec{h}\rangle\geqslant \mu\|-\alpha \cdot \vec{h}\|_2^2\right. \\-\alpha\langle\nabla f(\vec{x})-\nabla f(\vec{x}+\alpha \vec{h}), \vec{h}\rangle \geqslant \mu \alpha^2\|\vec{h}\|_2^2 \\\left\langle\frac{\nabla f(\vec{x}+\alpha \cdot \vec{h})-\nabla f(\vec{x})}{\alpha}, \vec{h}\right\rangle \geqslant \mu\|\vec{h}\|_2^2\end{aligned}$$letting $\alpha \rightarrow 0$, we have$$\begin{aligned}\left\langle\nabla^2 f(\vec{x}) \vec{h}, \vec{h}\right\rangle & \geqslant \mu\|\vec{h}\|_2^2 \\\vec{h}^{\top} \nabla^2 f(\vec{x}) \vec{h} & \geqslant \vec{h}^{\top} \mu I_n \vec{h} \\\vec{h}^{\top}\left(\nabla^2 f(\vec{x})-\mu I_n\right) \vec{h} & \geqslant 0 \quad \forall \vec{h}\in\mathbb{R}^n \\\therefore \nabla^2 f(\vec{x})-\mu I_n & \succeq 0 \\\therefore \nabla^2 f(\vec{x}) & \succeq \mu I_n\end{aligned}$$

> [!proof] Proof of the second inequality
> Since $f$ is L-Lipschitz Smooth, we have:$$\begin{aligned}\| \nabla f(\vec{x}) & -\nabla f(\vec{y})\left\|_2 \leq L\right\| \vec{x}-\vec{y} \|_2 \\\nabla^2 f(\vec{x}) \cdot \vec{h} & =\lim _{\alpha \rightarrow 0} \frac{\nabla f(\vec{x}+\alpha \cdot \vec{h})-\nabla f(\vec{x})}{\alpha} \\\therefore\left\|\nabla^2 f(\vec{x}) \cdot \vec{h}\right\|_2 & =\lim _{\alpha \rightarrow 0} \frac{\|\nabla f(\vec{x}+\alpha \cdot \vec{h})-\nabla f(\vec{x})\|_2}{|\alpha|} \\& \leq \lim _{\alpha \rightarrow 0} \frac{L\|\vec{x}+\alpha \cdot \vec{h}-\vec{x}\|_2}{|\alpha|} \\& =\lim _{\alpha \rightarrow 0} \frac{L|\alpha|\|\vec{h}\|_2}{|\alpha|} \\& =L\|\vec{h}\|_2 \\\therefore \vec{h}^{\top} \nabla^2 f(\vec{x}) \vec{h} & \leqslant \vec{h}^{\top} L I_n \vec{h} \\\vec{h}^{\top}\left(\nabla^2 f(\vec{x})-L \cdot I_n\right) \vec{h} & \leqslant 0 \quad \forall \vec{h} \in R^n \\\therefore \nabla^2 f(\vec{x})-L \cdot I_n & \leq 0 . \\\nabla^2 f(\vec{x}) & \leq L \cdot I_n .\end{aligned}$$


> [!corollary] Corollary - General Norm
> ![](../3_Convex_Optimization/Convex_Functions.assets/image-20231108161129458.png)



#### Summary
> [!summary]
>  总的来说，对于一个$\mu$-strongly convex且$L$-Smooth的函数，我们有:
> $\forall\vec{x},\vec{y}\in dom(f)$:
> $$\begin{aligned}f(\vec{y})&\leq f(\vec{x})+\nabla f(\vec{x})^{\top}(\vec{y}-\vec{x})+\frac{L}{2}\|\vec{y}-\vec{x}\|_2^2\\&\geq f(\vec{x})+\nabla f(\vec{x})^{\top}(\vec{y}-\vec{x})+\frac{\mu}{2}\|\vec{y}-\vec{x}\|_2^2\end{aligned}$$  



# Unconstrained Gradient Descents
> [!motiv] Motivation
> ![](Gradient_Descent.assets/image-20231108095325288.png)![](Gradient_Descent.assets/image-20231214220053728.png)




## First Order Descent Method Scheme
> [!algo] Algorithm
> ![](Gradient_Descent.assets/image-20231108095540460.png)![](Gradient_Descent.assets/image-20231214220141260.png)



## Steepest Gradient Descent
### Motivation
> [!motiv] Motivation
> ![](Gradient_Descent.assets/image-20231108102212825.png)


### Descent Direction
> [!thm]
> ![](Gradient_Descent.assets/image-20231117220151969.png)![](Gradient_Descent.assets/image-20231117220200437.png)![](Gradient_Descent.assets/image-20231117220207277.png)

> [!important]
> ![](Gradient_Descent.assets/image-20231214220128672.png)![](Gradient_Descent.assets/image-20231108095457055.png)





### Stepsize Selection
#### Constant Step Size
> [!example] Murphy pp282
> ![](Gradient_Descent.assets/image-20240128201031395.png)![](Gradient_Descent.assets/image-20240128201803338.png)
> The derivations of the upper bound of the step size is given in [Convergence Analysis of Steepest G.D.](Gradient_Descent.md#Convergence%20Analysis%20of%20Steepest%20G.D.)
> 
> Here, note that the book says that the largest eigenvalue of $A$ measures the steepest slope of the function, we give the derivation below:



#### Line Search Termination Conditions
> [!important] 
> In practice, the initialization of the line-search and how to backtrack can significantly affect performance.
> 
> We now introduce the termination conditions for line search algorithm. When these conditions are met, the corresponding step size are considered to be acceptable.
> 
>  Note here we have a **sufficient decrease condition** called **Armijo-Golstein Test**:
>  ![](Gradient_Descent.assets/image-20240128205147652.png)![](Gradient_Descent.assets/image-20240128204112705.png)
>  Here $c$ is some constant $\in (0,1)$ and is conventionally set to $10^{-4}$.
>  
>   In other words, the reduction in f should be proportional to both the step length $α_k$ and the directional derivative $\nabla f_k^{\top}p_k$.
>   
>   Now we focus on the RHS of the inequality, with $l(\alpha)=f(x_k)+c_1\alpha\nabla f_k^{\top}p_k$ being an affine function in $\alpha$.
>   
>   Since we set the descent direction to be opposite of the gradient, we have that $\nabla f_k^{\top}p_k$ is negative, so $l(\alpha)$ has negative slope.
>   
>   The **sufficient decrease condition** states that α is acceptable only if $φ(α) ≤ l(α)$
>   ![](Gradient_Descent.assets/image-20240128205608342.png)
>   The sufficient decrease condition is not enough by itself to ensure that the algorithm makes reasonable progress because,as we see from Figure 3.3, it is satisfied for all sufficiently small values of α. 
>   
>   To rule out unacceptably short steps we introduce a second requirement, called **curvature condition**:
>   
>   ![](Gradient_Descent.assets/image-20240128205715547.png)![](Gradient_Descent.assets/image-20240128205738489.png)![](Gradient_Descent.assets/image-20240128211239344.png)![](Gradient_Descent.assets/image-20240128211418916.png)


#### Wolfe Conditions
> [!important] Wolfe Conditions
> ![](Gradient_Descent.assets/image-20240128211250010.png)![](Gradient_Descent.assets/image-20240128211256563.png)![](Gradient_Descent.assets/image-20240128211302524.png)


#### Goldstein Conditions
> [!important]
> 




#### Exact Line Search
> [!important]
> ![](Gradient_Descent.assets/image-20240128205055924.png)

> [!example] Murphy pp283 Exact Line Search
> ![](Gradient_Descent.assets/image-20240128195838843.png)
> Here we use a very important property of convex function, [Affine Composition](../3_Convex_Optimization/Convex_Functions.md#Operations%20Preserving%20Convexity#Affine%20Composition). This means that $\phi(\eta)$ is convex in $\eta$ and thus we could set the derivative of $\phi(\eta)$ to 0 and get the global minimum.
> 
> **Note:** Using the optimal step size is known as exact line search . However, it is not usually necessary to be so precise.


#### Inexact Line Search
> [!bug] Insufficient Reduction
> ![](Gradient_Descent.assets/image-20240128205248037.png)

> [!Algo] Armijo Backtracking Line Search Algorithm
> We have mentioned that the sufficient decrease condition alone is not sufficient to ensure that the algorithm makes reasonable progress along the given search direction. 
> 
> However, if the line search algorithm chooses its candidate step lengths appropriately, by using a so-called backtracking approach, we can dispense with the extra condition  and use just the sufficient decrease condition to terminate the line search procedure. In its most basic form, backtracking proceeds as follows.
> ![](Gradient_Descent.assets/image-20231108102015113.png)
> The backtracking approach ensures either that the selected step length $α_k$ is some fixed value (the initial choice $\bar{\alpha}$), or else that it is short enough to satisfy the sufficient decrease condition but not too short. The latter claim holds because the accepted value $α_k$ is within a factor $ρ$ of the previous trial value, $\frac{α_k}{\rho}$, which was rejected for violating the sufficient decrease condition, that is, for being too long.




## Stochastic Gradient Descent
### Algorithm Scheme
> [!def]
> ![](Gradient_Descent.assets/image-20231214215810431.png)![](Gradient_Descent.assets/image-20231214215909745.png)




### Step Size Constraints
> [!important]
> Suppose at a particular time $t$, the step size is $\eta_t$, we have to enforce the following two constraints:
> 1. Not Summable: $\sum\limits_{i=1}^\infty\eta_i=\infty$. In real analysis [L11_L12__Absolute_Convergence_Tests_for_Series](../../../../Mathematics/Analysis/18_100A_Real_Analysis/L11_L12__Absolute_Convergence_Tests_for_Series.md) we know that if the series is finite, the underlying sequence converges to zero. Since we don't want our step size to converge to zero, this condition is necessary. You can think of it as a lower bound on the step size.
> 2. Square Summable: $\sum\limits_{i=1}^{\infty}\eta_i^2<\infty$. This prevents our step size from growing arbitrarily large. This is important because SGD incorporates a certain level of randomness due to the selection of a subset of data (mini-batch) at each iteration. As the algorithm proceeds, it's crucial to reduce the step size to dampen the effect of this randomness and to allow the algorithm to settle into a minimum.


### Choosing the step size







### Applications
### Finding Centroid
> [!example] Application: Finding Centroid
> ![](Gradient_Descent.assets/image-20231214220545511.png)![](Gradient_Descent.assets/image-20231214220551473.png)








# Constrained Gradient Descent
## Motivations
> [!motiv] Idea
> ![](Gradient_Descent.assets/image-20231214220923332.png)


## Projected Gradient Descent
> [!def]
> ![](Gradient_Descent.assets/image-20231214221002228.png)![](Gradient_Descent.assets/image-20231214221319887.png)




## Conditional Gradient Descent - Frank-Wolfe Method
> [!def]
> ![](Gradient_Descent.assets/image-20231214222310704.png)![](Gradient_Descent.assets/image-20231214222321331.png)




# Convergence Analysis of Steepest G.D.
## Matrix Limit Perspective
### Version 1 - Control Problem
> [!important]
> Consider this function $f(\vec{x})=\|A\vec{x}-\vec{b}\|$ and the umonstrained optimization problem$$\min _{\vec{x} \in R^n}\|A \vec{x}-\vec{b}\| \text {. }$$We want to show the condition that step size $\eta$ must fulfill in order for gradient descent to converge.
> The single step strepest gradient descent goes like this:$$\vec{x}_{k+1}=\vec{x}_k-\eta \cdot \nabla f\left(\vec{x}_k\right), \eta>0$$So we want to compute the gradient of $f(\vec{x})$ :$$\begin{aligned}\|A \vec{x}-\vec{b}\|_2^2 & =\vec{x}^{\top} A^{\top} A \vec{x}-2 \vec{b}^{\top} A \vec{x}+\|\vec{b}\|_2^2 \\\nabla f(\vec{x}) & =2 A^{\top} A \vec{x}-2 A^{\top} \vec{b} . \\& =2 A^{\top}(A \vec{x}-\vec{b})\end{aligned}$$Thus $\vec{x}_{k+1}=\vec{x}_k-\eta \cdot 2 A^{\top}(A \vec{x}-\vec{b})$
> In order for $\vec{x}_k$ to converge to our least-square solution we want to show that $\vec{x}_{k+1}-\vec{x}_* \rightarrow 0$ as $k \rightarrow \infty$, it's equivalent to show something like:
> $\vec{x}_{k+1}-\vec{x}_*=C^{k+1}\left(\vec{x}_0-\vec{x}_*\right)$ where $C$ controls our convergence.$$\begin{aligned}\because \vec{x}_{k+1}-\vec{x}_* & =\vec{x}_{k+1}-\left(A^{\top} A\right)^{-1} A^{\top} \vec{b} \\& =\vec{x}_k-2 \eta A^{\top}\left(A \vec{x}_k-\vec{b}\right)-\left(A^{\top} A\right)^{-1} A^{\top} \vec{b} \\& =\vec{x}_k-2 \eta A^{\top} A \vec{x}_k+2 \eta A^{\top} \vec{b}-\left(A^{\top} A\right)^{-1} A^{\top} \vec{b} \\& =\vec{x}_k-2 \eta A^{\top} A \vec{x}_k+2 \eta\left(A^{\top} A\right)\left(A^{\top} A\right)^{-1} A^{\top} \vec{b}-\left(A^{\top} A\right)^{-1} A^{\top} \vec{b} \\& =\left(I_n-2 \eta A^{\top} A\right) \vec{x}_k+\left(2 \eta A^{\top} A-I_n\right)\left(A^{\top} A\right)^{-1} A^{\top} \vec{b} \\& =\left(I_n-2 \eta A^{\top} A\right) \vec{x}_k-\left(I_n-2 \eta A^{\top} A\right)\left(A^{\top} A\right)^{-1} A^{\top} \vec{b} \\& =\left(I_n-2 \eta A^{\top} A\right)\left(\vec{x}_k-\vec{x}_*\right)\end{aligned}$$Let $\vec{z}_{k+1}=\vec{x}_{k+1}-\vec{x}_*$Then we have the following recurrence equation:$$\vec{z}_{k+1}=\left(I_n-2 \eta A^{\top} A\right) \vec{z}_k$$Solve for it and we get:$$\vec{z}_{k+1}=\left(I_n-2 \eta A^{\top} A\right)^{k+1} \vec{z}_0$$By the knowledge from [Stability_Feedback_Control](../../Control_LA_Circuit/EECS16B/Module2_Robotic_Control/Stability_Feedback_Control.md) for differential system we know that, in order for $\left\|\vec{z}_{k+1}\right\|$ to be bounded, the. eigenvalues of $I_n-2 \eta A^{\top} A$ should be between 0 and 1 . Thus the convergence condition requires.$$\begin{aligned}-1 & \leq 1-2 \eta \lambda_k\left(A^{\top} A\right) \leqslant 1 & \forall k=1,2, \cdots, n \\\Leftrightarrow & 0 \leq \eta \lambda_k\left(A^{\top} A\right) \leqslant 1 & \forall k=1,2, \cdots, n . \\\Leftrightarrow & 0 \leqslant \lambda_k\left(A^{\top} A\right) \leqslant \frac{1}{\eta} & \forall k=1,2, \cdots, n\end{aligned}$$
> Which means that $0<\eta<\frac{1}{\sigma_1^2}$, where $\sigma_1$ denotes the maximum singular value of $A$.


### Version 2 - Matrix Limit
> [!important]
> ![](Gradient_Descent.assets/image-20231109095850525.png)![](Gradient_Descent.assets/image-20231109100350318.png)![](Gradient_Descent.assets/image-20231109100357595.png)![](Gradient_Descent.assets/image-20231109100409620.png)![](Gradient_Descent.assets/image-20231109100417543.png)![](Gradient_Descent.assets/image-20231109100424425.png)![](Gradient_Descent.assets/image-20231109100431866.png)


## Eigenvalue Perspective
> [!example]
> NYU-DS-GA-1014 Fa20 HW12
> ![](Gradient_Descent.assets/image-20231109101156312.png)![](Gradient_Descent.assets/image-20231109101202437.png)

> [!proof] Proof (a)
> Since $\mu$-strongly convex implies strong convexity, we know that $f(\vec{x})$ is strongly convex. 
> By the first order condition we have $\forall \vec{x}\neq \vec{x}_*,f(\vec{x})>f(\vec{x}_{*})+\nabla f(\vec{x}_*)^{\top}(\vec{x}-\vec{x}_*)$. And for all the $\vec{x}_*$ that satisfies $\nabla f(\vec{x}_*)=0$, we know by the strong convexity that $f(\vec{x})>f(\vec{x}_*)$, which means that $\vec{x}_*$ is the global minimizer(which is also unique) if $\vec{x}_*$ satisfies the first order condition.
> Now since $\nabla f(\vec{x})=M\vec{x}-\vec{b}$, if we set it to zero we get $M\vec{x}_*=\vec{b}$. Now since $\nabla^2f(\vec{x})=M$ and by the property of $\mu$-strongly convex and $L$-smooth function, we know that $L\leq \lambda_k(M)\leq\mu,\forall k=1,2,\cdots, n$。Also since $\mu>0$(definition), we know that $\lambda_d>0$, which means $M$ is P.D. Thus, we are safely to conclude that $\vec{x}_*=M^{-1}\vec{b}$, which is unique global minimizer.

> [!proof] Proof (b)
> 

> [!proof] Proof (c)
> 

> [!proof] Proof (d)
> 

> [!proof] Proof (e)
> 

> [!proof] Proof (f)
> 



## Convergence Speed for Convex and  L-Smooth 
> [!thm]
> ![](Gradient_Descent.assets/image-20231214222857661.png)![](Gradient_Descent.assets/image-20240227140135803.png)

> [!proof] Proof for proposition
> ![](Gradient_Descent.assets/image-20231215000557219.png)![](Gradient_Descent.assets/image-20231215000602634.png)

> [!proof] Proof for theorem 8.3.3
> ![](Gradient_Descent.assets/image-20240227140210542.png)![](Gradient_Descent.assets/image-20240227140222686.png)![](Gradient_Descent.assets/image-20240227140233616.png)![](Gradient_Descent.assets/image-20240227140250242.png)





## Convergence Speed for U-strongly&L-Smooth Functions
### Important Lemma
> [!important]
> 从 [Quadratic Bounds](../3_Convex_Optimization/Convex_Functions.md#Quadratic%20Bounds)  我们知道，对于一个$\mu$-strongly convex且$L$-Smooth的函数，我们有:
> $\forall\vec{x},\vec{y}\in dom(f)$:
> $$\begin{aligned}f(\vec{y})&\leq f(\vec{x})+\nabla f(\vec{x})^{\top}(\vec{y}-\vec{x})+\frac{L}{2}\|\vec{y}-\vec{x}\|_2^2\\&\geq f(\vec{x})+\nabla f(\vec{x})^{\top}(\vec{y}-\vec{x})+\frac{\mu}{2}\|\vec{y}-\vec{x}\|_2^2\end{aligned}$$  
> 这个`Lemma`暗含了这类函数的一个重要性质：如果我们在这类函数上进行梯度下降算法，则总是存在一个`Step Size` $\eta=\frac{1}{L}$使得梯度下降的过程收敛。


### Convergence Rate on Optimal Points
> [!thm]
> (Main thm)Given the gradient step:$$\overrightarrow{x_{t+1}}=\overrightarrow{x_t}-\eta \cdot \nabla f\left(\overrightarrow{x_t}\right)$$, we want to prove: $$\left\|\overrightarrow{x_{t+1}}-\overrightarrow{x_*}\right\|_2^2 \leq\left(1-\frac{\mu}{L}\right)^{t+1}\left\|\overrightarrow{x_0}-\overrightarrow{x_*}\right\|_2^2 \text {. }$$ for all $\mu$-strongly convex and $L$-smooth function for some $\mu$ and $L$.
> 
> Here, the bigger then $\frac{\mu}{L}$ is, the faster the convergence is, that is, the fewer steps that we need to get to the desired error bound.
> 
> In the language of matrix, the smaller the conditional number of a matrix $\frac{L}{\mu}$ is, the faster the convergence rate is.

> [!proof]
> ![](Gradient_Descent.assets/image-20231213223350182.png)![](Gradient_Descent.assets/image-20231213223354658.png)


### Convergence Rate on Optimal Values
> [!thm]
> ![](Gradient_Descent.assets/image-20231215000714639.png)

> [!proof]
> ![](Gradient_Descent.assets/image-20231215000725589.png)






### Main Theorem - Guarantee to Descent
> [!thm]
> ![](Gradient_Descent.assets/image-20231213223751011.png)

> [!proof]
> ![](Gradient_Descent.assets/image-20231213223802742.png)![](Gradient_Descent.assets/image-20231213223817598.png)







## Optimal Learning Rate of G.D.
> [!example] EECS127 Fa22 HW08 P1
> ![](Gradient_Descent.assets/image-20231213221553740.png)![](Gradient_Descent.assets/image-20231213221558255.png)![](Gradient_Descent.assets/image-20231213221604911.png)![](Gradient_Descent.assets/image-20231213221611671.png)![](Gradient_Descent.assets/image-20231213221621496.png)![](Gradient_Descent.assets/image-20231213221627679.png)![](Gradient_Descent.assets/image-20231213221634487.png)



## Error Bound Analysis
> [!example] EECS182 Sp23 HW1 P3
> ![](Gradient_Descent.assets/image-20240130113232932.png)
> This is the problem of having a conditional number that's too large. When we solve least square problem, we have the equation:
> $$F\vec{w}=\vec{y}$$
> But in reality what we observe is the follow equation:
> $$F\vec{w}+\vec{\epsilon}=\vec{y}$$
> , which is the same as we are perturbing the value of $\vec{y}$, so based on the perturbation analysis we have learned before, we have:
> $$\frac{\|\delta_{\vec{w}}\|_2}{\|\vec{w}\|_2}\leq \mathbb{k}(F)\frac{\|\vec{\epsilon}\|_2}{\|\vec{y}\|_2}$$, which tells us that even when the error is very small in magnitude, if the conditional number of $F$(and thus the singular value of $F^{\top})$ is huge, then the error in our estimation for $\vec{w}$(denoted by $\|\delta_{\vec{w}}\|_2$)will be huge in magnitude.
> So we want to use gradient descent to control the error within a bound:
> 
> ![](Gradient_Descent.assets/image-20240130114121614.png)![](Gradient_Descent.assets/image-20240130114144528.png)
> **Note:** Here we use lots of important properties in matrix algebra:
> 1. For any matrix $A$, we have $\|A\vec{x}\|_2\leq\|A\|_2\|\vec{x}\|_2$
> 2. For any matrix $A\in \mathbb{S}^n$, we have $|\lambda_i(A)|=sigma_i(A)$
> 3. For any matrix $A$, we have $\|A\|_2=\sigma_{max}(A)$
> 4. For any two vectors of the same dimension, we have $\|\vec{x}+\vec{y}\|_2\leq\|\vec{x}\|_2+\|\vec{y}\|_2$
> 
> **Given the above lemma, we can prove the following:**
> 1. By induction we have $\|\vec{w}_k\|_2\leq\|\vec{w}_0\|+k\eta\alpha\|\vec{y}\|_2=k\eta\alpha\|\vec{y}\|_2$
> 2. By triangle inequality we have $\|\vec{w}_k-\vec{w}^*\|_2\leq\|\vec{w}_k\|_2+\|\vec{w}^*\|_2\leq k\eta \alpha\|\vec{y}\|_2+\|\vec{w}^*\|_2$ 
> 
> Thus, as is proved above, when we choose our step as fixed and satisfy convergence condition, our error is bounded above by a quadratic function in the optimal solution:
> $$\|\vec{w}_k-\vec{w}^*\|_2\leq k\eta \alpha\|\vec{y}\|_2+\|\vec{w}^*\|_2$$



















# Convergence for Stochastic G.D.





# Code Experiments
## Theory
> [!important] GD and SGD
> Consider the following ridge regression loss function minimization problem:
> $$\min _{\vec{x} \in \mathbb{R}^n} f_\lambda(\vec{x}) \quad \text { where } \quad f_\lambda(\vec{x}) \doteq \frac{1}{2}\left\{\frac{1}{m}\|A \vec{x}-\vec{y}\|_2^2+\lambda\|\vec{x}\|_2^2\right\} \text {. }$$
> The gradient for the GD is computed using all the datapoints, which computes: $\nabla f(\vec{x})=\frac{1}{m}A^{\top}(A\vec{x}-\vec{y})+\lambda\cdot\vec{x}$ The derivation comes from using chain rule of Jacobian and then take the transpose.
> 
> The gradient for the SGD is computed by first sampling from the datapoints, select from one of them and compute the gradient with that particular data point. Suppose we sample the $i$-th datapoint, then we get: $\nabla f(\vec{x})=\vec{a}_i\cdot(\vec{a}_i^{\top}\vec{x}-\vec{y}_i)+\lambda\cdot\vec{x}$, notice that since $\vec{a}_i$ and $\vec{x}$ has the same dimension, it won't trigger any errors. Also notice that the regularization term $\lambda\|\vec{x}\|_2$ won't be affected by the sampling process, which means we first sample the $(A\vec{x}-\vec{y})_i$ and then apply the gradient of $\lambda\|\vec{x}\|_2$ to the previous result so **we don't need a multiplier $m$ in front.**
> 
> The code implementations are as follows:
> ![](Gradient_Descent.assets/image-20240131131411223.png)![](Gradient_Descent.assets/image-20240131131358355.png)
> Now we start to do our experiments
> 


## Experiments
## n = 1


n = 2

n >> 2

