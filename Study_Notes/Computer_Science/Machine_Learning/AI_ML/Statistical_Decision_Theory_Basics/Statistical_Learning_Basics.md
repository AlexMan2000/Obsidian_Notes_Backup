



# Decision Theory Framework
## General Setup
> [!important]
> ![](Statistical_Learning_Basics.assets/image-20240204191500362.png)![](Statistical_Learning_Basics.assets/image-20240204191507845.png)



# Risk Minimization
## Frequentist Risk
> [!def]
> ![](Statistical_Learning_Basics.assets/image-20240204191516660.png)![](Statistical_Learning_Basics.assets/image-20240204191521298.png)


## Bayesian Posterior Risk
> [!def]
> ![](Statistical_Learning_Basics.assets/image-20240204191529633.png)


## Bayes Risk
> [!def]
> ![](Statistical_Learning_Basics.assets/image-20240204191542239.png)


## Risk Minimization Scheme
> [!def]
> ![](Statistical_Learning_Basics.assets/image-20240204191606163.png)

> [!example] Square Loss
> ![](Statistical_Learning_Basics.assets/image-20240204191616853.png)

> [!example] 0-1 Loss
> ![](Statistical_Learning_Basics.assets/image-20240204191915993.png)![](Statistical_Learning_Basics.assets/image-20240204191922544.png)


> [!example] Exponential Loss


> [!example] Logistic Loss
> 


> [!example] Hinge Loss




# Empirical Risk Minimization(ERM)
## General Setup
> [!def]
> We cannot compute $R(f)=\mathbb{E}[l(f(X),Y)]$ since we don't know $P_{\mathcal{X}\times\mathcal{Y}}$
> ![](Statistical_Learning_Basics.assets/image-20240204190646759.png)![](Statistical_Learning_Basics.assets/image-20240204191010553.png)![](Statistical_Learning_Basics.assets/image-20240204191021924.png)


## Constrained ERM
### Overfitting Problem Using ERM
> [!example]
> ![](Statistical_Learning_Basics.assets/image-20240204192535276.png)
> But under this prediction function, $\hat{f}$ has empirical risk = 0, since we correctly predict each data point. But the risk is 1 since for data point other than 0.25, 0.5, 0.75(unobserved one), the risk is 1, so the expectation should be 1.
> 
> ![](Statistical_Learning_Basics.assets/image-20240204192840260.png)


### Hypothesis Spaces
> [!def]
> ![](Statistical_Learning_Basics.assets/image-20240204192904703.png)



### CERM Algorithm
> [!def]
> ![](Statistical_Learning_Basics.assets/image-20240204192947030.png)



## Excess Risk Decomposition
### Error Decomposition
> [!def]
> ![](Statistical_Learning_Basics.assets/image-20240204193104265.png)



### Excess Risk Decomposition For ERM
> [!def]
> ![](Statistical_Learning_Basics.assets/image-20240204193229770.png)
> 
> **Approximation Error:** How good is the hypothesis class relative to all function? Should be a non-random value(the difference between two expectation).
> ![](Statistical_Learning_Basics.assets/image-20240204193310148.png)
> **Estimation Error:** Within hypothesis class, how good is the learned predictor? Should be a random variable, since $\hat{f}$ depends on the data and they are random.
> 
> ![](Statistical_Learning_Basics.assets/image-20240204193324762.png)



## Optimization Error
> [!def]
> ![](Statistical_Learning_Basics.assets/image-20240204194513195.png)![](Statistical_Learning_Basics.assets/image-20240204194448371.png)


## Error Decomposition in Practice
> [!def]
> ![](Statistical_Learning_Basics.assets/image-20240204194621134.png)





# Bias and Variance Decomposition

