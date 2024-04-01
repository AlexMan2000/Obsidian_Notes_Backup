# Input Normalization
## Batch Normalization
> [!def]
> A batch normalization layer uses a mini-batch of data to estimate the mean and standard deviation of each feature. These estimated means and standard deviations are then used to center and normalize the features of the mini-batch. 
> 
> A running average of these means and standard deviations is kept during training, and at test time these running averages are used to center and normalize features.
> 
> The batch normalization will become unstable when the batch size is too small.
> 
> For a minibatch $\mathcal{B}$, we have the following algorithm for each feature for each data point:
> ![](Normalization.assets/image-20240331113222047.png)![](Normalization.assets/image-20240331113728230.png)






## Layer Normalization










## Instance Normalization






# Parameter Normalization













# Group Normalization






