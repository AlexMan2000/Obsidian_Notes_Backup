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
> ![](Basic_Time_Series.assets/image-20240920114831085.png)
```python
def acf_impl(x, nlags):
    """
    Your implementation for the Autocorrelation Function.
    Your implementation will be checked against statsmodels.tsa.stattools.acf.
    @param x: a 1-d numpy array
    @param nlags: an integer
    @return a 1-d numpy array with (nlags+1) elements. 
    The first element denotes the acf at lag = 0 (1.0 by definition).
    """
    assert len(x) > nlags
    x_bar = np.mean(x)
    output = []
    for lag in range(nlags+1):
        top_len = len(x) - lag
        gamma = np.sum((x[lag:]-x_bar)*(x[:top_len]-x_bar))/len(x)
        output.append(gamma)
    return np.array(output)/output[0]
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
> **Some Lemmas:**
> - ACF only depends on lag
> - ACF is symmetric around the origin. $$\begin{aligned}\rho(h)&=\rho((t+h)-t)\\&=\operatorname{cov}\left(x_{t+h}, x_t\right)\\&=\operatorname{cov}\left(x_t, x_{t+h}\right)\\&=\rho(t-(t+h))\\&=\rho(-h)\end{aligned}$$




# White Noise
> [!def]
> $$X_t \sim N\left(0, \sigma^2\right)$$


# Random Walk with Drift
> [!def]
> ![](Basic_Time_Series.assets/image-20240920114140476.png)
> **Remarks:**
> - The constant $\delta$ is called the drift, when $delta = 0$, it is called "random walk" process.



# Signal in Noise
