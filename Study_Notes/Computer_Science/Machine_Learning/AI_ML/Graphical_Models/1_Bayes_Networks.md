# Probability Preliminaries
## Probabilistic Inference
> [!overview]
> ![](1_Bayes_Networks.assets/image-20240303084138074.png)![](1_Bayes_Networks.assets/image-20240303084146928.png)



## Inference by Enumeration
> [!def]
> ![](1_Bayes_Networks.assets/image-20240303084225746.png)![](1_Bayes_Networks.assets/image-20240303084243346.png)![](1_Bayes_Networks.assets/image-20240303084249860.png)


## Conditional Probabilities
> [!concept] Side Note on Conditional Probability
> ![](1_Bayes_Networks.assets/image-20240303104430468.png)![](1_Bayes_Networks.assets/image-20240303104445710.png)![](1_Bayes_Networks.assets/image-20240303104453830.png)



# Bayesian Network Representation
## Motivation
> [!bug] Curse of Dimensionality
> ![](1_Bayes_Networks.assets/image-20240303084456449.png)
> For example, if we want to model $P(X_1,X_{2,\cdots,}X_n|X_{n+1})$, if we assume $(X_{1,\cdots,}X_n)$ follows multivariable gaussian distribution, we would use $n+n^2$(mean vector plus covariance matrix) to represent.
> 
> But using bayesian independece assumption we only need 2 parameters for each conditional distribution $P(X_i|X_{n+1})~\forall n=1,2\cdots, n$. Thus in total we need only $2n$ parameters, which is a huge improvements.



## Definition of Bayes Net
> [!def]
> ![](1_Bayes_Networks.assets/image-20240303084818045.png)
> **Note:** It is important to remember that the edges between Bayes Net nodes do not mean there is specifically a causal relationship between those nodes, or that the variables are necessarily dependent on one another. It just means that there may be some relationship between the nodes.
> 
> ![](1_Bayes_Networks.assets/image-20240303102421648.png)





## Bayes Net Independence
> [!important]
> ![](1_Bayes_Networks.assets/image-20240303085806294.png)![](1_Bayes_Networks.assets/image-20240303085854922.png)


## Calculate Joint Probability From CPT
> [!important] Formula
> ![](1_Bayes_Networks.assets/image-20240303085506394.png)
> Derivations depend on Bayes Independece and Chain Rule of Probability.

> [!note] Derivations
> ![](1_Bayes_Networks.assets/image-20240303090219776.png)![](1_Bayes_Networks.assets/image-20240303090227343.png)

> [!example] Example 1 - CS188 Note 13
> ![](1_Bayes_Networks.assets/image-20240303085546664.png)![](1_Bayes_Networks.assets/image-20240303085554331.png)![](1_Bayes_Networks.assets/image-20240303085559927.png)

> [!example] Example 2: Pattern Recognition pp362
> ![](1_Bayes_Networks.assets/image-20240303085625104.png)

> [!example] More Examples
> ![](1_Bayes_Networks.assets/image-20240419134920883.png)![](1_Bayes_Networks.assets/image-20240419134928312.png)





 
# Bayesian Network Causal Structure
## Three-Node Model
> [!overview]
> ![](1_Bayes_Networks.assets/image-20240303090734175.png)


### Causal Chains
> [!def]
> ![](1_Bayes_Networks.assets/image-20240303090747439.png)![](1_Bayes_Networks.assets/image-20240303090822289.png)



### Common Cause
> [!def]
> ![](1_Bayes_Networks.assets/image-20240303090846689.png)



### Common Effect
> [!def]
> ![](1_Bayes_Networks.assets/image-20240303091015201.png)![](1_Bayes_Networks.assets/image-20240303091041529.png)




## D-Separation Algorithm
### Active / Inactive Paths
> [!def]
> ![](1_Bayes_Networks.assets/image-20240303094144963.png)




### Algorithm Procedures
> [!def]
> ![](1_Bayes_Networks.assets/image-20240303092036575.png)![](1_Bayes_Networks.assets/image-20240303093115958.png)

> [!bug] Intuitive Attempt
> ![](1_Bayes_Networks.assets/image-20240303094327302.png)
> The reason why the above algorithm is not right is that if we shade Y, then X is not reachable to Z and thus $X\perp Z|Y$, but this is not true by our probablistic analysis. The reason is that such triples are considered active triples so actually $X$ is reachable to $Z$ even if $Y$ is shaded and seems to block the path.

> [!success] D-Separation Algorithm
> ![](1_Bayes_Networks.assets/image-20240303094358176.png)


### Simple Examples
> [!example] Apply D-Separation Algorithm
> ![](1_Bayes_Networks.assets/image-20240303095424703.png)![](1_Bayes_Networks.assets/image-20240303095506873.png)![](1_Bayes_Networks.assets/image-20240303095511367.png)



### Complicated Examples
> [!example] Vitamin 6 P7
> ![](1_Bayes_Networks.assets/image-20240303200808275.png)![](1_Bayes_Networks.assets/image-20240303200826524.png)![](1_Bayes_Networks.assets/image-20240303200833608.png)![](1_Bayes_Networks.assets/image-20240303200841319.png)![](1_Bayes_Networks.assets/image-20240303200857557.png)![](1_Bayes_Networks.assets/image-20240303200905905.png)













## Topology and Distributions
> [!important] List all the independence
> ![](1_Bayes_Networks.assets/image-20240303100912961.png)
> Note that, we notice that we can use multiple bayes net to encode the same independence(distribution). 
> 
> **The reasons are that:**
> 1. Some bayes net structure is computationally easier then others.
> 2. Some causal effects are more suitable to be represented by some specific structures. For example, if there is a chained causal relationship, then it's better to use causal chain model instead of common cause model.


## Examples
### Calculating Probabilities
> [!example] Vitamin 6 P5
> ![](1_Bayes_Networks.assets/image-20240303203823324.png)![](1_Bayes_Networks.assets/image-20240303203833461.png)![](1_Bayes_Networks.assets/image-20240303203840866.png)




### Modeling Hypothesis
> [!example] Vitamin 6
> ![](1_Bayes_Networks.assets/image-20240303204503941.png)![](1_Bayes_Networks.assets/image-20240303204512120.png)![](1_Bayes_Networks.assets/image-20240303204519390.png)






# Bayesian Network Inference
> [!overview]
> ![](1_Bayes_Networks.assets/image-20240303103716348.png)

## Factors
> [!def]
> A **factor** is defined simply as an unnormalized probability. At all points during variable elimination, each factor will be proportional to the probability it corresponds to but the underlying distribution for each factor won’t necessarily sum to 1 as a probability distribution should.
> ![](1_Bayes_Networks.assets/image-20240303110914578.png)![](1_Bayes_Networks.assets/image-20240303111015089.png)![](1_Bayes_Networks.assets/image-20240303113140985.png)




 
## Operations on Factors
> [!def]
> ![](1_Bayes_Networks.assets/image-20240303111218031.png)![](1_Bayes_Networks.assets/image-20240303111225716.png)![](1_Bayes_Networks.assets/image-20240303111316381.png)


### Join Factors
> [!def]
> ![](1_Bayes_Networks.assets/image-20240303113012908.png)![](1_Bayes_Networks.assets/image-20240303113037693.png)
> 


### Eliminate Factors
> [!def]
> ![](1_Bayes_Networks.assets/image-20240303113205640.png)![](1_Bayes_Networks.assets/image-20240303113218052.png)
> Here if we join two factors $f_{1}(A, B)$($2^2$) and $f_{2}(B,E)$($2^2$), the resulting factor would be $f_{3}(A, B, E)$($2^3$), after we eliminate $A$, the resulting factor $f_{4}(B,E)$ would be of size $2^2$.





## Enumeration Inference
### Algorithm Procedures
> [!algo]
> ![](1_Bayes_Networks.assets/image-20240303110105375.png)![](1_Bayes_Networks.assets/image-20240303103731273.png)![](1_Bayes_Networks.assets/image-20240303103744856.png)



### Complexity
> [!important]
> ![](1_Bayes_Networks.assets/image-20240303120227538.png)![](1_Bayes_Networks.assets/image-20240303120237914.png)



## Variable Elimination
> [!bug] Low Efficiency of Inference by Enumeration
> ![](1_Bayes_Networks.assets/image-20240303104023315.png)



### Algorithm Procedure
> [!algo]
> ![](1_Bayes_Networks.assets/image-20240303105959918.png)


### Algorithm Example
> [!example]
> ![](1_Bayes_Networks.assets/image-20240303112158692.png)![](1_Bayes_Networks.assets/image-20240303112252804.png)![](1_Bayes_Networks.assets/image-20240303110738697.png)![](1_Bayes_Networks.assets/image-20240303110747149.png)

> [!proof] Proof for Correctness
> ![](1_Bayes_Networks.assets/image-20240303113423900.png)




## Variable Ordering and Variable Relevance
### Principles
> [!important]
> ![](1_Bayes_Networks.assets/image-20240303111652354.png)![](1_Bayes_Networks.assets/image-20240303111707293.png)

> [!example]
> ![](1_Bayes_Networks.assets/image-20240303113750669.png)![](1_Bayes_Networks.assets/image-20240303113756391.png)
> For the first ordering, when we eliminate variable $Z$, we get a large factor $f(X_1,X_2,\cdots,X_{n})$(since we have $f(Z), f(X_i|Z)\forall i=1,2,\cdots, n$ to start with), which corresponds to $2^{n}$ rows in CPT.
> 
> For the second ordering, after eliminating $X_1$, we get small factor $f(Y_1,Z)$, which corresponds to $2^2$ rows in CPT.
> ![](1_Bayes_Networks.assets/image-20240303114802837.png)
> The key is that in order to eliminate some variable, we have to at least join all the factors that contains this variable. The join operation of factors will be the bottleneck of our variable elimination algorithm since joining factors make the factor's CPT temporary table larger.


### Exercises
> [!example] CS188 Fa23 Disc08 P3
> ![](1_Bayes_Networks.assets/image-20240419151226033.png)




### Comparisons
> [!important]
> ![](1_Bayes_Networks.assets/image-20240303112754178.png)![](1_Bayes_Networks.assets/image-20240303113258138.png)![](1_Bayes_Networks.assets/image-20240303113302706.png)




## Solving CSP with Bayesian Network
> [!def]
> ![](1_Bayes_Networks.assets/image-20240303114936795.png)![](1_Bayes_Networks.assets/image-20240303115847968.png)
> See [Tree-Structured CSP](../Classical_Search_Algorithms/3_Constraint_Statisfaction_Problems.md#Tree-Structured%20CSP)



# Bayesian Network Modeling
## Bayesian Linear Regression
> [!def]
> ![](1_Bayes_Networks.assets/image-20240419135409900.png)
> Because of the bayes network's causal structure.
> 
> ![](1_Bayes_Networks.assets/image-20240419140409914.png)




## Polynomial Regression Model
> [!def]
> If we have training data $\mathbf{x}=(x_1,x_{2,\cdots,}x_n)$ where $x_{i}\in\mathbb{R}$, and observed output data $\mathbf{t}=(t_1,t_{2,\cdots,}t_n)$ and polynomial regression  coefficients $\mathbf{w}=(w_1,w_{2,\cdots,}w_n)$.
> 
> Assume now we are using $l_2$ regularization on the polynomial regression where the prior of $\mathbf{w}$ is parametrized by $\alpha$, then it suffices to get the posterior distribution of $\mathbf{w}$ given $\mathbf{t},\mathbf{x},\sigma^2,\alpha$, mathematically it is: $$p(\mathbf{w}|\mathbf{t},\mathbf{x},\sigma^2,\alpha)$$
> 
> Recall that in polynomial regression the model is of the form: $$t_i=f(x_i,\mathbf{w})+z_i$$ where $z_{i}\sim \mathcal{N}(0,\sigma^2)$ where $f$ is the interaction term. Notice that the interaction is not linear since we are interacting between $\mathbf{w}$ and some transformed feature of $\mathbf{x}$. So polynomial regression doesn't necessarily belong to GLM(except when $n=1$ where the feature only has first-order term of $x$).
> 
> Given this we know $t_i$ is dependent on $x_i,\mathbf{w},\sigma^2$, and $\mathbf{w}$ is dependent on $\alpha$, we could use the following bayesian network to represent the model compactly:
> ![](1_Bayes_Networks.assets/image-20240304111447616.png)
> where the _plate_(in blue rectangular) represents ($x_{i}\to t_{i}$ connection $\forall i=1,2\cdots, n$). 
> 
> Then in order to compute the posterior distribution mentioned earlier, we use bayes rule:
>$$\begin{aligned}p(\mathbf{w}|\mathbf{t},\mathbf{x},\sigma^{2},\alpha)&\propto p(\mathbf{t}|\mathbf{w},\mathbf{x},\sigma^2)p(\mathbf{w}|\alpha)\end{aligned}$$
> 
> Finally we get: $$\begin{aligned}p(\mathbf{t}|\mathbf{w},\mathbf{x},\sigma^2)p(\mathbf{w}|\alpha)=\prod_{i=1}^{N}p(t_i|\mathbf{w},x_i,\sigma^2)p(\mathbf{w}|\alpha)\end{aligned}$$
> 
> We can maximize this posterior probability across all parameters to find the MAP estimator for our polynomial regression model.
> 
> Now suppose we want to predict $\widehat{t}$ given a new test point $\widehat{x}$, we have:
> ![](1_Bayes_Networks.assets/image-20240304115305171.png)![](1_Bayes_Networks.assets/image-20240304115321926.png)
> Derivations of (8.8) is based on the first independence rule of [Bayes Net Independence](1_Bayes_Networks.md#Bayes%20Net%20Independence).



## Generative Models - Ancestral Sampling
> [!def]
> ![](1_Bayes_Networks.assets/image-20240304130141114.png)![](1_Bayes_Networks.assets/image-20240304130205465.png)

> [!algo]
> ![](1_Bayes_Networks.assets/image-20240419135213890.png)

> [!example]
> ![](1_Bayes_Networks.assets/image-20240723221454745.png)
> Here each random variable takes 0 or 1.







## Construct Joint Distributions
> [!overview]
> Suppose we want to construct a distribution of a random variable $\mathbf{x}\sim cat(\vec{\mu})$(categorical distribution), since we know its pdf, we can construct it as ![](1_Bayes_Networks.assets/image-20240304122323450.png)

> [!algo]
> ![](1_Bayes_Networks.assets/image-20240304122350031.png)![](1_Bayes_Networks.assets/image-20240304122413049.png)![](1_Bayes_Networks.assets/image-20240304122423102.png)![](1_Bayes_Networks.assets/image-20240304122434996.png)![](1_Bayes_Networks.assets/image-20240304122600577.png)![](1_Bayes_Networks.assets/image-20240304122611003.png)



## Linear Gaussian Models
> [!overview]
> We show how a multivariate Gaussian can be expressed as a directed graph corresponding to a linear-Gaussian model over the component vari- ables. 
> 
> This allows us to impose interesting structure on the distribution, with the general Gaussian and the diagonal covariance Gaussian representing opposite extremes.


### Definition
> [!def]
> ![](1_Bayes_Networks.assets/image-20240304123134640.png)


### Mean and Variance
> [!important] Recursive Computation of Parameters
> ![](1_Bayes_Networks.assets/image-20240304123204762.png)![](1_Bayes_Networks.assets/image-20240304123325580.png)![](1_Bayes_Networks.assets/image-20240304123358421.png)![](1_Bayes_Networks.assets/image-20240304124510675.png)




### Extreme Cases - No links
> [!def]
> 








# Bayesian Network Sampling
> [!motiv]
> ![](1_Bayes_Networks.assets/image-20240419163654488.png)


## Prior Sampling
> [!def]
> ![](1_Bayes_Networks.assets/image-20240419160456415.png)![](1_Bayes_Networks.assets/image-20240419152534506.png)![](1_Bayes_Networks.assets/image-20240419152539604.png)


## Rejection Sampling
> [!def]
> ![](1_Bayes_Networks.assets/image-20240419152609916.png)![](1_Bayes_Networks.assets/image-20240419160803441.png)![](1_Bayes_Networks.assets/image-20240419160807908.png)


## Likelihood Sampling
> [!def]
> **Why we need this?**
> If some conditional probability is hard to calculate(e.g. not so obvious from the CPT table), we can use sampling techniques to generate some samples(joint samples $(x_{1},\cdots, x_{n})_{m=1}^M$) and use these samples and counting principle to estimate the conditional probability.
> ![](1_Bayes_Networks.assets/image-20240419161041032.png)![](1_Bayes_Networks.assets/image-20240419161057753.png)![](1_Bayes_Networks.assets/image-20240419161105074.png)![](1_Bayes_Networks.assets/image-20240419161411623.png)

> [!algo]
> ![](1_Bayes_Networks.assets/image-20240419171629566.png)



## Gibbs Sampling
See [Gibbs Sampling](../Approximate_Inference/Sampling_Algorithms.md#Gibbs%20Sampling)
> [!motiv]
> ![](1_Bayes_Networks.assets/image-20240419172701205.png)![](1_Bayes_Networks.assets/image-20240419165129453.png)![](1_Bayes_Networks.assets/image-20240419165136444.png)![](1_Bayes_Networks.assets/image-20240419165143664.png)

> [!algo]
> ![](1_Bayes_Networks.assets/image-20240419183729028.png)![](1_Bayes_Networks.assets/image-20240419183531308.png)![](1_Bayes_Networks.assets/image-20240419183539976.png)



## Importance Sampling
> [!def]
> ![](1_Bayes_Networks.assets/image-20240419183113903.png)![](1_Bayes_Networks.assets/image-20240419183123290.png)![](1_Bayes_Networks.assets/image-20240419183210679.png)![](1_Bayes_Networks.assets/image-20240419183849681.png)



## Exercises
> [!example] CS188 Fa23 Disc9 P1
> ![](1_Bayes_Networks.assets/image-20240419172310630.png)![](1_Bayes_Networks.assets/image-20240419172317984.png)



