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




# Hoeffding/Chernoff Bounds
## Hoeffding's Lemma
> [!lemma]
> ![](Concentration_Inequalities&MGF.assets/image-20240126220124239.png)

> [!proof]
> ![](Concentration_Inequalities&MGF.assets/image-20240126220132498.png)


## Hoeffding's for Sub-Gaussian
### Lemma 
> [!lemma]
> ![](Concentration_Inequalities&MGF.assets/8c2998f687b36fa43c1c4f80a8dffad8_MD5.jpeg)

> [!proof]
> ![](Concentration_Inequalities&MGF.assets/8b69bb2d9c227a946ddd96180e3fda1b_MD5.jpeg)![](Concentration_Inequalities&MGF.assets/1b553171512721d192c3dbe756cdf396_MD5.jpeg)![](Concentration_Inequalities&MGF.assets/f2787b5c5b19c3e612d00a879d73f272_MD5.jpeg)


### Inequality
> [!important]
> ![](Concentration_Inequalities&MGF.assets/f358015da82ab57627963cf73e5a7341_MD5.jpeg)

> [!proof]
> ![](Concentration_Inequalities&MGF.assets/2b9b991c89c61033c51bd26111d21a2e_MD5.jpeg)![](Concentration_Inequalities&MGF.assets/7fbe0dfe8a3f95ce21d727fb6b9de8e5_MD5.jpeg)![](Concentration_Inequalities&MGF.assets/7a6680989ccb94eec64c68b66de19160_MD5.jpeg)



## Hoeffding Bound
> [!def]
> ![](Concentration_Inequalities&MGF.assets/image-20240315224137932.png)








# Chernoff Bounds
## Chernoff Bound for Bounded R.V.
> [!def]
> ![](Concentration_Inequalities&MGF.assets/image-20240315224049086.png)![](Concentration_Inequalities&MGF.assets/image-20240315224116039.png)![](Concentration_Inequalities&MGF.assets/image-20240315224121063.png)
> Alternative Representation is:
> 
> ![](Concentration_Inequalities&MGF.assets/image-20240316123440549.png)





## Chernoff Bounds for Bernoulli Sum
> [!def]
> ![](Concentration_Inequalities&MGF.assets/image-20240316122806791.png)

> [!proof] Proof
> ![](Concentration_Inequalities&MGF.assets/image-20240316123350271.png)![](Concentration_Inequalities&MGF.assets/image-20240316123402131.png)![](Concentration_Inequalities&MGF.assets/image-20240316123408548.png)![](Concentration_Inequalities&MGF.assets/image-20240316123413420.png)

> [!example] Coin Tossing
> ![](Concentration_Inequalities&MGF.assets/image-20240316123007440.png)



## Chernoff Bounds For Sub-Gaussian
> [!def]
> If $X$ is $\sigma^2$-[sub-gaussian](../../../../Mathematics/NYU_Master_Program/DS-GA-1005/Sub-Gaussian.md) 
> ![](Concentration_Inequalities&MGF.assets/93e93519470edff48faf200cbdecfa20_MD5.jpeg)![](Concentration_Inequalities&MGF.assets/bdb32d9ebd549e569cca28e63bc6e9e7_MD5.jpeg)





