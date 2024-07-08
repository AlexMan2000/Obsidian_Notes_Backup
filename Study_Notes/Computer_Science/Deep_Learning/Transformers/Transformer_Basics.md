# Motivation
> [!motiv]
> ![](Transformer_Basics.assets/image-20240706221804990.png)




# Self Attention
> [!important]
> ![](Transformer_Basics.assets/image-20240706221539230.png)![](Transformer_Basics.assets/image-20240706221615144.png)







# Improve 1: Positional Encoding
## Motivations
> [!motiv]
> Due to the fact that self-attention will look into the future time step of inputs or hidden states, the system is not causal, which means it loses information about the time ordering. But we can use positional encoding to address this issue. 
> - Self attention is permutation invariant. 
> - Position of words in a sentence carries information!
> 
> ![](Transformer_Basics.assets/image-20240706222213813.png)



## Naive Positional Encoding
> [!important]
> ![](Transformer_Basics.assets/image-20240706222352687.png)
> The frequency at eariler time steps are designed to be of high frequency since high-frequency signals are essential for capturing fine details and variations.



## Learned Positional Encoding
> [!def]
> ![](Transformer_Basics.assets/image-20240706230425999.png)![](Transformer_Basics.assets/image-20240706230543833.png)



# Improve 2: Multi-headed Attention
> [!def]
> ![](Transformer_Basics.assets/image-20240706230903712.png)![](Transformer_Basics.assets/image-20240706230911133.png)



# Improve 3: Adding Non-linearities
## Linearities
> [!important]
> ![](Transformer_Basics.assets/image-20240707104643346.png)![](Transformer_Basics.assets/image-20240707104653581.png)



# Improve 4: Masked Attention
## Motivations
> [!motiv]
> ![](Transformer_Basics.assets/image-20240707104958012.png)


## Mechanisms
> [!def]
> ![](Transformer_Basics.assets/image-20240707105851600.png)



# Classic Transformer
> https://arxiv.org/abs/1706.03762


## Model Structure
> [!def]
> ![](Transformer_Basics.assets/image-20240707110733248.png)



## Cross Attention
> [!def]
> ![](Transformer_Basics.assets/image-20240707111213345.png)
> In reality, cross-attention is multi-headed and the number of heads are the same for encoder and decoder.




## Layer Nomalization
> [!def]
> ![](Transformer_Basics.assets/image-20240707111404353.png)




## Pros and Cons
> [!bug] Caveats
> ![](Transformer_Basics.assets/image-20240707113530435.png)





# Implementations




