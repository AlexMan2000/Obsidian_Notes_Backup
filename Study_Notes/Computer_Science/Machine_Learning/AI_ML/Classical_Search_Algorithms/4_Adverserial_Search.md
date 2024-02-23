> Chapter 5 Edition 3


# Reflex Agent







# Minimax Algorithm
## Algorithm
> [!algo]
> ![](4_Adverserial_Search.assets/image-20240209113536268.png)
> **Note:** It's just like DFS Postorder traversal. Bottom up.


## Time Complexity
> [!important]
> ![](4_Adverserial_Search.assets/image-20240209155323260.png)




# Expectimax Algorithm
## Algorithm
> [!algo]
> ![](4_Adverserial_Search.assets/image-20240209150421471.png)![](4_Adverserial_Search.assets/image-20240209100729876.png)

> [!example]
> ![](4_Adverserial_Search.assets/image-20240209114854898.png)


## Examples
> [!example] Fa23 Exam Prep 04 P1
> ![](4_Adverserial_Search.assets/image-20240213133704266.png)![](4_Adverserial_Search.assets/image-20240213133711031.png)![](4_Adverserial_Search.assets/image-20240213133747197.png)![](4_Adverserial_Search.assets/image-20240213133751400.png)![](4_Adverserial_Search.assets/image-20240213135844684.png)![](4_Adverserial_Search.assets/image-20240213135849954.png)
















# Minimax vs Expectimax
> [!example] Vitamin3 Q3.4
> ![](4_Adverserial_Search.assets/image-20240209112347236.png)




# MedianMiniMax Algorithm
> [!example] Fa23 Exam Prep 4 P2
> ![](4_Adverserial_Search.assets/image-20240213141116859.png)![](4_Adverserial_Search.assets/image-20240213141121908.png)![](4_Adverserial_Search.assets/image-20240213141128868.png)![](4_Adverserial_Search.assets/image-20240213141601503.png)![](4_Adverserial_Search.assets/image-20240213142030255.png)![](4_Adverserial_Search.assets/image-20240213142036220.png)

 













# Suboptimal Strategies
> [!important]
> Sometimes your adverserial player may not act optimally, in the minimax context, suboptimal response will cause the min_node to return not the smallest value it can see, but may return a much bigger one, which would cause the max_node on the path to root to obtain higher than actual value. 
> 
> If your adverserial player may not act optimally and playing randomly. Then if the MAX player follows 


## Suboptimal Min Player

> [!example] Vitamin3 Q 7.1
> ![](4_Adverserial_Search.assets/image-20240209145216343.png)![](4_Adverserial_Search.assets/image-20240209145221446.png)


## Random MIN Player
> [!example] Vitamin3 Q7.2
> ![](4_Adverserial_Search.assets/image-20240209150450244.png)






# Resource Limit Pruning
## Alpha-Beta Pruning
### Algorithm
> [!algo]
> ![](4_Adverserial_Search.assets/image-20240209113616091.png)![](4_Adverserial_Search.assets/image-20240209155355731.png)

> [!example] Minimax Pruning
> ![](4_Adverserial_Search.assets/image-20240213132250798.png)
> In minimax setting, the middle child of the middle node can be pruned.


> [!example] Expectimax Pruning
> ![](4_Adverserial_Search.assets/image-20240213132346049.png)![](4_Adverserial_Search.assets/image-20240213132351193.png)![](4_Adverserial_Search.assets/image-20240213132358421.png)







### Possible Pruning Schema
> [!property]
> Perhaps the simplest check is as follows: pruning of children of a minimizer node m is possible (for some assignment to the terminal nodes), when both of the following conditions are met: 
> - (i) The value of another child of m has already been determined.
> - (ii) Somewhere on the path from m to the root node, there is a maximizer node M for which an alternative option has already been explored. 
> 
> The pruning will then happen if any such alternative option for the maximizer had a higher value than the value of the "another child" of m for which the value was already determined.

> [!example] Vitamin3 Q6.1
> ![](4_Adverserial_Search.assets/image-20240209120040241.png)
>
> Here in (c) The left-most child of the root would have $α=−∞$, so its direct children can never be pruned because they will always be greater than $−∞$−∞. Intuitively the root hasn't seen anything else yet, so any value returned by the minimizer might end up being taken by its parent.

> [!example] Vitamin3 Q6.2
> ![](4_Adverserial_Search.assets/image-20240209120517849.png)
> Simple observation for (d),(e), when we run the algorithm, by its DFS property we will never assign a new value to $\alpha$ along the path until we have finished at least a complete post order traversal, so we can never rule out the node on the left most children.
> 
> For (f), if we focus on the middle node of depth 1, we will see that the value of $\beta$ for this node is $+\infty$ and hasn't been updated, so we cannot just prune the child.




## Depth-Limited Search
> [!overview]
> Though alpha-beta pruning can help increase the depth for which we can feasibly run minimax, this still usually isn’t even close to good enough to get to the bottom of search trees for a large majority of games. As a result, we turn to evaluation functions, functions that take in a state and output an estimate of the true minimax value of that node.
> 
> Depth-limited search is not guaranteed to find the optimal solution to the original problem.
> 
> The depth-limit search is guided by evaluation function, which is a linear combination of the feature of the current state.
> 
> Different choices of evaluation function may generate different search depth for the same problem.


### Evaluation Function
> [!def]
> For depth-limited search, the evaluation function is a linear combination of features that could be manually extracted from each search state.
> ![](4_Adverserial_Search.assets/image-20240209155434437.png)


> [!example] Vitamin3 Q8
> ![](4_Adverserial_Search.assets/image-20240209153203832.png)![](4_Adverserial_Search.assets/image-20240209153322104.png)![](4_Adverserial_Search.assets/image-20240209153329211.png)![](4_Adverserial_Search.assets/image-20240209153339460.png)



## Monte Carlo Tree Search
> [!overview]
> ![](4_Adverserial_Search.assets/image-20240209153605757.png)

### Evaluation Function
> [!def]
> MCTS is a method to use randomization to estimate the evaluation of a search state, generally for the child node(suppose there are $T$ child nodes)of an arbitrary node $m$, we follows:
> 1. Choose a total number of rollout $R=\sum\limits_{n=1}^TN(n)$ where $N(n)$ is the number of rollouts(random experiments that are allocated to the child node $n$).
> 2. Allocate $N(n)$ to each child node across node $1$ to node $T$, more promising child node gets more rollouts
> 3. Starting from these child node, simulate the game results and accumulate the total number of wins in the terminal states, denote it by $U(n)$ for child node $n$.
> 4. **Upper Confidence Bounds:** Calculate the fraction $$\frac{U(n)}{N(n)}+C\times\sqrt{\frac{logN(Parent(n))}{N(n)}}$$ to be the evaluation of the child node $n$, where the first term is how promising this child node will lead $player(Parent(n))$ to win at the end, and the secdon term is how certain we are about this estimation and user can freely adjust $C$. Typically higher value in this expression means that we are more likely to explore this child node as next action.


### MCTS Algorithm
> [!algo]
> ![](4_Adverserial_Search.assets/image-20240209155043709.png)

> [!example]
> ![](4_Adverserial_Search.assets/image-20240209154747307.png)![](4_Adverserial_Search.assets/image-20240209154940981.png)![](4_Adverserial_Search.assets/image-20240209154945767.png)![](4_Adverserial_Search.assets/image-20240209155013606.png)![](4_Adverserial_Search.assets/image-20240209155113464.png)



### Summary
> [!summary]
> ![](4_Adverserial_Search.assets/image-20240209155212044.png)![](4_Adverserial_Search.assets/image-20240209155155958.png)





# Multi-Agent Utility
> [!def]
> ![](4_Adverserial_Search.assets/image-20240209113330268.png)


## Non-Zero Sum Games
> [!example] Vitamin3 Q5.2
> ![](4_Adverserial_Search.assets/image-20240209115152351.png)![](4_Adverserial_Search.assets/image-20240209115203552.png)

> [!example] Fa23 Disc04 P2
> ![](4_Adverserial_Search.assets/image-20240213132518523.png)![](4_Adverserial_Search.assets/image-20240213132522188.png)





# Utilities&Preferences
## Utility Definition
> [!def]
> ![](4_Adverserial_Search.assets/image-20240209155708514.png)


## Utility Scale
> [!def]
> ![](4_Adverserial_Search.assets/image-20240209160451949.png)




## MEU Principles
> [!def]
> ![](4_Adverserial_Search.assets/image-20240209155909706.png)

> [!example] Vitamin3 Q9.1
> ![](4_Adverserial_Search.assets/image-20240209155925461.png)

> [!example] Vitamin3 Q9.2
> ![](4_Adverserial_Search.assets/image-20240209160008011.png)




## (Rational) Preferences
> [!def]
> ![](4_Adverserial_Search.assets/image-20240209155732422.png)![](4_Adverserial_Search.assets/image-20240209155751933.png)![](4_Adverserial_Search.assets/image-20240209155802551.png)

> [!example] Vitamin3 Q9.3
> ![](4_Adverserial_Search.assets/image-20240209160236976.png)

> [!example] Vitamin3 Q11
> ![](4_Adverserial_Search.assets/image-20240209160640203.png)![](4_Adverserial_Search.assets/image-20240209160644635.png)![](4_Adverserial_Search.assets/image-20240209160659418.png)![](4_Adverserial_Search.assets/image-20240209160709931.png)![](4_Adverserial_Search.assets/image-20240209160840880.png)![](4_Adverserial_Search.assets/image-20240209160912956.png)![](4_Adverserial_Search.assets/image-20240209161137240.png)![](4_Adverserial_Search.assets/image-20240209161153776.png)







## Human Utilities
### Definition
> [!def]
> ![](4_Adverserial_Search.assets/image-20240209160432453.png)



### Risk Aversion
> [!def]
> ![](4_Adverserial_Search.assets/image-20240209160406043.png)

> [!example] Vitamin3 Q10
> ![](4_Adverserial_Search.assets/image-20240209160520032.png)

