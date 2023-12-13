# Graph Basics
## Simple Graph
### Definition
> [!def]
> ![image.png](Graph_Theory.assets/20231024_0840419132.png)![image.png](Graph_Theory.assets/20231024_0840433701.png)
> **Properties of Simple Graphs:**
> 🔔: Simple graphs do not have any self-loops  (that is, an edge of the form($\{a, a\}$) since an edge is deﬁned to be a set of two vertices. 
> 🔔: Simple graphs do not contain directed edges (that is, edges of the form $(a, b)$ instead of $\{a, b\}$)。也就是所有的`Edges`都没有方向性的箭头。
> 🔔: Simple graphs do not contain multiedges or multiple edges. In other words, there is at most one edge between any pair of vertices in a simple graph. 这个从我们的定义就可以推断出来，因为在Simple Graph中，所有的`Edges`都是以$\{a, b\}$的形式出现的(这表明$\{a,b\}$和$\{b,a\}$是相同的object)，而不是以$(a,b),(b,a)$的形式。因为`Multiedges`就违反了$E$作为`Set`的最基本的性质(元素必须唯一)。
> 下面是一个`Simple Graph`的例子：
> ![image.png](Graph_Theory.assets/20231024_0840458689.png)




### Degrees&Adjacency&Incidence
> ![image.png](Graph_Theory.assets/20231024_0840466165.png)
> 🔔: `Degree of a vertex`本质就是数`How many edges are connected to it?`
> ![image.png](Graph_Theory.assets/20231024_0840481459.png)
> 🔔: 一条`Edge`至多和两个`Vertices`构成`Incident`关系，因为`Vertices`只能出现在`Edge`的两端。
> **For example, in the simple graph shown in Figure 5.1:**
> 1. Vertex $a$ is `adjacent` to $b$ 
> 2. Vertex $b$ is `adjacent` to $d$
> 3. The edge $\{a, c\}$ is incident to vertices $a$ and $c$. 
> 4. Vertex $h$ has degree $1$, $d$ has degree $2$, and $deg(e)=3$ 
> 5. It is possible for a vertex to have degree $0$(就是孤立的顶点), in which case it is not adjacent to any other vertices. 
> 6. 🔔: `A simple graph`可以没有`Edges`  此时每个`Vertex`的`degree`都是零，也就是说$|E|=0$ , 但是至少需要有一个`Vertex`, 也就是$|V|=1$。



### Connectivity
> ![image.png](Graph_Theory.assets/20231024_0840496201.png)



### Connected Component
> 就是图中的一个个孤立的`Connected`的子图，且每个子图中的节点数量要尽可能多。
> ![image.png](Graph_Theory.assets/20231024_0840502520.png)![image.png](Graph_Theory.assets/20231024_0840517740.png)



### Handshake Lemma
> ![image.png](Graph_Theory.assets/20231024_0840537009.png)



## Some Common Simple Graphs
### Complete Graph(Kn, Km,n)
> 一个`Complete graph` with$n$ vertices,  denoted $K_n$, has an edge between every two vertices, for a total of $\frac{n(n-1)}{2}$ edges(除以$2$的原因是因为同一个`Edges`会被遍历两次) , 下图是$K_5$:
> ![image.png](Graph_Theory.assets/20231024_0840548035.png)
> 换句话说，就是任意两个`Vertex`之间都有一条`Edge`连接。
> ![image.png](Graph_Theory.assets/20231024_0840558517.png)![image.png](Graph_Theory.assets/20231024_0840576593.png)


### Empty Graph
> The empty graph 没有`Edges`(但是为了满足Simple Graph的定义，至少需要有一个Vertex). 
> 🔔: $|E|=0$且$|V|>0$。
> ![image.png](Graph_Theory.assets/20231024_0840584912.png)


### Line Graph(Tree)
> ![image.png](Graph_Theory.assets/20231024_0840584201.png)
> ![image.png](Graph_Theory.assets/20231024_0840594247.png)



### Simple Cycle(Cn)
> ![image.png](Graph_Theory.assets/20231024_0841006808.png)![image.png](Graph_Theory.assets/20231024_0841013831.png)![image.png](Graph_Theory.assets/20231024_0841015030.png)




### Wheel Graph(Wn)
> ![image.png](Graph_Theory.assets/20231024_0841022906.png)![image.png](Graph_Theory.assets/20231024_0841038483.png)



### Bipartite
> ![image.png](Graph_Theory.assets/20231024_0841053778.png)![image.png](Graph_Theory.assets/20231024_0841064864.png)![image.png](Graph_Theory.assets/20231024_0841074868.png)![image.png](Graph_Theory.assets/20231024_0841083077.png)



## Isomorphism(同构)
### Definition
> 两个图可能看起来非常的相似，但是又有本质上的不同，比如下面两个图的结构是一致的，但是$V$集合中的元素是不同的：
> ![image.png](Graph_Theory.assets/20231024_0841098081.png)
> 🔔: 上图中的的两个`Graph`都是拥有`4`个`Vertices`的`Simple Cycle`，结构上类似。但是$V_{(a)}=\{a,b,c,d\}$且$V_{(b)}=\{1, 2, 3, 4\}$. 所以严格上来说，这两个`Graphs`是不同的`mathematical objects` , 虽然他们看起来高度相似。
> 🔔: 这种高度相似性我们称为`Isomorphism`:
> ![image.png](Graph_Theory.assets/20231024_0841108755.png)
> 🔔: 假设我们有两个`Graphs`$G_1$和$G_2$, 则`Isomorphism`表示我从$G_1$中任意拿出一条边，将边的两端能够通过一个`bijection`映射到另一个`Graph`$G_2$中的某条`Edge`的两端，那么就说$G_1$和$G_2$是同构的。
> 🔔: 也就是说两个`Graphs`之间唯一的差别就是`Labeling`的不同。
> 上图中我们有:
> ![image.png](Graph_Theory.assets/20231024_0841117159.png)
> **🔔: 两个**`**Isomorphic**`**的**`**Graphs**`**也可以看起来非常不同, 下面是一个例子:**
> ![image.png](Graph_Theory.assets/20231024_0841126824.png)



### Degree Sequence
> ![image.png](Graph_Theory.assets/20231024_0841132720.png)
> 我们可以通过`Degree Sequence`来判断两个图是否同构。



### Preservation of Graph Properties
> **A property of a graph is said to be preserved under isomorphism if whenever G has that property, every graph isomorphic to G also has that property.  **
> **如果两个图同构，则:**
> 1. 同构的图节点数量相同
> 2. 同构的图的每个节点的`degree`相同。
> 
**所以我们可以通过图之间的**`**Degree Sequence**`**来判断两个图是否同构:**
> 1. 如果两个图同构，则`Degree Sequence`一定相同。即:
> 2. **考虑逆否命题，如果**`**Degree Sequence**`**不一致，则两个图不同构。**
> 
`Two Graphs are isomorphic => Same Degree Sequence`
> 但是逆命题不成立，如果两个图的`Degree Sequence`一致，不一定同构，比如：
> ![image.png](Graph_Theory.assets/20231024_0841134782.png)![image.png](Graph_Theory.assets/20231024_0841154446.png)![image.png](Graph_Theory.assets/20231024_0841153905.png)



### Examples
> ![image.png](Graph_Theory.assets/20231024_0841181161.png)![image.png](Graph_Theory.assets/20231024_0841198630.png)




## Other Types of Graphs
### Multigraph
> ![image.png](Graph_Theory.assets/20231024_0841211285.png)![image.png](Graph_Theory.assets/20231024_0841222023.png)
> Edge weight 只能是 1, 但是可以允许两个节点间有多个edges。


### Tree&Forest
> ![image.png](Graph_Theory.assets/20231024_0841248485.png)


### Subgraphs
> ![image.png](Graph_Theory.assets/20231024_0841256332.png)![image.png](Graph_Theory.assets/20231024_0841254718.png)![image.png](Graph_Theory.assets/20231024_0841265223.png)


### Weighted Graphs
> ![image.png](Graph_Theory.assets/20231024_0841285118.png)
> 就是`Edge`多了一些`Weight`而已。



## Adjacency Matrix
> ![image.png](Graph_Theory.assets/20231024_0841294442.png)


# Graph Traversals - Path&Walk
## Paths and Walks
> [!def] **Definition 5.4.1 Walk**
> A **walk** in a graph, $G$, is a sequence of vertices$v_0, v_1, \ldots, v_k$and edges
> $\left\{v_0, v_1\right\},\left\{v_1, v_2\right\}, \ldots,\left\{v_{k-1}, v_k\right\}$such that $\left\{v_i, v_{i+1}\right\}$ is an edge of $G$ for all $i$ where $0 \leq i<k$. 
> The walk is said to start at $v_0$ and to end at $v_k$, and the length of the walk is defined to be $k$. An edge, $\{u, v\}$, is traversed $n$ times by the walk if there are $n$ different values of $i$ such that $\left\{v_i, v_{i+1}\right\}=\{u, v\}$. 


> [!def] **Definition 5.4.1 Path and Walk**
> A **path** is a walk where all the $v_i$ 's are different, that is, $i \neq j$ implies $v_i \neq v_j$. For simplicity, we will refer to paths and walks by the sequence of vertices.
> 🔔: 总的来说, `Path`就是一条没有重复节点的`Walk`。
> ![image.png](Graph_Theory.assets/20231024_0841318619.png)![image.png](Graph_Theory.assets/20231024_0841336632.png)



## Disjoint Paths
> ![image.png](Graph_Theory.assets/20231024_0841354422.png)


## Finding a Path
> ![image.png](Graph_Theory.assets/20231024_0841367460.png)
> Where there' s a walk, there' s a path.

**Proof**![image.png](Graph_Theory.assets/20231024_0841386730.png)
上述证明过程实际上就是把`Graph`中的`Cycle`给删除了，得到的就是更短的`Walk`。直到删除所有的`Cycles`，我们就得到了一个`Path`。
> ![image.png](Graph_Theory.assets/20231024_0841396634.png)
> 🔔: 我们任选图中的两点，如果这两点之间存在很多`Walk`, 那么一定存在一个路径最短的`Walk`称为两点之间的一个`Path`。


## Walks&Adj Matrix
> 任取图中的两点，假设这两点间被长度为$k$的`Walk`连接，这样的长度为$k$的`Walk`可能有很多个:
> ![image.png](Graph_Theory.assets/20231024_0841415259.png)![image.png](Graph_Theory.assets/20231024_0841414574.png)

**Proof**![image.png](Graph_Theory.assets/20231024_0841439182.png)![image.png](Graph_Theory.assets/20231024_0841456238.png)
**Example**![image.png](Graph_Theory.assets/20231024_0841471049.png)


# Graph Tours - Cycle&Tour
## Cycles&Closed Walk
> ![image.png](Graph_Theory.assets/20231024_0841496368.png)![image.png](Graph_Theory.assets/20231024_0841528874.png)

**Example**![image.png](Graph_Theory.assets/20231024_0841534124.png)![image.png](Graph_Theory.assets/20231024_0841557764.png)


## Euler Walks/Tours
### Definition
> ![image.png](Graph_Theory.assets/20231024_0841574702.png)
> **An Euler walk** is deﬁned to be a **walk** that traverses** every edge in a graph exactly once.**
> **An Euler tour** is an **Euler walk** that **starts and ﬁnishes at the same vertex.**
> ![image.png](Graph_Theory.assets/20231024_0841585833.png)



### Conditions for Euler Walk
> **An undirected graph has an Eulerian walk** if and only if **it is connected (except for isolated vertices) and has at most two odd degree vertices. **

**Proof**![image.png](Graph_Theory.assets/20231024_0841594032.png)![image.png](Graph_Theory.assets/20231024_0842017344.png)
> ![image.png](Graph_Theory.assets/20231024_0842023708.png)

**Solution**![image.png](Graph_Theory.assets/20231024_0842043511.png)



### Conditions for Euler Tour⭐⭐⭐⭐⭐
```ad-thm
 ![image.png](Graph_Theory.assets/20231024_0842051213.png)

这里`Even Degree`说的是对所有的`Vertices`都成立。
```
> [!proof] Theoretic Proof
> ![image.png](Graph_Theory.assets/20231024_0842081442.png)![image.png](Graph_Theory.assets/20231024_0842109653.png)![image.png](Graph_Theory.assets/20231024_0842129188.png)![image.png](Graph_Theory.assets/20231024_0842149703.png)

> [!Proof] Proof by Picture
> **Proof of only if -  By Picture**![image.png](Graph_Theory.assets/20231024_0842159130.png)![image.png](Graph_Theory.assets/20231024_0842172485.png)
**Proof of if - By Picture**![image.png](Graph_Theory.assets/20231024_0842184686.png)![image.png](Graph_Theory.assets/20231024_0842195721.png)![image.png](Graph_Theory.assets/20231024_0842214651.png)![image.png](Graph_Theory.assets/20231024_0842245309.png)![image.png](Graph_Theory.assets/20231024_0842251348.png)![image.png](Graph_Theory.assets/20231024_0842276908.png)
**Proof of if - Recursive Algorithm**![image.png](Graph_Theory.assets/20231024_0842298955.png)


### Applications
#### Apply the procedure
> [!important]
> ![](Graph_Theory.assets/image-20231029213427294.png)![](Graph_Theory.assets/image-20231029213441744.png)


#### Practice Eulerian Tours
> [!example]
> ![image.png](Graph_Theory.assets/20231024_0842313210.png)![image.png](Graph_Theory.assets/20231024_0842339152.png)![image.png](Graph_Theory.assets/20231024_0842354469.png)


#### Number of Walks Covering All Edges
> HW03 Fa20

> [!example]
> ![](Graph_Theory.assets/image-20231029220228031.png)

> [!proof]
> ![](Graph_Theory.assets/image-20231029220314025.png)





## Hamiltonian Cycles
### Definition
> ![image.png](Graph_Theory.assets/20231024_0842372780.png)



## Summary-Path&Walk&Cycle&Tour
> [!summary]
> ![](Graph_Theory.assets/image-20231211195916351.png)




# Hypercubes
## Defintion
### Binary Code Definition
> ![image.png](Graph_Theory.assets/20231024_0843005673.png)
> **Also called n-cube for n-dimensional hypercube.**


### Recursion Definition
> ![image.png](Graph_Theory.assets/20231024_0843015737.png)![image.png](Graph_Theory.assets/20231024_0843039444.png)![image.png](Graph_Theory.assets/20231024_0843053366.png)



## Number of Edges
> ![image.png](Graph_Theory.assets/20231024_0843061196.png)![image.png](Graph_Theory.assets/20231024_0843082080.png)
> **Proof 1**中的$2^n$指的是`Vertex`的数量，$n$指的是每个`vertex`的`degree`大小，但是每个`edge`会被算两次，所以$\frac{n\times 2^n}{2}=n2^{n-1}$条边。
> **Proof 2**中$2E(n-1)$指的是我首先复制两个`subcubes`(分别为`0-subcube`和`1-subcube`)。$+2^{n-1}$指的是将`subcubes`的所有对应的顶点(比如$1-000$和$0-000$相联结起来)，一共新增$2^{n-1}$条边。于是递归式就是$E(n)=2E(n-1)+2^{n-1}$。
> ![image.png](Graph_Theory.assets/20231024_0843093416.png)
> **证明:**
> 1. **Base Step: **对于$n=1$我们有$E(1)=1\times 2^{1-1}=1$, 成立。
> 2. **Inductive Hypothesis:** 假设$P(k)$成立，即$E(k)=k2^{k-1}$成立，则
> 3. **Inductive Step: **$E(k+1)=2E(k)+2^{k}=k2^k+2^k=(k+1)2^{(k+1)-1}$**，成立。**
> 
所以$E(n)=n2^{n-1}$成立。
> ![image.png](Graph_Theory.assets/20231024_0843106513.png)
> **证明：**
> 证明比较简单，就是$n$位二进制的结果。



## Two-Colorability of n-cube
> **Some Observations:**
> 1. Hypercube的edge连接的两个vertices只有一个bit是不同的。如果两个vertices的bit有两位是不同的，则这两个vertices之间没有edge连接。
> 2. Hypercube一定是`Bipartite`，因为我们总是可以选取含有奇数个1的vertices作为一组，含有偶数个1的vertices作为一组，每一条edge都会将一个1flip成0, 所以每个odd # 1 vertex总会和一个even # 1 vertex相连接。



## Cuts in Graphs
> ![image.png](Graph_Theory.assets/20231024_0843119361.png)



## Connectivity Properties
> ![image.png](Graph_Theory.assets/20231024_0843132690.png)![image.png](Graph_Theory.assets/20231024_0843158172.png)

**Proof**![image.png](Graph_Theory.assets/20231024_0843169436.png)![image.png](Graph_Theory.assets/20231024_0843183036.png)


## *Hamiltonian Tour - Longest Simple Cycle
> ![image.png](Graph_Theory.assets/20231024_0843208448.png)

**Solution**


## Hypercubes and Boolean Functions
> ![image.png](Graph_Theory.assets/20231024_0843213289.png)



# Graph Coloring
## Problem Setting
> 每次到了考试周，学生需要在不同的时间参加考试。现在的问题是，如何保证学生`Enroll in`的课程的考试时间互相不冲突。我们可以用图来建模:
> 下图中，每个节点代表一门课的考试，如果两个节点之间存在`Edge`直接相连，代表学生同时`Enroll in`了这两门课，即这两门课的考试时间不能有冲突，也就是说`Edge`相连的两端的节点代表的考试时间不能相同。
> 如果我们用不同的颜色来代表考试时间，则`Edge`两端的节点颜色不能相同。
> 另外，一种很粗暴的方式就是将所有考试安排在不同的时间，但是因为考试周的时间有限，这么做不合实际。所以我们还要求考试时间段(比如`13:00~14:00`, `13:25~15:25`)尽可能少（尽量都安排在一起）。
> ![image.png](Graph_Theory.assets/20231024_0843232002.png)
> `**Graph-Coloring**`**问题的目标是:**
> 1. `Edge`相连的两端的节点的颜色必须不一样。
> 2. 颜色数量尽可能少。
> 
**围绕**`**Graph-Coloring**`**我们有:**
> 1. 我们称一个`Graph`具有一种`Coloring`当且仅当`Coloring`解决了:
>    1. `Edge`相连的两端的节点的颜色必须不一样。
>    2. 颜色数量尽可能少。
> 
的问题。
> 2. 一个`Graph`是`K-colorable`当且仅当`It has a coloring with at most k colors`。
> 
**总结一下:**
> ![image.png](Graph_Theory.assets/20231024_0843244127.png)



## Chromatic Number⭐⭐⭐⭐⭐
> ![image.png](Graph_Theory.assets/20231024_0843255176.png)
> 我们对$\chi(G)$有上界定义:
> ![image.png](Graph_Theory.assets/20231024_0843264909.png)![image.png](Graph_Theory.assets/20231024_0843283748.png)

**Proof of Theorem 5.3.2**![image.png](Graph_Theory.assets/20231024_0843294556.png)


### Graph-Width and Coloring
> ![image.png](Graph_Theory.assets/20231024_0843318425.png)![image.png](Graph_Theory.assets/20231024_0843318175.png)

**Proof**![image.png](Graph_Theory.assets/20231024_0843333132.png)



# Graph Connectivity
## Connectivity
> [!def]
> ![](Graph_Theory.assets/20231024_0843334367.png)![](Graph_Theory.assets/image-20231212201341626.png)
> 注意任意两点的`Connectivity`指的不是存在一条`Edge`直接相连，而是说存在一个`PATH`在两点之间。
> **Connected Example:**
> ![](Graph_Theory.assets/20231024_0843358912.png)
> **Disconnected Example:**
> ![](Graph_Theory.assets/20231024_0843368225.png)

> [!important] Negation on the definition
> We have two ways to negate the defintion, the first one is:
> 
> **There exists $u,v\in V$ such that $u\nleftrightarrow v$**
> 
> The second way, as we will introduce later, relies on a new concept: connected components.
> 
> **If the graph is not connected, then it must consist of several connected components.**




## Connectivity Properties
> [!property]
> ![](Graph_Theory.assets/image-20231212201318180.png)





## Connected Components
### Definition
> [!def]
> ![](Graph_Theory.assets/image-20231211191018068.png)
> ![](Graph_Theory.assets/20231024_0843372205.png)![](Graph_Theory.assets/20231024_0843388168.png)
> **🔔: 注意，**`Connected Components`**是**`Maximum Set of Connected Vertices`**，这里的**`Maximum`**是重点。**
> ![](Graph_Theory.assets/20231024_0843399098.png)![](Graph_Theory.assets/20231024_0843395106.png)![](Graph_Theory.assets/20231024_0843397133.png)




### Using DFS to find all connected components
```c
function DFS(v, visited, graph):
    visited[v] = true
    for each u in graph[v]:   // Iterating over neighbors
        if not visited[u]:
            DFS(u, visited, graph)

function computeConnectedComponents(graph):
    V = number of vertices in graph
    visited = [false, false, ...] (size V)
    count = 0

    for v = 0 to V-1:
        if not visited[v]:
            count += 1
            DFS(v, visited, graph)

    return count
```


### Each node -> At most One Conneced Component
> [!thm]
> ![](Graph_Theory.assets/image-20231211191154314.png)![](Graph_Theory.assets/image-20231211191201294.png)

> [!proof] Proof Sketch
> ![](Graph_Theory.assets/image-20231211191247647.png)

> [!proof] Formal Proof
> ![](Graph_Theory.assets/image-20231211191224078.png)


### Each node -> At Least One Conneced Component
> [!corollary] Corollary 1
> Another way of thinking about the theorem above is the following: 
> 
> **No node in a graph can belong to more than one connected component. In other words, any node in a graph can belong to at most one connected component.**  
> 
> You can see this as follows – suppose that a node could actually be in two different connected components. But by the previous theorem, we know that the intersection of those connected components must be empty, contradicting the fact that our chosen node belongs to both connected components.

> [!corollary] Corollary 2
> Then following the corollary 1, we want to investigate the following property:
> 
> **Any node in a graph belongs to at least one connected component.**
> ![](Graph_Theory.assets/image-20231211193628367.png)

> [!proof] Proof Idea
> ![](Graph_Theory.assets/image-20231211193556266.png)![](Graph_Theory.assets/image-20231211193612304.png)

> [!proof] Formal Proof
> ![](Graph_Theory.assets/image-20231211193638834.png)


> [!corollary] Corollary 3
> ![](Graph_Theory.assets/image-20231211193714452.png)



# K-Connected Graphs
## Motivation: Highway Break Downs
> [!motiv] Why K-connected
> ![](Graph_Theory.assets/image-20231211194029642.png)![](Graph_Theory.assets/image-20231211194035619.png)![](Graph_Theory.assets/image-20231211194042056.png)


## Definition: K-Connectedness
> [!def]
> ![](Graph_Theory.assets/20231024_0843403449.png)![](Graph_Theory.assets/20231024_0843411727.png)
> 1. $b$和$e$在删除掉了$\{b,c\}$和$\{b,h\}$之后整个就不再`Connected`, 所以是`2-edge connected`.
> 2. $c$和$e$在删除掉了$\{b,c\},\{c,d\},\{c,e\}$之后就不再`Connected`, 所以是`3-edge connected`.
> 3. $g$和$e$在删除掉了$\{f,g\}$之后就不再`Connected`, 所以是`1-edge connected`.
> 
> Intuitively, you can think of k-edge-connected graphs as graphs with the following property. 
> 
> Suppose that you have a collection of computers (nodes) linked together in a network by cables (edges). 
> 
> - Initially, each computer can communicate with each other computer either directly (because they are linked together), or indirectly (by routing messages through other computers). 
> - Then a saboteur finds these computers, then chooses and cuts her choice of k – 1 of these cables, breaking the links. 
> 	- If the graph of these computers is k-edgeconnected, then you don't need to worry about the cut cables. Every computer will still be able to reach every other computer.
> 	- That said, if the saboteur were to cut one more cable, it's possible (though not guaranteed) that the network might end up disconnected.



## Insights: 2-Edge-Connected Graphs⭐⭐⭐⭐⭐
> [!example]
> ![](Graph_Theory.assets/image-20231211194525374.png)![](Graph_Theory.assets/image-20231211194553210.png)


### Bridges
> [!important]
> ![](Graph_Theory.assets/image-20231211194707136.png)![](Graph_Theory.assets/image-20231211194907094.png)
> The above definition gives us a way to check if a graph is 2-edge-connected: we can check whether the graph is connected, and from there check each edge to see if it forms a bridge.


### What 2-edge-connectedness mean?
> [!concept]
> ![](Graph_Theory.assets/image-20231211195316299.png)![](Graph_Theory.assets/image-20231211195450077.png)
> Now, for a key insight. Suppose that we start off at u and take our initial path to v. We then take the secondary path from v back to u. This gives us a cycle that goes from u back to itself. It's not necessarily a cycle(could be a walk), though, since we might end up retracing some of the same nodes and edges. But nonetheless, this quick thought experiment shows that there is some kind of connection between 2-edge-connected graphs and cycles. 


### Graph with Simple Cycles
> [!concept]
> ![](Graph_Theory.assets/image-20231211200635230.png)![](Graph_Theory.assets/image-20231211200652437.png)

> [!thm]
> ![](Graph_Theory.assets/image-20231211200706088.png)

> [!proof]
> ![](Graph_Theory.assets/image-20231211200732568.png)

> [!corollary]
> ![](Graph_Theory.assets/image-20231211201117131.png)


### Cycle => 2-edge-connectedness
> [!concept]
> ![](Graph_Theory.assets/image-20231211201804911.png)![](Graph_Theory.assets/image-20231211201814444.png)

> [!thm]
> ![](Graph_Theory.assets/image-20231211201828295.png)



### 2-edge-connectedness => cycle
> [!important]
> ![](Graph_Theory.assets/image-20231211202415015.png)![](Graph_Theory.assets/image-20231211202436114.png)

> [!thm]
> ![](Graph_Theory.assets/image-20231211202457301.png)

> [!proof] Proof Idea
> ![](Graph_Theory.assets/image-20231211202507501.png)

> [!proof] Formal Proof
> ![](Graph_Theory.assets/image-20231211202520490.png)![](Graph_Theory.assets/image-20231211202525012.png)


## Minimum Edges in connected graph
> [!thm]
> ![](Graph_Theory.assets/20231024_0843425741.png)
> 证明的关键思路就是我们在`Inductive Step`的时候先删除了一个`Edge`回归到`Inductive Hypothesis`的状态。

> [!proof]
> ![](Graph_Theory.assets/20231024_0843448198.png)![](Graph_Theory.assets/20231024_0843448858.png)
> ![](Graph_Theory.assets/20231024_0843468897.png)
> 一个`Graph (with v vertices)`要想`Connected`, 则说明只有一个`Component`, 于是$e=1$, 所以是`v-1 edges`。




## Build Up Error⭐⭐⭐⭐⭐
> [!info]
![image.png](Graph_Theory.assets/20231024_0843461309.png)![image.png](Graph_Theory.assets/20231024_0843472331.png)

> [!bug] Buggy Proof
> ![image.png](Graph_Theory.assets/20231024_0843499491.png)![image.png](Graph_Theory.assets/20231024_0843513432.png)
> ![image.png](Graph_Theory.assets/20231024_0843532831.png)

> [!success] Successful Proof
> ![image.png](Graph_Theory.assets/20231024_0843553575.png)



# Minimally-Connected Graphs(2-connected Graph)
## Motivations: What is tree
> [!motiv] From 2-edge-connectedness
> Our discussion of 2-edge-connected graphs focused on graphs that were connected with some measure of redundancy. It is always possible to remove an edge from a 2-edge-connected graph without disconnecting that graph. 
> 
> In this section, we turn to the opposite extreme by focusing on the most fragile graphs possible – **graphs that are connected, but which have absolutely no redundancy at all.**



## Acyclic Graphs
> [!def]
> ![](Graph_Theory.assets/image-20231211215656426.png)


## Minimally Connected Graphs
### Definition
> [!def]
> ![](Graph_Theory.assets/image-20231211203228809.png)![](Graph_Theory.assets/image-20231211203235946.png)![](Graph_Theory.assets/image-20231211203244902.png)
> **Notes for Graph with Single Node:**
> 
> Notice that ==the graph of just a single node is considered to be minimally connected== because it is indeed connected (every node can reach every other node) and it is also true that removing any edge from the graph disconnects it. 
> 
> This second claim is true vacuously: there are no edges in the graph, so the claim “if any edge is the graph is removed, it disconnects the graph” is automatically true. We can thus think of a singlenode graph as a degenerate case of a minimally-connected graph.

> [!important] Negation on the definition
> Sometimes in the proof we may negate the statement so as to make progress. For minimally connectedness, the negation of definition should be:
> 
> **There exists an edge $\{u,v\}$, where $u\neq v$ such that when it is removed from the original graph $G=(V,E)$, the resulting graph $G'=(V,E')$ remains connected.**



### Property
> [!thm]
> ![](Graph_Theory.assets/image-20231211215907064.png)

> [!proof]
> ![](Graph_Theory.assets/image-20231211204306922.png)
> The proof utilize the corollary under this section [Graph with Simple Cycles](Graph_Theory.md#Graph%20with%20Simple%20Cycles), which says that 
> 
> **If a graph is connected, undirected and contains a simple cycle, then removing any edges from this cycle won't disconnect the graph.**

## Maximally Acyclic Graphs
> [!def]
> ![](Graph_Theory.assets/image-20231211220343592.png)![](Graph_Theory.assets/image-20231211220402468.png)![](Graph_Theory.assets/image-20231211215500204.png)


## Connected Acyclic Graphs
> [!thm]
> ![](Graph_Theory.assets/image-20231211215534814.png)

> [!proof] Formal Proof
> ![](Graph_Theory.assets/image-20231211220451757.png)


## Equivalent Statements ⭐⭐⭐⭐
> [!important]
> ![](Graph_Theory.assets/image-20231211220719985.png)
> Is the converse true? It turns out, however, that all of the above definitions are completely equivalent to one another.
> 
> ![](Graph_Theory.assets/image-20231211220731130.png)

> [!proof] Proof Sketch
> ![](Graph_Theory.assets/image-20231211221211108.png)![](Graph_Theory.assets/image-20231211221700126.png)![](Graph_Theory.assets/image-20231211221704624.png)

> [!proof] Formal Proof
> ![](Graph_Theory.assets/image-20231211221734160.png)![](Graph_Theory.assets/image-20231211221741256.png)



## Summary
> [!summary]
> ![](Graph_Theory.assets/image-20231211221755863.png)



# Trees
## Several Definitions
> [!def]
> ![](Graph_Theory.assets/image-20231211222817292.png)[](Graph_Theory.assets/20231024_0842415041.png)![](Graph_Theory.assets/20231024_0842427039.png)![](Graph_Theory.assets/20231024_0842449739.png)


## Unique Path between Nodes
> [!thm]
> The three properties we proved about trees – minimal connectivity, connectivity/acyclicity, and maximal acyclicity – give us a good intuition about many properties of trees. However, there is one property of trees that is in many cases even more useful than these three.
> ![](Graph_Theory.assets/image-20231211223412495.png)


### Forward Direction
> [!proof] Proof Sketch
> ![](Graph_Theory.assets/image-20231211223653965.png)

> [!proof] Formal Proof
> ![](Graph_Theory.assets/image-20231211223713109.png)


### Backward Direction
> [!proof] Proof Sketch
> ![](Graph_Theory.assets/image-20231211224553833.png)

> [!proof] Formal Proof
> ![](Graph_Theory.assets/image-20231211224625472.png)![](Graph_Theory.assets/image-20231211225134918.png)



## Connectivity Properties of Trees
### Remove Edges from Tree -> Two connected components
> [!lemma]
> If we remove any single edge, we will have the following observation:
> ![](Graph_Theory.assets/image-20231212191344134.png)

> [!proof] Proof Sketch
> ![](Graph_Theory.assets/image-20231212193426471.png)
> This proof utilize the fact that there is unique path between any two nodes in a tree.


> [!proof] Formal Proof(Hard)
> ![](Graph_Theory.assets/image-20231212193641943.png)![](Graph_Theory.assets/image-20231212193648248.png)


### Any subgraphs are tree
> [!thm]
> ![](Graph_Theory.assets/image-20231212194805969.png)

> [!proof] Formal Proof
> ![](Graph_Theory.assets/image-20231212194822026.png)


### |Edges| = |Nodes| - 1
> [!thm]
> ![](Graph_Theory.assets/image-20231212195347713.png)

> [!proof] Proof Sketch
> ![](Graph_Theory.assets/image-20231212195401392.png)

> [!proof] Inductive Proof
> ![](Graph_Theory.assets/image-20231212195412309.png)




### Many Corollaries
```ad-prop
![](Graph_Theory.assets/20231024_0842506585.png)![](Graph_Theory.assets/20231024_0842523835.png)
```

```ad-proof
![](Graph_Theory.assets/20231024_0842557408.png)![](Graph_Theory.assets/20231024_0842562132.png)
```


## Node Properties of Tree
### Leaf Node and Internal Node
> [!def]
> ![](Graph_Theory.assets/image-20231212200100760.png)


### Number of Leaf Nodes
> [!overview]
> ![](Graph_Theory.assets/image-20231212200146268.png)

> [!thm]
> ![](Graph_Theory.assets/image-20231212200158858.png)

> [!proof] Proof Idea
> ![](Graph_Theory.assets/image-20231212200212200.png)![](Graph_Theory.assets/image-20231212200219624.png)

> [!proof] Formal Proof
> ![](Graph_Theory.assets/image-20231212200742874.png)






## Tree Proof Exercises
### Degree One Node
> [!lemma]
> If v is degree 1 in connected graph G, G-v is connected.

```ad-proof
![](Graph_Theory.assets/image-20231029212319098.png)


```

### Binary Tree
> [!def] Definition
> ![](Graph_Theory.assets/image-20231029203531663.png)
> **Definition of the perfect binary trees**:
> ![](Graph_Theory.assets/image-20231029202048662.png)
```ad-thm
![](Graph_Theory.assets/image-20231029213510449.png)


```
> [!proof]
> ![](Graph_Theory.assets/image-20231029213556837.png)




### Tree's Falling Apart
> [!thm]
> ![](Graph_Theory.assets/20231024_0842583912.png)





# Planar Graphs
## Definition
> [!def]
> ![image.png](Graph_Theory.assets/20231024_0843562174.png)![image.png](Graph_Theory.assets/20231024_0843571759.png)


## Faces&Bridges
> [!important]
> When a planar graph is drawn in the plane, one can distinguish, besides its vertices and edges, its faces (more precisely, these are faces of the drawing, not of the graph itself). 
> **The faces are the regions into which the graph subdivides the plane**. 
> 1. One of them is inﬁnite.
> 2. The others are ﬁnite. 
> 
**Brideges are the edges that does not subdivide the plane. **For example, any edges in a tree is a bridge.




## Properties
### Bounding # Edges
> ![image.png](Graph_Theory.assets/20231024_0843592075.png)



### Degree Properties
> ![image.png](Graph_Theory.assets/20231024_0844019615.png)



## Planarity Proof - Euler's Formula
> [!info]
> ![image.png](Graph_Theory.assets/20231024_0844021319.png)![image.png](Graph_Theory.assets/20231024_0844033679.png)
> - Number of faces: f 
> - Number of vertices: v 
> - Number of edges: e

> [!proof]
> **Proof**![image.png](Graph_Theory.assets/20231024_0844056002.png)


## Non Planarity Proof
### Non-planarity for K5
> ![image.png](Graph_Theory.assets/20231024_0844076724.png)
> 其中`Edge-face adjacency`是证明的核心。
> 所以对于`K5`我们只需要检查$e\leq 3v-6$是否成立来判断图是否是`Planar`的。如果成立，则图是`Planar`的。注意这个不等式对不同的图来说也是不同的，需要结合实际图结构进行分析。


### Non-planarity for K3,3
> [!proof] Prove by Contradiction
> ![image.png](Graph_Theory.assets/20231024_0844088643.png)
> 可以看到，如果我们**使用**`K5`**的**`Edge-Face Adjacency`来判断`K3,3`的`Planarity`会出错，原因在于`K5`中的`Cycle length`至少是`3`，而`K3,3`中的`Cycle Length`至少是`4`。所以对于`K3,3`来说，我们的证明应该修改成下面的样子：
> 1. Each face is adjacent to at least four edges, so face-edge adjacencyeach faces is at least$4f$
> 2. Each edge is adjacent to at most two faces, so face-edge adjacenct is at most $2e$
> 
所以对于`K3,3`来说, 如果它是`Planar`的，则$4f\leq 2e$，带入`Euler's Formula`中我们有: $v+\frac{1}{2}e\geq e+2$, 所以$e\leq 2v-4$。所以如果`K3,3`是`Planar`的，就一定满足这个不等式。但是实际情况是$e=9,v=6$, $9>2\times 6-4=8$, 于是`K3,3`不是`Planar`的。
> **使用**`Total Number of Sides`**来证明:**
> Each face is adjacent to at least four edges, so total number of sides of faces in the K5 is $2e=\sum_{i=1}^f s_i\geq \sum_{i=1}^f4=4f$



### Non-planarity for all graphs
> [!Criterion]
> ![image.png](Graph_Theory.assets/20231024_0844117194.png)![image.png](Graph_Theory.assets/20231024_0844125525.png)![image.png](Graph_Theory.assets/20231024_0844144863.png)![image.png](Graph_Theory.assets/20231024_0844151900.png)


### Non-Planarity Example
> [!example] 
> ![](Graph_Theory.assets/image-20231029222415685.png)

> [!proof]
> ![](Graph_Theory.assets/image-20231029222710186.png)






## Duality of Planar Graph
> **Construction of Dual Graphs**
> - Given a planar graph G **without bridges or degree-two nodes**, its dual G* can be constructed by placing a node on each face of G.
> - An edge between two faces of G* is drawn such that it crosses an edge in G.
> - If you construct the dual of G*, it will result in the original graph G. This relationship can be represented as (G*)* = G.
> 
![image.png](Graph_Theory.assets/20231024_0844174207.png)



## Subgraph of Planar Graph
> ![image.png](Graph_Theory.assets/20231024_0844197309.png)

**Proof 1**![image.png](Graph_Theory.assets/20231024_0844192688.png)
**Proof 2**![image.png](Graph_Theory.assets/20231024_0844215164.png)![image.png](Graph_Theory.assets/20231024_0844238976.png)


## Planar Graph Coloring
### Bipartite&Coloring
> ![image.png](Graph_Theory.assets/20231024_0844256692.png)![image.png](Graph_Theory.assets/20231024_0844259821.png)


### Six-Color Theorem
> ![image.png](Graph_Theory.assets/20231024_0844287325.png)


### Five-Color Theorem
> ![image.png](Graph_Theory.assets/20231024_0844296274.png)![image.png](Graph_Theory.assets/20231024_0844316992.png)
> [https://www.youtube.com/watch?v=5mdH0UeBaR0](https://www.youtube.com/watch?v=5mdH0UeBaR0)

**Formal Proof**![image.png](Graph_Theory.assets/20231024_0844346542.png)

![image.png](Graph_Theory.assets/20231024_0844369724.png)


### Four-Color Theorem
> [!info]
> **Proof: **[https://www.youtube.com/watch?v=adZZv4eEPs8](https://www.youtube.com/watch?v=adZZv4eEPs8)
> **Any simple planar graph is four-colorable.**
> The proof is finally done by super computers, considering all the edge cases.




## Applications
### Edge Coloring
> [!example]
> ![image.png](Graph_Theory.assets/20231024_0844367910.png)

> [!success] Solution
> ![image.png](Graph_Theory.assets/20231024_0844398812.png)![image.png](Graph_Theory.assets/20231024_0844407706.png)
注意到$(c)$问中，如果我们选择非叶子节点删除，则可能会导致`Build up Error`, 因为`Resulting Graph`可能不是树。但是选择叶子节点删除就一定是树。



### Classifying Polyhedra
> [!def] Definition
> ![](Graph_Theory.assets/image-20231030085324526.png)![](Graph_Theory.assets/image-20231030085440096.png)![](Graph_Theory.assets/image-20231030090118794.png)![](Graph_Theory.assets/image-20231030090125265.png)





> [!thm] Searching for Regular Polyhedra
> ![](Graph_Theory.assets/image-20231030090033762.png)![](Graph_Theory.assets/image-20231030090042809.png)









# Graph Modeling
## Banquet Arrangement
> [!example] Banquet Arrangement
> ![image.png](Graph_Theory.assets/20231024_0844448382.png)

> [!proof]
> ![image.png](Graph_Theory.assets/20231024_0844468020.png)![image.png](Graph_Theory.assets/20231024_0844487585.png)


## City Roads
> [!example]
> ![](Graph_Theory.assets/image-20231029215551805.png)

> [!proof]
> ![](Graph_Theory.assets/image-20231029215609249.png)






# Related Resources
[MIT6_042JF10_rec06.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1694382246995-5f282bc3-9b6e-4d47-9f93-335d70a6797f.pdf)
[MIT6_042JF10_rec06_sol.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1694382246989-4dae6d87-1199-47e0-9a1e-bd5948729f23.pdf)
[dis02b-Graphs1.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1694382253945-e6ee6787-d38e-4334-9f33-9417956f81db.pdf)
[dis02b-sol.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1694382253945-e3146beb-dfda-453e-9ce6-af377890dd85.pdf)
[dis03a-Graphs2.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1694382253949-6c220d0e-29b1-4608-adf7-81b50948d881.pdf)
[dis03a-sol.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1694382253948-0f7957b9-cb1a-43d6-9122-927478d39f27.pdf)
[hw03-Graphs.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1694382394652-b66e341c-a282-4073-97a5-1bf02795b1f3.pdf)
[hw03-sol.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1694382394950-5f861352-b792-4fc3-bc7c-1e4ca2d1d03d.pdf)

