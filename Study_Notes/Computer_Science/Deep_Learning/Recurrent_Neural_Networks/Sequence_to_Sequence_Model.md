# Conditional Language Model
## Encoder-Decoder Structure
> [!def]
> ![](Sequence_to_Sequence_Model.assets/image-20240706180646957.png)![](Sequence_to_Sequence_Model.assets/image-20240706180823038.png)



## Seq-to-Seq Model
> [!def]
> ![](Sequence_to_Sequence_Model.assets/image-20240706180904517.png)![](Sequence_to_Sequence_Model.assets/image-20240706180910385.png)







# Beam Search Decoding
## Text Generation
> [!important]




## Get Better Decoding by BS
> [!bug] Caveats
> ![](Sequence_to_Sequence_Model.assets/image-20240706190946422.png)![](Sequence_to_Sequence_Model.assets/image-20240706191009757.png)

> [!algo]
> ![](Sequence_to_Sequence_Model.assets/image-20240706190911678.png)



# Cross Attention
## Motivation
> [!motiv]
> ![](Sequence_to_Sequence_Model.assets/image-20240706213156233.png)![](Sequence_to_Sequence_Model.assets/image-20240706220240317.png)



## Mechanisms
> [!important]
> ![](Sequence_to_Sequence_Model.assets/image-20240706220322995.png)![](Sequence_to_Sequence_Model.assets/image-20240706220402729.png)
> One question we should ask is how to choose the function that maps $h_{t}$ to $k_{t}$ and also $s_{t}$ to $q_{l}$. Here are some choices we could pick:
> - Identity function.
> - Linear multiplicative attention.
> 
> ![](Sequence_to_Sequence_Model.assets/image-20240706220756741.png)![](Sequence_to_Sequence_Model.assets/image-20240706220808339.png)![](Sequence_to_Sequence_Model.assets/image-20240706220819152.png)



## Summary
> [!summary]
> ![](Sequence_to_Sequence_Model.assets/image-20240706220840285.png)












 