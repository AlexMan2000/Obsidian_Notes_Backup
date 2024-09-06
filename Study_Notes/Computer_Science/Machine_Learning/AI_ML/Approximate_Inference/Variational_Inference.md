# Motivations
> [!motiv]
> The log marginal likelihood is a central object for Bayesian inference with latent variable models:$$
> \ln p_{\theta}(x)=\ln \int p_{\theta}(x, z) d z$$
> where $x$ are observations, $z$ are latent variables, and $\theta$ are parameters. 
> 
> Remember in latent variable model we have:
> ![](Variational_Inference.assets/670cfa1392cde3f982dbccd7438ca802_MD5.jpeg)
> where it is impossible to compute $\ln \int p_{\theta}(x | z)p(z) d z$ since there are infinitely many possible $z$ so that this integral has no closed form solution.
> 
> So in practice, we train the latent variable model using expected log-likelihood:
![](Variational_Inference.assets/181066769695765b3eee7026d9dd52a8_MD5.jpeg)![](Variational_Inference.assets/4ea005f8a7fc1982c502bfb6e955ad95_MD5.jpeg)



# ELBO
> https://lips.cs.princeton.edu/the-elbo-without-jensen-or-kl/


## Definition
> [!def]
> ![](Variational_Inference.assets/a90d82e92f1b1999d603f04e8e847b79_MD5.jpeg)
> Simplified: 
> 
> ![](Variational_Inference.assets/0431b18de39685c2d030366034a8e0be_MD5.jpeg)
> 
> 


## Derivations
### Derivation 1: Jensen's Inequality
> [!important]
> ![](Variational_Inference.assets/691fcd7ba019b66662e08adade35ec90_MD5.jpeg)



### Derivation 2: KL Divergence
> [!important]
> ![](Variational_Inference.assets/Pasted%20image%2020240905165337.png)![](Variational_Inference.assets/a1be9a82983b0b20a6bf4d7b48c5fb90_MD5.jpeg)



### Derivation 3: Course Notes
> [!important]
> ![](Variational_Inference.assets/4bf52d565980cd11e100b8ddae009d9f_MD5.jpeg)



## Optimization
### Naive Approach
> [!important]
> First, start with a model:
> $$p(z, x)$$
> Next, choose a variational approximation:
> $$q(z;\lambda)$$
> Write down the ELBO:
> $$\mathscr{L}(\boldsymbol{\lambda})=\mathbb{E}_{q(\mathbf{z} ; \boldsymbol{\lambda})}[\log p(\mathbf{x}, \mathbf{z})-\log q(\mathbf{z} ; \boldsymbol{\lambda})]$$
> Compute the expectation(for example):
> $$\text { Example: } \mathscr{L}(\boldsymbol{\lambda})=x \lambda^2+\log \lambda$$
> Take derivatives:
> $$\text { Example: } \nabla_\lambda \mathscr{L}(\lambda)=2 x\lambda+\frac{1}{\lambda}$$
> Optimize:
> $$\lambda_{t+1}=\lambda_t+\rho_t \nabla_\lambda \mathscr{L}$$
> ![](Variational_Inference.assets/38860c751313508b2fe8b683754ae973_MD5.jpeg)

> [!example]
> ![](Variational_Inference.assets/e3cd7d637f7fcb7bf381f615b1bce8cb_MD5.jpeg)![](Variational_Inference.assets/c18143b2612fcad398a9255b205ba5ff_MD5.jpeg)![](Variational_Inference.assets/43b7a5bd2e9949d262bbd738989647d6_MD5.jpeg)




# BBVI
## Motivations
> [!motiv]
> ![](Variational_Inference.assets/Pasted%20image%2020240905170923.png)![](Variational_Inference.assets/Pasted%20image%2020240905170928.png)


## BBVI Definitions
> [!def]
> ![](Variational_Inference.assets/73031c5d7d9afd55ea0b7d07a316d353_MD5.jpeg)![](Variational_Inference.assets/ecf6288e6b721770430c6f38cdb6e9cc_MD5.jpeg)



## Score Function Gradients
> [!important]
> ![](Variational_Inference.assets/1f322a6ce3279f15bb25eb0d2434383e_MD5.jpeg)![](Variational_Inference.assets/9b5c1eb680b58d21628276ed1b9d0496_MD5.jpeg)



## Basic BBVI
### Algorithm
> [!algo]
> ![](Variational_Inference.assets/37487151a039ad90b5584a165d7d9e50_MD5.jpeg)![](Variational_Inference.assets/5bb85d4f9471a728430ebcd6948727f4_MD5.jpeg)
> 

 
### Problems
> [!bug] Caveats
> ![](Variational_Inference.assets/b1ef99a8314312be49a3e75e307af575_MD5.jpeg)



### Control Variates
> [!important]
> ![](Variational_Inference.assets/ab4047b251ae53e23e2cf81cda5ce202_MD5.jpeg)![](Variational_Inference.assets/dd921b21782f4b45e4cd8716965311e1_MD5.jpeg)![](Variational_Inference.assets/35b78eede7b753d3a2dc0e7900b89dfd_MD5.jpeg)


## Reparameteriztion Grdients




# CAVI





# SVI



# ADVI
