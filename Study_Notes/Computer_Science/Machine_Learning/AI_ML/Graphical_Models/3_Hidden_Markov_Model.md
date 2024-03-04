# Canonical Definition
> [!def]
> ![](3_Hidden_Markov_Model.assets/image-20240303213113873.png)

# Model Assumptions
> [!important]
> ![](3_Hidden_Markov_Model.assets/image-20240303213144269.png)


# Three Fundamental Problems of HMM
> [!def]
> ![](3_Hidden_Markov_Model.assets/image-20240303213759004.png)

> [!example]
> ![](3_Hidden_Markov_Model.assets/image-20240303213836778.png)




## P1: Likelihood Computation
### Motivation
> [!motiv] Motivation
> ![](3_Hidden_Markov_Model.assets/image-20240303213923371.png)


### Naive Computing Procedure
> [!example] EECS189 Fa23 Notes
> ![](3_Hidden_Markov_Model.assets/image-20240303214258319.png)![](3_Hidden_Markov_Model.assets/image-20240303214346414.png)![](3_Hidden_Markov_Model.assets/image-20240303214415339.png)![](3_Hidden_Markov_Model.assets/image-20240303214520383.png)

> [!bug] Time Complexity
> ![](3_Hidden_Markov_Model.assets/image-20240304125608545.png)![](3_Hidden_Markov_Model.assets/image-20240303214855641.png)





### Forward Algorithm - DP
> [!algo]
> ![](3_Hidden_Markov_Model.assets/image-20240303215930656.png)

> [!example] EECS189 Notes - Computing Example and Visualization
> ![](3_Hidden_Markov_Model.assets/image-20240303215737286.png)![](3_Hidden_Markov_Model.assets/image-20240303215723916.png)![](3_Hidden_Markov_Model.assets/image-20240303215906932.png)




## P2: Decoding - Viterbi Algorithm
### Motivation
> [!motiv] Motivation
> ![](3_Hidden_Markov_Model.assets/image-20240303220543630.png)![](3_Hidden_Markov_Model.assets/image-20240303221604926.png)


### Viterbi Trellis - DP
> [!def]
> ![](3_Hidden_Markov_Model.assets/image-20240303221719392.png)![](3_Hidden_Markov_Model.assets/image-20240303221752097.png)


### Algorithm Procedures
> [!algo]
> ![](3_Hidden_Markov_Model.assets/image-20240303221949962.png)![](3_Hidden_Markov_Model.assets/image-20240303222002928.png)![](3_Hidden_Markov_Model.assets/image-20240303222047068.png)![](3_Hidden_Markov_Model.assets/image-20240303222110071.png)



## P3: Training HMM 
### Motivation
> [!motiv] Motivation
> ![](3_Hidden_Markov_Model.assets/image-20240303222346041.png)![](3_Hidden_Markov_Model.assets/image-20240303222353178.png)



# Particle Filtering - Sampling HMM






