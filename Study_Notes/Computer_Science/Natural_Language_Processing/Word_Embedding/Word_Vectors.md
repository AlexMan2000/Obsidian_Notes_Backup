# Motivations
> [!overview]
> In this section we are going to discuss several frequently used methods for word embedding.



# Count-Based Methods
## Co-occurrence Matrix
### Definition
> [!def]
> ![](Word_Embedding/Word_Vectors.assets/image-20240710141902818.png)


### How to Build One
> [!code]
> ![](Word_Embedding/Word_Vectors.assets/image-20240708230216904.png)
```python
import numpy as np
from collections import defaultdict
from itertools import combinations

def tokenize(document):
    # Simple tokenization, assuming words are separated by spaces
    return document.lower().split()

def build_cooccurrence_matrix(documents):
    # Step 1: Tokenize the documents
    tokenized_docs = [tokenize(doc) for doc in documents]
    
    # Step 2: Create a list of unique terms
    all_terms = set(term for doc in tokenized_docs for term in doc)
    term_list = list(all_terms)
    term_index = {term: idx for idx, term in enumerate(term_list)}
    
    # Step 3: Initialize the co-occurrence matrix
    size = len(term_list)
    cooccurrence_matrix = np.zeros((size, size), dtype=np.int32)
    
    # Step 4: Populate the matrix
    for doc in tokenized_docs:
        unique_terms_in_doc = set(doc)
        # Prevent from double counting the pair
        for term1, term2 in combinations(unique_terms_in_doc, 2):
            idx1, idx2 = term_index[term1], term_index[term2]
            cooccurrence_matrix[idx1, idx2] += 1
            cooccurrence_matrix[idx2, idx1] += 1  # Symmetric matrix
    
    return cooccurrence_matrix, term_list

# Example usage
documents = [
    "this is a sample document",
    "this document is another sample",
    "sample document with sample text"
]

cooccurrence_matrix, term_list = build_cooccurrence_matrix(documents)

# Display results
import pandas as pd
df = pd.DataFrame(cooccurrence_matrix, index=term_list, columns=term_list)
print(df)

```



### Applying SVD 
> [!algo]
> ![](Word_Embedding/Word_Vectors.assets/image-20240710142054627.png)![](Word_Embedding/Word_Vectors.assets/image-20240710142106669.png)




# Window-Based Methods
> [!overview]
> Word2vec is a family of models of **distributional semantics**.
> - Words that occur in similar contexts tend to have similar meanings.
> - It is a predictive model.


## CBOW Model
### Algorithmic Idea
> [!algo]
> ![](Word_Embedding/Word_Vectors.assets/image-20240710143209276.png)![](Word_Embedding/Word_Vectors.assets/image-20240710143227631.png)



### Objective Function
> [!def]
> ![](Word_Embedding/Word_Vectors.assets/image-20240710143916533.png)












## Skipgram Model
### Algorithmic Idea
> [!algo]
> ![](Word_Embedding/Word_Vectors.assets/image-20240710144007435.png)






### Objective Function
> [!def] Objective Function
> ![](Word_Embedding/Word_Vectors.assets/image-20240710134404462.png)![](Word_Embedding/Word_Vectors.assets/image-20240710135912179.png)

> [!important] Alternative Representations
> ![](Word_Embedding/Word_Vectors.assets/image-20240710154731484.png)





### Parameters
> [!def]
> ![](Word_Embedding/Word_Vectors.assets/image-20240710134718809.png)![](Word_Embedding/Word_Vectors.assets/image-20240710134725484.png)
> Here, every word has two vectors:
> - $\vec{u}_{w}$ is the embedding for the word $w$ that appears as a context word.
> - $\vec{v}_{w}$ is the embedding for the word $w$ that appears as a center word.
> 
> ![](Word_Embedding/Word_Vectors.assets/image-20240710134739937.png)



### Training
> [!def] Empirical Loss
> ![](Word_Embedding/Word_Vectors.assets/image-20240710135838211.png)


#### Gradient Descent
> [!def]
> ![](Word_Embedding/Word_Vectors.assets/image-20240710140641414.png)







#### S.G.D Intuition
> [!def]
> ![](Word_Embedding/Word_Vectors.assets/image-20240710140704251.png)![](Word_Embedding/Word_Vectors.assets/image-20240710140714414.png)![](Word_Embedding/Word_Vectors.assets/image-20240710140720054.png)![](Word_Embedding/Word_Vectors.assets/image-20240710140728701.png)


### Optimizations
#### Negative Sampling Techniques
> [!def]
> ![](Word_Embedding/Word_Vectors.assets/image-20240710161837423.png)




#### Hierarchical Softmax
> [!important]
> https://medium.com/@gridflowai/optimizing-word2vec-with-hierarchical-softmax-a9d46ebe545a#:~:text=Hierarchical%20SoftMax%20offers%20a%20solution,to%20as%20a%20Huffman%20tree.
> 
> https://www.youtube.com/watch?v=pzyIWCelt_E
> 在先前的Skipgram model中，我们为了计算$P(O=o|C=c)$, 需要$\vec{v}_c$和所有`vocab`中的$\vec{u}_o$做内积得到$P(O|C=c)$的条件概率分布，但是如果`vocab size`过大的话，这个内积的运算就会消耗很多时间，所以为了优化这个计算过程，我们提出`Hirarchical Softmax`的算法，本质上是利用了一个数据压缩算法[Huffman Encoding](../../Data_Structures_Algorithms/Algorithms/Data_Compression.md#Huffman%20Encoding)。


##### Definition
> [!def]
> Hierarchical softmax (introduced by Morin and Bengio, 2005), is a computationally efficient approximation of the full softmax.
> ![](Word_Embedding/Word_Vectors.assets/image-20240825205725798.png)


##### Algorithm
> [!algo]
> ![](Word_Embedding/Word_Vectors.assets/image-20240825205933483.png)
> 为了得到$P(O=active|C=chupacabra)$, 我们从根节点出发调用`find("active")`方法，($log(N), N$为`vocab size`), 在路径上的每一个`internal node`都计算一个内积$\vec{v}_c^{\top}\vec{u}_o$(其中$\vec{u}_o$为`internal node`的`outside vector`), 然后将每个内积通过一个`sigmoid`函数得到概率，将路径上的所有概率乘起来就可以得到我们要求的概率，可以看到，我们不用考虑所有的`vocab size`, 而是将其转化为了一连串(数量远小于`vocab size`)概率的乘积。











### Skipgram Derivatives
#### Formulas
> [!important]
> Here are some importants results to remember:
> - $U$ is the outside word vectors of shape (`vocab_size, word_dim`)
> - $V$ is the center word vectors of shape (`vocab_size, word_dim`)
> - $J_{naive-{softmaxloss}}(\vec{v}_{c,}o,U)=-log(\hat{y}_o)$, 其中$\hat{y}_o=softmax(U\vec{v}_{c})[oIndex]$, `oIndex`是`outside word index in the vocab size`
> 	- Derivative w.r.t $\vec{v}_c$, $\frac{\partial J}{\partial \vec{v}_c}=U^{\top}(\hat{y}-\vec{y})\in\mathbb{R}^{dim}$, where $\vec{y}$ is the probability vector that has shape `(vocab_size,)`
> 	- Derivative w.r.t $U$, $\frac{\partial J}{\partial U}=(\hat{y}-\vec{y})\vec{v}_c^{\top}\in\mathbb{R}^{vocab\times dim}$
> - $J_{{negative}-{sample}}(\vec{v}_{c},o,U)=-log(\sigma(\vec{u}_o^{\top}\vec{v}_c))-\sum\limits_{s=1}^Klog(\sigma(-\vec{u}_{w_s}^{\top}\vec{v}_c))$
> 	- Derivative w.r.t $\vec{v}_c=-U_o^{\top}(\mathbf{1}-\sigma(U_o\vec{v}_c))$ where $U_o=\begin{bmatrix}-\vec{u}_o^{\top}-\\-(-\vec{u}_{w_{1}}^{\top})-\\\cdots\\-(-\vec{u}_{w_K}^{\top})-\end{bmatrix}$
> 	- Derivative w.r.t $U$, could derive row by row from the following:
> 		- $\frac{\partial \boldsymbol{J}_{\text {neg-sample }}\left(\boldsymbol{v}_c, o, \boldsymbol{U}\right)}{\partial \boldsymbol{u}_o}=-\left(1-\sigma\left(\boldsymbol{u}_o^{\top} \boldsymbol{v}_c\right)\right) \boldsymbol{v}_c$
> 		- $\frac{\partial \boldsymbol{J}_{\text {neg-sample }}\left(\boldsymbol{v}_c, o, \boldsymbol{U}\right)}{\partial \boldsymbol{u}_{w_s}}=\left(1-\sigma\left(-\boldsymbol{u}_{w_s}^{\top} \boldsymbol{v}_c\right)\right) \boldsymbol{v}_c$
> 		- Notice that not every row in $\frac{\partial J}{\partial U}$ have non-zero values since we only sample $K$ negative samples, which results in at least `vocab_size - K - 1`(no duplicates on negative samples) and at most `vocab_size - 2`(all duplicates) zero vectors in the $U$ matrix.

#### Mathematical Derivations
> [!thm]
> ![](Word_Embedding/Word_Vectors.assets/image-20240721181056747.png)![](Word_Embedding/Word_Vectors.assets/image-20240721181103302.png)![](Word_Embedding/Word_Vectors.assets/image-20240721181110140.png)![](Word_Embedding/Word_Vectors.assets/image-20240721181116347.png)![](Word_Embedding/Word_Vectors.assets/image-20240721181208972.png)![](Word_Embedding/Word_Vectors.assets/image-20240813133956196.png)![](Word_Embedding/Word_Vectors.assets/image-20240813134002472.png)![](Word_Embedding/Word_Vectors.assets/image-20240813134010987.png)![](Word_Embedding/Word_Vectors.assets/image-20240813134018829.png)![](Word_Embedding/Word_Vectors.assets/image-20240813134026082.png)![](Word_Embedding/Word_Vectors.assets/image-20240813134033513.png)



## Skipgram Implementations
> [!code]
```python
def sigmoid(x):
    """
    Compute the sigmoid function for the input here.
    Arguments:
    x -- A scalar or numpy array.
    Return:
    s -- sigmoid(x)
    """

    ### YOUR CODE HERE (~1 Line)

    return 1 / (np.exp(-x) + 1)
    ### END YOUR CODE

    return s


def naiveSoftmaxLossAndGradient(
    centerWordVec,
    outsideWordIdx,
    outsideVectors,
    dataset
):
    """ Naive Softmax loss & gradient function for word2vec models

    Implement the naive softmax loss and gradients between a center word's 
    embedding and an outside word's embedding. This will be the building block
    for our word2vec models. For those unfamiliar with numpy notation, note 
    that a numpy ndarray with a shape of (x, ) is a one-dimensional array, which
    you can effectively treat as a vector with length x.

    Arguments:
    centerWordVec -- numpy ndarray, center word's embedding
                    in shape (word vector length, )
                    (v_c in the pdf handout)
    outsideWordIdx -- integer, the index of the outside word
                    (o of u_o in the pdf handout)
    outsideVectors -- outside vectors is
                    in shape (num words in vocab, word vector length) 
                    for all words in vocab (tranpose of U in the pdf handout)
    dataset -- needed for negative sampling, unused here.

    Return:
    loss -- naive softmax loss
    gradCenterVec -- the gradient with respect to the center word vector
                     in shape (word vector length, )
                     (dJ / dv_c in the pdf handout)
    gradOutsideVecs -- the gradient with respect to all the outside word vectors
                    in shape (num words in vocab, word vector length) 
                    (dJ / dU)
    """

    ### YOUR CODE HERE (~6-8 Lines)

    ### Please use the provided softmax function (imported earlier in this file)
    ### This numerically stable implementation helps you avoid issues pertaining
    ### to integer overflow.

    vocab_size = outsideVectors.shape[0]
    z = (outsideVectors @ centerWordVec).squeeze()   # shape (vocab_size, )
    prediction = softmax(z)   # shape (vocab_size,)
    truth = np.zeros(vocab_size)   # shape (vocab_size,) one hot
    truth[outsideWordIdx] = 1
    loss = - np.log(np.sum(prediction * truth)) # scalar
    gradCenterVec = outsideVectors.T @ (prediction - truth) # (word_dim, )
    gradOutsideVecs = ( np.outer((prediction - truth), centerWordVec)).squeeze() # (vocab_size, word_dim)
    ### END YOUR CODE

    return loss, gradCenterVec, gradOutsideVecs


def getNegativeSamples(outsideWordIdx, dataset, K):
    """ Samples K indexes which are not the outsideWordIdx """

    negSampleWordIndices = [None] * K
    for k in range(K):
        newidx = dataset.sampleTokenIdx()
        while newidx == outsideWordIdx:
            newidx = dataset.sampleTokenIdx()
        negSampleWordIndices[k] = newidx
    return negSampleWordIndices


def negSamplingLossAndGradient(
    centerWordVec,
    outsideWordIdx,
    outsideVectors,
    dataset,
    K=10
):
    """ Negative sampling loss function for word2vec models

    Implement the negative sampling loss and gradients for a centerWordVec
    and a outsideWordIdx word vector as a building block for word2vec
    models. K is the number of negative samples to take.

    Note: The same word may be negatively sampled multiple times. For
    example if an outside word is sampled twice, you shall have to
    double count the gradient with respect to this word. Thrice if
    it was sampled three times, and so forth.

    Arguments/Return Specifications: same as naiveSoftmaxLossAndGradient
    """

    # Negative sampling of words is done for you. Do not modify this if you
    # wish to match the autograder and receive points!
    negSampleWordIndices = getNegativeSamples(outsideWordIdx, dataset, K)
    indices = [outsideWordIdx] + negSampleWordIndices

    ### YOUR CODE HERE (~10 Lines)

    ### Please use your implementation of sigmoid in here.
    outside_vec = outsideVectors[outsideWordIdx]
    loss = - np.log(sigmoid(outside_vec @ centerWordVec)) \
           - np.sum(np.log(sigmoid(- outsideVectors[negSampleWordIndices] @ centerWordVec)))

    Uo = outsideVectors[indices]
    Uo[0, :] = - Uo[0, :]
    Uo[:, :] = -Uo[:, :]
    Uo_Vc = Uo @ centerWordVec
    gradCenterVec = - Uo.T @ (np.ones_like(Uo_Vc) - sigmoid(Uo_Vc))

    gradOutsideVecs = np.zeros_like(outsideVectors)
    for i in range(len(indices)):
        indice = indices[i]
        if indice == outsideWordIdx:
            gradOutsideVecs[indice, :] = - (1 - sigmoid(outside_vec @ centerWordVec)) * centerWordVec
        else:
            gradOutsideVecs[indice, :] += (1 - sigmoid(-outsideVectors[indice] @ centerWordVec)) * centerWordVec
    ### END YOUR CODE

    return loss, gradCenterVec, gradOutsideVecs


def skipgram(currentCenterWord, windowSize, outsideWords, word2Ind,
             centerWordVectors, outsideVectors, dataset,
             word2vecLossAndGradient=naiveSoftmaxLossAndGradient):
    """ Skip-gram model in word2vec

    Implement the skip-gram model in this function.

    Arguments:
    currentCenterWord -- a string of the current center word
    windowSize -- integer, context window size
    outsideWords -- list of no more than 2*windowSize strings, the outside words
    word2Ind -- a dictionary that maps words to their indices in
              the word vector list
    centerWordVectors -- center word vectors (as rows) is in shape 
                        (num words in vocab, word vector length) 
                        for all words in vocab (V in pdf handout)
    outsideVectors -- outside vectors is in shape 
                        (num words in vocab, word vector length) 
                        for all words in vocab (transpose of U in the pdf handout)
    word2vecLossAndGradient -- the loss and gradient function for
                               a prediction vector given the outsideWordIdx
                               word vectors, could be one of the two
                               loss functions you implemented above.

    Return:
    loss -- the loss function value for the skip-gram model
            (J in the pdf handout)
    gradCenterVecs -- the gradient with respect to the center word vector
                     in shape (num words in vocab, word vector length)
                     (dJ / dv_c in the pdf handout)
    gradOutsideVecs -- the gradient with respect to all the outside word vectors
                    in shape (num words in vocab, word vector length) 
                    (dJ / dU)
    """

    loss = 0.0
    gradCenterVecs = np.zeros(centerWordVectors.shape)
    gradOutsideVectors = np.zeros(outsideVectors.shape)

    ### YOUR CODE HERE (~8 Lines)
    centerWordIdx = word2Ind[currentCenterWord]
    centerWordVec = centerWordVectors[centerWordIdx]
    for out_word in outsideWords:
        lossI, gradCenterVecsI, gradOutsideVectorsI = word2vecLossAndGradient\
            (centerWordVec, word2Ind[out_word], outsideVectors, dataset)
        loss += lossI
        gradCenterVecs[centerWordIdx] += gradCenterVecsI
        gradOutsideVectors += gradOutsideVectorsI

    ### END YOUR CODE
    
    return loss, gradCenterVecs, gradOutsideVectors

```
> [!test] Training Results
> ![](Word_Embedding/Word_Vectors.assets/image-20240816204848560.png)![](Word_Embedding/Word_Vectors.assets/image-20240816204957954.png)



# Global Vectors Methods(Glove)
> [!important]
> It is a count-based model with ALS training techniques.



## Ratio of Co-occurrence
> [!def]
> ![](Word_Embedding/Word_Vectors.assets/image-20240710181958334.png)![](Word_Embedding/Word_Vectors.assets/image-20240710183304224.png)




## Least Squares Objective
> [!def]
> ![](Word_Embedding/Word_Vectors.assets/image-20240710182025005.png)![](Word_Embedding/Word_Vectors.assets/image-20240710182031725.png)![](Word_Embedding/Word_Vectors.assets/image-20240710183517129.png)








## Summary
> [!summary]
> ![](Word_Embedding/Word_Vectors.assets/image-20240710182301632.png)





# Word Vectors Evaluation
