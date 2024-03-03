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


### Examples
> [!example] Apply D-Separation Algorithm
> ![](1_Bayes_Networks.assets/image-20240303095424703.png)![](1_Bayes_Networks.assets/image-20240303095506873.png)![](1_Bayes_Networks.assets/image-20240303095511367.png)


## Topology and Distributions
> [!important] List all the independence
> ![](1_Bayes_Networks.assets/image-20240303100912961.png)
> Note that, we notice that we can use multiple bayes net to encode the same independence(distribution). 
> 
> **The reasons are that:**
> 1. Some bayes net structure is computationally easier then others.
> 2. Some causal effects are more suitable to be represented by some specific structures. For example, if there is a chained causal relationship, then it's better to use causal chain model instead of common cause model.




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


### Eliminate Factors
> [!def]
> ![](1_Bayes_Networks.assets/image-20240303113205640.png)![](1_Bayes_Networks.assets/image-20240303113218052.png)





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
> [!important]
> ![](1_Bayes_Networks.assets/image-20240303111652354.png)![](1_Bayes_Networks.assets/image-20240303111707293.png)

> [!example]
> ![](1_Bayes_Networks.assets/image-20240303113750669.png)![](1_Bayes_Networks.assets/image-20240303113756391.png)
> For the first ordering, when we eliminate factor $f(Z)$, we get a large factor $f(X_1,X_2,\cdots,X_{n})$(since we have $f(Z), f(X_i|Z)\forall i=1,2,\cdots, n$ to start with), which corresponds to $2^{n}$ rows in CPT.
> 
> For the second ordering, after eliminating $X_1$, we get small factor $f(Y_1,Z)$, which corresponds to $2^2$ rows in CPT.
> ![](1_Bayes_Networks.assets/image-20240303114802837.png)





## Comparisons
> [!important]
> ![](1_Bayes_Networks.assets/image-20240303112754178.png)![](1_Bayes_Networks.assets/image-20240303113258138.png)![](1_Bayes_Networks.assets/image-20240303113302706.png)




## Solving CSP with Bayesian Network
> [!def]
> ![](1_Bayes_Networks.assets/image-20240303114936795.png)![](1_Bayes_Networks.assets/image-20240303115847968.png)
> See [Tree-Structured CSP](../Classical_Search_Algorithms/3_Constraint_Statisfaction_Problems.md#Tree-Structured%20CSP)


# Bayesian Network Sampling
## Prior Sampling




## Rejection Sampling


## Likelihood Sampling


## Gibbs Sampling



