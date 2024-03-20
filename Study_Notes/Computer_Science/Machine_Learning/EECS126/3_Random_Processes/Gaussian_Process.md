# Basic Definition
## Stochastic Process
> [!def]
> ![](Gaussian_Process.assets/image-20240320121353977.png)



## Mean and Covariance Function
> [!def]
> ![](Gaussian_Process.assets/image-20240320121427634.png)


### Mean Function
> [!def]
> ![](Gaussian_Process.assets/image-20240320121456935.png)





### Covariance Function
> [!def]
> ![](Gaussian_Process.assets/image-20240320121513395.png)



### Kernel Choice for Covariance
> [!def]
> ![](Gaussian_Process.assets/image-20240320121539154.png)![](Gaussian_Process.assets/image-20240320121547380.png)![](Gaussian_Process.assets/image-20240320122124007.png)![](Gaussian_Process.assets/image-20240320122131011.png)


### Code Implementations
> [!code]
```python
from __future__ import division
import numpy as np
import matplotlib.pyplot as pl

def kernel(a, b):
    """ GP squared exponential kernel """
    sqdist = np.sum(a**2, 1).reshape(-1, 1) + np.sum(b**2, 1) - 2 * np.dot(a, b.T)
    return np.exp(-.5 * sqdist)

n = 50
Xtest = np.linspace(-5, 5, n).reshape(-1, 1)
K_ = kernel(Xtest, Xtest)

# draw samples from the prior at our test points.
# Here, we can think of L as our function mapping from x to f(x) as a vector.
L = np.linalg.cholesky(K_ + 1e-6*np.eye(n))
f_prior = np.dot(L, np.random.normal(size=(n, 10)))

pl.plot(Xtest, f_prior)
```




# Covariance Function Tuning






# Control the Gaussian Process
> [!def]
> ![](Gaussian_Process.assets/image-20240320113701407.png)

> [!example]
> ![](Gaussian_Process.assets/image-20240320113729402.png)



# Combining Kernels
> [!def]
> ![](Gaussian_Process.assets/image-20240320113804032.png)









