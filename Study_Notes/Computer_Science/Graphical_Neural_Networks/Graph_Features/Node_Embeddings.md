# Node-Level Features
## Node Degrees
> [!def]
> ![](Node_Embeddings.assets/image-20240817173117545.png)


## Node Centrality
### Eigenvector Centrality
> [!def]
> ![](Node_Embeddings.assets/image-20240817173157887.png)![](Node_Embeddings.assets/image-20240817173214040.png)


### Betweeness Centrality
> [!def]
> ![](Node_Embeddings.assets/image-20240817173247822.png)
> - Could be used to identify the bottleneck node in a graph.



### Closeness Centrality
> [!def]
> ![](Node_Embeddings.assets/image-20240817190811371.png)![](Node_Embeddings.assets/image-20240817204142709.png)![](Node_Embeddings.assets/image-20240817204206462.png)
```python
def closeness_centrality(G, node=5):
  # TODO: Implement the function that calculates closeness centrality
  # for a node in karate club network. G is the input karate club
  # network and node is the node id in the graph. Please round the
  # closeness centrality result to 2 decimal places.

  closeness = 0

  ## Note:
  ## 1: You can use networkx closeness centrality function.
  ## 2: Notice that networkx closeness centrality returns the normalized
  ## closeness directly, which is different from the raw (unnormalized)
  ## one that we learned in the lecture.
  import numpy as np
  return np.round(nx.closeness_centrality(G, node) * (G.number_of_nodes() - 1), 2)
  #########################################

  return closeness

node = 5
closeness = closeness_centrality(G, node=node)
print("The node 5 has closeness centrality {}".format(closeness))
```




## Clustering Coefficients
> [!def]
> ![](Node_Embeddings.assets/image-20240817190634815.png)
> 
```python
import numpy as np
def average_clustering_coefficient(G):
 
  return np.round(nx.average_clustering(G), 2)

avg_cluster_coef = average_clustering_coefficient(G)
print("Average clustering coefficient of karate club network is {}".format(avg_cluster_coef))
```



## Graphlets
> [!def]
> ![](Node_Embeddings.assets/image-20240817191001801.png)![](Node_Embeddings.assets/image-20240817191010712.png)![](Node_Embeddings.assets/image-20240817191026651.png)





## Pagerank Importance
### Definition of Flow Model
> [!def]
> ![](Node_Embeddings.assets/image-20240817192432114.png)![](Node_Embeddings.assets/image-20240817192527713.png)

> [!example]
> ![](Node_Embeddings.assets/image-20240817192732177.png)


### How to Solve
> [!important]
> ![](Node_Embeddings.assets/image-20240817193309979.png)![](Node_Embeddings.assets/image-20240817193322998.png)

> [!example]
> ![](Node_Embeddings.assets/image-20240817193348628.png)![](Node_Embeddings.assets/image-20240817193358866.png)




### Pagerank Problems
> [!important]
> ![](Node_Embeddings.assets/image-20240817193446062.png)


#### Spider-Trap Problem
> [!def]
> ![](Node_Embeddings.assets/image-20240817193552154.png)![](Node_Embeddings.assets/image-20240817193812366.png)







#### Dead-ends Problem
> [!def]
> ![](Node_Embeddings.assets/image-20240817193724215.png)![](Node_Embeddings.assets/image-20240817193823546.png)



### Google Algorithm
> [!important]
> ![](Node_Embeddings.assets/image-20240817193915807.png)![](Node_Embeddings.assets/image-20240817193932205.png)![](Node_Embeddings.assets/image-20240817193944158.png)![](Node_Embeddings.assets/image-20240817193955731.png)




### Code Implementations
> [!code]
> ![](Node_Embeddings.assets/image-20240817192826266.png)
```python
def one_iter_pagerank(G, beta, r0, node_id):
  # TODO: Implement this function that takes a nx.Graph, beta, r0 and node id.
  # The return value r1 is one interation PageRank value for the input node.
  # Please round r1 to 2 decimal places.

  r1 = 0

  ############# Your code here ############
  ## Note:
  ## 1: You should not use nx.pagerank
  for neighbor_id in nx.neighbors(G, node_id):
    r1 += beta * r0 / G.degree(neighbor_id)
  r1 += (1 - beta) / G.number_of_nodes()
  r1 = round(r1, 2)
  #########################################

  return r1

beta = 0.8
r0 = 1 / G.number_of_nodes()
node = 0
r1 = one_iter_pagerank(G, beta, r0, node)
print("The PageRank value for node 0 after one iteration is {}".format(r1))
```










# Node Embeddings
## Objective
> [!def]
> ![](Node_Embeddings.assets/6afec62d448d7e5d8ad467fe0cf53614_MD5.jpeg)




### Node Similarities
> [!motiv]
> ![](Node_Embeddings.assets/3a983ed7bb0bb68ed2b46cf1d6a1c610_MD5.jpeg)



## Encoder-Decoder Structure
### Definition
> [!important]
> ![](Node_Embeddings.assets/14dc10376cfe970f957d60ec3836fb3f_MD5.jpeg)![](Node_Embeddings.assets/79a920759c20dbf2fd844c56ed739088_MD5.jpeg)




### Shallow Encoding
> [!def]
> ![](Node_Embeddings.assets/a57f13ed02c82123df95d0e8332c087b_MD5.jpeg)




## DeepWalk
### How to Learn - Random Walk
> [!important]
> ![](Node_Embeddings.assets/5eac4c865e9a7685ad8418797a48aab3_MD5.jpeg)![](Node_Embeddings.assets/6817ff8a6ccfa793c67b6032d7121488_MD5.jpeg)


### Algorithm
> [!algo]
> ![](Node_Embeddings.assets/4368cee034ad0e1a5b08126f375e79ed_MD5.jpeg)![](Node_Embeddings.assets/9cc152124ccb585bde085718122ce951_MD5.jpeg)![](Node_Embeddings.assets/3c8f0d57d02aa48660aa4dc74e8f35d2_MD5.jpeg)


### Optimization
#### Negative Sampling
> [!important]
> ![](Node_Embeddings.assets/4d4d7e8c8030497fb84f94a52c74f4e8_MD5.jpeg)![](Node_Embeddings.assets/62b2df5eaf319f8d371de31d4d952b04_MD5.jpeg)

> [!algo]
> ![](Node_Embeddings.assets/823d53ef063dfa62f96024a62190d929_MD5.jpeg)![](Node_Embeddings.assets/0a78809ce5dbd42911c3d23b15c6c16c_MD5.jpeg)



#### SGD
> [!algo]
> ![](Node_Embeddings.assets/290faa6d8ece043cb9b7ad21710cc402_MD5.jpeg)





### Random Walk Strategy
> [!def]
> ![](Node_Embeddings.assets/c8442fe84394c00fd028abab7c2aa752_MD5.jpeg)




## Node2Vec
### Motivations
> [!motiv]
> ![](Node_Embeddings.assets/f4cef9ff1ffaf5efeb2f0d23f5b106e9_MD5.jpeg)



### Biased Walk
> [!def]
> ![](Node_Embeddings.assets/86030e754b2ea04ad5c3ac5f6183130e_MD5.jpeg)![](Node_Embeddings.assets/fbf98c5f05314963f574717ed36f2a59_MD5.jpeg)


### One-step of Biased Walk
> [!important]
> ![](Node_Embeddings.assets/4d3d2d925f01f31b5e23c62292e0e7a1_MD5.jpeg)![](Node_Embeddings.assets/f53e1dfda5ede751d71cb6cc327ae914_MD5.jpeg)![](Node_Embeddings.assets/f4dd6440509cbb0584e711b628c62470_MD5.jpeg)![](Node_Embeddings.assets/6677b36effa201cd10776f64fb0adb50_MD5.jpeg)

> [!algo]
> ![](Node_Embeddings.assets/13bc54584aac72e0295c22b46ae53a0c_MD5.jpeg)
> Details in [Node2Vec](Node2Vec.md)





## Matrix Factorization
### Definition
> [!def]
> ![](Node_Embeddings.assets/5a88baf07555ebeb9f1a27c81e3eca81_MD5.jpeg)![](Node_Embeddings.assets/b1dea4a0ca0c7b7bdcde51962a64bb53_MD5.jpeg)


### Objectives
> [!important]
> ![](Node_Embeddings.assets/96382d8ada3aa7830cc2a85bffaac345_MD5.jpeg)





# Limitations
> [!important]
> ![](Node_Embeddings.assets/96a179b1c22612c6a8490442aa1758fe_MD5.jpeg)![](Node_Embeddings.assets/93860dca04edb1b60f9495fc9d2360d3_MD5.jpeg)![](Node_Embeddings.assets/df7752748fd9e072f5933e3e0a16cc62_MD5.jpeg)



