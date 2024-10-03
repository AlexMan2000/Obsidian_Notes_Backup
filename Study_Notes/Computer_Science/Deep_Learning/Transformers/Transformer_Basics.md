# Motivation
> [!motiv]
> ![](Transformer_Basics.assets/image-20240706221804990.png)




# Self Attention
> [!important]
> ![](Transformer_Basics.assets/image-20240706221539230.png)![](Transformer_Basics.assets/image-20240706221615144.png)







# Improve 1: Positional Encoding
## Motivations
> [!motiv]
> Due to the fact that self-attention will look into the future time step of inputs or hidden states, the system is not causal, which means it loses information about the time ordering. But we can use positional encoding to address this issue. 
> - Self attention is permutation invariant. 
> - Position of words in a sentence carries information!
> 
> ![](Transformer_Basics.assets/image-20240706222213813.png)



## Naive Positional Encoding
> [!important]
> ![](Transformer_Basics.assets/image-20240706222352687.png)
> The frequency at eariler time steps are designed to be of high frequency since high-frequency signals are essential for capturing fine details and variations.
>
> **Why introducing sinusoidal functions?**
> https://medium.com/@gunjassingh/positional-encoding-in-transformers-a-visual-and-intuitive-guide-0761e655cea7
> 
> **Importance of Linear Transformation in Positional Encoding?**
> https://blog.timodenk.com/linear-relationships-in-the-transformers-positional-encoding/



## Learned Positional Encoding
> [!def]
> ![](Transformer_Basics.assets/image-20240706230425999.png)![](Transformer_Basics.assets/image-20240706230543833.png)



# Improve 2: Multi-headed Attention
> [!def]
> ![](Transformer_Basics.assets/image-20240706230903712.png)![](Transformer_Basics.assets/image-20240706230911133.png)



# Improve 3: Adding Non-linearities
## Linearities
> [!important]
> ![](Transformer_Basics.assets/image-20240707104643346.png)![](Transformer_Basics.assets/image-20240707104653581.png)



# Improve 4: Masked Attention
## Motivations
> [!motiv]
> ![](Transformer_Basics.assets/image-20240707104958012.png)


## Mechanisms
> [!def]
> ![](Transformer_Basics.assets/image-20240707105851600.png)



# Classic Transformer
> https://arxiv.org/abs/1706.03762


## Model Structure
> [!def]
> ![](Transformer_Basics.assets/image-20240707110733248.png)



## Cross Attention
> [!def]
> ![](Transformer_Basics.assets/image-20240707111213345.png)
> In reality, cross-attention is multi-headed and the number of heads are the same for encoder and decoder.
> 
> ![](Transformer_Basics.assets/image-20240922182804167.png)






## Layer Nomalization
> [!def]
> ![](Transformer_Basics.assets/image-20240707111404353.png)




## Pros and Cons
> [!bug] Caveats
> ![](Transformer_Basics.assets/image-20240707113530435.png)



# Transformer Attention Variants
## K, Q, V Attention
> [!def]
> ![](Transformer_Basics.assets/image-20240922180911435.png)![](Transformer_Basics.assets/image-20241002121613322.png)
> In this model, all the values in the $K, Q, V$ matrices are learned fromd data.
> 
> ![](Transformer_Basics.assets/image-20240714152418150.png)![](Transformer_Basics.assets/image-20240714161507788.png)

> [!proof] Statistics
> ![](Transformer_Basics.assets/image-20240922180925572.png)![](Transformer_Basics.assets/image-20240922180930917.png)
```python
def attention(query, key, value, mask=None, dropout=None):
    # Your code here
    """
    input:
    @param query: (batch_size, seq_len, d_q)
    @param key: (batch_size, seq_len, d_k)
    @param value: (batch_size, seq_len, d_v)
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
> [!def]
> ![](Transformer_Basics.assets/image-20241002121803891.png)![](Transformer_Basics.assets/image-20241002121810348.png)![](Transformer_Basics.assets/image-20241002121637725.png)
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
        self.d_k = d_model // h
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



## Argmax Attention
> [!def]
> ![](Transformer_Basics.assets/image-20240714180243070.png)![](Transformer_Basics.assets/image-20240714180255095.png)![](Transformer_Basics.assets/image-20240714180303902.png)




## Kernelized Linear Attention
> [!def]





# Implementations
## Self-Attention
### Scaled Dot Product Attention
> [!task]
> ![](Transformer_Basics.assets/image-20240714124642225.png)![](Transformer_Basics.assets/image-20240714131235876.png) 
> where $d_{k}$ is the dimension for query/key vectors.
> 
> In this model, all the values in the $K, Q, V$ matrices are learned fromd data.
> ![](Transformer_Basics.assets/image-20240714152418150.png)![](Transformer_Basics.assets/image-20240714161507788.png)![](Transformer_Basics.assets/image-20240714154207229.png)

> [!proof]
> **Claim:** For two random vectors $\vec{q}\in \mathbb{R}^d$ and $\vec{k}\in \mathbb{R}^d$, whose entries are i.i.d with zero mean and unit variance.(For example gaussian), then the variance of $\vec{q}^{\top}\vec{k}$ is proportional to $d$.
> 
> **Proof:** 
> ![](Transformer_Basics.assets/image-20240714153941798.png)![](Transformer_Basics.assets/image-20240714153949043.png)![](Transformer_Basics.assets/image-20240714153956468.png)





### Self-Attention: Attention by Content
> [!def]
> ![](Transformer_Basics.assets/image-20240714132024569.png)
> There are several important hints:
> - 1. To attend to a specific element, ensure that its pre-softmax score is significantly higher than that of the other elements.
> - 2. Attending to a particular element is more manageable if the keys are orthogonal.
> 	- Suppose we have $\mathbf{k}_{1}\cdot \mathbf{k}_{2}=\mathbf{k}_{2}\cdot \mathbf{k}_{3}=\mathbf{k}_{1}\cdot \mathbf{k}_{3}=0$(Orthogonal Keys).
> 	- With orthogonal keys, if $\mathbf{q}$ is close to $\mathbf{k}_{1}$​, the score for $\mathbf{k}_{1}$​ will be significantly higher, leading to a higher softmax value for $\mathbf{k}_{1}$​ and near-zero values for $\mathbf{k}_{2}$​​ and $\mathbf{k}_{3}$​. This clear distinction simplifies the attention mechanism's task of focusing on the relevant key.
> 	- ![](Transformer_Basics.assets/image-20240714174337223.png)
> - 3. When there are repeated elements in a sequence with the same content, attending to all of them rather than a single one will be simpler. Since they have the same content, taking a "weighted average" over values weighted by attention scores will produce the same output as attending to a single one.
> 
> In general, when designing $K, Q, V$ matrices:
> - $K$ might as well be orthogonal
> - $Q$ should have large values at the index it wants to pay attention to.
> 




### Self-Attention: Attention by Position
> [!def]
>![](Transformer_Basics.assets/image-20240714175732010.png)





