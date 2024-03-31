# Motivations
> [!motiv] Why we need T-SNE
> ![](T-SNE.assets/image-20240330112457586.png)![](T-SNE.assets/image-20240330112525617.png)


# Locally Linear Embedding(LLE)
## Definition
> [!def]
> ![](T-SNE.assets/image-20240330115107940.png)
> Here $j\in N_{\epsilon}(\vec{x_i})$。
> 
> Then we want to find a dimension reduction scheme such that $\vec{x}_{i}\to \vec{z}_{i}$ and $W$ remains unchanged.
> ![](T-SNE.assets/image-20240330115513966.png)



## Choose Number of Neighbors
> [!important]
> ![](T-SNE.assets/image-20240330115654868.png)
> K must be just right.


## Problem on LLE
> [!example]
> ![](T-SNE.assets/image-20240330120446431.png)




# Laplacian Eigenmaps
> More on [Laplacian Matrix](../../EECS127AB/1_Linear_Algebra_Review/Structured_Matrices.md#Laplacian%20Matrix)

> [!def]
> ![](T-SNE.assets/image-20240330120051932.png)![](T-SNE.assets/image-20240330120314228.png)



# Spectral Embedding
> [!def]
> ![](T-SNE.assets/image-20240330123233061.png)![](T-SNE.assets/image-20240330123238274.png)






# Neighborhood Embeddings
## Definitions
> [!def]
> ![](T-SNE.assets/image-20240330114015426.png)



## NE - Isomap
> [!important]
> ![](T-SNE.assets/image-20240330114242726.png)![](T-SNE.assets/image-20240330114351279.png)![](T-SNE.assets/image-20240330114709037.png)



## Stochastic NE(SNE)
> [!def]
> ![](T-SNE.assets/image-20240330120732676.png)


### Probability Matrix
> [!important]
> ![](T-SNE.assets/image-20240330120801014.png)


### Perplexity
> [!def]
> ![](T-SNE.assets/image-20240330121002707.png)![](T-SNE.assets/image-20240330121013359.png)


### SNE-Objective
> [!def]
> ![](T-SNE.assets/image-20240330121031413.png)![](T-SNE.assets/image-20240330121318565.png)




# T-SNE
## Definition
> [!def]
> ![](T-SNE.assets/image-20240330121527100.png)![](T-SNE.assets/image-20240330122911867.png)![](T-SNE.assets/image-20240330122958683.png)




## Gradient
> [!important]
> ![](T-SNE.assets/image-20240330124239656.png)![](T-SNE.assets/image-20240330121534230.png)

> [!proof] Derivations
> ![](T-SNE.assets/image-20240330124559067.png)![](T-SNE.assets/image-20240330124605370.png)![](T-SNE.assets/image-20240330124610776.png)![](T-SNE.assets/image-20240330124620102.png)![](T-SNE.assets/image-20240330124627281.png)![](T-SNE.assets/image-20240330124635256.png)



## Algorithms
> [!algo]
> ![](T-SNE.assets/image-20240330121556609.png)





# Comparison between PCA and T-SNE
> [!important]
> ![](T-SNE.assets/image-20240330125302485.png)
> t-SNE is a nonlinear technique that focuses on preserving the pairwise similarities between data points in a lower-dimensional space. t-SNE is concerned with preserving small pairwise distances whereas, PCA focuses on maintaining large pairwise distances to maximize variance.
> 
> In summary, PCA preserves the variance in the data, whereas t-SNE preserves the relationships between data points in a lower-dimensional space, making it quite a good algorithm for visualizing complex high-dimensional data.







