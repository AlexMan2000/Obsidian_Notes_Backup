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

### Main Definition
> [!thm] 
> We say that a random sequence $(X_n)_{n\in \mathbb{N}}$ converges almost surely if:
> ![](Convergence_Theory.assets/image-20231109173519754.png)



### How to Show?
> [!motiv] Motivation
> Sometimes, going straight from the definition to determine whether a random sequence converge almost surely is difficult. 
> 
> Alternatively, we can utilize the theorem below to determine a.s. convergence:


#### Sufficient Condition
> [!thm]
> ![](Convergence_Theory.assets/image-20231109180656666.png)

> [!example]
> ![](Convergence_Theory.assets/image-20231109181402769.png)


#### Sufficient and Necessary Condition
> [!thm]
> ![](Convergence_Theory.assets/image-20231109180714274.png)

> [!example]
> ![](Convergence_Theory.assets/image-20231109222948150.png)![](Convergence_Theory.assets/image-20231109222953016.png)



#### Borel-Cantelli Lemma
> [!thm]
> ![](Convergence_Theory.assets/image-20240126154051288.png)



### Examples
#### SLLN
> [!important]
> ![](Convergence_Theory.assets/image-20231110102910609.png)![](Convergence_Theory.assets/image-20240126153933864.png)
> Borel-Cantelli Lemma is used to show strong law of large number. Proof see [Borel-Cantelli&Strong Law](Probability_Formulas_and_Theorems.md#Borel-Cantelli&Strong%20Law)



#### Discrete Sample Space - Not Convergent
> [!example]
> https://www.probabilitycourse.com/chapter7/7_2_7_almost_sure_convergence.php
> ![](Convergence_Theory.assets/image-20231109173636369.png)


#### Continuous Sample Space - Convergent
> [!example]
> ![](Convergence_Theory.assets/image-20231109180010709.png)![](Convergence_Theory.assets/image-20231109222932099.png)


## Convergence in Probability
### Motivation
> [!motiv] Motivation
> ![](Convergence_Theory.assets/image-20231110102423742.png)
> 总的来说，`Converge Almost Surely`是一个比`Convergence In Probability`更强的条件。
> - 因为对于`Convergence in Probability`来说，他只能保证事件$|X_n-X|>\epsilon$的概率趋近于零，而$0<|X_n-X|<\epsilon$这个事件仍然会发生, 也就是说只要时间足够长我们总能观测到$X_n$偏离$X$的事件。
> - 但是对于`Convergence Almost Sure`来说，他能保证事件$X_n\neq X$ 的概率为零，也就是只要时间足够长，$X_n$就完全不会偏离$X$。




### Main Theorem
> [!thm]
> In particular, for a sequence $X_1, X_2, X_3, \cdots$ to converge to a random variable $X$, we must have that $P\left(\left|X_n-X\right| \geq \epsilon\right)$ goes to 0 as $n \rightarrow \infty$, for any $\epsilon>0$. To say that $X_n$ converges in probability to $X$, we write$$X_n \stackrel{p}{\rightarrow} X$$![](Convergence_Theory.assets/image-20231109223821031.png)


### WLLN
> [!important]
> ![](Convergence_Theory.assets/image-20240127150434568.png)




### Examples
#### P Convergence but not A.S. Convergence
> [!important]
> ![](Convergence_Theory.assets/image-20240127155151342.png)
> Note that here we need $\lim_\limits{n\to \infty}P(|Y_n|>\epsilon)=0,\forall\epsilon>0$. If $\epsilon\in(0,1)$, then $P(|Y_n|>\epsilon)=P(Y_n=1)$. If $\epsilon>1$, then $P(|Y_n|>\epsilon)=0$.
> 
> In either case, we have convergence in probabilty.
> 
> ![](Convergence_Theory.assets/image-20231110103608173.png)


#### Uniform Distribution
> [!example] Uniform Distribution: Fa23 Disc05 P2
> ![](Convergence_Theory.assets/image-20240127161228451.png)
> Here when $\epsilon>1$, we have $P(|X_n|>\epsilon^{\frac{1}{n}})=0$. So we only need to focus on the cases where $\epsilon\in (0,1)$.
> 
> We want to test whether:$$\begin{aligned}\lim _{n \rightarrow \infty} P\left(\left|Y_n-0\right|>\varepsilon\right) & =0 \\\Leftrightarrow \lim _{n \rightarrow \infty} P\left(\left|X_n\right|^n>\varepsilon\right) & =0\end{aligned}$$When $\mathcal{E}>1$, we have:$$\lim _{n \rightarrow \infty} P\left(\left|X_n\right|>\varepsilon^{\frac{1}{n}}\right)=0$$
> 
> When $0<\varepsilon \leqslant 1$, we have$$\begin{aligned}\lim _{n \rightarrow \infty} p\left(\left|x_n\right|>\varepsilon^{\frac{1}{n}}\right) & =\lim _{n \rightarrow \infty} P\left(\varepsilon^{\frac{1}{n}}<x_n<1\right)+P\left(-1<x_n<-\varepsilon^{\frac{1}{n}}\right) \\& =\lim _{n \rightarrow \infty} \frac{1-\varepsilon^{\frac{1}{n}}}{2} \cdot 2 \\& =\lim _{n \rightarrow \infty} 1-\varepsilon^{\frac{1}{n}} \\& =0\end{aligned}$$




## Convergence in Distribution
> [!def]
> ![](Convergence_Theory.assets/image-20240127160427003.png)



## Convergence in L1
> [!def]
> ![](Convergence_Theory.assets/image-20240127160412423.png)



## Convergence in Lp


### Examples
> [!example] Fa23 Disc05 P3
> ![](Convergence_Theory.assets/image-20240127162053591.png)



# Relationship Between Convergence
## a.s => p
> [!thm]
> ![](Convergence_Theory.assets/image-20231109223356198.png)

> [!proof] Detailed Proof
> ![](Convergence_Theory.assets/image-20240204113644187.png)



## Lp =>  p
> [!thm]
> ![](Convergence_Theory.assets/image-20240127162347485.png)


## p => d
> [!thm]
> ![](Convergence_Theory.assets/image-20240127162605105.png)



# Integrated Exercises
## On Almost Sure Convergence
> [!example] Fa23 Disc05 P1
> ![](Convergence_Theory.assets/image-20240127155707492.png)![](Convergence_Theory.assets/image-20240127155736066.png)



