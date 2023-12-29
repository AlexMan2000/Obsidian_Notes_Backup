# Matching in General Graphs
## Matching Problem Motivations
> [!motiv] Motivation
> ![](Directed%20Graph.assets/image-20231221081323513.png)![](Directed%20Graph.assets/image-20231221081333629.png)![](Directed%20Graph.assets/image-20231221081340140.png)![](Directed%20Graph.assets/image-20231221081347243.png)



## Matching Definitions
> [!def]
> ![](Directed%20Graph.assets/image-20231221081247126.png)



## Perfect Matchings
> [!def]
> ![](Directed%20Graph.assets/image-20231221081520515.png)



## Maximum Matching
> [!def]
> ![](Directed%20Graph.assets/image-20231221081726877.png)
> **Notes:**
> 
> ![](Directed%20Graph.assets/image-20231221081812049.png)

> [!example] Possible Algorithm to Find Maximum Matching
> The approach is very simple, just starting from any node, keep ading edges until we cannot any valid edges or the addition of edges cause some pair of edges to share the same endpoints.
> ![](Directed%20Graph.assets/image-20231221082023734.png)![](Directed%20Graph.assets/image-20231221082036382.png)



## Maximal Matching
> [!def]
> ![](Directed%20Graph.assets/image-20231221082546128.png)
> **Distinction between maximum/maximal matching:**
> 
> The concept of maximal matching comes out from our iterative growing algorithm, which may get stuck in the middle and that the set of edges cannot grow any further and thus cannot reach maximum matching. 
> 
> But both maximum matching and maximal matching are valid matching outcome. The difference are just the number of edges in total.
> 
> ![](Directed%20Graph.assets/image-20231221082909229.png)




# Finding Matchings in General Graphs
## Motivation
> [!example] Update on the interative edge addition algorithm
> ![](Directed%20Graph.assets/image-20231221083149890.png)![](Directed%20Graph.assets/image-20231221084752890.png)
> The observation here is, for any maximal matching, if we remove some edges and add some other edges, we will end up having some special paths that we will define below.



## Alternating Path/Cycles
> [!def]
> ![](Directed%20Graph.assets/image-20231221085055800.png)![](Directed%20Graph.assets/image-20231221090655735.png)
> The alternating path in fig 1 doesn't contain endpoints that is already matched(contained in some edges).
> 
> ![Fig 1](Directed%20Graph.assets/image-20231221090711401.png)
> The alternating path in fig 2 contain endpoints that is already matched.
> 
> ![Fig 2](Directed%20Graph.assets/image-20231221091325143.png)
> The observation is that for fig 2 if we remove the red edge and add the green edges, the current matching will be broken.




## Augmenting Path
> [!def]
> ![](Directed%20Graph.assets/image-20231221091234206.png)![](Directed%20Graph.assets/image-20231221091624267.png)



## Berge's Theorem - Algorithm
> [!algo]
> ![](Directed%20Graph.assets/image-20231221091759568.png)




## Berge's Theorem - Proof(Optional)
> [!thm]
> 








# Bipartite Matching
## Bipartite Graph
> [!def]
> ![](Stable%20Matching%20Problem.assets/image-20231221110226185.png)



## Motivation: Sex in America
> [!motiv] Motivation
> 假设美国有1.47亿男性和1.52亿女性，现在我们要探究一个问题: 男性的平均伴侣(假设没有基佬，即伴侣只能为异性)数量比女性的平均伴侣数量多还是少？
> 很多科学研究报告试图回答这个问题，为此网络上有很多类似的实验报告，其中有些甚至动用了大量的人力资源和金钱。但是实际上这个问题在数学家看来非常的愚蠢，他们只需要15分钟时间就可以完成这个问题的推导和证明。

> [!thm]
> 假设男性的数量是$|M|$, 女性的数量是$|F|$, 则男性的平均伴侣数量是女性平均伴侣数量的$\frac{|F|}{|M|}$倍。

> [!proof]
> 证明的过程依赖于一个重要的图类型，`bipartite`。假设我们有一个简化的模型如下, 模型假设任意一条`edge`连接着一个男性（左侧的节点表示）和一个女性（右侧的节点表示），代表一段关系。
> ![](Stable%20Matching%20Problem.assets/image-20231030092618527.png)
> 根据图论基础知识我们知道，$\sum_{x\in M}deg(x)=\sum_{y\in F}deg(y)=|E|$。
> 所以男性的平均伴侣数量是$A_M=\frac{|E|}{|M|}$，女性的平均伴侣数量是$\frac{|E|}{|F|}$，于是我们可以很轻松地得到男性平均伴侣数量是女性平均伴侣数量的$\frac{\frac{|E|}{|M|}}{\frac{|E|}{|F|}}=\frac{|F|}{|M|}$倍。因为获取人口普查数据相对容易，所以我们很轻松可以得到$\frac{|F|}{|M|}=1.035$，也就是说男性平均比女性的伴侣数量多$3.5\%$。
> 



## Bipartite Matching For Men
### Motivation
> [!motiv] Motivation
> 现在我们考虑另一个问题，如何使得每一对配对的男性女性都是高兴的，换句话说就是对自己的伴侣是满意的，那么我们能否达成这个目的呢?
> 由于女性比男性多，所以如果我们要求每个女性都要和一个男性配对，则肯定会有两个女性喜欢同一个男性，所以一定会有一个女性对自己现在的伴侣没有那么满意，而且一定会有多个女性会先后和同一个男性结婚，以保证女性有异性配对记录，所以对女性群体来说，这个目的不能达成。
> ==对于男性这个目的是可以满足的==，下面我们就来探究在什么条件下这个目的能被满足。

### Matching Condition - Informal
> [!info]
> ![](Stable%20Matching%20Problem.assets/image-20231209210307343.png)![](Stable%20Matching%20Problem.assets/image-20231030094857247.png)![](Stable%20Matching%20Problem.assets/image-20231030094906586.png)
> **We have some assumptions here:**
> 
> Each man has to like at least one women. Geometrically speaking, there should be an edge from each man to a woman. In other words, no men should be isolated. 
> 
> First we define the set of women to be to be those who are liked by at least one man, where those isolated women are not considered(not painted in the graph above).
> 
> **Then we define the matching condition:**
> 
> Every subset of men likes at least as large a set of women.
> 
> For example, we cannot find a matching if some of 4 men like only 3 women. 


> [!thm] **Stable Matching Theorem - For Men(Set with smaller Cardinality)**
> ![](Stable%20Matching%20Problem.assets/image-20231221092151365.png)

> [!proof]
> ![](Stable%20Matching%20Problem.assets/image-20231030095344697.png)![](Stable%20Matching%20Problem.assets/image-20231030095352213.png)![](Stable%20Matching%20Problem.assets/image-20231030095615162.png)



### Hall's Theorem - Formalized
#### Matching in a graph
> [!def] Definition
>  ![](Stable%20Matching%20Problem.assets/image-20231030100335803.png)


#### Bottleneck in a graph
> [!def]
> ![](Stable%20Matching%20Problem.assets/image-20231030100341717.png)
> This definition is a little bit tricky. At first sight, $N(S)$ contains at least all points in $S$ and thus $|N(S)|\geq|S|$。
> 
> But there exists some graphs, especially for bipartite graph that can be divided into $L$ and $R$, if we choose the point in $L$, then by definition of the bipartite, any two nodes in $L$ are not connected by edge. Thus $N(L)$ is just the nodes in $R$ that are incident to some nodes in $L$。


#### Main Theorem
> [!thm]
> ![](Stable%20Matching%20Problem.assets/image-20231030100357015.png)
> What Hall's Theorem is saying is just the formalized version of our matching condition. No subset of L is a bottleneck means no subset of men likes less women. In other words, every subset of men likes as least as large the set of women.


### Bipartite Matching Condition
#### Motivation
> [!motiv] Motivation
> 上面的`Hall Theorem`告诉我们，如果我们要验证`G`中是否有`Matching`的存在，我们需要检验所有的左侧集合的子集不是`bottleneck`，在$|L|$较小的时候验证起来还比较容易，因为我们的子集数量不多，但是我们知道对于一个元素数量为$|T|$的集合他有$2^{|T|}$这么多的子集，当$|T|$很大的时候子集的数量也会爆炸型增长。所以我们需要有一种更加简便的方法来检验一个`Graph`中是否满足`Matching Condition`。

#### Degree-Constrained Graph
> [!def] Definition
> ![](Stable%20Matching%20Problem.assets/image-20231030101235813.png)![](Stable%20Matching%20Problem.assets/image-20231030101256485.png)


#### Degree-Constrained => Matching Covering L
> [!thm]
> ![](Stable%20Matching%20Problem.assets/image-20231030101513278.png)

> [!proof]
> ![](Stable%20Matching%20Problem.assets/image-20231030102343596.png)
> 其中$|N(S)|x\geq |S|x$的由来如下：
> 因为$$\begin{align}|N(S)|x&\geq |N(S)|\cdot deg(r)\\&=\sum_{r\in R}deg(r)\\&=\sum_{l\in S}deg(l)\\&\geq\sum_{l\in S}x\\&=|S|x\end{align}$$, where the third equality is a property of bipartite graph.




## Regular Graph - Deg Constrained
### Definition
> [!def]
> ![](Stable%20Matching%20Problem.assets/image-20231030102831095.png)


### Perfect Matching Condition
> [!thm] Theorem
> ![](Stable%20Matching%20Problem.assets/image-20231030102858628.png)


# Bipartite Matching Problems
## Stable Marriage Problem
### Motivation
> [!motiv] Motivation
> 下面我们探究一类问题，这类问题假设有一群男性和一群女性，并且男性数量和女性数量是相等的。现在我们要求每一对男女都是彼此的唯一，换句话说，我们不允许在一起的某对男女对彼此不满意（吃着盘里的，想着锅里的）。
> 


### Stable Matching/Rogue Couple
> [!important]
> ![](Stable%20Matching%20Problem.assets/image-20231030110037482.png)
> 在任何一对`Matching`中，如果彼此都看不顺眼且都喜欢别的男人或女人，则我们称这个`Matching`或者`Couple`为`Rogue Couple`。换句话说，`Rogue Couple`指的是那些本可以在一起而因为种种原因没能在一起的`Couple`。
> 
> ![](Stable%20Matching%20Problem.assets/image-20231030110009725.png)![](Stable%20Matching%20Problem.assets/image-20231030110128907.png)![](Stable%20Matching%20Problem.assets/image-20231030110001825.png)![](Stable%20Matching%20Problem.assets/image-20231030110155871.png)![](Stable%20Matching%20Problem.assets/image-20231221110707234.png)



## Buddy Matching Problem
> [!lemma]
> The fact that the stable marriage problem can always be modeled as a bipartite matching problem gives the existence of a stable marriage, always. But for buddy matching problem, we cannot utilize the bipartite matching framework and thus cannot guarantee the existence of a matching, as shown in the following example.
> ![](Stable%20Matching%20Problem.assets/image-20231221110900419.png)

> [!proof] Proof of Lemma
> ![](Stable%20Matching%20Problem.assets/image-20231221110914151.png)


## Job Candidate Matching Problem
> [!motiv] Motivation
> 


# Stable Matching Algorithms
## Propose and Reject Algorithm
> [!algo] Algorithm
> ![](Stable%20Matching%20Problem.assets/image-20231030111212987.png)

> [!note]
> ![](Stable%20Matching%20Problem.assets/image-20231030111312546.png)



## Properties of PR Algorithm

### Lemma
> [!lemma]
> ![](Stable%20Matching%20Problem.assets/image-20231030111552470.png)


### Stability
> 



