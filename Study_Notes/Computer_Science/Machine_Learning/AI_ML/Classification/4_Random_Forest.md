# Trainng of Random Forests
## Overview
> [!def]
> ![](4_Random_Forest.assets/image-20240219141340073.png)![](4_Random_Forest.assets/image-20240219141344984.png)![](4_Random_Forest.assets/image-20240219141803226.png)




## Bagging
> [!def]
> ![](4_Random_Forest.assets/image-20240219153655056.png)![](4_Random_Forest.assets/image-20240219153706629.png)![](4_Random_Forest.assets/image-20240219155111636.png)




### Bootstrap
> [!def]
> ![](4_Random_Forest.assets/image-20240219154010882.png)


### Aggregation
> [!def]
> ![](4_Random_Forest.assets/image-20240219154203359.png)![](4_Random_Forest.assets/image-20240219154208518.png)
> Derivations about why $\frac{1}{3}$ of the original training data points will be left out:
> 
> ![](4_Random_Forest.assets/image-20240219160430165.png)

> [!algo]
> ![](4_Random_Forest.assets/image-20240219153749042.png)


### Issue with Bagging
> [!important]
> ![](4_Random_Forest.assets/image-20240219155140929.png)![](4_Random_Forest.assets/image-20240219155158939.png)![](4_Random_Forest.assets/image-20240219155206992.png)


## Feature Randomization
> [!def]
> ![](4_Random_Forest.assets/image-20240219155229536.png)![](4_Random_Forest.assets/image-20240219155321386.png)






## AdaBoosting
> [!def]
> ![](4_Random_Forest.assets/image-20240219154440905.png)![](4_Random_Forest.assets/image-20240219155337745.png)





### AdaBoost
> [!def]
> ![](4_Random_Forest.assets/image-20240219141905299.png)

> [!algo]
> ![](4_Random_Forest.assets/image-20240219141936207.png)![](4_Random_Forest.assets/image-20240219141940941.png)
> **Remarks:**
> 
> ![](4_Random_Forest.assets/image-20240219143931915.png)


### Derivation of AdaBoost
> [!important]
> ![](4_Random_Forest.assets/image-20240219144710419.png)![](4_Random_Forest.assets/image-20240219145229169.png)![](4_Random_Forest.assets/image-20240219145258502.png)![](4_Random_Forest.assets/image-20240219145309439.png)![](4_Random_Forest.assets/image-20240219145319380.png)

> [!info]
> ![](4_Random_Forest.assets/image-20240219145351891.png)




# Gradient Boosting
## Overview
> [!def]
> ![](4_Random_Forest.assets/image-20240219151116684.png)![](4_Random_Forest.assets/image-20240219151133240.png)![](4_Random_Forest.assets/image-20240219161111072.png)



## GB for Regression
### Motivations
> [!motiv] Motivation
> ![](4_Random_Forest.assets/image-20240219161303815.png)![](4_Random_Forest.assets/image-20240219161311519.png)![](4_Random_Forest.assets/image-20240219161337728.png)![](4_Random_Forest.assets/image-20240219161449822.png)


### Relation to Gradient Descent
> [!important]
> ![](4_Random_Forest.assets/image-20240219161608304.png)![](4_Random_Forest.assets/image-20240219161624773.png)![](4_Random_Forest.assets/image-20240219161642220.png)






### Algorithm Procedures
> [!algo]
> ![](4_Random_Forest.assets/image-20240219161759859.png)![](4_Random_Forest.assets/image-20240219163101267.png)![](4_Random_Forest.assets/image-20240219163106052.png)
> The term "negative gradient pays less attention to outliers" means that when the error is large (beyond the threshold $\delta$), the update is capped at $\delta$. 
> 
> This means large errors (often due to outliers) do not disproportionately influence the model update. 
> 
> Their influence is limited to a fixed value $\delta$, preventing outliers from having too much weight in the model fitting process, which could skew the model and harm its performance on the rest of the data.




### Loss Function for GB
> [!def]
> ![](4_Random_Forest.assets/image-20240219162549455.png)![](4_Random_Forest.assets/image-20240219162611247.png)


### GB with Absolute Loss
> [!def]
> ![](4_Random_Forest.assets/image-20240219162706666.png)



### GB with Huber Loss
> [!def]
> ![](4_Random_Forest.assets/image-20240219162715785.png)


## GB for Classification
### Motivations
> [!motiv] Motivations
> ![](4_Random_Forest.assets/image-20240219163640561.png)![](4_Random_Forest.assets/image-20240219163715651.png)


### Algorithm Procedures
> [!algo]
> ![](4_Random_Forest.assets/image-20240219164306224.png)![](4_Random_Forest.assets/image-20240219164324251.png)



### Difference with GB for Regression
> [!def]
> ![](4_Random_Forest.assets/image-20240219164345945.png)![](4_Random_Forest.assets/image-20240219164352435.png)![](4_Random_Forest.assets/image-20240219164424090.png)

> [!example] 
> ![](4_Random_Forest.assets/image-20240219164610292.png)![](4_Random_Forest.assets/image-20240219164817926.png)![](4_Random_Forest.assets/image-20240219164824158.png)![](4_Random_Forest.assets/image-20240219164842492.png)![](4_Random_Forest.assets/image-20240219164849214.png)![](4_Random_Forest.assets/image-20240219164856048.png)


## Choosing Learning Rate for GB





# Prediction with Random Forests
> [!def]
> ![](4_Random_Forest.assets/image-20240219144200311.png)




# Evaluation of Random Forests
## Margin Function
> [!def]
> ![](4_Random_Forest.assets/image-20240219114632196.png)
> The larger the margin, the more confidence in the classification
> 
> 


 
## Generalization Error
> [!def]
> ![](4_Random_Forest.assets/image-20240219114800253.png)
> $mg(X,Y)<0$ means that on average there are more trees that are predicting incorrectly.

> [!thm]
> Overfitting is not a problem:
> ![](4_Random_Forest.assets/image-20240219114751693.png)

> [!proof]
> ![](4_Random_Forest.assets/image-20240220174243947.png)






