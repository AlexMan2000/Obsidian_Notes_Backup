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










# Node Similarities




# Node Embeddings
## DeepWalk




## Node2Vec




## Matrix Factorization

