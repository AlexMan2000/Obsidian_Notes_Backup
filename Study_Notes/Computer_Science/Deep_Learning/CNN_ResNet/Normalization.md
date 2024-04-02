# Motivations
## Why we need normalization?
> [!important]
> Normalizing our training data before inputting them into neural networks has a similar effect of scaling the parameters such that the **raw magnitudes of the values don’t necessarily impact the gradient calculation during the gradient descent** backpropagating step (if we had massive, un-normalized values, the gradient would always be large).
> 
> Moreover, the data points are generally centered at zero because the ReLU layers are often initialized at that point, making the neural net most sensitive and expressive when input values are around zero. **Thus, normalization can sometimes additionally decrease the neural network’s training time.**
> 

> [!bug] Caveats
> However, there are scenarios where normalization might not only be unnecessary but could also hinder the model's ability to accurately classify instances. **One such scenario involves cases where the magnitude of the values itself carries significant information that is critical for accurate classification.**

> [!example]
> ![](Normalization.assets/image-20240401173541458.png)




# Input Normalization
## Batch Normalization
### ID Case
> [!def]
> **Batch Normalization during Training:**
> 
> A batch normalization layer uses a mini-batch of data to estimate the mean and standard deviation of each feature. These estimated means and standard deviations are then used to center and normalize the features of the mini-batch. 
> 
> A running average of these means and standard deviations is kept during training, and at test time these running averages are used to center and normalize features.
> 
> The batch normalization will become unstable when the batch size is too small.
> 
> For a minibatch $\mathcal{B}$, we have the following algorithm for each feature for each data point:
> ![](Normalization.assets/image-20240331113222047.png)
> **Batch Normalization during Testing:**
> 
> We cache all the $\vec{u}$ and $\vec{\sigma}$ that are computed during the training process and calculate a mean vector and standard deviation vector for testing datapoints.
> 
> ![](Normalization.assets/image-20240331113728230.png)
> This is just one way of normalizing the test data point. We could alternatively use the last epoch's mean of mean vector and standard deviation vector.


### High-dimensional Case
> [!important]
> Problem 2: Suppose our input data points have a high dimensionality $(\gg d)$, what do we average together?
> 
> To illustrate, imagine our data points represent images of size $W \times H$. We arrange the batch data points into a box of size $N_B \times C \times(W \cdot H)$ (Figure 1), where $N_B$ is the number of samples in the batch, $C$ is the number of channels in the image (e.g., $C=3$ for RGB images), and $(W \cdot H)$ is the number of different pixels in the image.
> ![](Normalization.assets/image-20240401155025106.png)![](Normalization.assets/image-20240401173235188.png)
> 
> In the standard ML perspective (Figure 1a) we would take a particular pixel on a particular channel and average it across the batch. But since we do not have enough things in a batch, we need to average across more things. And we should average across things that are alike. Think of it as 1D normalization.
> 
> In the case of **batch normalization** (Figure 1b) it is considered that the different pixels are all alike each other, but the different channels can be qualitatively different because they correspond to different features. So we average across the different pixels. Think of it as 2D normalization.
> 
> Another kind of normalization also used in practice is **layer normalization** (Figure 1c) where the different channels are averaged together. 
> - This can be done more frequently at later layers in the convolutional process because these features become learned features and there is no reason for them to be much larger than the others. 
> - This gives the advantage of a lot more averaging and removes the need to look deeper into your batch. 
> - Additionally, layer norm is computationally less costly than batch norm and in practice useful if we have hardware constraints. 
> - There are also variations of layer normalizations, such as group normalization, which consists in averaging groups of channels - average only certain channels together, channels that make sense to be averaged together.






## Layer Normalization
> [!def]
> Layer normalization normalizes input across all channels in one image.









## Instance Normalization
> [!def]
> Instance normalization normalizes across each channel in each training images. The problem instance normalization tries to address is that the network should be agnostic to the contrast of the original image.





# Parameter Normalization













# Group Normalization






