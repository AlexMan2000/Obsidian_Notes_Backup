# MVG Basics
## What makes a MVG
> [!important]
> ![](1_Multivariable_Gaussian.assets/image-20240202202846309.png)

> [!example] Check MVG
> ![](1_Multivariable_Gaussian.assets/image-20240202202945458.png)![](1_Multivariable_Gaussian.assets/image-20240202204448181.png)![](1_Multivariable_Gaussian.assets/image-20240202204459308.png)


## Correlatedness and  Independence
> [!important]
> Generally, for two Gaussian RVs $X_1$ and $X_2$, we have:
> 1. If $X_1$ and $X_2$ are jointly gaussian, then $Cov(X_1,X_2)=0\implies X_1\perp X_2$ 
> 2. If $X_1$ and $X_2$ are both gaussian but **not jointly gaussian**, then $Cov(X_1,X_2)=0$ doesn't imply $X_1\perp X_2$, as is shown in the example 4 above.
> 
> ![](1_Multivariable_Gaussian.assets/image-20240202204911653.png)


## Linear Transformation of Random Vector
> [!important]
> Suppose $Z=VX$ where $V\in \mathbb{R}^{2\times 2}$ and $X\sim \mathcal{N}(\vec{0},I_2)$, then we have: $E[Z]=0$ and $\Sigma_Z=V\Sigma_XV^{\top}$ and the derivations are as follows:
> ![](1_Multivariable_Gaussian.assets/image-20240202205844546.png)
> 
> Note that this is true for all random vectors.

> [!example] Application
> ![](1_Multivariable_Gaussian.assets/image-20240202205924738.png)



# Conditional Gaussian
## 2-d Case
> [!important]
> Suppose we have jointly gaussian random vector $\begin{bmatrix} Z_1&Z_2\end{bmatrix}^{\top}\sim\mathcal{N}(\begin{bmatrix} \mu_1\\\mu_2\end{bmatrix},\Sigma_Z)$ where $\Sigma_Z=\begin{bmatrix} \Sigma_{11}&\Sigma_{12}\\\Sigma_{21}&\Sigma_{22}\end{bmatrix}=\begin{bmatrix} \sigma_1^2&\rho\sigma_1\sigma_2\\\rho\sigma_1\sigma_2&\sigma_2^2\end{bmatrix}$, then we have:
> $$Z_1|Z_2=z_2\sim\mathcal{N}(\mu_1+\rho\sigma_1(\frac{z_2-\mu_2}{\sigma_2}),(1-\rho^2)\cdot\sigma_1^2)$$
> 
> Several Observations we made:
> 1. The posterior variance $\sigma_{Z_1|Z_2}^2\leq\sigma_{Z_1}^2$ is smaller then prior variance, meaning that data makes us more certain where the parameter lies.

> [!proof] Proof by algebra
> ![](1_Multivariable_Gaussian.assets/image-20240202210938022.png)![](1_Multivariable_Gaussian.assets/image-20240202211000153.png)

> [!proof] Proof by Linear Algebra(Zero Mean Case)
> ![](1_Multivariable_Gaussian.assets/image-20240202210904662.png)![](1_Multivariable_Gaussian.assets/image-20240202210909207.png)
> Note that the last step follows from dividing by the marginal pdf of $Z_2=z_2$
> 
> **Remarks:**
> 1. Recall that $\Sigma_{11}-\frac{\Sigma_{12}^2}{\Sigma_{22}}$ is actually the schur complement of the matrix $\Sigma_{22}$ in matrix $\Sigma_Z$.




## General Case
> [!important]
> Preliminary:
> 
> ![](1_Multivariable_Gaussian.assets/image-20240203111528178.png)![](1_Multivariable_Gaussian.assets/image-20240202192028129.png)
> Derivations:
> 
> ![](1_Multivariable_Gaussian.assets/image-20240202191958620.png)![](1_Multivariable_Gaussian.assets/image-20240202192007789.png)![](1_Multivariable_Gaussian.assets/image-20240202192014027.png)



# Bayes Rule for Gaussians


