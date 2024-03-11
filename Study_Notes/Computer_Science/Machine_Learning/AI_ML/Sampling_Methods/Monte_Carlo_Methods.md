# Monte Carlo Integral
## Calculating Bounded Integrals
> [!def]
> ![](Monte_Carlo_Methods.assets/image-20240311100031455.png)

> [!code]
```r
# underlying uniforms
U <- runif(100000, 0, 2*pi)

# calculate h(U)
hU <- sin(U*cos(U))

# monte carlo approximation
2*pi*mean(hU)
[1] -1.048418

# R’s numerical integration approximation
h <- function(u) sin(u*cos(u))
integrate(h, 0, 2*pi)$val
[1] -1.041727
```



## Calculating Unbounded Integrals
> [!def]
> ![](Monte_Carlo_Methods.assets/image-20240311100058273.png)

> [!code]
```r
X <- rnorm(100000)
Y <- sin(X*cos(X))/dnorm(X)
mean(Y)
[1] -0.3657281

```




# Importance Sampling
## Motivations
> [!motiv] Motivation
> One of the principal reasons for wishing to sample from complicated probability distributions is to be able to evaluate expectations of the tasrget distribution.
> 
> The technique of importance sampling provides a framework for approximating **expectations** directly but **does not** itself provide a mechanism for drawing samples from distribution p(z).
> ![](Monte_Carlo_Methods.assets/image-20240310230935332.png)![](Monte_Carlo_Methods.assets/image-20240310230942435.png)
> The art of this method lies in the choice of a good proposed distribution $g(\cdot)$


## Examples
### Laplacian Distribution Expectation
> [!example] Solution 1: Use Monte Carlo Integration Approximation
> ![](Monte_Carlo_Methods.assets/image-20240310231241173.png)![](Monte_Carlo_Methods.assets/image-20240311100200136.png)

> [!example] Solution 2: Important Sampling, Gaussian as Proposed Distribution
> ![](Monte_Carlo_Methods.assets/image-20240311095824543.png)![](Monte_Carlo_Methods.assets/image-20240311100552777.png)![](Monte_Carlo_Methods.assets/image-20240311095839222.png)![](Monte_Carlo_Methods.assets/image-20240311095844397.png)



### Double Exponential Density
> [!def]
> 



 


## Algorithm Procedure
> [!algo]




> [!proof]
> ![](Basic_Sampling_Algorithms.assets/image-20240310213733875.png)


## Advantages
> [!important]
> 





## Code Example
> [!code]



## Advantages
> [!important]
> **Importance sampling is likely to be useful when:**
> 1. _p(x)_ is difficult or impossible to sample from.
> 2. We need to be able to evaluate _p(x)_. Meaning we can plug in an _x_ and get a value. In fact, that’s a little more than we need we actually only need. The ability to compute an unnormalized density but we’d have to tweak our procedure a bit. See sources if you’re curious.
> 3. _q(x)_ needs to be easy to evaluate and sample from since our estimate will ideally be made of many samples from it.
> 4. Lastly, and the hard part, is that you need to be able to choose _q(x)_ to be high where the absolute value of _p(x)_ times _f(x_) is high which is not necessarily an easy task.


## Drawback
> [!bug] Caveats


# Monte Carlo Markov Chain




# Metropolis Hastin Algorithm




# Hybrid Monte Carlo Algorithm