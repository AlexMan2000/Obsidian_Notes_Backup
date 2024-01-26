# Indicator Variables
## Sample Without Replacement
> [!example] Sp23 Disc03 p2
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20240126130817625.png)![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20240126131627349.png)
> 



# Balls In Bins
## Big Theorem - Collision
> [!thm]
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109112905240.png)![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109113215353.png)
![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109112956789.png)

> [!proof] Chain Rule
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109113039659.png)![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109113117028.png)



## Applications 
### Birthday Problem
> [!important]
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109113237261.png)![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109113325234.png)


> [!example] Example - CS70 Fa20 Disc 12B P1
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109140901599.png)

> [!proof]
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109140926026.png)![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109140931116.png)






### CheckSum
> [!important]
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109113351889.png)







# Coupon Collector
## Big Theorem 1 - Missing Items
> [!thm]
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109113440537.png)

> [!proof]
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109113522875.png)![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109133756103.png)![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109133826173.png)



## Big Theorem 2 - Time to Collect Coupons
> [!thm]
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109133953132.png)
![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109133849812.png)



# Hashing
> [!motiv] Motivation
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109140520558.png)



## Union Bound
> [!important]
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109140539339.png)![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109140545489.png)





## Accurate Bound
> [!important]
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109140623710.png)![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109140637260.png)



# Loading Balancing
> [!motiv] Motivation
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109140720274.png)![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109141257791.png)







## Balls and Bins Perspective
### Motivation
> [!important]
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109141125631.png)


### Analysis
> [!important]
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109141548715.png)![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109141556094.png)![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109141607605.png)![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109141651949.png)![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109141658733.png)















> [!example] Example - CS70 Fa20 Disc12B P2
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109141016956.png)

> [!proof]
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109141023921.png)![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231109141028697.png)


# Conditional Probability
## Clustering Coefficients
> [!example]
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20231119215406310.png)






# Correlation
## Uncorrelatedness and Independence
> [!example] Fa23 Disc03 P1
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20240125223330143.png)![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20240125223337618.png)
> Note: Here there is a notion called Rademacher random variable, which is a type of discrete random variable that can take one of two values, typically +1 or -1 such that $P(X=1)=P(X=-1)=\frac{1}{2}$.
> 
> This kind of random variable is named after Hans Rademacher, a German mathematician known for his work in various areas of mathematics, including probability theory.



# Memoryless Property
## Minimum and Maximum of Exponentials
> [!example] Fa23 Disc03 P3
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20240126101349013.png)
> Recall that in order to show independence among two random variables $X$ and $Y$, we can use the following methods:
> 1. $P(X=x,Y=y)=P(X=x)P(Y=y),\forall x,y\in\mathbb{D}$, this is proving by Joint PDF.
> 2. $P(X\leq x,Y\leq y)=P(X\leq x)P(Y\leq y),\forall x,y\in\mathbb{D}$, this is proving by joint CDF.
> 
> Here, in order to prove the independence for continuous random variable, using the first method is difficult, since:
> 1. Iterating over all the continuous values is tedious.
> 2. We cannot further utilize the memoryless property of exponential distribution.
> 
> ![](Important%20Applications%20Of%20Basic%20Probability.assets/image-20240126101925885.png)
> There are some calculation details missing on $P(U\leq u)$ and $P(U-V\leq w)$, we will calculate them using conditional probability
> 
> To compute $P(U\leq u)$, we have to compute$P(U \leq u)=P(U  \left.\leqslant u, X_1<X_2\right)+P\left(U \leq u, X_2>X_1\right)$
> 
> $$\begin{aligned}P\left(U \leq u, X_1<X_2\right) & =P\left(X_1 \leq u, X_1<X_2\right) \\& =\int_0^u \int_{X_1}^{\infty} \lambda_1 e^{-\lambda_1 x_1} \lambda_2 e^{-\lambda_2 x_2} d x_2 d x_1 \\& =\left.\int_0^u \lambda_1 e^{-\lambda_1 x_1}\left(-e^{-\lambda_2 x_2}\right)\right|_{x_1} ^{\infty} d x_1 \\& =\int_0^u \lambda_1 e^{-\lambda_1 x_1} e^{-\lambda_2 x_1} d x_1 \\& =\left.\left(-\frac{\lambda_1}{\lambda_1+\lambda_2} e^{-\left(\lambda_1+\lambda_2\right) x_1}\right)\right|_0 ^u \\& =\frac{\lambda_1}{\lambda_1+\lambda_2}-\frac{\lambda_1}{\lambda_1+\lambda_2} e^{-\left(\lambda_1+\lambda_2\right) u}\end{aligned}$$
> By symmetry, we have $P\left(U \leq u, X_2<X_1\right) =P\left(X_1 \leq u, X_2<X_1\right)=\frac{\lambda_2}{\lambda_1+\lambda_2}-\frac{\lambda_2}{\lambda_1+\lambda_2} e^{-\left(\lambda_1+\lambda_2\right) x_1}$
> 
> Thus, we have $$P(U\leq u)=1- e^{-\left(\lambda_1+\lambda_2\right) u}$$ 
> It may be tempting to compute $P(U\leq u)$ as:
> 
> $$\begin{aligned}P(U\leq u)&=P(U\leq u|X_1<X_2)P(X_1<X_2)+P(U\leq u|X_1>X_2)P(X_1>X_2)\\&=P(X_{1}\leq u)\cdot\frac{\lambda_1}{\lambda_1+\lambda_2}+P(X_{2}\leq u)\cdot\frac{\lambda_2}{\lambda_1+\lambda_2}\\&=(1-exp(-\lambda_1 u))\cdot\frac{\lambda_1}{\lambda_1+\lambda_2}+(1-exp(-\lambda_2 u))\cdot\frac{\lambda_2}{\lambda_1+\lambda_2}\end{aligned}$$  
> 
> But such calculation is flawed in that $P(U\leq u|X_1<X_2)$ is different from $P(X_1\leq u)$ because the event $\{X_1<X_2\}$ is not independent of $X_1\leq u$ .
> 
> Now we move on:
> $$\begin{aligned}P(V-U\leq w)&=P(V-U\leq w|X_1<X_2)P(X_1<X_2)+P(V-U\leq w|X_1>X_2)P(X_1>X_2)\\&=P(X_{2}-X_1\leq w\mid X_2>X_1)\cdot\frac{\lambda_1}{\lambda_1+\lambda_2}+P(X_{1}-X_2\leq w \mid X_1>X_2)\cdot\frac{\lambda_2}{\lambda_1+\lambda_2}\\&=P(X_{2}\leq w)\cdot\frac{\lambda_1}{\lambda_1+\lambda_2}+P(X_{1}\leq w )\cdot\frac{\lambda_2}{\lambda_1+\lambda_2}\\&=(1-exp(-\lambda_2 w))\cdot\frac{\lambda_1}{\lambda_1+\lambda_2}+(1-exp(-\lambda_1 w))\cdot\frac{\lambda_2}{\lambda_1+\lambda_2} \end{aligned}$$
> Here the probability of the event $\{X_1<X_2\}$ can quickly be obtained by modeling this as an arrival process, where $X_1$ and $X_2$ can be interpreted as the first arrival time of the merge of two poisson process with parameter $\lambda_1$ and $\lambda_2$, so the probability of the first arrival to be from the first poisson process is $\frac{\lambda_1}{\lambda_1+\lambda_2}$, the same logic applies to the probability of the event $\{X_1>X_2\}$.
>  
> Finally, we find that $P(U\leq u,V-U\leq w)=P(U\leq u)P(V-U\leq w)$, which indicates that $U$ and $V-U$ are independent.








