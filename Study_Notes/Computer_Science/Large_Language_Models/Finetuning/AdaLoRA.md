**Reference:** https://athekunal.medium.com/adaptive-lora-adalora-paper-explanation-7cb5ac04d0cb

**Paper:** https://arxiv.org/abs/2303.10512
# Paper Analysis
## Idea
> [!def]
> **LoRA:** $W+\Delta W = W+BA$ where $B\in \mathbb{R}^{d_{1}\times r}$ and $A\in \mathbb{R}^{r \times d_{2}}$
> **AdaLoRA:** $W+\Delta W = W+P\Lambda Q$ where $P\in \mathbb{R}^{d_{1}\times r}$, $Q\in \mathbb{R}^{r \times d_{2}}$ and $\Lambda \in \mathbb{R}^{r\times r}$
> 
> Adalora出现的原因是其作者认为Lora训练的时候对于所有的秩一矩阵的weights都是一样的，也就是Lora没有考虑importance of weights. 所以在Adalora中，作者assign rank to weights dynamically based on SVD and based on the importance score, they prune the weights.
> 
> 其中$\Lambda$是用来控制ranking.


## Findings
> [!important]
> ![](AdaLoRA.assets/d1598279e14b932b6b8b6ad1875a1c60_MD5.jpeg)![](AdaLoRA.assets/c71baeae9ca2d25ed3f89f08b4b903f2_MD5.jpeg)


## SVD Training
> [!algo]
> ![](AdaLoRA.assets/2ae9e94e511b149f1552d5686d5101a2_MD5.jpeg)![](AdaLoRA.assets/fb7b2927b676b097cbe21a3446920a7c_MD5.jpeg)![](AdaLoRA.assets/4f590a1ddf7715cc35521f6ca763ba9c_MD5.jpeg)![](AdaLoRA.assets/fc198bb539ad1ed132539cd41a8c382e_MD5.jpeg)
> 定义$s(\cdot)$, 以下是可视化深度神经网络中某个参数的重要性的方式:
> 
> ![](AdaLoRA.assets/ce0eff063bd582dff6a71bb9f41ff776_MD5.jpeg)
> Exponential Smoothed Version(Momentum):
> 
> ![](AdaLoRA.assets/9cef0510c8caccf0ad1970d62b614a0d_MD5.jpeg)



# Code Experiments






