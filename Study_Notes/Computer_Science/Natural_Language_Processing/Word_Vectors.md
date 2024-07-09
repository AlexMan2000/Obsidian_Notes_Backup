# Motivations
> [!overview]
> In this section we are going to discuss several frequently used methods for word embedding.


# Co-occurrence
## Algorithmic Idea
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



## Window Size
> [!important]
> Window size varies, 


