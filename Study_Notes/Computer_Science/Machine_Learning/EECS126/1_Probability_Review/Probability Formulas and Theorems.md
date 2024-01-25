# Tail Sum Formula
## Discrete Random Variables
> [!thm]
> ![](Probability%20Formulas%20and%20Theorems.assets/image-20231119220916357.png)![](Probability%20Formulas%20and%20Theorems.assets/image-20231119220926438.png)![](Probability%20Formulas%20and%20Theorems.assets/image-20231119221844257.png)

> [!important] Graphical Explanation
> ![](Probability%20Formulas%20and%20Theorems.assets/image-20231119221916664.png)
> ![](Probability%20Formulas%20and%20Theorems.assets/image-20231119221903603.png)



## Continuous Random Variables
> [!thm]
> ![](Probability%20Formulas%20and%20Theorems.assets/image-20231119222250112.png)![](Probability%20Formulas%20and%20Theorems.assets/image-20231119222322601.png)


# Tail Sum Formula For Higher Moments
## Discrete Moments
### Formula 1
> [!thm]
> ![](Probability%20Formulas%20and%20Theorems.assets/image-20231119222700662.png)![](Probability%20Formulas%20and%20Theorems.assets/image-20231119222707471.png)

### Formula 2
> [!thm]
> ![](Probability%20Formulas%20and%20Theorems.assets/image-20231119223008121.png)



## Continuous Moments
> [!thm]
> ![](Probability%20Formulas%20and%20Theorems.assets/image-20231119222437318.png)![](Probability%20Formulas%20and%20Theorems.assets/image-20231119222523846.png)

> [!proof] EECS126 Fa23 HW2 P4
> This proof uses lots of important techniques:
> $$\begin{aligned}\int_0^{\infty} p y^{p-1} \mathbb{P}(Y>y) d y &=\int_0^{\infty} p y^{p-1} \mathbb{E}\left(\mathbb{1}_{Y>y}\right) d y\text{          (Indicator Function)}\\& =\int_0^{\infty} \mathbb{E}\left(p y^{p-1} \mathbb{1}_{Y>y}\right) d y \text{          (Linearity)}\\& =\mathbb{E}\left(\int_0^{\infty} p y^{p-1} \mathbb{1}_{Y>y} d y\right) \text{          (Swapping)}\\& =\mathbb{E}\left(\int_0^Y p y^{p-1} d y\right)\text{          (Integral Limit)}\\& =\mathbb{E}\left(Y^p\right) \end{aligned}$$
> The last but two equality dwells thinking. We know that the integral limit $dy$ controls our integration process. $\mathbb{1}_{Y>y}$ here upper bounds the $y$ to be $Y$ because if $y\geq Y$, $\mathbb{1}_{Y> y}=0$, making the integrand equal to zero. So we don't need to consider the region $\int_y^{\infty}$.



# Borel-Cantelli&Strong Law
## Borel-Cantelli Lemma
> [!lemma] EECS126 Fa23 HW2 P2
> ![](Probability%20Formulas%20and%20Theorems.assets/image-20231217202045111.png)

> [!proof] Proof from Textbook
> First note that
> $$\left\{A_n \text {, i.o. }\right\}=\cap_n B_n=: B,$$where $B_n=\cup_{m \geq n} A_m$ is a decreasing sequence of sets. 
> To see this, note that the outcome $\omega$ is in infinitely many sets $A_n$, i.e., that $\omega \in\left\{A_n\right.$, i.o. $\}$, if and only if for every $n$, the outcome $\omega$ is in some $A_m$ for $m \geq n$. 
> 
> Also, $\omega$ is in $\cup_{m \geq n} A_m=B_n$ for all $n$ if and only if $\omega$ is in $\cap_n B_n=B$. Hence $\omega \in\left\{A_n\right.$, i.o. $\}$ if and only if $\omega \in B$.
> 
> Now, $B_1 \supseteq B_2 \supseteq \cdots$, so that $P\left(B_n\right) \rightarrow P(B)$. Thus,$$P\left(A_n, \text { i.o. }\right)=P(B)=\lim _{n \rightarrow \infty} P\left(B_n\right)$$
> and $P\left(B_n\right) \leq \sum_{m=n}^{\infty} P\left(A_m\right)$, so that $$
> P\left(B_n\right) \rightarrow 0 \text { as } n \rightarrow \infty .$$
> Consequently, $P\left(A_n\right.$, i.o. $)=0$.
> ![](Probability%20Formulas%20and%20Theorems.assets/image-20231217204014726.png)

## Borel-Cantelli => SLLN
> [!thm] EECS126 Fa21 HW2 P4
> ![](Convergence%20Theory.assets/image-20231119214025067.png)




# Law of Unconscious Statistician
## Law of R.V.
> [!def]
> ![](Probability%20Formulas%20and%20Theorems.assets/image-20231217211643270.png)![](Probability%20Formulas%20and%20Theorems.assets/image-20231217211532355.png)
> **The key takeaways:**
> - X is a ==deterministic== function on a probability space
> - ==The probability space supplies the randomness==.



## LOTUS
> [!thm] Theorem - EECS126 Fa23 Disc02 P3
> In probability theory and statistics, the law of the unconscious statistician, or LOTUS, is a theorem which expresses the expected value of a function g(X) of a random variable X in terms of g and the probability distribution of X.
> ![](Probability%20Formulas%20and%20Theorems.assets/image-20231217205842658.png)

> [!proof]
> ![](Probability%20Formulas%20and%20Theorems.assets/image-20231217212130904.png)![](Probability%20Formulas%20and%20Theorems.assets/image-20231217212141097.png)





