# Approximating Sums
## Main Theorem
> [!thm]
> ![](Sum&Asymptotics.assets/image-20231209153615054.png)

> [!proof]
> For the first part of the theorem $I+f(1)\leq S\leq I+f(n)$, we have the following graph approximation:
> ![](Sum&Asymptotics.assets/image-20231209153829820.png)![](Sum&Asymptotics.assets/image-20231209153832994.png)![](Sum&Asymptotics.assets/image-20231209153840693.png)
> For the second part of the theorem  $I+f(1)\geq S\geq I+f(n)$, we have the following graph approximation:
> ![](Sum&Asymptotics.assets/image-20231209153952698.png)


## Harmonic Numbers
> [!def]
> ![](Sum&Asymptotics.assets/image-20231209154108332.png)
> If we use Theorem above to approximate its sum we would get:
> 
> ![](Sum&Asymptotics.assets/image-20231209154202280.png)
> **Remarks:** The bound above is not the global bound for the harmonic function, it is only the pointwise bound for the function. In fact, in real analysis we could show that the harmonic series diverges and thus the partial sum defined here is unbounded.



## Asymptotic Equality
> [!def]
> ![](Sum&Asymptotics.assets/image-20231209154456577.png)




# Double Summations
> [!thm] Geometric Series
> ![](Sum&Asymptotics.assets/image-20231209154843496.png)

## Definition
> [!def] Double Summation
> 
![](Sum&Asymptotics.assets/image-20231209154748249.png)![](Sum&Asymptotics.assets/image-20231209154856640.png)



### Sum of Harmonic Numbers
> [!def]
> ![](Sum&Asymptotics.assets/image-20231209155138418.png)![](Sum&Asymptotics.assets/image-20231209155148155.png)






# Approximating Products
## Factorial
> [!def]
> ![](Sum&Asymptotics.assets/image-20231209155405010.png)![](Sum&Asymptotics.assets/image-20231209155433775.png)



## Sterling Approximation
> [!important]
> ![](Sum&Asymptotics.assets/image-20231209155508365.png)![](Sum&Asymptotics.assets/image-20231209155638792.png)![](Sum&Asymptotics.assets/image-20231209155642990.png)![](Sum&Asymptotics.assets/image-20231209155651613.png)



# Asymptotic Notations
## Little Oh
> [!def]
> ![](Sum&Asymptotics.assets/image-20231209155728605.png)

> [!lemma]
> ![](Sum&Asymptotics.assets/image-20231209155743816.png)


## Big Oh
> [!def]
> ![](Sum&Asymptotics.assets/image-20231209160732374.png)![](Sum&Asymptotics.assets/image-20231209160301417.png)![](Sum&Asymptotics.assets/image-20231209160309304.png)




## Big Omega
> [!def]
> ![](Sum&Asymptotics.assets/image-20231209160744903.png)![](Sum&Asymptotics.assets/image-20231209160752304.png)


## Little Omega
> [!def]
> ![](Sum&Asymptotics.assets/image-20231209160813714.png)![](Sum&Asymptotics.assets/image-20231209160818219.png)



## Theta
> [!def]
> ![](Sum&Asymptotics.assets/image-20231209160824910.png)


## Summary
> [!summary]
> ![](Sum&Asymptotics.assets/image-20231210200513451.png)![](Sum&Asymptotics.assets/image-20231210200518915.png)






# Pitfalls with Asymptotic Notation
## The Exponential Fiasco
> [!bug]
> ![](Sum&Asymptotics.assets/image-20231209161332776.png)


## Constant Confusion
> [!bug]
> ![](Sum&Asymptotics.assets/image-20231209161344274.png)




## Falsely Treating Function as Constant
> [!bug]
> ![](Sum&Asymptotics.assets/image-20231209161240715.png)



## Lower Bound Blunder
> [!bug]
> ![](Sum&Asymptotics.assets/image-20231209161358239.png)


## Equality Blunder
> [!bug]
> ![](Sum&Asymptotics.assets/image-20231209161406646.png)

