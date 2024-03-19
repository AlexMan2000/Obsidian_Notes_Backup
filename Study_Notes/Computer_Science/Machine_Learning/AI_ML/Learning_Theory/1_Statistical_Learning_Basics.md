# Decision Theory Framework
## General Setup
> [!important]
> ![](1_Statistical_Learning_Basics.assets/image-20240204191500362.png)![](1_Statistical_Learning_Basics.assets/image-20240204191507845.png)



# Risk Minimization
## Frequentist Risk
> [!def]
> ![](1_Statistical_Learning_Basics.assets/image-20240204191516660.png)![](1_Statistical_Learning_Basics.assets/image-20240204191521298.png)


## Bayesian Posterior Risk
> [!def]
> ![](1_Statistical_Learning_Basics.assets/image-20240204191529633.png)


## Bayes Risk
> [!def]
> ![](1_Statistical_Learning_Basics.assets/image-20240204191542239.png)


## Risk Minimization Scheme
> [!def]
> ![](1_Statistical_Learning_Basics.assets/image-20240204191606163.png)

> [!example] Square Loss
> ![](1_Statistical_Learning_Basics.assets/image-20240204191616853.png)

> [!example] 0-1 Loss
> ![](1_Statistical_Learning_Basics.assets/image-20240204191915993.png)![](1_Statistical_Learning_Basics.assets/image-20240204191922544.png)


> [!example] Exponential Loss


> [!example] Logistic Loss
> 


> [!example] Hinge Loss




# Empirical Risk Minimization(ERM)
## General Setup
> [!def]
> We cannot compute $R(f)=\mathbb{E}[l(f(X),Y)]$ since we don't know $P_{\mathcal{X}\times\mathcal{Y}}$
> ![](1_Statistical_Learning_Basics.assets/image-20240204190646759.png)![](1_Statistical_Learning_Basics.assets/image-20240204191010553.png)![](1_Statistical_Learning_Basics.assets/image-20240204191021924.png)


## Constrained ERM
### Overfitting Problem Using ERM
> [!example]
> ![](1_Statistical_Learning_Basics.assets/image-20240204192535276.png)
> But under this prediction function, $\hat{f}$ has empirical risk = 0, since we correctly predict each data point. But the risk is 1 since for data point other than 0.25, 0.5, 0.75(unobserved one), the risk is 1, so the expectation should be 1.
> 
> ![](1_Statistical_Learning_Basics.assets/image-20240204192840260.png)


### Hypothesis Spaces
> [!def]
> ![](1_Statistical_Learning_Basics.assets/image-20240204192904703.png)



### CERM Algorithm
> [!def]
> ![](1_Statistical_Learning_Basics.assets/image-20240204192947030.png)



## Excess Risk Decomposition
### Error Decomposition
> [!def]
> ![](1_Statistical_Learning_Basics.assets/image-20240204193104265.png)



### Excess Risk Decomposition For ERM
> [!def]
> ![](1_Statistical_Learning_Basics.assets/image-20240204193229770.png)
> 
> **Approximation Error:** How good is the hypothesis class relative to all function? Should be a non-random value(the difference between two expectation).
> ![](1_Statistical_Learning_Basics.assets/image-20240204193310148.png)
> **Estimation Error:** Within hypothesis class, how good is the learned predictor? Should be a random variable, since $\hat{f}$ depends on the data and they are random.
> 
> ![](1_Statistical_Learning_Basics.assets/image-20240204193324762.png)



## Optimization Error
> [!def]
> ![](1_Statistical_Learning_Basics.assets/image-20240204194513195.png)![](1_Statistical_Learning_Basics.assets/image-20240204194448371.png)


## Error Decomposition in Practice
> [!def]
> ![](1_Statistical_Learning_Basics.assets/image-20240204194621134.png)





# Bias and Variance Decomposition
## Metric
> [!def]
> ![](1_Statistical_Learning_Basics.assets/image-20240319094558292.png)![](1_Statistical_Learning_Basics.assets/image-20240319094605651.png)





## Generalization Error
> [!def]
> ![](1_Statistical_Learning_Basics.assets/image-20240219103920706.png)
> Note that the generalization error could be chosen as MSE, defined by:
> $$\mathbb{E}_{\mathcal{D},Y}[(h(\mathbf{x};\mathcal{D})-Y)^2]$$
> where $h(\cdot)$ is our model, which is trained on a random data $\mathcal{D}$.
> 
> Note that we can choose different error function to do such decomposition.



 

## BV Decomposition
> [!important]
> ![](1_Statistical_Learning_Basics.assets/image-20240219103858369.png)![](1_Statistical_Learning_Basics.assets/image-20240319094511065.png)
> Here the irreducible error is the lower bound for our generalization error, which is the error that any model will not be able to get rid of, indicating the difficulty of this task.
> 
> ![](1_Statistical_Learning_Basics.assets/image-20240219104211581.png)![](1_Statistical_Learning_Basics.assets/image-20240219104218402.png)

> [!important] Alternative Derivations
> ![](1_Statistical_Learning_Basics.assets/image-20240319103135230.png)![](1_Statistical_Learning_Basics.assets/image-20240319103144608.png)





## Summary
> [!summary] 
> ![](1_Statistical_Learning_Basics.assets/image-20240219104306732.png)![](1_Statistical_Learning_Basics.assets/image-20240219104316356.png)



# Bias-Variance Tradeoff and Regularization
> [!example] DS-GA-1003 Sp24 P5 / EECS189 Fa23 HW5 P1
> ![](1_Statistical_Learning_Basics.assets/image-20240319110344044.png)![](1_Statistical_Learning_Basics.assets/image-20240319110348880.png)![](1_Statistical_Learning_Basics.assets/image-20240319110357655.png)![](1_Statistical_Learning_Basics.assets/image-20240319110402703.png)![](1_Statistical_Learning_Basics.assets/image-20240319110413484.png)![](1_Statistical_Learning_Basics.assets/image-20240319110420811.png)![](1_Statistical_Learning_Basics.assets/image-20240319110429089.png)
















