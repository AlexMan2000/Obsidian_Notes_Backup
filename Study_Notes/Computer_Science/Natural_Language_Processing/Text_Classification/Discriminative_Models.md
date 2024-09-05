# Logistic Regression
## Modeling
> [!def]
> ![](Discriminative_Models.assets/dce51e1eb42a061dc05db258cd350682_MD5.jpeg)![](Discriminative_Models.assets/0df03875996a8e9dcdfb111966b61cf8_MD5.jpeg)


## Learning: MLE
> [!important]
> ![](Discriminative_Models.assets/475fc606fa12f6369733af70a494859c_MD5.jpeg)



## Inference
> [!important]
> ![](Discriminative_Models.assets/070810add2dcb51ac7f1fbe2c0a0858e_MD5.jpeg)




## Features
### Bag of Words
> [!def]
> ![](Discriminative_Models.assets/06c6b67c0f5eb383402292030edd8fe6_MD5.jpeg)


### N-gram
> [!def]
> ![](Discriminative_Models.assets/bb0293c6609e57ab4a89acfd1d8cac82_MD5.jpeg)![](Discriminative_Models.assets/9fe7caaffaba39802dfdd3df37d329a6_MD5.jpeg)



# TF-IDF Implementations
> [!code]
```python
# TF-IDF as features
from sklearn.feature_extraction.text import TfidfVectorizer
tfidf_vectorizer = TfidfVectorizer()
tfidf_vectorizer.fit(train_sentence_list)
train_feature_list = tfidf_vectorizer.transform(train_sentence_list)
# LogisticRegression
from sklearn.linear_model import LogisticRegression
lr_classifier = LogisticRegression()
lr_classifier.fit(train_feature_list, train_label_list)
test_feature_list = tfidf_vectorizer.transform(test_sentence_list)
lr_classifier.predict(test_feature_list)
```



# Comparisons
> [!important]
> ![](Discriminative_Models.assets/feee50c398f8842a26e79c21ec311832_MD5.jpeg)

