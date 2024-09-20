# Basic Statistics of a Time Series
> [!summary]
> ![](ARMA.assets/image-20240920110304183.png)
> **Remarks:**
> - **(Auto)Covariance**: Measures the linear dependence between two points on the same series.
> - **Cross-covariance**: Measures the linear dependence between two series.



## ACF
> [!def]
> ![](ARMA.assets/image-20240920110712706.png)
> The ACF measures the linear predictability of the series at time $t$,say $x_t$, using only the value $x_s$.
> 
> Here we can show that $-1\leq \rho(s,t)\leq 1$ using Cauchy-Schwarz inequality.
> 
> **Remarks:** 
> - If we can predict $x_t$ **perfectly from** $x_s$ through a linear relationship, $x_{t}= \beta_{0}+ \beta_1x_s$, then the correlation will be $+1$ when $\beta_{1}> 0$, and $-1$ when $\beta_{1}< 0$.
> 


> [!code]
```python


```





## CCF
> [!def]
> ![](ARMA.assets/image-20240920110837032.png)




## Stationarity
### Strong Stationarity
> [!def]
> ![](ARMA.assets/image-20240920112526245.png)![](ARMA.assets/image-20240920112439342.png)


### (Weak) Stationarity
> [!def]
> ![](ARMA.assets/image-20240920112353559.png)







# Auto-regressive Process
## AR(1)
> [!def]
> ![](ARMA.assets/image-20240916173726936.png)
> where $W_t$(i.i.d across $t$) is drawn from $\mathcal{N}(0, \sigma_{W}^2)$ and $|\phi| < 1$.
> 
> **Autoregressive:** Since each value of the random variable in our series depend on another random variable in the series.
> 
> **Causal:** $X_t$ only depends on $X_{m}$ where $m\leq t$.
> 
> **Zero Mean:** By expanding the recursion we have:
> ![](ARMA.assets/image-20240916174017960.png)
> **Weakly Stationary: We prove by definition:**
> 
> ![](ARMA.assets/image-20240916174036753.png)




## AR(p)
> [!def]
> ![](ARMA.assets/image-20240916174108060.png)



# Moving Average
## MA(1)
> [!def]
> ![](ARMA.assets/image-20240916174226990.png)



## MA(p)
> [!def]
> ![](ARMA.assets/image-20240916174232948.png)



# AR and MA Prediction
### Linear Process
> [!important]
> A **linear stochastic process** is a type of stochastic (random) process where the future state of the process is a linear function of its past states and a random disturbance or noise term. 
> $$X_t=c+\sum_{i=1}^p \phi_i X_{t-i}+\epsilon_t$$
> where:
> - $X_t$ is the value of the process at time $t$,
> - $c$ is a constant term (intercept),
> - $\phi_i$ are the coefficients of the linear function (these represent the dependence of the current value $X_t$ on past values),
> - $X_{t-i}$ represents the past values of the process (lagged terms),
> - $\epsilon_t$ is a stochastic or random noise term (often assumed to be white noise, i.e., uncorrelated random noise with a mean of zero).
> 
> ![](ARMA.assets/image-20240920111753334.png)


## Prediction





# Random Walk




# Autoregressive Moving Average Model
> [!def]
> ![](ARMA.assets/image-20240916174157103.png)


