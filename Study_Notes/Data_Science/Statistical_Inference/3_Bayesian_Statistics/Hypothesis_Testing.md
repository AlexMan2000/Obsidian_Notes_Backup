# Bayesian Updating
> [!summary]
> ![](Hypothesis_Testing.assets/image-20240203193620143.png)![](Hypothesis_Testing.assets/image-20240203193627960.png)![](Hypothesis_Testing.assets/image-20240203193636975.png)![](Hypothesis_Testing.assets/image-20240203193728701.png)










# Beta Priors
## Definition
> [!def] Beta Distribution
> ![](Hypothesis_Testing.assets/image-20240203150929128.png)![](Hypothesis_Testing.assets/image-20240203151022485.png)![](Hypothesis_Testing.assets/image-20240203151203745.png)
>

> [!important] Beta Constant
> ![](Hypothesis_Testing.assets/image-20240203151826287.png)![](Hypothesis_Testing.assets/image-20240203151831896.png)
> Deriving this is a bit complicated and not suitable for the purpose of learning.
> 
> To see this in gaussian, recall that the gaussian pdf is $$f(\theta)=\frac{1}{\sqrt{2\pi}\sigma}exp\{-\frac{1}{2}(\frac{x-\mu}{\sigma})^2\}$$
> and the $\theta\in (-\infty,\infty)$.
> 
> Here the $\sqrt{2\pi}$ is the normalizing constant and can be computed by $\int_{-\infty}^{\infty}\frac{1}{\sigma}e^{-\frac{1}{2}(\frac{\theta-\mu}{\sigma})^2}d\theta=\sqrt{2\pi}$ by change of variable.
> 
> To see this in exponential distribution, recall that the exponential pdf is $$f(\theta)=\lambda e^{\lambda\theta}$$
> where $\theta\in [0,\infty)$ and we can compute the normarlizing constant by $$\int_{0}^{\infty}e^{-\lambda\theta}d\theta=\frac{1}{\lambda}$$


## Hyperparameters Interpretations
> [!important]
> When $a>b$, large values have higher probability.
> ![](Hypothesis_Testing.assets/image-20240203202109189.png)
> When $a<b$, small values have higher probability.
> 
> ![](Hypothesis_Testing.assets/image-20240203202121230.png)
> When $a=b=1$, we have a uniform distribution over $[0,1]$
> 
> ![](Hypothesis_Testing.assets/image-20240203202322911.png)






## Conjugate Priors
> [!important]
> 
> Beta prior is a conjugate prior for binomial bernoulli and geometric likelihood.
> ![](Hypothesis_Testing.assets/image-20240203154324208.png)![](Hypothesis_Testing.assets/image-20240203154533887.png)![](Hypothesis_Testing.assets/image-20240203154545328.png)![](Hypothesis_Testing.assets/image-20240203154558888.png)
> **Note:** To memorize, the posterior beta parameter follows (a + # success, b + # failure) where # success + # failure = total number of experiments.


# Guassian Priors
## Conjugate Priors
> [!important]
> Gaussian prior is the conjugate prior of itself.
> ![](Hypothesis_Testing.assets/image-20240203155042492.png)![](Hypothesis_Testing.assets/image-20240203155047356.png)

> [!example] One data point
> ![](Hypothesis_Testing.assets/image-20240203155843086.png)![](Hypothesis_Testing.assets/image-20240203155849487.png)

> [!example] Multiple Data Point
> ![](Hypothesis_Testing.assets/image-20240203155933251.png)

> [!proof]
> Suppose we have datapoint $x_1, x_2, \cdots, x_n$ and a parameter $\theta$ if $f(\theta) \sim N\left(\mu_0, \sigma_0^2\right), f\left(x_i \mid \theta\right) \sim N\left(\theta, \sigma^2\right)$, then the posterior distribution is still gaussian:$$\begin{aligned}& f\left(\theta \mid x_1, x_2, \cdots, x_n\right)=\frac{f\left(x_1, x_2, \cdots x_n \mid \theta\right) f(\theta)}{f\left(x_1, x_2, \cdots, x_n\right)} \\& f\left(x_1, x_2, \cdots, x_n \mid \theta\right) f(\theta) \propto \prod_{i=1}^n \exp \left\{-\frac{1}{2 \sigma^2}\left(x_i-\theta\right)^2\right\} \exp \left\{-\frac{1}{2 \sigma_0^2}\left(\theta-\mu_0\right)^2\right\} \\& \alpha=-\left\{\frac{\sum_{i=1}^n\left(x_i-\theta\right)^2}{2 \sigma^2}+\frac{\left(\theta-\mu_0\right)^2}{2 \sigma_0^2}\right\} \\& =\frac{\sigma_0^2\left(\sum_{i=1}^n x_i^2-2 n \bar{x} \cdot \theta+n \theta^2\right)+\sigma^2\left(\theta^2-2 \mu_0 \cdot \theta+\mu_0^2\right)}{2 \sigma^2 \sigma_0^2} \\& =\frac{\left(n \sigma_0^2+\sigma^2\right) \theta^2-\left(2 n \sigma_0^2 \bar{x}+2 \mu_0 \sigma^2\right) \theta+\sigma_0^2 \sum_{i=1}^n x_i^2+\sigma^2 \mu_0^2}{2 \sigma^2 \sigma_0^2} \\& \therefore \mu_{\text {post }}=\frac{n \sigma_0^2 \bar{x}+\mu_0 \sigma^2}{n \sigma_0^2+\sigma^2} \quad \sigma_{\text {post }}^2=\frac{n \sigma_0^2+\sigma^2}{\sigma^2 \sigma_0^2} \\& =\frac{a \mu_0+b \bar{x}}{a+b}=\frac{1}{a+b} \\& \text { where } a=\frac{1}{\sigma_0^2}, b=\frac{n}{\sigma^2} \\&\end{aligned}$$


## Weighted Average of Prior and Data
> [!important]
> ![](Hypothesis_Testing.assets/image-20240203160504368.png)
> This correlates with the finding in n-d case in [Tug of War between Prior and Likelihood](../../../Computer_Science/Machine_Learning/AI_ML/Regression/3_Regression&Reparametrization.md#Overview) 
> 
> Generally, if we have a strong prior(the variance is small), then the MAP estimate will be close to the prior than to the data point(likelihood).

> [!example] 
> ![](Hypothesis_Testing.assets/image-20240203165319246.png)



# Gamma Priors
## PDF
> [!def]
> ![](Hypothesis_Testing.assets/image-20240203202603577.png)
> Gamma Function is just $\Gamma(\alpha)=(\alpha-1)!$, can be used to simplify some integrations.
> 
> The normalization terms in beta distribution $(a,b)$ can be rewritten in $\frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)}$.



## Conjugate Priors
> [!example] Exponential Likelihood
> ![](Hypothesis_Testing.assets/image-20240203202759544.png)




# Prior and Posterior Predictive
> [!important]
> Suppose you roll a dice, which could equally likely to be 4, 6, 8, 12, 20 sided. Then suppose you observe a roll that gives 7. ($D_1=7$)
> 
> Model this as a Bayesian Updating Problem we have $H_{4,}H_{6,}H_{8,}H_{12}, H_{20}$ with equal probability(flat prior) where $p(H_4)=p(H_6)=p(H_8)=p(H_{12})=p(H_{20})=\frac{1}{5}$
> 
> **Prior Predictive:** $$p(D_1=7)=\sum\limits_{H\in \mathcal{H}}p(D_1|H)p(H)$$
> Basically this is computing using total probability law.
> 
> **Posterior Predictive:** $$p(D_2=7|D_1=7)=\sum\limits_{H\in \mathcal{H}}p(D_2=7|H,D_1=7)p(H|D_1=7)$$
> Same reasoning, but using posterior probability.



# Applications
## Monty Hall Problem
> [!example] Sp22 MIT 1805 HW7 P1
> ![](Hypothesis_Testing.assets/image-20240203193924409.png)![](Hypothesis_Testing.assets/image-20240203194120502.png)![](Hypothesis_Testing.assets/image-20240203194502645.png)![](Hypothesis_Testing.assets/image-20240203194506626.png)



## Posterior Prediction
> [!example] Sp22 MIT 1805 HW7 P2
> ![](Hypothesis_Testing.assets/image-20240203195340654.png)![](Hypothesis_Testing.assets/image-20240203195419407.png)![](Hypothesis_Testing.assets/image-20240203195425438.png)![](Hypothesis_Testing.assets/image-20240203195739750.png)![](Hypothesis_Testing.assets/image-20240203200103370.png)![](Hypothesis_Testing.assets/image-20240203200109363.png)![](Hypothesis_Testing.assets/image-20240203200115528.png)


## Odds
> [!example] Sp22 MIT 1805 HW7 P2
> ![](Hypothesis_Testing.assets/image-20240203201051701.png)![](Hypothesis_Testing.assets/image-20240203201206519.png)![](Hypothesis_Testing.assets/image-20240203201212986.png)














