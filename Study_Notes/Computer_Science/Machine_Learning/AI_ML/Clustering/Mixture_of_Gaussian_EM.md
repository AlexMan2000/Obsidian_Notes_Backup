Also See [GMMEMNotes](GMMEMNotes.pdf)
# Basic Definition
> [!def]
> ![](Mixture_of_Gaussian_EM.assets/image-20240418143717405.png)

> [!example]
> ![](Mixture_of_Gaussian_EM.assets/image-20240418143738509.png)![](Mixture_of_Gaussian_EM.assets/image-20240418143748323.png)




# Fitting GMM
## Problem Descriptions
> [!def]
> ![](Mixture_of_Gaussian_EM.assets/image-20240418143924762.png)



## Trick 1: Latent Variables
> [!def]
> ![](Mixture_of_Gaussian_EM.assets/image-20240418143950976.png)![](Mixture_of_Gaussian_EM.assets/image-20240418144043588.png)

## Trick 2: MLE
> [!def]
> ![](Mixture_of_Gaussian_EM.assets/image-20240418144224984.png)![](Mixture_of_Gaussian_EM.assets/image-20240418144235919.png)
> More see [GDA](../Classification_Decision/2_Gaussian_Discriminative_Analysis.md#GDA)
> Here:
> - $\mu_k$ is the group mean. The mean of samples that belong to label $k$.
> - $\Sigma_k$ is the group variance. The covariance matrix of samples that belong to label $k$.
> - $\pi_k$ is the probability of this group(number of samples with label $k$).




# EM Algorithm - Version 1
## Motivation
> [!motiv]
> ![](Mixture_of_Gaussian_EM.assets/image-20240418144823030.png)![](Mixture_of_Gaussian_EM.assets/image-20240418144930668.png)






## E-Step: Responsabilities
> [!important]
> ![](Mixture_of_Gaussian_EM.assets/image-20240418145002322.png)
> $\gamma_k$ is an auxiliary random variable, different from $\pi_k$ where $\pi_k$ is our GMM parameter.
> ![](Mixture_of_Gaussian_EM.assets/image-20240825225417881.png)![](Mixture_of_Gaussian_EM.assets/image-20240825225433885.png)








## M-Step: Estimate Parameters
> [!important]
> ![](Mixture_of_Gaussian_EM.assets/image-20240418145026978.png)![](Mixture_of_Gaussian_EM.assets/image-20240418145058031.png)![](Mixture_of_Gaussian_EM.assets/image-20240418150548482.png)


## Summary
> [!summary]
> ![](Mixture_of_Gaussian_EM.assets/image-20240418150706368.png)




# EM Algorithm - Version 2
## Algorithm
> [!def]
> ![](Mixture_of_Gaussian_EM.assets/image-20240418150642626.png)![](Mixture_of_Gaussian_EM.assets/image-20240418150649179.png)





## Derivations
> [!important]
> ![](Mixture_of_Gaussian_EM.assets/image-20240418150739673.png)![](Mixture_of_Gaussian_EM.assets/image-20240418150744841.png)![](Mixture_of_Gaussian_EM.assets/image-20240418150749694.png)![](Mixture_of_Gaussian_EM.assets/image-20240418150755537.png)![](Mixture_of_Gaussian_EM.assets/image-20240418150800550.png)![](Mixture_of_Gaussian_EM.assets/image-20240418150810254.png)



# Genreal EM Algorithm
> [!important]
> ![](Mixture_of_Gaussian_EM.assets/image-20240418151728887.png)![](Mixture_of_Gaussian_EM.assets/image-20240418151707770.png)




# GMM vs K-Means
> [!important]
> ![](Mixture_of_Gaussian_EM.assets/image-20240418150934884.png)




# EM Implementations
> [!code]
```python



```





# EM Algorithm Optimization Details
## Surrogate Optimization
> [!important]
> More in [GMMEMNotes](GMMEMNotes.pdf)
> ![](Mixture_of_Gaussian_EM.assets/image-20240418152923363.png)



## Convergence of EM
> [!def]
> ![](Mixture_of_Gaussian_EM.assets/image-20240418160650407.png)![](Mixture_of_Gaussian_EM.assets/image-20240418160724634.png)![](Mixture_of_Gaussian_EM.assets/image-20240418160730764.png)![](Mixture_of_Gaussian_EM.assets/image-20240418160920891.png)![](Mixture_of_Gaussian_EM.assets/image-20240418160929071.png)![](Mixture_of_Gaussian_EM.assets/image-20240418161044721.png)![](Mixture_of_Gaussian_EM.assets/image-20240418161127131.png)















