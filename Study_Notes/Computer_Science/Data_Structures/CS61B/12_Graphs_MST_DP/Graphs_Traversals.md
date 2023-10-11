[cs61b 2019 lec23 graphs1 - intro to graphs.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1677073640724-2c1fd3d5-86ac-4c42-89b8-3bcf36293d79.pdf)
[cs61b 2019 lec 24 graphs2 - dfs, bfs.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1677076231918-67bcb910-7f55-4c0d-b632-71200bc77440.pdf)

# Tree Recap
## Tree Definition
> ![image.png](./Graphs_Traversals.assets/20230415_1816387478.png)![image.png](./Graphs_Traversals.assets/20230415_1816385336.png)



## Tree Examples
> ![image.png](./Graphs_Traversals.assets/20230415_1816389327.png)![image.png](./Graphs_Traversals.assets/20230415_1816394751.png)![image.png](./Graphs_Traversals.assets/20230415_1816396176.png)




# Tree Traversals
## Ordering Overview
> ![image.png](./Graphs_Traversals.assets/20230415_1816397337.png)



## Depth First Traversal
### Pre-Order Traversal
> ![image.png](./Graphs_Traversals.assets/20230415_1816399131.png)![image.png](./Graphs_Traversals.assets/20230415_1816395573.png)



### In-Order Traversal
> ![image.png](./Graphs_Traversals.assets/20230415_1816406738.png)



### Post-Order Traversal
> ![image.png](./Graphs_Traversals.assets/20230415_1816405507.png)![image.png](./Graphs_Traversals.assets/20230415_1816405058.png)



### Visualization
> ![image.png](./Graphs_Traversals.assets/20230415_1816407441.png)


### Runtime Analysis
> [https://www.enjoyalgorithms.com/blog/binary-tree-traversals-preorder-inorder-postorder](https://www.enjoyalgorithms.com/blog/binary-tree-traversals-preorder-inorder-postorder)
> - `T(n)` is the time complexity of the traversal of n size binary tree
> - `k` nodes are present in the left subtree and `n - k - 1` node on the right subtree. Here `0≤ k ≤ n - 1`.
> - We are doing `O(1)` operation with each node.
> 
`T(n)` = Time complexity of traversing left subtree + Time complexity of traversing right subtree + Time complexity of processing root node = `T(k)` + `T(n - k - 1)` + `O(1)` = `T(k) + T(n - k - 1) + c`
> **⭐ Recurrence relation of DFS traversal: T(n) = T(k) + T(n - k - 1) + c**
> - **Case 1: Skewed Binary Tree with **`**k=0**`** so that there is no nodes in the left subtree and **`**n-1**`** nodes in the right subtree. Then **`**T(n)=T(n-1) + c = cn = O(n)**`**.**
> - **Case 2: Balanced Binary Tree with **`**k = (n-1)/2**`**, then **`**T(n)=T2(n/2)+O(1) => T(n)=O(n)**`**.**


# Graphs
## Graph vs Tree Definition
> ![image.png](./Graphs_Traversals.assets/20230415_1816419086.png)![image.png](./Graphs_Traversals.assets/20230415_1816417986.png)
> In general, note that **all trees are also graphs, but not all graphs are trees.**




## Simple Graph
> ![image.png](./Graphs_Traversals.assets/20230415_1816412987.png)




## Graph Types
> Graphs are simple in the following text, and in this course, unless specified otherwise. But there are more categorizations.
> There are** undirected graphs**, where an edge `(u,v)` can mean that the edge goes from the nodes `u` to `v` and from the nodes `v` to `u` too. 
> There are **directed graphs**, where the edge `(u,v)` means that the edge starts at `u`, and goes to `v` (and the vice versa is not true, unless the edge `(v,u)` also exists.) Edges in directed graphs have an arrow.
> There are also **acyclic graphs**. These are graphs that don't have any cycles. And then there are cyclic graphs, i.e., there exists a way to start at a node, follow some **unique** edges, and return back to the same node you started from.
> ![image.png](./Graphs_Traversals.assets/20230415_1816416944.png)
> In the above picture, we can clearly see the difference between how we draw directed and undirected edges.
> Take a look at the cyclic graphs. If you start at a, you can run back around using only distinct edges and get back to a. Thus, the graph is cyclic.
> Take a look at the top-left graph. Is there any node n, such that if you start at n, you can follow some distinct edges, and get back to n? Nope! (Remember than for directed edges, you must follow the directions. You can go from a to b but not b to a.)




## Graph Terminology⭐⭐⭐⭐
> ![image.png](./Graphs_Traversals.assets/20230415_1816412083.png)



## Graph Example
> ![image.png](./Graphs_Traversals.assets/20230415_1816427053.png)![image.png](./Graphs_Traversals.assets/20230415_1816425358.png)




# Graph Problems
## 0 Graph Problems Overview
> ![image.png](./Graphs_Traversals.assets/20230415_1816426995.png)![image.png](./Graphs_Traversals.assets/20230415_1816425839.png)
> What's cool and also weird about graph problems is that it's very hard to _tell_ which problems are very hard, and which ones aren't all that hard.
> For example, consider the Euler Tour and the Hamilton Tour problems. The former... is a solved problem. It was solved as early as 1873. The solution runs in $O(E)$ where $E$ is the number of edges in the graph.
> The latter? If you were to solve it efficiently today, you would win every Math award there was, become one of the most famous computer scientists, win a million dollars, etc. No one has been able to solve this **efficiently**. The best known algorithms run in exponential times. People have been working on it for many decades!
> ![image.png](./Graphs_Traversals.assets/20230415_1816435616.png)




## 1 Connectivity⭐⭐⭐
> ![image.png](./Graphs_Traversals.assets/20230415_1816431589.png)



### Attempt 1: Infinite Loop
> ![image.png](./Graphs_Traversals.assets/20230415_1816436015.png)

**Fix the Bug**![image.png](./Graphs_Traversals.assets/20230415_1816434722.png)
[cs61b s-t connectivity demo.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1677075466979-b7ee8533-b3c5-4687-baf6-02cc77b0f13f.pdf)


### Attempt 2: DFS
> ![image.png](./Graphs_Traversals.assets/20230415_1816433711.png)![image.png](./Graphs_Traversals.assets/20230415_1816434885.png)




## 2 Path Finding(DFS)
> ![image.png](./Graphs_Traversals.assets/20230415_1816446913.png)

[61B depth first paths demo.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1677075881914-dde546fd-fcf8-467a-a708-dfcc7fad8864.pdf)



## 3 Shortest Path Finding(BFS)
> ![image.png](./Graphs_Traversals.assets/20230415_1816444725.png)![image.png](./Graphs_Traversals.assets/20230415_1816443424.png)
> A _**fringe**_ is just a term we use for the data structure we are using to store the nodes on the frontier of our traversal's discovery process (the next nodes it is waiting to look at). For BFS, we use a **queue** for our fringe.
> **The reasons we use the queue are that:**
> 1. **The queue is obeying the rules that we are always looking at things in the order that we traverse nodes and in this BFS example, the element at the frontier of the queue always has the shortest distance from the source.**
> 2. **BFS Invariant: Distance to all items on queue is always k or k + 1 for some k.**
> 3. **BFS will jump between different nodes (those nodes don't necessarily have to be adjacent) while travesing the graph, but for DFS, the next node to visit is always among the neighbors of the current node.**
> 
`edgeTo[...]`is a map that helps us track how we got to node `n`; we got to it by following the edge from `v` to `n`.
> `distTo[...]` is **a map that helps us track how far **`**n**`** is from the starting vertex.** Assuming that each edge is worth a distance of `1`, then the distance to `n` is just one more than the distance to get to `v`. Why? We can use the way we know how to get to `v`, then pay one more to arrive at `n` via the edge that necessarily exists between `v` and `n` (it must exist since in the `for` loop header, `n` is defined as a neighbor of `v`).
> [BFS Demo Link](https://docs.google.com/presentation/d/1JoYCelH4YE6IkSMq_LfTJMzJ00WxDj7rEa49gYmAtc4/edit#slide=id.g76e0dad85_2_380)

[cs61b Breadth First Paths Demo (2019).pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1677114870835-fa2b12c3-43af-4892-ad44-7614c872d537.pdf)
> ![image.png](./Graphs_Traversals.assets/20230415_1816442286.png)![image.png](./Graphs_Traversals.assets/20230415_1816448683.png)



## 4 Cycle Detection
> ![image.png](./Graphs_Traversals.assets/20230415_1816455446.png)


### Undirected Graph
#### Approach 1: DFS
> ![image.png](./Graphs_Traversals.assets/20230415_1816456870.png)



#### Approach 2: WQU
> ![image.png](./Graphs_Traversals.assets/20230415_1816454825.png)



### Directed Graph
#### Approach 3: BFS
> 见`Discussion`的`Shortest Cycle Problem`。




## BFS vs DFS for Path Finding
> ![image.png](./Graphs_Traversals.assets/20230415_1816456510.png)



# Graph APIs
## Graph API Decision
> ![image.png](./Graphs_Traversals.assets/20230415_1816454410.png)![image.png](./Graphs_Traversals.assets/20230415_1816464095.png)




## Princeton Graph API
### Degree API
> ![image.png](./Graphs_Traversals.assets/20230415_1816463059.png)![image.png](./Graphs_Traversals.assets/20230415_1816463801.png)




### Print API
> ![image.png](./Graphs_Traversals.assets/20230415_1816464307.png)
> 注意这里我们允许`1-2`和`2-1`同时出现，意味着我们不需要标记已经访问过的`Nodes`，所以代码比较简单。




# Graph Representations
> ![image.png](./Graphs_Traversals.assets/20230415_1816461741.png)



## Approach 1: Adjacency Matrix
### Representation Rules
> ![image.png](./Graphs_Traversals.assets/20230415_1816461047.png)![image.png](./Graphs_Traversals.assets/20230415_1816479803.png)


### Runtime Analysis
#### Iterate Over Neighbors
> ![image.png](./Graphs_Traversals.assets/20230415_1816471620.png)
> 找到某个节点`v`的所有`neighbors`需要花费$\Theta(V)$时间，是因为在`Adjacency Matrix`的表示法下，尽管`v`的`neighbor`只有一个，但是我们仍然需要遍历所有的`(v,w)=(0,0), (0,1), (0,2), (0,3)`来确认到底哪一个是`1`(即哪一个节点和`v`相连，是`neighbor`)。


#### Print All Nodes
> ![image.png](./Graphs_Traversals.assets/20230415_1816478063.png)



## Approach 2: Edge Sets
> ![image.png](./Graphs_Traversals.assets/20230415_1816474554.png)
> 不是很常用。



## Approach 3: Adjacency List⭐⭐⭐⭐⭐
### Representation Rules
> ![image.png](./Graphs_Traversals.assets/20230415_1816473084.png)



### Runtime Analysis
#### Iterate Over Neighbors
> ![image.png](./Graphs_Traversals.assets/20230415_1816478012.png)
> 当某个节点对应的`Edge List`很短的时候，就是`O(1)`，如果很长到包含了所有节点(`Spindly Tree`), 则需要`O(V)`（不是$\Theta(V)$是因为`Neighbors`的数量不能超过`V`个）。



#### Print All Nodes
> ![image.png](./Graphs_Traversals.assets/20230415_1816474498.png)![image.png](./Graphs_Traversals.assets/20230415_1816484183.png)



## Runtime Summary
> ![image.png](./Graphs_Traversals.assets/20230415_1816488250.png)




# Graph Implementations - Adj List
## Undirected Graph Implementation
> ![image.png](./Graphs_Traversals.assets/20230415_1816487195.png)




## DFS Implementation
### Recursive Implementation
> ![image.png](./Graphs_Traversals.assets/20230415_1816481051.png)![image.png](./Graphs_Traversals.assets/20230415_1816483092.png)

**Client Class**![image.png](./Graphs_Traversals.assets/20230415_1816492933.png)![image.png](./Graphs_Traversals.assets/20230415_1816493093.png)

### Iterative Implementation
> 如果使用递归实现，我们不需要额外的数据结构，但是如果使用`while`, 我们需要使用`stack`数据结构:
> ![image.png](./Graphs_Traversals.assets/20230415_1816496831.png)
> 对某个节点的操作逻辑在`visit vertex`, 比如改变其值等。
> 🔔: 使用迭代法的实现注意点在于:
> 1. 如果我们的`Graph`中有`Cycle`, 那么我们在`DFS`过程中可能在某一步将节点`V`压入栈(`unmarked`, 未访问), 然后在之后遍历的过程中中又遍历到了这个节点(`unmarked`, 未访问), 又一次将其压入栈。所以栈中会有指向同一个节点的实例化对象多次出现。比如`[N1, N2, N3, N1]`
> 2. 如果我们最终访问了`1`中的那个节点`V`(`marked`，标记访问), 此时我们从栈顶将其移除。但是我们的栈中之前还有一个`V`的引用，如果没有`if vertex is not marked`的条件判断，就会导致我们重新将`V`的`Neighbor`压入栈，陷入无限循环。 



### Runtime Analysis
> ![image.png](./Graphs_Traversals.assets/20230415_1816494908.png)




## BFS Implementation
> ![image.png](./Graphs_Traversals.assets/20230415_1816492888.png)
> 一般比`DFS`更早结束执行，最合适用于`Shortest Path Problem`。



## Runtime Analysis
### Using Adj List
> ![image.png](./Graphs_Traversals.assets/20230415_1816507978.png)



### Using Adj Matrix
> ![image.png](./Graphs_Traversals.assets/20230415_1816507822.png)


# Summary
## Tree Traversal
> ![image.png](./Graphs_Traversals.assets/20230415_1816506238.png)




## Graph Traversals
### DFS PreOrder
> ![image.png](./Graphs_Traversals.assets/20230415_1816503893.png)



### DFS PostOrder
> ![image.png](./Graphs_Traversals.assets/20230415_1816508241.png)


### BFS Overview
> ![image.png](./Graphs_Traversals.assets/20230415_1816512165.png)



## Graph Problems
> ![image.png](./Graphs_Traversals.assets/20230415_1816515405.png)



## Graph Implementations
> ![image.png](./Graphs_Traversals.assets/20230415_1816512266.png)![image.png](./Graphs_Traversals.assets/20230415_1816513692.png)


