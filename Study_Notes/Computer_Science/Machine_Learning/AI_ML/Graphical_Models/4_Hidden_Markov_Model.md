# Canonical Definition
> [!def]
> ![](4_Hidden_Markov_Model.assets/image-20240303213113873.png)

# Model Assumptions
> [!important]
> ![](4_Hidden_Markov_Model.assets/image-20240303213144269.png)![](4_Hidden_Markov_Model.assets/image-20240418170007885.png)![](4_Hidden_Markov_Model.assets/image-20240418170036085.png)
> Consider the following initial distribution, transition model, and sensor model:
> 
> ![](4_Hidden_Markov_Model.assets/image-20240418170053297.png)





# Three Fundamental Problems of HMM
> [!def]
> ![](4_Hidden_Markov_Model.assets/image-20240303213759004.png)

> [!example]
> ![](4_Hidden_Markov_Model.assets/image-20240303213836778.png)




## P1: Likelihood Computation
### Motivation
> [!motiv] Motivation
> ![](4_Hidden_Markov_Model.assets/image-20240303213923371.png)


### Naive Computing Procedure
> [!example] EECS189 Fa23 Notes
> ![](4_Hidden_Markov_Model.assets/image-20240303214258319.png)![](4_Hidden_Markov_Model.assets/image-20240303214346414.png)![](4_Hidden_Markov_Model.assets/image-20240303214415339.png)![](4_Hidden_Markov_Model.assets/image-20240303214520383.png)

> [!bug] Time Complexity
> ![](4_Hidden_Markov_Model.assets/image-20240304125608545.png)![](4_Hidden_Markov_Model.assets/image-20240303214855641.png)





### Forward Algorithm - DP
> [!algo]
> ![](4_Hidden_Markov_Model.assets/image-20240303215930656.png)

> [!example] EECS189 Notes - Computing Example and Visualization
> ![](4_Hidden_Markov_Model.assets/image-20240303215737286.png)![](4_Hidden_Markov_Model.assets/image-20240303215723916.png)![](4_Hidden_Markov_Model.assets/image-20240303215906932.png)



### Exercises
> [!example] EECS188 Fa23 Disc10 P1
> ![](4_Hidden_Markov_Model.assets/image-20240418171004819.png)





## P2: Decoding - Viterbi Algorithm
### Motivation
> [!motiv] Motivation
> ![](4_Hidden_Markov_Model.assets/image-20240303220543630.png)![](4_Hidden_Markov_Model.assets/image-20240303221604926.png)


### Viterbi Trellis - DP
> [!def]
> ![](4_Hidden_Markov_Model.assets/image-20240303221719392.png)![](4_Hidden_Markov_Model.assets/image-20240303221752097.png)


### Algorithm Procedures
> [!algo]
> ![](4_Hidden_Markov_Model.assets/image-20240303221949962.png)![](4_Hidden_Markov_Model.assets/image-20240303222002928.png)![](4_Hidden_Markov_Model.assets/image-20240303222047068.png)![](4_Hidden_Markov_Model.assets/image-20240303222110071.png)



## P3: Training HMM 
### Motivation
> [!motiv] Motivation
> ![](4_Hidden_Markov_Model.assets/image-20240303222346041.png)![](4_Hidden_Markov_Model.assets/image-20240303222353178.png)![](4_Hidden_Markov_Model.assets/image-20240418172545267.png)









# Particle Filtering - Sampling HMM






