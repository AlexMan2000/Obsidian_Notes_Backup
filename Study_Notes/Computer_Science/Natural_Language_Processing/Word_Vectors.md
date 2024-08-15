  # Motivations
> [!overview]
> In this section we are going to discuss several frequently used methods for word embedding.



# Count-Based Methods
## Co-occurrence Matrix
### Definition
> [!def]
> ![](Word_Vectors.assets/image-20240710141902818.png)


### How to Build One
> [!code]
> ![](Word_Vectors.assets/image-20240708230216904.png)
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
> ![](Word_Vectors.assets/image-20240710142054627.png)![](Word_Vectors.assets/image-20240710142106669.png)




# Window-Based Methods
> [!overview]
> Word2vec is a family of models of **distributional semantics**.
> - Words that occur in similar contexts tend to have similar meanings.


## CBOW Model
### Algorithmic Idea
> [!algo]
> ![](Word_Vectors.assets/image-20240710143209276.png)![](Word_Vectors.assets/image-20240710143227631.png)



### Objective Function
> [!def]
> ![](Word_Vectors.assets/image-20240710143916533.png)












## Skipgram Model
### Algorithmic Idea
> [!algo]
> ![](Word_Vectors.assets/image-20240710144007435.png)






### Objective Function
> [!def] Objective Function
> ![](Word_Vectors.assets/image-20240710134404462.png)![](Word_Vectors.assets/image-20240710135912179.png)

> [!important] Alternative Representations
> ![](Word_Vectors.assets/image-20240710154731484.png)







### Parameters
> [!def]
> ![](Word_Vectors.assets/image-20240710134718809.png)![](Word_Vectors.assets/image-20240710134725484.png)
> Here, every word has two vectors:
> - $\vec{u}_{w}$ is the embedding for the word $w$ that appears as a context word.
> - $\vec{v}_{w}$ is the embedding for the word $w$ that appears as a center word.
> 
> ![](Word_Vectors.assets/image-20240710134739937.png)



### Training & Optimization
> [!def] Empirical Loss
> ![](Word_Vectors.assets/image-20240710135838211.png)


#### Gradient Descent
> [!def]
> ![](Word_Vectors.assets/image-20240710140641414.png)







#### S.G.D Intuition
> [!def]
> ![](Word_Vectors.assets/image-20240710140704251.png)![](Word_Vectors.assets/image-20240710140714414.png)![](Word_Vectors.assets/image-20240710140720054.png)![](Word_Vectors.assets/image-20240710140728701.png)


### Skipgram Derivatives
> [!important]
> Here are some importants results to remember:
> - $U$ is the outside word vectors of shape (`vocab_size, word_dim`)
> - $V$ is the center word vectors of shape (`vocab_size, word_dim`)
> - $J_{naive-{softmaxloss}}(\vec{v}_{c,}o,U)=-log(\hat{y}_o)$, 其中$\hat{y}_o=softmax(U\vec{v}_{c})[oIndex]$, `oIndex`是`outside word index in the vocab size`
> 	- Derivative w.r.t $\vec{v}_c$, $\frac{\partial J}{\partial \vec{v}_c}=U^{\top}(\hat{y}-\vec{y})\in\mathbb{R}^{dim}$, where $\vec{y}$ is the probability vector that has shape `(vocab_size,)`
> 	- Derivative w.r.t $U$, $\frac{\partial J}{\partial U}=(\hat{y}-\vec{y})\vec{v}_c^{\top}\in\mathbb{R}^{vocab\times dim}$
> - $J_{{negative}-{sample}}(\vec{v}_{c},o,U)=-log(\sigma(\vec{u}_o^{\top}\vec{v}_c))-\sum\limits_{s=1}^Klog(\sigma(-\vec{u}_{w_s}^{\top}\vec{v}_c))$
> 	- Derivative w.r.t $\vec{v}_c$
> 	- Derivative w.r.t $\vec{u}_o$
> 	- Derivative w.r.t $\vec{u}_{w_{s}}$

> [!thm]
> ![](Word_Vectors.assets/image-20240721181056747.png)![](Word_Vectors.assets/image-20240721181103302.png)![](Word_Vectors.assets/image-20240721181110140.png)![](Word_Vectors.assets/image-20240721181116347.png)![](Word_Vectors.assets/image-20240721181208972.png)![](Word_Vectors.assets/image-20240813133956196.png)![](Word_Vectors.assets/image-20240813134002472.png)![](Word_Vectors.assets/image-20240813134010987.png)![](Word_Vectors.assets/image-20240813134018829.png)![](Word_Vectors.assets/image-20240813134026082.png)![](Word_Vectors.assets/image-20240813134033513.png)
























## Negative Sampling Techniques
> [!def]
> ![](Word_Vectors.assets/image-20240710161837423.png)



## Word2Vec Implementations






# Global Vectors Methods(Glove)
## Ratio of Co-occurrence
> [!def]
> ![](Word_Vectors.assets/image-20240710181958334.png)![](Word_Vectors.assets/image-20240710183304224.png)




## Least Squares Objective
> [!def]
> ![](Word_Vectors.assets/image-20240710182025005.png)![](Word_Vectors.assets/image-20240710182031725.png)![](Word_Vectors.assets/image-20240710183517129.png)








## Summary
> [!summary]
> ![](Word_Vectors.assets/image-20240710182301632.png)





# Word Vectors Evaluation
