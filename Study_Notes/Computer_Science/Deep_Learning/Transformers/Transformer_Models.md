# Motivation
> [!motiv]
> ![](Transformer_Models.assets/image-20240706221804990.png)


# Model Structure
> [!important]
> ![](Transformer_Models.assets/d179d0db460ba38e158ec60c31d864e9_MD5.jpeg)




# Encoder Structure
## Positional Encoding
### Motivations
> [!motiv]
> Due to the fact that self-attention will look into the future time step of inputs or hidden states, the system is not causal, which means it loses information about the time ordering. But we can use positional encoding to address this issue. 
> - Self attention is permutation invariant. 
> - Position of words in a sentence carries information!
> 
> ![](Transformer_Models.assets/image-20240706222213813.png)



### Naive Positional Encoding
> [!important]
> ![](Transformer_Models.assets/image-20240706222352687.png)
> The frequency at eariler time steps are designed to be of high frequency since high-frequency signals are essential for capturing fine details and variations.
>
> **Why introducing sinusoidal functions?**
> https://medium.com/@gunjassingh/positional-encoding-in-transformers-a-visual-and-intuitive-guide-0761e655cea7
> 
> **Importance of Linear Transformation in Positional Encoding?**
> https://blog.timodenk.com/linear-relationships-in-the-transformers-positional-encoding/
> 
> **总结:**
> - sin和cos函数的值域有限，可以很好地限制编码位置的数字的大小, 否则如果使用pos的数值直接来encoding的话，一旦序列很长，pos就会很大。
> - 通过调节频率，可以得到多种多样的sin和cos函数，从而可以加你个位置信息投射到每个feature index 维度都各具特色，各不相同的高维空间，以形成对位置信息的更好表示
> - 通过独特的计算公式，我们可以让特征编号小的特征被投射到剧烈变化的维度上，并且让特征编号大的特征被投射到轻微变化、甚至完全单调的维度上，从而可以让小编号特征去捕捉样本之间的局部细节差异，让大编号特征去捕捉样本之间按顺序排列的全局趋势
> 
> **额外的好处:**
> - 首先最重要的是其**函数的周期性带来泛化性**：在模型训练过程中，我们可能使用的都是序列长度小于20的数据，但是当实际应用中遇到一个序列长度为50的数据，**正弦和余弦函数的周期性**意味着，即使模型在训练时未见过某个位置，它仍然可以生成一个合理的位置编码。它可用泛化到不同长度的序列。
> - **不增加额外的训练参数**：当我们在一个已经很大的模型（如 GPT-3 或 BERT）上添加位置信息时，我们不希望增加太多的参数，因为这会增加训练成本和过拟合的风险。正弦和余弦位置编码不增加任何训练参数。
> - **即便是相同频率下的正余弦函数，也可以通过周期性带来部分的相对位置信息，可以比绝对位置信息更有效**：正弦和余弦函数的周期性特征为模型提供了一种隐含的相对位置信息，使得模型能够更有效地理解序列中不同位置之间的相对关系。

> [!code] Implementation
> ![](Transformer_Models.assets/d1051efd90d8421a839d4bbe6d8d8e22_MD5.jpeg)![](Transformer_Models.assets/e7c96515f54d62e5cbbb6eb0b7893f82_MD5.jpeg)![](Transformer_Models.assets/image-20241010154519584.png)
```python
class PositionalEncoding(nn.Module):
    """
    - 位置编码完全没有使用我们embedding层输出的具体值，而仅仅利用了输出的形状，所以位置编码与语义无关
    - 位置编码层没有任何需要学习的参数，于是用不到nn.Parameter
    - max_seq_len旨在帮助我们的位置编码快速预先计算好所有的正余弦函数值，让代码执行速度更快
    """
    def __init__(self, d_model, dropout, max_seq_len=5000):
        super().__init__()

        self.dropout = nn.Dropout(dropout)
        positional_matrix = torch.zeros((max_seq_len, d_model))

        position = torch.arange(0, max_seq_len).unsqueeze(1)  # (max_seq_len, 1), waiting to be broadcasted
        div_term = torch.exp(
            torch.arange(0, d_model, 2) * -(math.log(10000.0) / d_model)
        ) # (d_model, )

        # position * div_term will be (max_seq_len, d_model)
        # 预先计算好max_seq_len个位置的编码，在前向传播的过程中仅需要索引即可，速度是很快的
        positional_matrix[:, 0::2] = torch.sin(position * div_term)
        positional_matrix[:, 1::2] = torch.sin(position * div_term)

        # Used for those parameters that are fixed/not learnable, but are used across training and testing
        # Used for faster retrieval
        self.register_buffer("pe", positional_matrix)

    def forward(self, x):
        """
        Input should be the embedding src token sequence
        :param x: (batch_size, seq_len, d_model)
        :return: x + pe(x)
        """
        pe = self.pe.unsqueeze(0) # (1, seq_len, d_model), broadcast it across all samples in the batch

        # This disabling grad is optional since pe is not a learnable parameter by definition
        x = x + pe[:, :x.size(1)].requires_grad_(False)
        return self.dropout(x)

```


### Learned Positional Encoding
> [!def]
> ![](Transformer_Models.assets/image-20240706230425999.png)![](Transformer_Models.assets/image-20240706230543833.png)



## Multi-headed Attention
### Definition
> [!def]
> ![](Transformer_Models.assets/image-20240706230903712.png)![](Transformer_Models.assets/image-20240706230911133.png)
> Details see below [Multi-headed KQV Attention](Transformer_Models.md#Multi-headed%20KQV%20Attention)



### Attending to particular vectors
> [!important]
> ![](Transformer_Models.assets/73fc423013cb0488581b4e4a08b7274e_MD5.jpeg)![](Transformer_Models.assets/b3cd20cf37e30d3a1e2ab83fdb9ffa9c_MD5.jpeg)![](Transformer_Models.assets/fa69b9122132fdcb453c935bfad224bb_MD5.jpeg)![](Transformer_Models.assets/4b74a6dc83c31015dcf9f216f6da93c7_MD5.jpeg)![](Transformer_Models.assets/8a3a01a02f0ee5a16285d3f5e4826cc8_MD5.jpeg)



### Drawback of Single-headed Attention
> [!important]
> ![](Transformer_Models.assets/d5a743dce42723ec71c6469c9fea5224_MD5.jpeg)![](Transformer_Models.assets/ba668c29f437ca465cdf0a9e402385bc_MD5.jpeg)![](Transformer_Models.assets/97a380fa8a5feea6ecc3bc1e30158278_MD5.jpeg)





### Benefits of Multi-headed Attention
> [!important]
> ![](Transformer_Models.assets/95b74d5def18e14f0324b18298c9767e_MD5.jpeg)![](Transformer_Models.assets/4c7c98d5dc9aa379c5868763c69f9ace_MD5.jpeg)![](Transformer_Models.assets/386e18dd5b793c59f0effb26940f14f0_MD5.jpeg)![](Transformer_Models.assets/a69b0511fc029bd9de9548a5c067c52f_MD5.jpeg)
> 
> 所以我们通过上面的例子发现多头注意力的几个优点:
> ![](Transformer_Models.assets/a68fa5b44c8f4bcf2b31b6a81202ea30_MD5.jpeg)![](Transformer_Models.assets/6405b09f4408356fb51f4366c0d26c22_MD5.jpeg)



## Feed-forward Networks
### Linearities
> [!important]
> ![](Transformer_Models.assets/image-20240707104643346.png)![](Transformer_Models.assets/image-20240707104653581.png)



### FFN-Structure
> [!def]
> 根据Transformer的结构图可以看出，每一个多头注意力机制层都链接了一个前馈网络层。前馈网络（Feed-Forward Networks，FFNs），在神经网络的语境中，是指那些信息单向流动的网络结构。在这样的网络中，信息从输入层流向输出层，中间可能会经过多个隐藏层，但不会有任何反向的信息流，即不存在循环或者回路。因此在Transformer当中，实际上前馈神经网络就是**由线性层组成的深度神经网络结构**。它的主要职责是对输入数据进行**非线性变换，同时也负责产生输出值**。它的作用暗示了一个关键的事实——**自注意力机制大多数时候是一个线性结构**：加权求和是一个线性操作，即便我们是经过丰富的权重变化、由丰富的Q、K、V等矩阵点积的结果，还有softmax函数，但是自注意力机制依然是一个线性的过程。因此，在加入前馈神经网络之前，transformer本身不带有传统意义上的非线性结构。
> 


## 填充掩码
> [!def]
> ![](Transformer_Models.assets/fff7559242060374847e5ae59ef9510a_MD5.jpeg)![](Transformer_Models.assets/a7843470838112020a9c028f892a6c5a_MD5.jpeg)
```python
def create_padding_mask(seq, pad_token=0):
    # seq: (batch_size, seq_len, embedding_dim)
    # 检查填充值位置
    padding_mask = (seq == pad_token).all(dim=-1)  # (batch_size, seq_len)
    
    # 增加维度以匹配注意力权重矩阵的形状
    # (batch_size, num_heads, seq_len, seq_len)
    padding_mask = padding_mask.unsqueeze(1).unsqueeze(3).expand(-1, -1, -1, seq.size(1))
    
    # 将填充值部分设置为负无穷大，有效数据部分设置为0
    padding_mask = padding_mask.float() * -1e9  # (batch_size, num_heads, seq_len, seq_len)
    
    return padding_mask
```
> [!code] 不使用升维的掩码实现
> ![](Transformer_Models.assets/3d34d12ef1a4f5b6ede9a8cff3c0fb07_MD5.jpeg)
```python
def create_padding_mask(seq, pad_token=0):
    # seq: (batch_size, seq_len, d_model)
    # 检查填充值位置
    padding_mask = (seq == pad_token).all(dim=-1)  # (batch_size, seq_len)
    padding_mask = padding_mask.float() * -1e9
    
    return padding_mask
```







# Decoder Structure
## 训练数据格式
> [!important]
> ![](Transformer_Models.assets/3e561c74fc8c765b86af4ab3ecdc2d82_MD5.jpeg)![](Transformer_Models.assets/cd502b29b34d8afd45198ff1c9aac40e_MD5.jpeg)


## 训练流程 - Teacher Forcing
> [!important]
> ![](Transformer_Models.assets/69d4b1c4304c8d2cb14ec9b06c1c8df7_MD5.jpeg)![](Transformer_Models.assets/a275cf4103e4d11ca5ac1119cd038b2e_MD5.jpeg)![](Transformer_Models.assets/image-20241010120602232.png)



## 测试流程 - Autoregressive
> [!important]
> ![](Transformer_Models.assets/800fcc2aa65c7835e68372a536593272_MD5.jpeg)![](Transformer_Models.assets/c3ceadeb2a4bf3c67e7165cc83b0a398_MD5.jpeg)![](Transformer_Models.assets/0105c85b66d1e8a35663a9a88cf1d169_MD5.jpeg)


## 前瞻掩码
> [!def]
> ![](Transformer_Models.assets/49025c400940007bc7869d46dfa0d4c6_MD5.jpeg)![](Transformer_Models.assets/9fa6eee2e3ce3ddf6686cea578dc3714_MD5.jpeg)![](Transformer_Models.assets/673911832947816cead3cf0902b81e48_MD5.jpeg)![](Transformer_Models.assets/2337fff8cae782ceb5bc81b2dc0271b2_MD5.jpeg)
```python
import torch

def create_look_ahead_mask(seq_len, start_seq = 1):
    mask = torch.triu(torch.ones((seq_len, seq_len)),diagonal=start_seq)  # triu 左下方的三角矩阵，diagonal控制对角线位置
    #mask = mask.float() * -1e9  # 将未来的位置设置为负无穷大
    return mask
```



## 交叉掩码
> [!important]
> ![](Transformer_Models.assets/42dee99dd12cf4854528f42be35719a4_MD5.jpeg)![](Transformer_Models.assets/9ae551fbf57d8b2c6d7d44b9ed66cdea_MD5.jpeg)![](Transformer_Models.assets/f8382d672af6e5bbd3161a952cdcb959_MD5.jpeg)



# Classic Transformer
> https://arxiv.org/abs/1706.03762


## Model Structure
> [!def]
> ![](Transformer_Models.assets/image-20240707110733248.png)



## Cross Attention
> [!def]
> ![](Transformer_Models.assets/image-20240707111213345.png)
> In reality, cross-attention is multi-headed and the number of heads are the same for encoder and decoder.
> 
> ![](Transformer_Models.assets/image-20240922182804167.png)






## Layer Nomalization
> [!def]
> ![](Transformer_Models.assets/image-20240707111404353.png)![](Transformer_Models.assets/0295afce5882750b3a04e1580d9ee16a_MD5.jpeg)![](Transformer_Models.assets/image-20241009144530278.png)






## Pros and Cons
> [!bug] Caveats
> ![](Transformer_Models.assets/image-20240707113530435.png)



# Transformer Attention Variants
## K, Q, V Attention
> [!def]
> ![](Transformer_Models.assets/image-20240922180911435.png)![](Transformer_Models.assets/image-20241002121613322.png)
> In this model, all the values in the $K, Q, V$ matrices are learned fromd data.
> 
> ![](Transformer_Models.assets/image-20240714152418150.png)![](Transformer_Models.assets/image-20240714161507788.png)

> [!proof] Statistics
> ![](Transformer_Models.assets/image-20240922180925572.png)![](Transformer_Models.assets/image-20240922180930917.png)
```python
def attention(query, key, value, mask=None, dropout=None):
    # Your code here
    """
    input:
    @param query: (batch_size, seq_len, num_head, d_q)
    @param key: (batch_size, seq_len, num_head, d_k)
    @param value: (batch_size, seq_len, num_head, d_v)
    @param mask: (batch_size, seq_len) of 1 and 0 where 1 means
    @param dropout: A predefined layer that apply dropout to the attention weights

    returns:
    - attention_out: (batch_size, seq_len, d_v)
    - attention_weights: (batch_size, seq_len, seq_len)
    """
    # Step 1: Get the query/key embedding dim
    d_k = query.size(-1)

    # Step 2: Apply softmax(QK.T/sqrt{d_k}) to get the attn_weights ()
    # Step 2.1 Calculate the dot product (batch_size, seq_len, seq_len)
    batch_scores = torch.matmul(query, key.transpose(-2, -1)) / math.sqrt(d_k)

    # Step 2.2 Apply the mask so that the q_i * k_j is zero where mask[:, j] is 0
    if mask is not None:
        # broadcast along seq_len, since we are masking out along the last dimension
        mask = mask.unsqueeze(1)
        batch_scores = batch_scores.masked_fill_(mask == 0, float("-inf"))
    # Step 2.3 Calculate attention weights with softmax
    attention_weights = batch_scores.softmax(dim=-1) # (batch_size, seq_len, seq_len)

    # Step 3: Apply dropout
    if dropout is not None:
        attention_weights = dropout(attention_weights)

    attention_out = torch.matmul(attention_weights, value)
    return attention_out, attention_weights
```



## Multi-headed KQV Attention
### Definition
> [!def]
> ![](Transformer_Models.assets/image-20241002121803891.png)![](Transformer_Models.assets/image-20241002121810348.png)![](Transformer_Models.assets/image-20241002121637725.png)
> 本质上是对于`embedding_dim`(比如说是`512`), 分成`n=8`个维度为`64`的注意力头，然后计算完每个头的注意力向量之后再拼接起来。






### Implementations
> [!code]
```python
class MultiHeadedAttention(nn.Module):
    def __init__(self, h, d_model, dropout=0.1):
        # Your code here
        """
        Input:
        @param h: number of heads to use
        @param d_model: d_k * h, used for d_q = d_k, d_v
        @param dropout: layer to dropout attention
        """
        super().__init__()
        self.num_head = h
        self.d_model = d_model
        self.d_k = d_model // h  # 分割
        self.dropout = nn.Dropout(p=dropout)
        # Wq, Wk, Wv, Wo projections
        self.projections = clones(nn.Linear(d_model, d_model), 4)

    def forward(self, query, key, value, mask=None):
        # Your code here
        """
        Inputs:
        - query/key/value: (batch_size, seq_len, d_model), d_model = h * d_k
        - mask: (batch_size, d_model)
        """

        # Step 1: Calculate Attention(QWq, KWk, VWv)
        kqv_packed = [query, key, value]
        batch_size = query.size(0)
        [query_input, key_input, value_input] = [
            projection(mat).view(batch_size, -1, self.num_head, self.d_k).transpose(1, 2)
            for projection, mat
            in zip(self.projections[:-1], kqv_packed)]
        # here query_input/key_input are (batch_size, num_head, seq_len, d_k)

        # Step 2: Calculate multi-headed attention score
        attention_out, self.attn = attention(query_input, key_input, value_input
                                             , mask=mask, dropout=self.dropout)
        # (batch_size, num_head, seq_len, d_v), (batch_size, num_head, seq_len, seq_len)

        # Step 3: Perform concatenation
        # Need Contiguous to make sure view() works fine
        attention_out = attention_out.transpose(1, 2) \
            .contiguous() \
            .view(batch_size, -1, self.d_model)
        return self.projections[-1](attention_out)
```



### Manipulation of Attention Scores
> [!def]










## Argmax Attention
> [!def]
> ![](Transformer_Models.assets/image-20240714180243070.png)![](Transformer_Models.assets/image-20240714180255095.png)![](Transformer_Models.assets/image-20240714180303902.png)




## Kernelized Linear Attention
> [!def]





# Implementations
## Self-Attention
### Scaled Dot Product Attention
> [!task]
> ![](Transformer_Models.assets/image-20240714124642225.png)![](Transformer_Models.assets/image-20240714131235876.png) 
> where $d_{k}$ is the dimension for query/key vectors.
> 
> In this model, all the values in the $K, Q, V$ matrices are learned fromd data.
> ![](Transformer_Models.assets/image-20240714152418150.png)![](Transformer_Models.assets/image-20240714161507788.png)![](Transformer_Models.assets/image-20240714154207229.png)

> [!proof]
> **Claim:** For two random vectors $\vec{q}\in \mathbb{R}^d$ and $\vec{k}\in \mathbb{R}^d$, whose entries are i.i.d with zero mean and unit variance.(For example gaussian), then the variance of $\vec{q}^{\top}\vec{k}$ is proportional to $d$.
> 
> **Proof:** 
> ![](Transformer_Models.assets/image-20240714153941798.png)![](Transformer_Models.assets/image-20240714153949043.png)![](Transformer_Models.assets/image-20240714153956468.png)





### Self-Attention: Attention by Content
> [!def]
> ![](Transformer_Models.assets/image-20240714132024569.png)
> There are several important hints:
> - 1. To attend to a specific element, ensure that its pre-softmax score is significantly higher than that of the other elements.
> - 2. Attending to a particular element is more manageable if the keys are orthogonal.
> 	- Suppose we have $\mathbf{k}_{1}\cdot \mathbf{k}_{2}=\mathbf{k}_{2}\cdot \mathbf{k}_{3}=\mathbf{k}_{1}\cdot \mathbf{k}_{3}=0$(Orthogonal Keys).
> 	- With orthogonal keys, if $\mathbf{q}$ is close to $\mathbf{k}_{1}$​, the score for $\mathbf{k}_{1}$​ will be significantly higher, leading to a higher softmax value for $\mathbf{k}_{1}$​ and near-zero values for $\mathbf{k}_{2}$​​ and $\mathbf{k}_{3}$​. This clear distinction simplifies the attention mechanism's task of focusing on the relevant key.
> 	- ![](Transformer_Models.assets/image-20240714174337223.png)
> - 3. When there are repeated elements in a sequence with the same content, attending to all of them rather than a single one will be simpler. Since they have the same content, taking a "weighted average" over values weighted by attention scores will produce the same output as attending to a single one.
> 
> In general, when designing $K, Q, V$ matrices:
> - $K$ might as well be orthogonal
> - $Q$ should have large values at the index it wants to pay attention to.
> 




### Self-Attention: Attention by Position
> [!def]
>![](Transformer_Models.assets/image-20240714175732010.png)




## PyTorch_Implementations





