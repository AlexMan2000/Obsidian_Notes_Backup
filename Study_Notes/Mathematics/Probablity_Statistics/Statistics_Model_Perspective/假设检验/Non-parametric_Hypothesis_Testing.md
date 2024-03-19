# 1 Permutation Test
## Testing Setup
> [!def]
> Suppose we have two groups of data. $D_A$ and $D_B$, and we want to compare the distribution(parametrized by mean) between them. A typical choice of null/alt hypothesis is:
> $$\mathcal{H}_0:\mu_{A}=\mu_{B}\quad \mathcal{H}_A:\mu_{A}\neq \mu_{B}$$
> 
> The idea of permutation test is that, **if we assume that the null hypothesis is true, then the labeling of the data should be meaningless since they have the same distribution.** So we could permute the data points so that the data points in each group is changing across different permutations and we can calculate a lot of $m(D_A)-m(D_B)$ and compare our test statistics with it to determine if the test statistic is too extreme for null hypothesis.

> [!example] 
> ![](Non-parametric_Hypothesis_Testing.assets/image-20240315123612386.png)![](Non-parametric_Hypothesis_Testing.assets/image-20240315123818511.png)


## P-Value of the Test
> [!def]
> ![](Non-parametric_Hypothesis_Testing.assets/image-20240315175410691.png)![](Non-parametric_Hypothesis_Testing.assets/image-20240315175421700.png)


## Exchangeability
> [!property]
> ![](Non-parametric_Hypothesis_Testing.assets/image-20240315175823130.png)



## P-Value under exchangeability
> [!def]
> ![](Non-parametric_Hypothesis_Testing.assets/image-20240315180558178.png)![](Non-parametric_Hypothesis_Testing.assets/image-20240315180605542.png)![](Non-parametric_Hypothesis_Testing.assets/image-20240315180610741.png)





## Permutation Test via Monte Carlo Method
> [!def]
> ![](Non-parametric_Hypothesis_Testing.assets/image-20240315181146781.png)

  









# 2 Kolmogorov-Smirnov Test
> 不用任何离散化和参数化的估计，而仅仅依赖于`Empirical Distirbution`就可以检验一个数据集的分布。


## Test Settings
> ![image.png](./Non-parametric_Hypothesis_Testing.assets/20230302_1227369460.png)![image.png](./Non-parametric_Hypothesis_Testing.assets/20230302_1227362277.png)



## Test Statistics
### Formula
> ![image.png](./Non-parametric_Hypothesis_Testing.assets/20230302_1227367814.png)
> 本质上是`Maximum Deviation of` $F_n(x)$from $F_0(x)$  


### Distribution
> ![image.png](./Non-parametric_Hypothesis_Testing.assets/20230302_1227367683.png)

**Graphs**![image.png](./Non-parametric_Hypothesis_Testing.assets/20230302_1227361816.png)


## Two-Sample Test
> ![image.png](./Non-parametric_Hypothesis_Testing.assets/20230302_1227366813.png)![image.png](./Non-parametric_Hypothesis_Testing.assets/20230302_1227376229.png)

