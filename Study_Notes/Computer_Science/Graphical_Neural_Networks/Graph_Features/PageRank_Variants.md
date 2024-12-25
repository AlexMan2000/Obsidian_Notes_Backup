# Overview
> [!overview]
> ![](PageRank_Variants.assets/e66accedefd63726444bc57c2d3526fb_MD5.jpeg)




# PageRank
## Overview - Flow Model
> [!overview] 
> ![](PageRank_Variants.assets/02cf09f25ed8a965c322db2370b63f26_MD5.jpeg)![](PageRank_Variants.assets/ea738bf391dcbedebaafeace9b819441_MD5.jpeg)




## Flow Equation
> [!def]
> ![](PageRank_Variants.assets/599d6b28a726611020fabd24c7292ea1_MD5.jpeg)![](PageRank_Variants.assets/d57ed241687a21397383a982e38a6866_MD5.jpeg)![](PageRank_Variants.assets/85cbb18ab358e2060070b25eb08535c9_MD5.jpeg)



## Matrix Formulation
> [!important]
> ![](PageRank_Variants.assets/047088324e3e29dba3b8d3578bfdef44_MD5.jpeg)![](PageRank_Variants.assets/8490322fbf7a6f63552c1d8eb5d94867_MD5.jpeg)




## How to solve?
> [!algo] Power Iteration Method
> ![](PageRank_Variants.assets/94abec92c82cc5805b3da751849695c4_MD5.jpeg)![](PageRank_Variants.assets/d4eb2aadf7a109be98f96ac27b426fdf_MD5.jpeg)

> [!example]
> ![](PageRank_Variants.assets/d8860d24acb8eed87636128e3906950c_MD5.jpeg)



## Problems
### Dead Ends
> [!def]
> ![](PageRank_Variants.assets/4fdddc60353525a74e4d233517cc70c3_MD5.jpeg)![](PageRank_Variants.assets/b3b699048e8891d0f3a34043ce540fad_MD5.jpeg)![](PageRank_Variants.assets/5353904980f84f2a54bb289649477375_MD5.jpeg)





### Spider Traps
> [!def]
> ![](PageRank_Variants.assets/fe2c27416350e6ee1c3074d3676d3945_MD5.jpeg)![](PageRank_Variants.assets/a4471c95e7586ec560e5005230dcb332_MD5.jpeg)![](PageRank_Variants.assets/8648a963667af6fd9d2e2eafabe643e8_MD5.jpeg)


### Comparisons
> [!def]
> ![](PageRank_Variants.assets/08d3225ea601d959b53a753a2fd8e93c_MD5.jpeg)





## Google Algorithm
> [!algo]
> ![](PageRank_Variants.assets/6d2796987eac8bea734f74f9b80ce3ee_MD5.jpeg)![](PageRank_Variants.assets/4c3a81eb85de154ada36e18c1d452ffb_MD5.jpeg)
> Page Rank measures importance of nodes in a graph using the link structure of the web. A "vote" from an important page is worth more. Specifically, if a page $i$ with importance $r_i$ has $d_i$ out-links, then each link gets $\frac{r_i}{d_i}$ votes. Thus, the importance of a Page $j$, represented as $r_j$ is the sum of the votes on its in links.
> 
> $$r_j=\sum_{i \rightarrow j} \frac{r_i}{d_i}$$, 
> where $d_i$ is the out degree of node $i$.
> 
> The PageRank algorithm (used by Google) outputs a probability distribution which represent the likelihood of a random surfer clicking on links will arrive at any particular page. At each time step, the random surfer has two options
> 
> - With prob. $\beta$, follow a link at random
> - With prob. $1-\beta$, jump to a random page
> 
> Thus, the importance of a particular page is calculated with the following PageRank equation:
> $$r_j=\sum_{i \rightarrow j} \beta \frac{r_i}{d_i}+(1-\beta) \frac{1}{N}$$

> [!example]
> ![](PageRank_Variants.assets/3224f78a8505ee13ad741a4c72927cca_MD5.jpeg)



# Personalized PageRank
## Algorithm Procedure
> [!algo]
> ![](PageRank_Variants.assets/45da28d506f28606954ba5b7f916d46e_MD5.jpeg)![](PageRank_Variants.assets/06f3d7f204de9390a6e7c89714e82b93_MD5.jpeg)


## Benefits
> [!important]
> ![](PageRank_Variants.assets/d031b1e05c017b26b8151fa5806af353_MD5.jpeg)


# Random Walk with Restarts
> [!def]
> ![](PageRank_Variants.assets/039b60cb787915a9d25ae81f17121ddc_MD5.jpeg)




## Code Practices
**Dataset Link:** http://data.openkg.cn/dataset/ch4masterpieces
**Colab Link:** https://colab.research.google.com/drive/1ilsfffYuQHosgIEQugTS5FRDXUMNmRdc#scrollTo=WdWI2ksN__cM

