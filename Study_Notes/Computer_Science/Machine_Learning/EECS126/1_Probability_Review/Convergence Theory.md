# Types of Convergence 
## Convergence Almost Surely
### Motivation
> [!motiv] Motivation
> Suppose we have a probability space $(\Omega,\mathcal{F},\mathbb{P})$ and a random variable $X:\Omega\to \mathbb{R}$, then almost sure convergence tries to describe whether for all possible discrete outcome $s\in \Omega$ or continuous one$[a,b]\in \Omega$, we have $\lim_{n\to \infty}X_n(s)=X(s)$. (For simplicity we consider the discrete case).
> **Remarks:**
> 1. $X_n(s)$ is a random sequence when the input outcome is $s$.
> 2. $X_n(s_i)$ is usually different for different $s_{i}$.
> 
> **Note:**
> `Convergence almost surely` is also called `Convergence with Probablity 1`

### Main Theorem
> [!thm] 
> We say that a random sequence $(X_n)_{n\in \mathbb{N}}$ converges almost surely if:
> ![](Convergence%20Theory.assets/image-20231109173519754.png)



### Criterion Theorem
> [!motiv] Motivation
> Sometimes, going straight from the definition to determine whether a random sequence converge almost surely is difficult. 
> Alternatively, we can utilize the theorem below to determine a.s. convergence:


#### Sufficient Condition
> [!thm]
> ![](Convergence%20Theory.assets/image-20231109180656666.png)

> [!example]
> ![](Convergence%20Theory.assets/image-20231109181402769.png)


#### Sufficient and Necessary Condition
> [!thm]
> ![](Convergence%20Theory.assets/image-20231109180714274.png)

> [!example]
> ![](Convergence%20Theory.assets/image-20231109222948150.png)![](Convergence%20Theory.assets/image-20231109222953016.png)


### SLLN
> [!important]
> ![](Convergence%20Theory.assets/image-20231110102910609.png)




### Examples
#### Discrete Sample Space - Not Convergent
> [!example]
> https://www.probabilitycourse.com/chapter7/7_2_7_almost_sure_convergence.php
> ![](Convergence%20Theory.assets/image-20231109173636369.png)


#### Continuous Sample Space - Convergent
> [!example]
> ![](Convergence%20Theory.assets/image-20231109180010709.png)![](Convergence%20Theory.assets/image-20231109222932099.png)




## Convergence in Probability
### Motivation
> [!motiv] Motivation
> ![](Convergence%20Theory.assets/image-20231110102423742.png)
> 总的来说，`Converge Almost Surely`是一个比`Convergence In Probability`更强的条件。
> - 因为对于`Convergence in Probability`来说，他只能保证事件$|X_n-X|>\epsilon$的概率趋近于零，而$0<|X_n-X|<\epsilon$这个事件仍然会发生, 也就是说只要时间足够长我们总能观测到$X_n$偏离$X$的事件。
> - 但是对于`Convergence Almost Sure`来说，他能保证事件$X_n\neq X$ 的概率为零，也就是只要时间足够长，$X_n$就完全不会偏离$X$。




### Main Theorem
> [!thm]
> In particular, for a sequence $X_1, X_2, X_3, \cdots$ to converge to a random variable $X$, we must have that $P\left(\left|X_n-X\right| \geq \epsilon\right)$ goes to 0 as $n \rightarrow \infty$, for any $\epsilon>0$. To say that $X_n$ converges in probability to $X$, we write$$X_n \stackrel{p}{\rightarrow} X$$![](Convergence%20Theory.assets/image-20231109223821031.png)


### WLLN
> [!important]
> ![](Convergence%20Theory.assets/image-20231110103100145.png)


### Examples
#### P Convergence but not A.S. Convergence
> [!important]
> ![](Convergence%20Theory.assets/image-20231110103608173.png)




## Convergence in Distribution



## Convergence in Expectation




# Relationship Between Convergence
## a.s => p
> [!thm]
> ![](Convergence%20Theory.assets/image-20231109223356198.png)









# Continuous Mapping Theorem