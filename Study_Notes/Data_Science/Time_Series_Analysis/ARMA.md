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
> ![](ARMA.assets/image-20240916174036753.png)![](ARMA.assets/image-20240920112954376.png)
> **Linear Process:**
> 
> ![](ARMA.assets/image-20240920165942679.png)



## AR(p)
> [!def]
> ![](ARMA.assets/image-20240916174108060.png)


## ACF of AR process
> [!important]


 


# Causality
## Backshift Operator
> [!important]
> ![](ARMA.assets/image-20240920165103325.png)![](ARMA.assets/image-20240920165118044.png)![](ARMA.assets/image-20240920165235065.png)![](ARMA.assets/image-20240920165355926.png)





## Causality Definition
> [!def]
> ![](ARMA.assets/image-20240920170247701.png)



## AR(1) and Causality
> [!important]
> ![](ARMA.assets/image-20240920170655460.png)![](ARMA.assets/image-20240920170728814.png)
> But we can redefine the white noise sequence to make it causal:
> 
> ![](ARMA.assets/image-20240920170815278.png)





# Moving Average
## MA(1)
> [!def]
> ![](ARMA.assets/image-20240916174226990.png)



## MA(p)
> [!def]
> ![](ARMA.assets/image-20240916174232948.png)



# Invertibility
## Invertibility Definition
> [!def]
> ![](ARMA.assets/image-20240920171401823.png)





## MA(1) and Invertibility
> [!important]
> ![](ARMA.assets/image-20240920171257365.png)![](ARMA.assets/image-20240920171310083.png)

> [!summary]
> ![](ARMA.assets/image-20240920171427735.png)![](ARMA.assets/image-20240920171435772.png)



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







# Autoregressive Moving Average Model
## Model Definition
> [!def]
> ![](ARMA.assets/image-20240916174157103.png)
> **Using Operator/Polynomial Notations we would have:**
> 
> ![](ARMA.assets/image-20240920172529763.png)


## Stationarity, Causality and Invertibility
> [!important]
> ![](ARMA.assets/image-20240920172703440.png)





### Casuality
> [!example]
> 





### Invertibility
> [!example]



## Parameter Redundancy
> [!example]
> ![](ARMA.assets/image-20240920172616427.png)![](ARMA.assets/image-20240920172634668.png)










