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
> 其中:
> 1. $\lambda_i>0$ 的时候，表明我们的最优解在边界上。
> 2. $\lambda_i=0$的时候，表明我们的最优解在Critical Points。 

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



## Practical Examples
> More examples see [Methodology on Optimization](Methodology%20on%20Optimization.md)
### Complementary Slackness
> [!example] Disc 10 P2 Fa22
> ![](Lagrangian_Duality_Theory.assets/image-20231119172755070.png)![](Lagrangian_Duality_Theory.assets/image-20231119172759663.png)![](Lagrangian_Duality_Theory.assets/image-20231119172811079.png)![](Lagrangian_Duality_Theory.assets/image-20231119172816337.png)![](Lagrangian_Duality_Theory.assets/image-20231119172821277.png)





# Dual of the Dual
## Linear Program
> [!important]
> ![](Lagrangian_Duality_Theory.assets/image-20231128165002827.png)![](Lagrangian_Duality_Theory.assets/image-20231128165009509.png)![](Lagrangian_Duality_Theory.assets/image-20231128165028738.png)![](Lagrangian_Duality_Theory.assets/image-20231128165035300.png)


# Duality of Norms
## Dual Norm - Functional Analysis
> [!def]
> In functional analysis, the dual norm is a measure of size for a continuous linear function defined on a normed vector space.
> ![](Lagrangian_Duality_Theory.assets/image-20240227141757525.png)


## Duality of L1 and L-inf
> [!example] EECS127 Fa22 Disc11 P1
> ![](Lagrangian_Duality_Theory.assets/image-20231217220848002.png)![](Lagrangian_Duality_Theory.assets/image-20231217220917792.png)![](Lagrangian_Duality_Theory.assets/image-20231217221029649.png)![](Lagrangian_Duality_Theory.assets/image-20231217221715742.png)
> This problem makes very clever use of the sign function.




# Code Experiments
## Experiment 1: Comparison between Primal and Dual - Linear Program
> [!example] HW09 Fa22 P3 
> ![](Lagrangian_Duality_Theory.assets/image-20231119203053954.png)![](Lagrangian_Duality_Theory.assets/image-20231119202959122.png)![](Lagrangian_Duality_Theory.assets/image-20231119203017151.png)![](Lagrangian_Duality_Theory.assets/image-20231119203023836.png)![](Lagrangian_Duality_Theory.assets/image-20231119203246026.png)


## Experiment 2: Minimzing Exponentials
> [!example] HW09 Fa22 P3
> ![](Lagrangian_Duality_Theory.assets/image-20231119203331714.png)![](Lagrangian_Duality_Theory.assets/image-20231119203552389.png)![](Lagrangian_Duality_Theory.assets/image-20231119203705343.png)![](Lagrangian_Duality_Theory.assets/image-20231119203714897.png)![](Lagrangian_Duality_Theory.assets/image-20231119203729318.png)![](Lagrangian_Duality_Theory.assets/image-20231119203804480.png)


 














