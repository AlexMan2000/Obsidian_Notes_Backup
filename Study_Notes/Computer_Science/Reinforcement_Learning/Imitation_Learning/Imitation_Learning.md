# Terminology
> [!def]
> ![](../Q-Learning/Q-Learning.assets/bd49f678f9b43e7cc54b8c66352c2040_MD5.jpeg)
> Here $o_t$ is always the derived properties from $s_t$(think of $s_t$ as hidden states, model configurations unreadable to human while $o_t$ as observed states readable to humans).
> - $o_t$ doesn't have Markov Property, $s_{t}$ does.
> - If you observe a car image, call it $o_5$ , it is static so you cannot deduce where it will be at $o_6$ just from $o_5$. But if you consider the $o_{1,}o_{2},\cdots,o_4$, you will likely to know in which direction the car is moving.
> - The $s_t$ however, could give you something like acceleration, velocity information about the car, which is totally enough to deduce the $s_{t+1}$ without the help of $s_{1,\cdots,}s_{t-1}$



# Imitation Learning
> [!def]
> ![](../Q-Learning/Q-Learning.assets/b0ef6a689733369d476bdb3811dec2f7_MD5.jpeg)



# Dataset Aggregation
## Approach
> [!important]
> ![](Imitation_Learning.assets/360aa3057f9e87ad34381d15059b815d_MD5.jpeg)![](Imitation_Learning.assets/bdcc6699a05aab89baa4a5e62366f77e_MD5.jpeg)![](Imitation_Learning.assets/81885ecefae1912bde247b2800a830c2_MD5.jpeg)



## Non-Markovian 
> [!bug] Caveats
> ![](Imitation_Learning.assets/9bbb006148191705fed23b6b0c326c91_MD5.jpeg)


## Causal Confusion
> [!important]
> ![](Imitation_Learning.assets/089e4c3dc87583f522bc4c17b81f2b6d_MD5.jpeg)



## Multi-Modal
> [!important]
> ![](Imitation_Learning.assets/3b57fe73637eefb1d4acad8ae8e46f3b_MD5.jpeg)


### Sol1: GMM
> [!def]
> ![](Imitation_Learning.assets/27f848a8b2e947985f92771d942daac1_MD5.jpeg)


### Sol2: Latent Variable Model
> [!def]
> ![](Imitation_Learning.assets/8cb3617b942216ccf870743b5d7626dd_MD5.jpeg)




### Sol3: Autoregressive Discretiztion
> [!def]

