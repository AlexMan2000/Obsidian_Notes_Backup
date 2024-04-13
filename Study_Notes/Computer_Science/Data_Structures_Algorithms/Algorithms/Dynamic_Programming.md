# DP Formulation
> [!important]
> ![](Dynamic_Programming.assets/image-20240214225052055.png)![](Dynamic_Programming.assets/image-20240214225041101.png)![](Dynamic_Programming.assets/image-20240214225102209.png)


# Fibonacci Number and DP
## Naive Algorithm
> [!concept]
> ![](Dynamic_Programming.assets/image-20240201170309701.png)



## Memoized DP Algorithm
> [!concept]
> ![](Dynamic_Programming.assets/image-20240201170333612.png)![](Dynamic_Programming.assets/image-20240201170342846.png)


## Bottom-up DP Algorithm
> [!concept]
> ![](Dynamic_Programming.assets/image-20240201170555933.png)



# Merge Sort





# Shortest Path
## DAG DP
> [!concept]
> ![](Dynamic_Programming.assets/image-20240201171402110.png)![](Dynamic_Programming.assets/image-20240201171409172.png)
> **Note:** Subproblem dependencies should be acyclic in order for memoization to work, otherwise infinite recursion.
> 
> If the subproblem dependencies are acyclic, then the runtime is # subproblems * time/subproblem.
> 
> With memoization, time/subproblem is $\Theta(1)$
> 
> Here, # subproblems = V choice for k and E choice for v(indegree), so $O(VE)$


## How to Design Recurrence
> [!important]
> ![](Dynamic_Programming.assets/image-20240201231020304.png)![](Dynamic_Programming.assets/image-20240201231025023.png)





## Cyclic => Acyclic
> [!important]
> If the graph contains cycles(non-negative ones), traditional DP won't work, so we need to transform the cyclic graph to acyclic one. The cost is that we are making more subproblems for DP.
> ![](Dynamic_Programming.assets/image-20240201230123149.png)![](Dynamic_Programming.assets/image-20240201230130981.png)![](Dynamic_Programming.assets/image-20240201230137089.png)




# Text Justification
> [!algo]
> ![](Dynamic_Programming.assets/image-20240410215701040.png)![](Dynamic_Programming.assets/image-20240410215728529.png)
> `DP[n]` can be thought of as empty line, which doesn't have badness since we have no words to fit that line.




# Parent Pointers

 

# Subsequences




# Edit Distance





# Perfect-Information Blackjack
> [!algo]
> ![](Dynamic_Programming.assets/image-20240411132735561.png)![](Dynamic_Programming.assets/image-20240411132742466.png)








# Knapsack





# Chain Matrix Multiplication