# Source Coding
> [!overview]
> ![](Channel_Coding.assets/image-20240204092913737.png)





## Source Coding Theorem
> [!thm]
> ![](Channel_Coding.assets/image-20240204093715553.png)



## Typical Set
> [!def]
> ![](Channel_Coding.assets/image-20240204093317014.png)

> [!property]
> ![](Channel_Coding.assets/image-20240204093324285.png)

> [!example] Flipping Coins
> ![](Channel_Coding.assets/image-20240204094035515.png)![](Channel_Coding.assets/image-20240204094227152.png)

> [!example] Coin Flipped Again
> ![](Channel_Coding.assets/image-20240204094523701.png)



## Asymptotic Equiparition Property(AEP)
> [!thm]
> ![](Channel_Coding.assets/image-20240204094659135.png)
> **Implications:**
> 
> ![](Channel_Coding.assets/image-20240204095143533.png)



> [!proof]
> ![](Channel_Coding.assets/image-20240204092953280.png)![](Channel_Coding.assets/image-20240204093025446.png)![](Channel_Coding.assets/image-20240204093037148.png)



## Huffman Coding Algorithm








# Channel Coding
> [!overview]
> The two simplest models studied are the binary symmetric channel (BSC) and binary erasure channel (BEC).


## Binary Symmetric Channel(BSC)




## Binary Erasure Channel(BEC)
> [!def]
> We will focus on the BEC, which erases the input to the channel with probability $p ∈ (0, 1)$.
> 
> We are interested in the maximum number of bits that the transmitter can send over the channel per transmission without error.
> ![](Channel_Coding.assets/image-20240204102652501.png)



### Rate of the Code(R)
> [!def]
> ![](Channel_Coding.assets/image-20240204102729530.png)



### Input and Output Alphabet
> [!def]
> ![](Channel_Coding.assets/image-20240204102747143.png)


### Maximum Probability of Error
> [!def]
> ![](Channel_Coding.assets/image-20240204102807580.png)![](Channel_Coding.assets/image-20240204102843059.png)



### Capacity of BEC
> [!thm]
> ![](Channel_Coding.assets/image-20240204103006254.png)![](Channel_Coding.assets/image-20240204103019081.png)







### Channel Coding Theorem
> [!thm]
> ![](Entropies.assets/image-20240204092315458.png)![](Channel_Coding.assets/image-20240204102448998.png)

> [!example] Rolling Dice
> ![](Channel_Coding.assets/image-20240204101319091.png)![](Channel_Coding.assets/image-20240204101759069.png)
> A bit derivation on how we figure out $\max_{p_X}H(X)$:
> 
> Note that $X\sim Bernoulli(p)$, thus $H(X)=plog(\frac{1}{p})+(1-p)log(\frac{1}{1-p})=-plogp-(1-p)log(1-p)$, which is concave in $p$ if we take the second derivative, so we set the derivative $log(\frac{1-p}{p})=0$ where $1-p=p$ and $p=\frac{1}{2}$. 
> 
> Thus we fit $p=\frac{1}{2}$ into the $H(X)$ and get $C=1$.







