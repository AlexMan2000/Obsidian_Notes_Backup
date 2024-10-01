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
## AR Operator
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
## MA Operator
> [!important]
> ![](ARMA.assets/image-20240923172955092.png)


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










