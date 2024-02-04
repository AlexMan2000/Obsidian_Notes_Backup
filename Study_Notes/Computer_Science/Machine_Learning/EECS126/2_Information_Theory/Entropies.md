# Entropy of R.V.
## Definition
> [!def]
> ![](Entropies.assets/image-20240127163138806.png)![](Entropies.assets/image-20240127163613712.png)
> Generally, the base of the logarithm is 2 and the entropy has units ’bits’. The expected number of bits needed to express the information in X is a natural choice to measure its uncertainty. It turns out that the expected number of bits required to describe the random variable is roughly the entropy H(X).

> [!property]
> ![](Entropies.assets/image-20240127163738370.png)
> We verify that $(xlog(x))''=\frac{1}{x}$. If we let $x=p_X(x)$, then $f(p_X(x))$ is convex in $p_X(x)$, which means that $H(X)$ is concave in $p_X(x)$ since $p_X(x)log\frac{1}{p_X(x)}=-p_X(x)logp_X(x)$.
> 
> ![](Entropies.assets/image-20240127164007074.png)


# Joint/Conditional Entropy
> [!def]
> ![](Entropies.assets/image-20240127164152365.png)

> [!property]
> ![](Entropies.assets/image-20240127164204642.png)![](Entropies.assets/image-20240127164235670.png)
> **Proof of 2:**
> If $X$ and $Y$ are independent, then$$\begin{aligned}H(Y \mid X) & =\sum_X p_X(x) \sum_y p_{Y \mid X}(y \mid x) \log \frac{1}{p_{Y \mid X}(y \mid x)} \\& =\sum_x p_X(x) \sum_y p_Y(y) \log \frac{1}{p_Y(y)} \\& =\sum_x p_X(x) H(Y) \\& =H(Y) \sum\limits_{x} p_X(x) \\& =H(Y)\end{aligned}$$
> ![](Entropies.assets/image-20240127164546492.png)



# Relative Entropy - KL Divergence
## Distance Definition
> [!def]
> ![](Entropies.assets/image-20240202112403935.png)
> KL Divergence measures the distance between two distributions. Above is the definition of KL Divergence for two continuous distributions.
> 
> When two distributions are the same, we expect the KL Divergence to be zero, otherwise it's bigger than zero.
> 
> The definition is similar for two discrete distributions:
> ![](Entropies.assets/image-20240202112541681.png)


## Variational Definition
> [!def]
> This definition is called Donsker Varahdan variational formula:
> ![](Entropies.assets/image-20240202112816647.png)



## Properties
> [!property] Nonnegativity
> ![](Entropies.assets/image-20240202112617670.png)




# Mutual Information
> [!def]
> ![](Entropies.assets/image-20240127164635594.png)![](Entropies.assets/image-20240127164640526.png)




# Source Coding






