# Laplace Transformation
## Step and Delta Function



## Definition
> [!def]
> ![](Concentration_Inequalities&MGF.assets/image-20240127115312776.png)![](Concentration_Inequalities&MGF.assets/image-20240127115349811.png)



## Computing Examples
> [!example]
> 



# Moment Generating Function
## Definition
> [!def]
> ![](Concentration_Inequalities&MGF.assets/image-20240127150840198.png)

## Examples
> [!example]
> ![](Concentration_Inequalities&MGF.assets/image-20240127150916261.png)






# Basic Bounds
## Markov Bound
> [!def]
> ![](Concentration_Inequalities&MGF.assets/image-20240126212651711.png)


## Chebyshev's Bound
> [!def]
> ![](Concentration_Inequalities&MGF.assets/image-20240126212714417.png)![](Concentration_Inequalities&MGF.assets/image-20240126212724162.png)




# Moment Bounds
## Moment Methods
> [!def]
> ![](Concentration_Inequalities&MGF.assets/image-20240204112004630.png)![](Concentration_Inequalities&MGF.assets/image-20240126212941709.png)

> [!proof] Proof: First Moment

> [!proof] Proof: Second Moment



## Higher-Order Markov Bounds
> [!important]
> ![](Concentration_Inequalities&MGF.assets/image-20240204112603591.png)![](Concentration_Inequalities&MGF.assets/image-20240204112610570.png)




## Chernoff Moment Bounds
> [!def]
> ![](Concentration_Inequalities&MGF.assets/image-20240126212536464.png)![](Concentration_Inequalities&MGF.assets/image-20240126220850345.png)![](Concentration_Inequalities&MGF.assets/image-20240126220854410.png)

> [!example] Chernoff Mement Bound for Gaussian
> ![](Concentration_Inequalities&MGF.assets/image-20240127151024751.png)![](Concentration_Inequalities&MGF.assets/image-20240127151141756.png)
> **Derivations for 9.2:** 
> 
> Suppose we know the MGF of $X$, which is $M_x(s)$, then by markov inequality we have:
> $$P\left(e^{-s x} \geqslant e^{s k}\right) \leqslant \frac{E\left[e^{-s x}\right]}{e^{s k}}$$
> $\because f(x)=e^x$ is monotonically increasing.
> 
> $$\begin{aligned}\therefore P(x \leqslant-k) & \leqslant \frac{E\left[e^{-s x}\right]}{e^{s k}} \\& =\frac{M_x(-s)}{e^{s k}} \\& =\frac{e^{\frac{1}{2} s^2}}{e^{s k}}\end{aligned}$$
> 
> Minimizing $g(s)=e^{\frac{1}{2} s^2-k \cdot s}$ we get $g^*(s)=e^{-\frac{1}{2} k^2}$
> $$\begin{aligned}\therefore P(X \leq-k) & \leq e^{-\frac{1}{2} k^2} \\\therefore P(|X| \geqslant k) & =P(X \geqslant k)+P(X \leq-k) \\& =2 e^{-\frac{1}{2} k^2}\end{aligned}$$








# Hoeffding Bounds
## Hoeffding's Lemma
> [!lemma]
> ![](Concentration_Inequalities&MGF.assets/image-20240126220124239.png)

> [!proof]
> ![](Concentration_Inequalities&MGF.assets/image-20240126220132498.png)



