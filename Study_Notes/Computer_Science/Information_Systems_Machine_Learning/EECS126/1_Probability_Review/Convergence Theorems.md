# Almost Sure Convergence
## Motivation
> [!motiv] Motivation
> Suppose we have a probability space $(\Omega,\mathcal{F},\mathbb{P})$ and a random variable $X:\Omega\to \mathbb{R}$, then almost sure convergence tries to describe whether for all possible discrete outcome $s\in \Omega$ or continuous one$[a,b]\in \Omega$, we have $\lim_{n\to \infty}X_n(s)=X(s)$. (For simplicity we consider the discrete case).
> Remarks:
> 1. $X_n(s)$ is a random sequence when the input outcome is $s$.
> 2. $X_n(s_i)$ is usually different for different $s_{i}$.

## Definition
> [!def]
> We say that a random sequence $(X_n)_{n\in \mathbb{N}}$ converges almost surely if:
> ![](Convergence%20Theorems.assets/image-20231109173519754.png)



## Criterion Theorem
> [!motiv] Motivation
> Sometimes, going straight from the definition to determine whether a random sequence converge almost surely is difficult. 
> Alternatively, we can utilize the theorem below to determine a.s. convergence:


### Sufficient Condition
> [!thm]
> ![](Convergence%20Theorems.assets/image-20231109180656666.png)

> [!example]
> ![](Convergence%20Theorems.assets/image-20231109181402769.png)


### Sufficient and Necessary Condition
> [!thm]
> ![](Convergence%20Theorems.assets/image-20231109180714274.png)

> [!example]
> 



## Examples
### Discrete Sample Space - Not Convergent
> [!example]
> https://www.probabilitycourse.com/chapter7/7_2_7_almost_sure_convergence.php
> ![](Convergence%20Theorems.assets/image-20231109173636369.png)


### Continuous Sample Space - Convergent
> [!example]
> ![](Convergence%20Theorems.assets/image-20231109180010709.png)






# Convergence in Probability



# Convergence in Distribution



# Convergence in Expectation