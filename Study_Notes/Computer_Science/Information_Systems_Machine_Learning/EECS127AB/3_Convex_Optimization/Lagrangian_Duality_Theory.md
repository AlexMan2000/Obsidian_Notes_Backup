#  Motivation for Lagrangian
## Primal Problem
> [!def]
> ![](Lagrangian_Duality_Theory.assets/image-20231119092014229.png)


## Indicator Form - Unconstrained Formulation
> [!important]
> ![](Lagrangian_Duality_Theory.assets/image-20231119092056999.png)![](Lagrangian_Duality_Theory.assets/image-20231119092115017.png)
> 所以我们可以将原问题转化成等价的`Indicator-Unconstrained Formulation`, 但是这个$F_0(\vec{x})$是不可导的，所以我们的梯度下降算法不能正常工作。
> **注意: 这个问题等价于原问题!**



## Lagrangian - Differentiable Approximation
> [!important]
> ![](Lagrangian_Duality_Theory.assets/image-20231119092500799.png)
> **注意: 这个问题等价于原问题!**
> 但是如果仅仅是$min_{\vec{x}\in \mathbb{R}^n}L(\vec{x},\vec{\lambda},\vec{v})$, 则这个问题和原问题不等价。





# Lagrangian Form
## Definition
> [!def]
> ![](Lagrangian_Duality_Theory.assets/image-20231119094727877.png)![](Lagrangian_Duality_Theory.assets/image-20231119094850749.png)

## Properties
> [!property]
> ![](Lagrangian_Duality_Theory.assets/image-20231119094908880.png)


## Practical Examples
### Quadratic Inequality
> [!example] Quadratic Inequality
> ![](Lagrangian_Duality_Theory.assets/image-20231119181609376.png)![](Lagrangian_Duality_Theory.assets/image-20231119181614517.png)![](Lagrangian_Duality_Theory.assets/image-20231119181621076.png)![](Lagrangian_Duality_Theory.assets/image-20231119181628189.png)![](Lagrangian_Duality_Theory.assets/image-20231119181633878.png)![](Lagrangian_Duality_Theory.assets/image-20231119181640408.png)![](Lagrangian_Duality_Theory.assets/image-20231119181654168.png)






# Weak Duality
## Motivation
> [!motiv] Motivation
> ![](Lagrangian_Duality_Theory.assets/image-20231119095614350.png)![](Lagrangian_Duality_Theory.assets/image-20231119095631891.png)


## Dual Problam
### Definition
> [!def]
> ![](Lagrangian_Duality_Theory.assets/image-20231119095643705.png)
 

### Properties
> [!property] Concaveness
> ![](Lagrangian_Duality_Theory.assets/image-20231119095702121.png)![](Lagrangian_Duality_Theory.assets/image-20231119095753991.png)

> [!property] Inequality Relationship
> ![](Lagrangian_Duality_Theory.assets/image-20231119095942181.png)![](Lagrangian_Duality_Theory.assets/image-20231119095949491.png)![](Lagrangian_Duality_Theory.assets/image-20231119100003097.png)



## Deriving Dual Function
### Convex Lagrangian
> [!example] Disc08 P1 Fa22
> ![](Lagrangian_Duality_Theory.assets/image-20231119091222817.png)![](Lagrangian_Duality_Theory.assets/image-20231119091230464.png)![](Lagrangian_Duality_Theory.assets/image-20231119091241787.png)![](Lagrangian_Duality_Theory.assets/image-20231119091248367.png)

> [!example] Disc08 P2 Fa22
> ![](Lagrangian_Duality_Theory.assets/image-20231119100107847.png)![](Lagrangian_Duality_Theory.assets/image-20231119100124378.png)![](Lagrangian_Duality_Theory.assets/image-20231119100128992.png)

> [!example] Lecture Notes Example Fa23
> ![](Lagrangian_Duality_Theory.assets/image-20231119095840601.png)![](Lagrangian_Duality_Theory.assets/image-20231119095846872.png)


### Unbounded Lagrangian
> [!example] Lecture Note Fa23 Linear Program
> ![](Lagrangian_Duality_Theory.assets/image-20231119192049774.png)![](Lagrangian_Duality_Theory.assets/image-20231119192054973.png)


> [!example] Lecture Note Fa23 Shadow Price
> ![](Lagrangian_Duality_Theory.assets/image-20231119192122633.png)![](Lagrangian_Duality_Theory.assets/image-20231119192127339.png)


## Types of Duality
> [!def]
> ![](Lagrangian_Duality_Theory.assets/image-20231119100226241.png)




# Minmax Inequality
> [!property] Minimax Inequality
> ![](Lagrangian_Duality_Theory.assets/image-20231119100257854.png)
> **We will provide a clearer proof for Proposition 150:**
> For fixed $x_0\in X,y_0\in Y$, we define:
> $$\begin{align}h(y_0)=min_{x\in X}f(x,y_0)\\g(x_0)=max_{y\in Y}f(x_0,y)\end{align}$$
> Then:
> $$h(y_0)=min_{x\in X}f(x,y_0)\leq f(x_0,y_0)\leq max_{y\in Y}f(x_0,y)=g(x_0),\forall x_0,y_0\in X\times Y$$
> So we have:
> $$\forall x_0,y_0\in X\times Y,h(y_0)\leq g(x_0)$$
> Then we know that:
> $$max_{y_0\in Y}h(y_0)\leq min_{x_0\in X}g(x_0)$$
> Finally we conclude that:
> $$max_{y\in Y}min_{x\in X}f(x,y)\leq min_{x\in X}max_{y\in Y}f(x,y)$$
> **Then the proof for Proposition 149 goes as below:**
> 
> ![](Lagrangian_Duality_Theory.assets/image-20231119115546613.png)
> **Vector Version of Proposition 150:**
> ![](Lagrangian_Duality_Theory.assets/image-20231119184828823.png)
> 证明的核心思想就是如果一个不等式对所有$\vec{x},\vec{y}$均成立，那么对某一个$\vec{x}_0,\vec{y}_0$肯定也成立。




# Certificate of Optimality
> [!important]
> ![](Lagrangian_Duality_Theory.assets/image-20231119115540066.png)



# Strong Duality
## Slater's Condition - Theorem
> [!thm]
> **Refined Slater's Conditions:** 当有一些不等式约束是`Affine Functions`时使用。
> ![](Lagrangian_Duality_Theory.assets/image-20231119105412537.png)![](Lagrangian_Duality_Theory.assets/image-20231119105419305.png)
> **Slater's Condition:**
> 
> ![](Lagrangian_Duality_Theory.assets/image-20231119112504596.png)
> Note that Slater's Condition Only Works for Convex Problems.


> [!proof] Proof Sketch
> 



## Slater's Condition - Geometric Interpretation
> 


## Practical Examples
### Recover the Solutions to Primal Problems
> [!example] Lecture Notes
> ![](Lagrangian_Duality_Theory.assets/image-20231119163850539.png)![](Lagrangian_Duality_Theory.assets/image-20231119163857217.png)







### Changing Constraints to Obtain Strong Duality
#### Strong Duality Doesn't Hold
> [!example] Disc 09 P1 Fa22
> ![](Lagrangian_Duality_Theory.assets/image-20231119151029934.png)![](Lagrangian_Duality_Theory.assets/image-20231119151044223.png)![](Lagrangian_Duality_Theory.assets/image-20231119151050535.png)![](Lagrangian_Duality_Theory.assets/image-20231119151056553.png)![](Lagrangian_Duality_Theory.assets/image-20231119151102422.png)![](Lagrangian_Duality_Theory.assets/image-20231119151136257.png)![](Lagrangian_Duality_Theory.assets/image-20231119151503698.png)


#### Strong Duality Holds
> [!example]
> ![](Lagrangian_Duality_Theory.assets/image-20231119151718669.png)![](Lagrangian_Duality_Theory.assets/image-20231119151725300.png)![](Lagrangian_Duality_Theory.assets/image-20231119151732152.png)![](Lagrangian_Duality_Theory.assets/image-20231119151738314.png)



### Convexity Alone doesn't guaratee Strong Duality
> [!example] EECS127 Fa22 HW10 P1
> ![](Lagrangian_Duality_Theory.assets/image-20231214203225587.png)![](Lagrangian_Duality_Theory.assets/image-20231214203239121.png)




# KKT Conditions
## Main Theorem
> [!thm]
> ![](Lagrangian_Duality_Theory.assets/image-20231119114130874.png)

## Some Important Propositions
> [!thm]
> ![](Lagrangian_Duality_Theory.assets/image-20231119114232462.png)

> [!thm]
> ![](Lagrangian_Duality_Theory.assets/image-20231119114241048.png)
> The key logic is that convexity implies that any variable that fulfills stationary condition is a global minimizer of the primal problem.

> [!corollary]
> ![](Lagrangian_Duality_Theory.assets/image-20231119114316286.png)


## Important Summary
> [!summary]
> ![](Lagrangian_Duality_Theory.assets/image-20231119165105607.png)![](Lagrangian_Duality_Theory.assets/image-20231119165135932.png)



## Practical Example
### Complementary Slackness
> [!example] Disc 10 P2 Fa22
> ![](Lagrangian_Duality_Theory.assets/image-20231119172755070.png)![](Lagrangian_Duality_Theory.assets/image-20231119172759663.png)![](Lagrangian_Duality_Theory.assets/image-20231119172811079.png)![](Lagrangian_Duality_Theory.assets/image-20231119172816337.png)![](Lagrangian_Duality_Theory.assets/image-20231119172821277.png)




# Dual of the Dual
## Linear Program
> [!important]
> ![](Lagrangian_Duality_Theory.assets/image-20231128165002827.png)![](Lagrangian_Duality_Theory.assets/image-20231128165009509.png)![](Lagrangian_Duality_Theory.assets/image-20231128165028738.png)![](Lagrangian_Duality_Theory.assets/image-20231128165035300.png)







# Problem Solving Strategy
## Optimizing Over Multiple Variables
> [!important]
> The first part shows that if we are minimizing over multiple variables, we can minimize them one at a time and reach the joint minimum.
> ![](Lagrangian_Duality_Theory.assets/image-20231214213101144.png)
> The second part shows that the order of partial minimization doesn't matter.
> 
> ![](Lagrangian_Duality_Theory.assets/image-20231119184700016.png)
> Actually in the BV textbook, it says that we can always minimize a function by first minimizing over some of the variables, and then minimizing over the remaining ones. This simple and general principle can be used to transform problems into equivalent forms.
> 
> ![](Lagrangian_Duality_Theory.assets/image-20231214214208694.png)



## Partial Dualizing
> [!important]
> If strong duality doesn't hold, then different dual problem won't always be equivalent. But the optimal value of the dual problem is always the same.


### Example 1: Strong Duality -> Same Dual Problem
> [!example] HW09 Fa22 P3 
> ![](Lagrangian_Duality_Theory.assets/image-20231119202233597.png)![](Lagrangian_Duality_Theory.assets/image-20231119202241617.png)![](Lagrangian_Duality_Theory.assets/image-20231119202252586.png)


### Example 2: No Strong Duality -> Different Dual Problem
> [!example] HW09 Fa22 P3 Different Dualization, Same Optimal Value
> ![](Lagrangian_Duality_Theory.assets/image-20231119202038125.png)
> (1): Dualizing $x \geqslant 1$ :
> $$
> d^*=\max _{\lambda \geqslant 0} \min _{x \geqslant 0} x^3+\lambda(1-x)$$
> For $\min _{x \geqslant 0} L(x, \lambda)=\min _{x \geqslant 0} x^3+\lambda(1-x)$,
> Set: $\nabla_x L(x, \lambda)=0 \Rightarrow x^*=\sqrt{\frac{\lambda}{3}} \Rightarrow L\left(x^*, \lambda\right)=\left(\frac{\lambda}{3}\right)^{\frac{3}{2}}+\lambda\left(1-\sqrt{\frac{\lambda}{3}}\right)$
> Since $L(x, \lambda)$ isn't convex, for the boundary point $x=0$, we have: $L(0, \lambda)=\lambda$
> $$\begin{aligned}& \because\left(\frac{\lambda}{3}\right)^{\frac{3}{2}}+\lambda\left(1-\sqrt{\frac{\lambda}{3}}\right)-\lambda<0 \\
> & \therefore x^*=\sqrt{\frac{\lambda}{3}} \\& \therefore d^*=\max _{\lambda \geqslant 0}\left(\frac{\lambda}{3}\right)^{\frac{3}{2}}+\lambda\left(1-\sqrt{\frac{\lambda}{3}}\right)\end{aligned}$$
> Since dual function is always concave, we set: $\nabla_\lambda g(\lambda)=0$
> $$
> \begin{aligned}& \therefore \quad \frac{3}{2} \cdot \frac{1}{3} \cdot \sqrt{\frac{\lambda}{3}}+1-\sqrt{\frac{\lambda}{3}}-\lambda \cdot \frac{1}{2} \cdot \frac{1}{3} \cdot \sqrt{\frac{3}{\lambda}}=0 \\& \therefore \lambda=3 \\& \therefore d^*=1\end{aligned}$$
> (2): Dualizing $x \geqslant 0$ and $x \geqslant 1$
> $$d^*=\max _{\lambda_1, \lambda_2 \geq 0} \min _x x^3+\lambda_1(-x)+\lambda_2(1-x)$$
> For $\min _x x^3+\lambda_1(-x)+\lambda_2(1-x)$
> Set $\nabla_x L(x, \vec{\lambda})=0 \Rightarrow 3 x^2-\lambda_1-\lambda_2=0 \Rightarrow x= \pm \sqrt{\frac{\lambda_1+\lambda_2}{3}}$
> $$\nabla_x^2 L(x, \vec{\lambda})=6 x$$
> This imply $x^*=\sqrt{\frac{\lambda_1+\lambda_2}{3}}$
> $$\therefore g(\vec{\lambda})=\left(\frac{\lambda_1+\lambda_2}{3}\right)^{\frac{3}{2}}-\lambda_1 \sqrt{\frac{\lambda_1+\lambda_2}{3}}+\lambda_2\left(1-\sqrt{\frac{\lambda_1+\lambda_2}{3}}\right)$$
> $\because g$ is concave
> $$\begin{aligned}& \therefore \nabla \rightarrow g\left(x_2\right)=\left[\begin{array}{l}\frac{3}{2} \cdot \frac{1}{3} \cdot \sqrt{\frac{\lambda_1+\lambda_2}{3}}-\sqrt{\frac{\lambda_{1+2}+\lambda_2}{3}}-\frac{1}{6} \lambda_1 \sqrt{\frac{3}{\lambda_1+\lambda_2}}-\frac{1}{6} \lambda_2 \sqrt{\frac{3}{\lambda_1+\lambda_2}} \\\frac{3}{2} \cdot \frac{1}{3} \sqrt{\frac{\lambda_1+\lambda_2}{3}}-\frac{1}{6} \lambda_1 \sqrt{\frac{3}{\lambda_1+\lambda_2}}+1-\sqrt{\frac{\lambda_1+\lambda_2}{3}}-\frac{\lambda_2}{6} \lambda_2 \sqrt{\frac{3}{\lambda_1+\lambda_2}}\end{array}\right]=\left[\begin{array}{l}0 \\0\end{array}\right] \\& =\left[\begin{array}{l}-\frac{1}{2} \sqrt{\frac{\lambda_1+\lambda_2}{3}}-\frac{1}{6} \sqrt{3\left(\lambda_1+\lambda_2\right)} \\-\frac{1}{2} \sqrt{\frac{\lambda_1+\lambda_2}{3}}+1-\frac{1}{6} \sqrt{3\left(\lambda_1+\lambda_2\right)}\end{array}\right]=\left[\begin{array}{l}0 \\0\end{array}\right] \\& =\left[\begin{array}{c}-\frac{\sqrt{3}}{3} \sqrt{x_1+\lambda_2} \\1-\frac{\sqrt{3}}{3} \sqrt{\lambda_1+\lambda_2}\end{array}\right]=\left[\begin{array}{l}0 \\0\end{array}\right] \\&\end{aligned}$$
> $\therefore$ No solution
> Now checking the boundary
> (1):$$
> \begin{aligned} g(\vec{\lambda})=\left(\frac{\lambda_2}{3}\right)^{\frac{3}{2}}+\lambda_2-\lambda_2 \sqrt{\frac{\lambda_2}{3}} \\& \nabla g(\vec{\lambda})=-\sqrt{\frac{\lambda_2}{3}+1}=0 \\& \Rightarrow \lambda_2=3, d=1\end{aligned}$$
> (2):$$\text { (2): } \begin{aligned}& \lambda_2=0, g(\vec{\lambda})=\left(\frac{\lambda_1}{3}\right)^{\frac{3}{2}}-\lambda_1 \sqrt{\frac{\lambda_1}{3}} \\& \Rightarrow g(\vec{\lambda})=-\sqrt{\frac{\lambda_1}{3}}=0 \\& \Rightarrow \lambda_1=0, d=0 \\& \therefore d^*=1\end{aligned}$$


### Example 3: Quadratic Programming
> [!example] Disc10 P1 Fa22
> ![](Lagrangian_Duality_Theory.assets/image-20231119172628183.png)![](Lagrangian_Duality_Theory.assets/image-20231119172647795.png)![](Lagrangian_Duality_Theory.assets/image-20231119172653053.png)![](Lagrangian_Duality_Theory.assets/image-20231119172657944.png)![](Lagrangian_Duality_Theory.assets/image-20231119172703059.png)![](Lagrangian_Duality_Theory.assets/image-20231119172710081.png)
> **Notes:**
> We should see that when we are dualizing, we can choose to partial dualize the constraint, but when using KKT, we have to use all the constraints.



## Problem Transformations - Relaxing Affine Constraints
> [!example] Minimizing a Sum of Logarithms - EECS127 Fa22 HW09 P5
> ![](Lagrangian_Duality_Theory.assets/image-20231129100612169.png)


### Equivalent Problem
> [!tech] Equivalent Problem
> ![](Lagrangian_Duality_Theory.assets/image-20231129100758985.png)


### Relaxing Constraints
> [!tech] Relaxing Constraints
> ![](Lagrangian_Duality_Theory.assets/image-20231129100824276.png)![](Lagrangian_Duality_Theory.assets/image-20231129100830080.png)
> We want to show that:$$
> \begin{aligned}p^* r= & \min _{\vec{x} \in R^n} \sum_{i=1}^n-\alpha_i \log \left(x_i\right) \\& \text { s.t } \vec{x} \geqslant 0, \quad 1^{\top} \vec{x} \leqslant C\end{aligned}$$has the same solutions as the original minimization problem:$$\begin{aligned}P_{\text {min }}^*= & \min _{\vec{x} \in \mathbb{R}^{-}} \sum_{i=1}^n-\alpha_i \log \left(x_i\right) \\& \text { s.t. } \quad \vec{x} \geq 0,1^{\top} \vec{x}=c\end{aligned}$$
> We first prove that $p_{\text {min }}^*=p^*_{r}$ :
> 
> Since the relaxed optimization problem has a larger feasible set than the original one, we are safe to conclude that $p^*_r \leqslant p^*_\min$.
> 
> Now we just need to show $p^*_r \geqslant p^*_{min}$ .
> 
> Suppose for the sale of contradiction, $\vec{x}^r$ is an optimal solution to the relaxed minimization problem such that $p^*{ }_r<p^*_{min}$.
> 
> Then $I^{\top} \vec{x}^r \leqslant C$ and $\sum_{i=1}^n-\alpha_i \log \left(x_i^r\right)=p^*_r$.
> 
> - If $\vec{x}^r$ is feasible for the original problem, then $1^{\top} \vec{x}^r=c$ and $\sum_{i=1}^n-\alpha_i \log \left(x_i^r\right)=p^* r<p_{\text {min }}$, which is a contradiction to the definition of $P_{\text {min }}^*$.
> - If $\vec{x}^r$ is nt feasible for the original problem, since $1^{\top} \vec{x}^r \leq C$, we know that $1^{\top} \vec{x}^r<C$. 
> 
> Under this case, we can construct the vector:
> $$\vec{x}^*=\left[\begin{array}{c} \\c-1^{\top} \vec{x}^r+x_1^r \\x_2^r \\\vdots \\x_n^r\end{array}\right]$$
> which is feasible for the original problem, since$$\begin{aligned}
> 1^{\top} \vec{x}^*=c-1^{\top} \vec{x}^r+1^{\top} \vec{x}^r=c & \\
> \text { But } \sum_{i=1}^n-\alpha_i \log \left(x_i^*\right) & =-\alpha_1 \log \left(c-1^{\top} \vec{x}^r+x_1^r\right)+\sum_{i=2}^n-\alpha_i \log \left(x_i^r\right) \\
> & <-\alpha_1 \log \left(x_1^r\right)+\sum_{i=2}^n-\alpha_i \log \left(x_i^r\right) \\
> & =\sum_{i=1}^n-\alpha_i \log \left(x_i^r\right) \\
> & =p^*_r
> \end{aligned}$$
> 
> This implies that $p^*_{\min} \leq \sum_{i=1}^n-\alpha_i \log \left(x_i^*\right)<p^*_r$, which is a contradiction.
> $\therefore$ We conduce that $p_r^* \geqslant p^* \min$ and thus $p^*_r=p_{\text {min }}^*$.
> 
> Now we aim to show that the original problem and relaxed problem have the same set of solution.
> 
> Suppose $\vec{x}^r$ is an optimal solution for relaxed problem, then $\sum_{i=1}^n-\alpha_i \log \left(x_i^r\right)=p_r^*$ and $1^{\top} \vec{x}^r \leq c, x_i^r \geq 0 \forall i$.
>  
> - If $\vec{x}$ is infeasible for the original problem, then $\mathcal{1}^{\top} \vec{x}^r<c$(since it has to satisfy $\mathcal{1}^{\top} \vec{x}^r\neq c$ and $\mathcal{1}^{\top} \vec{x}^r\leq c$), we construct the same solution vector as above and could find that $p^*_{min}<p^*_r$, a contradiction to $p^*_r=p^*_{min}$that we hove proved. $\therefore \vec{x}$ is feasible for the original problem.
> 
> - Now suppose $\vec{x}^*$ is an optimal solution for original problem, we have $\sum_{i=1}^n-\alpha_i \log \left(x_i^*\right)=p^*_{min}$  and $1^{\top} \vec{x}^*=c$. $\because 1^{\top} \vec{x}^*=c \Rightarrow 1^{\top} \vec{x}^* \leq c, \therefore \vec{x}^*$ is feasible for the relaxed problem and we know that $\vec{x}^*$ is also optimal since $p^*_r=p^*_{min}$.
> 
> ![](Lagrangian_Duality_Theory.assets/image-20231214211835100.png)




### Lagrangian Function
> [!example]
> ![](Lagrangian_Duality_Theory.assets/image-20231129110211118.png)


### Finding Dual Function
> [!important]
> ![](Lagrangian_Duality_Theory.assets/image-20231129111638323.png)![](Lagrangian_Duality_Theory.assets/image-20231129111644871.png)


### Establishing Strong Duality
> [!example]
> ![](Lagrangian_Duality_Theory.assets/image-20231129112530491.png)


### Using Strong Duality to Recover Primal Solutions
> [!example]
> ![](Lagrangian_Duality_Theory.assets/image-20231129113506899.png)



## Summary
> [!summary]
> ![](Lagrangian_Duality_Theory.assets/image-20231119114301278.png)


# Code Experiments
## Experiment 1: Comparison between Primal and Dual - Linear Program
> [!example] HW09 Fa22 P3 
> ![](Lagrangian_Duality_Theory.assets/image-20231119203053954.png)![](Lagrangian_Duality_Theory.assets/image-20231119202959122.png)![](Lagrangian_Duality_Theory.assets/image-20231119203017151.png)![](Lagrangian_Duality_Theory.assets/image-20231119203023836.png)![](Lagrangian_Duality_Theory.assets/image-20231119203246026.png)


## Experiment 2: Minimzing Exponentials
> [!example] HW09 Fa22 P3
> ![](Lagrangian_Duality_Theory.assets/image-20231119203331714.png)![](Lagrangian_Duality_Theory.assets/image-20231119203552389.png)![](Lagrangian_Duality_Theory.assets/image-20231119203705343.png)![](Lagrangian_Duality_Theory.assets/image-20231119203714897.png)![](Lagrangian_Duality_Theory.assets/image-20231119203729318.png)![](Lagrangian_Duality_Theory.assets/image-20231119203804480.png)



# Using Lagrangian to Solve Eigenvalue Problem
## Maximum Eigenvalue Problems
> 

















