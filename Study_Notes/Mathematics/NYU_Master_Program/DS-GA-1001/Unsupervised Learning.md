# PCA
## Eigenvalues
> [!important]
> Eigenvalues of the principal components corresponds to its explained variance, the larger, the more information it contained.



## Kaiser Criterion
> [!important]
> According to the Kaiser criterion, only those factors or principal components whose eigenvalues are greater than 1 should be retained. The rationale behind this rule is that an eigenvalue of 1 represents the amount of variance that is accounted for by one original variable. Thus, any factor or principal component with an eigenvalue less than 1 contributes less to explaining the variance than a single variable and is therefore considered less important.




# Clustering
## K-Means Clustering
### Basics
> [!important]
> ![](Unsupervised%20Learning.assets/image-20231217141129077.png)
> **K-Means yields:**
> 1. The optimal location of cluster centers (centroids) that minimize the distance of all data to all cluster centers
> 2. Labeling the data in the clusters in terms of their nearest center
> 
> **Doesn't yield:**
> 1. The number of clusters
> 2. We can only eyeball the elbow point, which is inaccurate.
> 
> 

### Pros and Cons
> [!important]
> ![](Unsupervised%20Learning.assets/image-20231217150148117.png)




## Sihouette Evaluation
> [!important]
> ![](Unsupervised%20Learning.assets/image-20231217145852053.png)
> The bigger, the better classification it is.



## DBSCAN
### Basic Concepts
> [!important]
> We have several useful concepts:
> 1. **Core points:** Those points are defined to be the points that contain at least $M$ points within its $\epsilon$ neighbor. Here the $M$ and $\epsilon$ is hyperparametrized by the programmers.
> 2. **Reachability:** We say that a point $q$ is reachable from $p$ if there exists a sequence $p = p_1,p_2,\cdots,p_i=q$ where $p_i$ is within the $\epsilon$ neighbor of $p_i$, forall $i=1,2,\cdots, i=1$. Here each $p_i$ should be a core point, except for the last one $q$.
> 3. **Border Point:** Reachable from core points. 
> 4. **Outlier Point:** Unreachable from core points.



### Expand Cluster Procedure
> [!important]
> ![](Unsupervised%20Learning.assets/image-20231217150839782.png)
> You can use the DFS algorithm to determine all the clusters.


### Pros and Cons
> [!important]
> ![](Unsupervised%20Learning.assets/image-20231217151315345.png)




