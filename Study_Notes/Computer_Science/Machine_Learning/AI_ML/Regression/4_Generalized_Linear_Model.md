# Generalized Linear Models
## Exponential Family Distrubution
> [!def]
> Suppose we have $\mathcal{D}=\{(\vec{x}_1,y_1),(\vec{x}_2,y_2),\cdots, (\vec{x}_n,y_n)\}$ where $\vec{x}_i\in\mathbb{R}^p$.
> 
> And then we have to model output $\vec{y}$ by some distribution which is parametrized by some **natural parameter** $\vec{\theta}$, then we can write the probability density of $\vec{y}$ as $$f(\vec{y}|\vec{\theta},\vec{\phi})=e^{\frac{\vec{y}^{\top}\vec{\theta}-b(\vec{\theta})}{a(\vec{\phi})}}f_0(\vec{y},\sigma^2)$$ where 
> - $\vec{\theta}$ is the (input dependent) **natural parameter** of the distribution and is determined by the dataset structure. 
> - $\vec{\phi}$ is called the **dispersion parameter** of the exponential family distribution, which contains the assumptions we made on the model. In the normal case, we have $\vec{\theta}=\vec{\mu}$ and $\vec{\phi}=$
> - $b(\vec{\theta})=log(\int_{\mathbb{R}^n}e^{\vec{y}^{\top}\vec{\theta}-b(\vec{\theta})}f_0(\vec{y},\sigma^2)d\vec{y})$ is called log-normalizer that ensures that $f(\vec{y},\vec{\theta},\sigma^2)$ is a valid probability distribution.



## GLM Formulation
> [!def]
> ![](4_Generalized_Linear_Model.assets/image-20240213112841290.png)![](4_Generalized_Linear_Model.assets/image-20240213112908437.png)![](4_Generalized_Linear_Model.assets/image-20240213113035121.png)




## MLE Formulation
> [!concept]
> Suppose the model coefficients are fixed(frequentist perspective), the MLE is equivalent to the following optimization problem:
> $$\max_{\vec{\beta}}f(\vec{y},X\vec{\beta})$$




# Exponential Distribution Examples
## Bernoulli Model
> [!def]
> ![](4_Generalized_Linear_Model.assets/image-20240213113259477.png)![](4_Generalized_Linear_Model.assets/image-20240213113607868.png)
> Here the canonical link function is calculated as follows:
> 1. $\mu=\mathbb{E}_{Y\sim{\mathbb{R}_{Y\mid X}}}[Y|X]=p$
> 2. $\eta=\vec{\beta}^{\top}X=\theta$
> 3. We already know from the exponential distribution that $\theta=log(\frac{1-p}{p})$, thus $g(\mu)=log(\frac{1-\,u}{\mu})=\eta$



## Possion Model
> [!def]
> ![](4_Generalized_Linear_Model.assets/image-20240213113626717.png)
> Here the canonical link function $g(\mu)=log\mu$ so that $g(\mu)=loge^{\theta}=\theta=\eta$



## Gaussian Model
> [!def]
> ![](4_Generalized_Linear_Model.assets/image-20240213113645180.png)
> Here the canonical link function $g(\mu)=\mu$



## Multinomial Model
> [!def]
> Suppose $\vec{y}\sim Multinomial(n,\vec{\pi})$, then:
> 1. $y_i$ denotes the number of elements in categorial $i$, which is probability $\pi_i$
> 2. $\vec{\pi}$ is a probability vector that satisfies $\sum\limits_{i=1}^K\pi_i=1$
> 3. $\vec{y}$ is a counting vector that satisfies $\sum\limits_{i=1}^Ky_i=N$
> 4. $N$ is total counts.
> 5. 
> We know for multinomial distribution:$$\begin{aligned}P(\vec{y}, \vec{\pi}) & =\frac{N !}{\prod_{i=1}^K y_{i} !} \prod_{i=1}^K \pi_i^{y_i} \\& =\frac{N !}{\prod_i^k y_{i} !} \exp \left\{\sum_{i=1}^K y_i \log \pi_i\right\}\end{aligned}$$
> 
> The function $l(\vec{\pi})=\sum_{i=1}^k y_i \log \pi_i$ is concave in $\vec{\pi}$ since it is $\sum_{i=1}^k y_i \log \left(A_i \vec{\pi}\right)$ where $A_i$ is a identity matrix with the i-th diagonal being 1, other diagonal being 0, $\log \left(A_i \vec{\pi}\right)$ is concave in $\vec{\pi}$ since it's concave composition of linear mapping of $\vec{\pi}$ and that $\sum_{i=1}^K y_i \log \left(A_i \vec{\pi}\right)$ is concave since it's nonnegative sum of concave functions in $\vec{\pi}$, thus setting gradient to 0 is safe.
> 
> $$\begin{aligned}\nabla l(\vec{\pi})_i & =\frac{y_i}{\pi_i}-\frac{n-\sum_{i=1}^K y_i}{1-\sum_{i=1}^{k-1} \pi_i}=0 \quad i=1,2, \cdots, k-1 \\\hat{\pi}_i & =\frac{y_i}{N} \quad \forall i=1,2, \cdots, k-1 \\\widehat{\pi}_k & =1-\sum_{i=1}^{K-1} \pi_i \\& =\frac{y_k}{N} \\\therefore \hat{\pi}_i & =\frac{y_i}{N}\quad \forall i=1,2, \cdots, K\end{aligned}$$



## Categorical Model
> [!def]
> ![](4_Generalized_Linear_Model.assets/image-20240227133659062.png)![](4_Generalized_Linear_Model.assets/image-20240227133743759.png)![](4_Generalized_Linear_Model.assets/image-20240227133634137.png)![](4_Generalized_Linear_Model.assets/image-20240227133807898.png)
> Here basically $\mu=N$, the number of training data points.


# Properties of Exp Family
## Log Normalizer
### Mean - First Order Derivative
> [!property]
> $$\begin{aligned}& f(\vec{y}, \vec{\theta})=e^{\vec{y}^{\top} \vec{\theta}-b(\vec{\theta})} f_0(\vec{y}) \\& b(\vec{\theta})=\log \int_{\vec{y} \in R^p} e^{\vec{y}^T \vec{\theta}} f_0(\vec{y}) d \vec{y} \\& \therefore \nabla_{\vec{\theta}} b(\vec{\theta})=\frac{\int_{\vec{y} \in R^p} \nabla e^{\vec{y}^{\top} \vec{\theta}} f_0(\vec{y}) d \vec{y}}{\int_{\vec{y} \in R^p} e^{\vec{y}^{\top} \vec{\theta}} f_0(\vec{y}) d \vec{y}} \\& =\frac{\int_{\vec{y} \in R^p} \vec{y} e^{\vec{y}^{\top} \vec{\theta}} f_0(\vec{y}) d \vec{y}}{e^{b(\vec{\theta})}} \\& =\int_{\vec{y} \in R^p} \vec{y}\left(e^{\vec{y}^{\top} \vec{\theta}-b(\vec{\theta})} f_0(\vec{y})\right) d \vec{y} \\& =E[\vec{y}] \text {. } \\&\end{aligned}$$


### Covariance - Hessian
> [!property]
> Another very important property of log normalizer is that: $Cov(\vec{y})=\nabla^2_{\vec{\theta}}b(\vec{\theta})$
> ![](4_Generalized_Linear_Model.assets/image-20240213205103422.png)![](4_Generalized_Linear_Model.assets/image-20240213205113941.png)

> [!property] Covariance Matrix is PSD
> ![](4_Generalized_Linear_Model.assets/image-20240213210251684.png)
> Here since the hessian of $b(\vec{\theta})$ is PSD, so $b(\vec{\theta})$ is convex in $\vec{\theta}$.



## Repeated Sampling
> [!property]
> Suppose we sample $\vec{y_{1}},\vec{y_{2}},\cdots, \vec{y_{n}}\sim \mathbb{P}_{\theta}(\vec{y})$ i.i.d, then we will have:
> $p_{\vec{\theta}}(\vec{y}_1,\cdots,\vec{y}_n)=exp\{\theta^{\top}(\sum\limits_{i=1}^n\vec{y}_i)-nb(\vec{\theta})\}\prod_{i=1}^nf_0(\vec{y}_i)$ and that $(\vec{y}_1,\cdots,\vec{y}_n)$ belongs to a new exponential family:$$\left\{\begin{array}{l}\vec{\theta}^{(n)}=n \vec{\theta} \\T^{(n)}\left(\vec{y}_1, \cdots, \vec{y}_n\right)=\frac{1}{n} \sum_{i=1}^n \vec{y_i} \\b^{(n)}\left(\vec{\theta}^{(n)}\right)=n b\left(\vec{\theta}^{(n)} / n\right) \\f_0^{(n)}\left(\vec{y}_1, \cdots, \vec{y}_n\right)=\prod_{1=1}^n f_0\left(\vec{y}_i\right)\end{array}\right.$$


## Conditioning
> [!property]
> Suppose we have exponential family $$f(\vec{y}|\vec{\theta})=e^{\vec{y}^{\top}\vec{\theta}-b(\vec{\theta})}f_0(\vec{y})$$
> Then, conditioning on an event $\vec{y}\in \mathcal{\vec{Y}}_0$, the resulting conditional distribution is still an exponential family distribution:
> $$f(\vec{y}|\vec{\theta},\vec{y}\in \mathcal{\vec{Y}}_0)=e^{\vec{y}^{\top}\vec{\theta}-\tilde{b}(\vec{\theta})}\tilde{f_0}(\vec{y})$$

> [!proof]
> The proof is as follows:
> $$\begin{aligned}f\left(\vec{y} \mid \vec{\theta}, \vec{y} \in \vec{\mathcal{Y}}_0\right) & =\frac{f(\vec{y}) \cdot \mathbb{1}\left\{\vec{y} \in \vec{\mathcal{Y}}_0\right\}}{P_{\vec{\theta}}\left(\vec{y} \in \vec{\mathcal{Y}}_0\right)} \\& =\frac{e^{\vec{\theta}^{\top} \vec{y}-b(\vec{\theta})} f_0(\vec{y}) \cdot \mathbb{1}\left\{\vec{y} \in \vec{\mathcal{Y}}_0\right\}}{P_{\vec{\theta}}\left(\vec{y} \in \vec{\mathcal{Y}}_0\right)} \\& =e^{\vec{\theta}^{\top} \vec{y}-b(\vec{\theta})-\log P_{\vec{\theta}}\left(\vec{y} \in \vec{\mathcal{Y}}_0\right) }\cdot f_0(\vec{y}) \mathbb{1}\left\{\vec{y} \in \vec{\mathcal{Y}}_0\right\} \\& =e^{\vec{\theta}^{\top} \vec{y}-\tilde{b}(\vec{\theta})} \cdot \tilde{f}_0(\vec{y})\end{aligned}$$ where $\tilde{f}_0(\vec{y})=f_0(\vec{y})\cdot\mathbb{1}\left\{\vec{y} \in \vec{\mathcal{Y}}_0\right\}$ and $\tilde{b}(\vec{\theta})=b(\vec{\theta})-\log P_{\vec{\theta}}(\vec{y} \in \vec{\mathcal{Y}}_0)$




## Conjugate Prior
> [!def]
> 




# Regression Models in GLM 
## General Settings
> [!def]
> ![](4_Generalized_Linear_Model.assets/image-20240215221723746.png)![](4_Generalized_Linear_Model.assets/image-20240215221730872.png)![](4_Generalized_Linear_Model.assets/image-20240215221743943.png)![](4_Generalized_Linear_Model.assets/image-20240215221803946.png)






## Linear Regression - Gaussian GLM
> [!def]
> 





## Logistic Regression - Bernoulli GLM
> [!def]
> 





## Possion Regression - Poisson GLM
> [!def]





## Multinomial Regression - Multinomial GLM
> [!def]



