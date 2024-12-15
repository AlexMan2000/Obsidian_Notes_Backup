# Gradient Policy Optimization
## Formulations
> [!def]
> ![](RLHF.assets/218df89f26e8577bf66237d17b8fee62_MD5.jpeg)


## Objectives
> [!important]
> ![](RLHF.assets/335285ddee67abb40242fe11137de09f_MD5.jpeg)




## Policy Gradient
> [!important]
> ![](RLHF.assets/36ca00b348ebe86e89b29ce72db79189_MD5.jpeg)![](RLHF.assets/e0065720fb1eb51d6d8f7d84a74a0ea8_MD5.jpeg)


## Compute the gradient
> [!important]
> ![](RLHF.assets/4ceec9daae6c65b4ff0b6cb02a685b6b_MD5.jpeg)![](RLHF.assets/cd7baebc6f31d6c02e7bd8dd490e749b_MD5.jpeg)





## Full Algorithms
> [!algo]
> ![](RLHF.assets/9d17cd4fa2f0119d04374942e93d5561_MD5.jpeg)



## Examples
### Gaussian Policies
> [!def]
> ![](RLHF.assets/0ef04b47c2052be9798e1574eefb8337_MD5.jpeg)







# GPO Problems
## Problem List
### Slow Update
> [!important]
> ![](RLHF.assets/83bbdd8499d1da25363b6ec25e012b45_MD5.jpeg)



### High Variance
> [!important]
> ![](RLHF.assets/606ed2d7339d5fd094e9a32b1d973c19_MD5.jpeg)






## Reducing Variance
### Method 1: Rewards to go
> [!important] Rewards to go
> ![](RLHF.assets/9a4194455167adc37aa276fd2f1c4ee6_MD5.jpeg)



### Method 2: Optimal Baseline
> [!def]
> ![](RLHF.assets/138c54bd0ca53549b48f7e368e8ec6fd_MD5.jpeg)
> We don't typically use it, using the expected rewards as baseline is just fine.


### Method 3: Adding Baseline
> [!important] Baseline
> Make PGO algorithm increase the policy trajectories that have rewards above the average.
> ![](RLHF.assets/c0fd1b5bb3f11a3c92ffbe6f0d13186b_MD5.jpeg)


### Method 4: Discounting
> [!important]
> ![](Policy_Gradient_Optimization.assets/bae68c42e84376e414c4c5093ef05972_MD5.jpeg)


### Method 5: GAE(PPO)
> [!important]
> ![](Policy_Gradient_Optimization.assets/777f297cb848575016793c4fe101c172_MD5.jpeg)![](Policy_Gradient_Optimization.assets/99e69814a74e226bd79022823364d8cf_MD5.jpeg)




# Off-Policy-Learning
## Motivations
> [!motiv]
> ![](Policy_Gradient_Optimization.assets/a452726dfe854fa419d73457f71e75ae_MD5.jpeg)
> The on-policy means every time we want to calculate the policy gradient with sampling techniques, we have to sample from the current policy $\pi_{\theta}(a_{t}|s_{t]})$ that's parametrized by $\theta$. 
> 
> We can not utilize the policy from previous iteration steps. In other words, we have to generate a fresh bunch of samples every iteration in our algorithm.
> 
> We know using the gradient update may be small at each time step, but in order to get that tiny gradient update, we have to perform a sampling(which requires time). Thus on-policy learning is not necessarily the best choice.
> 
> **So the flip side would be:** If the trajectory sampling procedure is simple and not compuy intensive, then the policy gradient algorithm will be very good at picking the best policy in terms of time and performance.



## Workflow
> [!algo]
> ![](Policy_Gradient_Optimization.assets/769914c0b9da71f00d0b5b6877ac9017_MD5.jpeg)



## Importance Sampling
> [!important]
> ![](Policy_Gradient_Optimization.assets/fb84458128ae9e0470627f10a79bdd77_MD5.jpeg)![](Policy_Gradient_Optimization.assets/a66e1ec31737630f89e31a2c95d969f5_MD5.jpeg)



## Off Policy Gradient
> [!def]
> ![](Policy_Gradient_Optimization.assets/2a55e1b5f7af8eb1e3f002b3dd7eb35f_MD5.jpeg)![](Policy_Gradient_Optimization.assets/49db95d645667f1f7346f4c9b1cb8200_MD5.jpeg)






## Reward Hacking
> [!important]
> ![](Policy_Gradient_Optimization.assets/image-20241114132359598.png)












