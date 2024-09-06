# MDP and RL
> [!def]
> ![](2_Types_of_RL.assets/image-20240221104239336.png)![](2_Types_of_RL.assets/image-20240221104505220.png)
> In reinforcement learning, you only know somethong is bad after you have actually experienced that bad scenario.
> 
> ![](2_Types_of_RL.assets/image-20240221120804620.png)








# Passive Reinforcement Learning
> [!overview]
> ![](2_Types_of_RL.assets/image-20240221104616807.png)


## Model-Based Learning
> [!def]
> ![](2_Types_of_RL.assets/image-20240221104906434.png)

> [!example]
> ![](2_Types_of_RL.assets/image-20240221105309898.png)![](2_Types_of_RL.assets/image-20240221105408127.png)



## Model Free Learning
> [!motiv] Motivation
> ![](2_Types_of_RL.assets/image-20240221105801998.png)


### Idea
> [!concept]
> ![](2_Types_of_RL.assets/image-20240221120920056.png)![](2_Types_of_RL.assets/image-20240221120933331.png)![](2_Types_of_RL.assets/image-20240221120943845.png)![](2_Types_of_RL.assets/image-20240221120949933.png)![](2_Types_of_RL.assets/image-20240221121000831.png)



### Direct Evaluation
> [!def]
> ![](2_Types_of_RL.assets/image-20240221105911401.png)

> [!example]
> ![](2_Types_of_RL.assets/image-20240221105942626.png)![](2_Types_of_RL.assets/image-20240221110230787.png)![](2_Types_of_RL.assets/image-20240221110548906.png)

> [!bug] Problems
> ![](2_Types_of_RL.assets/image-20240221105956580.png)![](2_Types_of_RL.assets/image-20240221110839152.png)![](2_Types_of_RL.assets/image-20240221110001644.png)


### Temporal Difference Learning
> [!motiv] Motivation
> ![](2_Types_of_RL.assets/image-20240221111109156.png)![](2_Types_of_RL.assets/image-20240221111127965.png)![](2_Types_of_RL.assets/image-20240221111143500.png)

> [!def]
> ![](2_Types_of_RL.assets/image-20240221111310871.png)![](2_Types_of_RL.assets/image-20240221111634420.png)![](2_Types_of_RL.assets/image-20240221111758810.png)

> [!example]
> ![](2_Types_of_RL.assets/image-20240221111723356.png)
> In this example, each transition is a sample, and we calculate the value of these samples one by one:
> - Assume $V_k^{\pi}(B)=V_k^{\pi}(C)=0$.
> - For (B, east, C, -2), $$\begin{aligned}V_{k+1}^{\pi}(B)&\leftarrow (1-\alpha)V_k^{\pi}(B)+\alpha(R(B,east, C)+\gamma V_k^{\pi}(C))\\&\leftarrow (1-\alpha)\times 0+\alpha(-2+\gamma \times 0)\\&\leftarrow -2\alpha=-1\end{aligned}$$
> - For (C, east, D, -2), $$\begin{aligned}V_{k+1}^{\pi}(C)&\leftarrow (1-\alpha)V_k^{\pi}(C)+\alpha(R(C,east, D)+\gamma V_k^{\pi}(D))\\&\leftarrow (1-\alpha)\times 0+\alpha(-2+\gamma \times 8)\\&\leftarrow \alpha\times (-2 + 8)=3\end{aligned}$$

> [!bug] Problem
> ![](2_Types_of_RL.assets/image-20240221114716358.png)![](2_Types_of_RL.assets/image-20240221114800660.png)


# Active Reinforcement Learning
> [!overview]
> ![](2_Types_of_RL.assets/image-20240221114952650.png)


## Q-Learning
> [!motiv] Motivation
> ![](2_Types_of_RL.assets/image-20240221115246135.png)

> [!def]
> ![](2_Types_of_RL.assets/image-20240221115306496.png)

> [!example] Fa23 Disc05 P2
> ![](2_Types_of_RL.assets/image-20240223124156766.png)
> Each transition can be regarded as a sample in the above figure:
> - **Transition 1**: We will update $Q(D, east)$ to be $(1-0.5)\times 0+0.5\times (-1+\max_{a'}Q(E,a'))=0.5\times(-1)=-0,5$
> - **Transition 2**: We will update $Q(E, east)$ to be $(1-0.5)\times 0+0.5\times (2+\max_{a'}Q(E,a'))=0.5\times(2+\max\{0\})=1$
> - **Transition 3**: We will update $Q(E, west)$ to be $(1-0.5)\times 0+0.5\times (0+\max_{a'}Q(E,a'))=0.5\times(0+\max\{0\})=0$
> - **Transition 4**: We will update $Q(D, east)$ to be $(1-0.5)\times (-0.5)+0.5\times (-1+\max_{a'}Q(E,a'))=0.5\times(-1+1)=-0.25$




## Q-Learning Properties
> [!property]
> ![](2_Types_of_RL.assets/image-20240221120614363.png)



# Exploration and Exploitation
> [!motiv] Motivation
> ![](2_Types_of_RL.assets/image-20240221121411797.png)
> **Some differences:**
> - Exploration means adventuring into new paths.
> - Exploitation means taking actions repeatedly along the same or similar paths.



## Method 1: ε-Greedy Policies
> [!def]
> ![](2_Types_of_RL.assets/image-20240221121757048.png)
> If we choose $\epsilon$ to be too close to 1, then after many learning iterations, we are not using the learning results(i.e. the Q-values), instead we are still acting randomly. So we want to lower $\epsilon$ alongside our exploration process.
> 
> ![](2_Types_of_RL.assets/image-20240221122256590.png)
> But manually tuning $\epsilon$ requires some philosophy and it's not easy to find a one-fit-all value, so we opt to **Exploration Function** to avoid manual tuning.




## Method 2: Exploration Functions
> [!def]
> ![](2_Types_of_RL.assets/image-20240221122451939.png)![](2_Types_of_RL.assets/image-20240221122457341.png)![](2_Types_of_RL.assets/image-20240221122509986.png)![](2_Types_of_RL.assets/image-20240221122933227.png)





# Approximate Q-Learning
## Memory Restriction
> [!motiv] Motivation
> ![](2_Types_of_RL.assets/image-20240221123133946.png)



## Feature Representation of States
> [!def]
> ![](2_Types_of_RL.assets/image-20240221123423782.png)![](2_Types_of_RL.assets/image-20240221123439130.png)


## Linear Value Functions
> [!def]
> ![](2_Types_of_RL.assets/image-20240221123508602.png)



## Approximation Procedure
> [!def]
> ![](2_Types_of_RL.assets/image-20240221123650068.png)
> **Remarks:**
> - $f_n(s.a)$ could be 0, meaning that certain feature may not be present at the state $(s,a)$.
> - If the difference < 0, it means that the current estimate of $Q(s,a)$ is bigger than the sample we observe, so we want to update our new $Q(s,a)$ to be lower(i.e. to be closer to the observed sample). This is realized by multiplying difference < 0 in the update step.
> - If the difference > 0, it means that the current estimate of $Q(s,a)$ is smaller than the sample we observe, so we want to update our new $Q(s,a)$ to be higher(i.e. to be closer to the observed sample). This is realized by multiplying difference > 0 in the update step.
> - If the $f_i(s,a)$ is big, then the update is more active.

> [!example] Pacman
> ![](2_Types_of_RL.assets/image-20240221123737153.png)



# Policy Search


