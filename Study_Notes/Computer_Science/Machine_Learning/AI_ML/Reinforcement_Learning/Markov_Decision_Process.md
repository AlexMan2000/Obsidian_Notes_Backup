# Non-deterministic Search
> [!def]
> ![](Markov_Decision_Process.assets/image-20240214095238433.png)![](Markov_Decision_Process.assets/image-20240214095248803.png)



# MDP Terminology
## MDP States
> [!def]
> ![](Markov_Decision_Process.assets/image-20240215143034306.png)



## Optimal Quantities
> [!def]
> ![](Markov_Decision_Process.assets/image-20240215142949729.png)



# Bellman Equation
> [!thm]
> ![](Markov_Decision_Process.assets/image-20240214173827373.png)![](Markov_Decision_Process.assets/image-20240214173845448.png)




# Value-Based MDP
## Value of States
> [!def]
> ![](Markov_Decision_Process.assets/image-20240214173630886.png)



## Value Iteration Procedure
> [!algo]
> ![](Markov_Decision_Process.assets/image-20240215134429484.png)![](Markov_Decision_Process.assets/image-20240215134439231.png)![](Markov_Decision_Process.assets/image-20240215141034808.png)



> [!example] 
> ![](Markov_Decision_Process.assets/image-20240215134703504.png)
> For this value iteration, we can quickly determine which action the MDP will pick by observation:
> 1. For A, we notice that choosing clockwise action will generate higher utility since there is no negative portion. So the update for A should be $U_{k+1}(A)=R(A,clockwise,B)+\gamma\times U^{clockwise}_{k}(B)$.
> 2. For B, we notice that choosing clockwise action will put more weight on the positive reward, so the update for $B$ should be $\begin{aligned}U_{k+1}(B)=0.5\times \{R(B,clockwise,A)+\gamma\times U^{clockwise}_{k}(A)\}\\ +0.5\times \{R(B,clockwise,C)+\gamma\times U^{clockwise}_{k}(C)\}\end{aligned}$
> 3. For C, we still choose the clockwise for similar reasons,  so the update for $B$ should be $\begin{aligned}U_{k+1}(B)=0.6\times \{R(C,clockwise,A)+\gamma\times U^{clockwise}_{k}(A)\}\\ +0.4\times \{R(C,clockwise,B)+\gamma\times U^{clockwise}_{k}(B)\}\end{aligned}$

> [!code]
> To write the above in code, we can construct a [linear system](../../Control_LA_Circuit/EECS16B/Module2_Robotic_Control/Discretization_System_ID.md#Discrete-Time%20LTI%20Difference%20Equation):
> $\begin{bmatrix}U_{k+1}(A)\\U_{k+1}(B)\\U_{k+1}(C) \end{bmatrix}=\begin{bmatrix}0&0.5&0\\0.2&0&0.3\\0.3&0.2&0 \end{bmatrix}\begin{bmatrix}U_{k}(A)\\U_{k}(B)\\U_{k}(C) \end{bmatrix}+\begin{bmatrix}0\\0.8\\2 \end{bmatrix}$
```python
value_iter_vec = np.array([0,0,0])

def transition_func(A, b):

    def transition(x):
        return A @ x + b
    return transition

markov_A = np.array([[0, 0.5, 0], [0.2, 0, 0.3], [0.3, 0.2, 0]])
markov_b = np.array([0, 0.8, 2])

def update_iteration(value_iter_vec, transition_func):
    new_value_vec = transition_func(value_iter_vec)
    return new_value_vec
    
transition_updater = transition_func(markov_A, markov_b)
new_value = value_iter_vec
for i in range(25):
    print(new_value)
    new_value = update_iteration(new_value, transition_updater)
```
> [!test] Output
> ![](Markov_Decision_Process.assets/image-20240215135551841.png)

> [!example] Compute Q-value
> ![](Markov_Decision_Process.assets/image-20240215135648294.png)




## Convergence Analysis
> [!thm]
> ![](Markov_Decision_Process.assets/image-20240215134500251.png)![](Markov_Decision_Process.assets/image-20240215134516118.png)![](Markov_Decision_Process.assets/image-20240215134606790.png)

> [!quiz] 
> ![](Markov_Decision_Process.assets/image-20240215135727704.png)

> [!example] Vitamin4 P6
> ![](Markov_Decision_Process.assets/image-20240215135802615.png)![](Markov_Decision_Process.assets/image-20240215135813158.png)

> [!code]
> We could also write the above iteration process in code:
```python
value_iter_vec = np.array([0,0,0,0,0,0])
markov_A = np.array([[0, 0.25, 0.25, 0, 0, 0], [0, 0, 0, 0.5, 0, 0], [0, 0.25, 0, 0, 0.25, 0], [0,0,0,0,0,0.5], [0,0,0,0.25,0,0.25],[0,0,0,0,0,0]])
markov_b = np.array([1,1,1,1,1,0])
transition_updater = transition_func(markov_A, markov_b)
new_value = value_iter_vec
for i in range(25):
    print(new_value)
    new_value = update_iteration(new_value, transition_updater)
```
> [!test] Output
> We can see that the value iteration process converges, since we have $0<\gamma<1$.
> 
> Also note that different states converge in different speeds. For example, state E converges in just 2 steps, while state A takes 4 steps since it is farthest from the terminal.
> ![](Markov_Decision_Process.assets/image-20240215135909584.png)



## Problem with Value Iteration
> [!important]
> ![](Markov_Decision_Process.assets/image-20240215140606806.png)
> **Problem 1: It's slow – O(S^2A) per iteration**
> 
> Suppose we have $S$ states, and for each state we have $A$ actions, so for each state $s$, we have to consider $A$ possible actions, and in order to determine which action to choose, for each action we have to compute its Q-value, which involves another $S$ states($s'$) to compute the expectimax, so overall it is $O(S\times A\times S)=O(S^{2}\times A)$.
> 
> **Problem 2: The "max" at each state rarely changes**
> 
> Problem 2 refers to the phenomenon where the action that yields the maximum value for a particular state in a value iteration algorithm doesn't change frequently even though the values themselves might still be updating(very slowly yet not convergent).
> 
> **Problem 3: The policy often converges long before the values**
> 
> In many instances, the optimal policy (the best action to take from each state) converges to the correct policy well before the value function converges to the true values. This is because the relative value of different actions can become clear even when the exact values are not accurately known. Hence, continuing to iterate until the value function fully converges can be unnecessary for determining the optimal policy.

> [!example]
> We see in this example that even if the value iteration still doesn't converge, the optimal policy is already stabablized or converged.
> ![](Markov_Decision_Process.assets/image-20240215142103631.png)![](Markov_Decision_Process.assets/image-20240215142135701.png)



# Policy-Based MDP
## Policy Evaluation
> [!def]
> ![](Markov_Decision_Process.assets/image-20240215142415409.png)
> Since we don't have to consider all the action at each V-state, we omit a factor $A$ and reach $O(S^2)$ as our time complexity.
> 
> Very important properties, since we don't have to do maximizing for each Q-state, we can simplify our iteration as a [linear system](../../Control_LA_Circuit/EECS16B/Module2_Robotic_Control/Discretization_System_ID.md#Discrete-Time%20LTI%20Difference%20Equation), which only involves matrix multiplication and addition.

> [!example]
> We see that different policy yields different value iteration update results.
> ![](Markov_Decision_Process.assets/image-20240215142658593.png)




## Policy Extraction
> [!ovreview]
> ![](Markov_Decision_Process.assets/image-20240215140359940.png)



### Extract from Values(Bad)
> [!def]
> ![](Markov_Decision_Process.assets/image-20240215140423961.png)
> It’s useful to keep in mind for performance reasons that it’s better for policy extraction to have the optimal Q-values of states, in which case a single argmax operation is all that is required to determine the optimal action from a state. 
> 
> Storing only each $U^*(s)$ means that we must recompute all necessary Q-values with the Bellman equation before applying argmax, equivalent to performing a depth-1 expectimax.


### Extract from Q-Value(RL)
> [!def]
> ![](Markov_Decision_Process.assets/image-20240215140539599.png)




## Policy Iteration Algorithms
> [!overview]
> ![](Markov_Decision_Process.assets/image-20240215143331371.png)

> [!algo]
> ![](Markov_Decision_Process.assets/image-20240215142232391.png)![](Markov_Decision_Process.assets/image-20240215142239607.png)![](Markov_Decision_Process.assets/image-20240215142252843.png)

> [!example] Vitamin4 P9
> ![](Markov_Decision_Process.assets/image-20240215145121664.png)![](Markov_Decision_Process.assets/image-20240215145132020.png)![](Markov_Decision_Process.assets/image-20240215145142891.png)![](Markov_Decision_Process.assets/image-20240215145151991.png)




# MDP Properties
## Discount Factor
> [!def]
> ![](Markov_Decision_Process.assets/image-20240215145417891.png)![](Markov_Decision_Process.assets/image-20240215145548148.png)



## Convergence Property
> [!property]
> ![](Markov_Decision_Process.assets/image-20240215145750876.png)



## Expectimax and Value Iteration
> [!property] Expectimax and Value Iteration
> ![](Markov_Decision_Process.assets/image-20240215150154398.png)![](Markov_Decision_Process.assets/image-20240215145932691.png)
> The key realization is that, in order to compute the value of each state with the [Expectimax Algorithm](../Classical_Search_Algorithms/4_Adverserial_Search.md#Expectimax%20Algorithm) in each iteration, even if we have pruning techniques, we still have to traverse through the entire tree(with horizon $H$), looking ahead with $H$ steps.
> 
> But for value iteration, due to its dynamic programming essense, for each iteration we only need to look ahead by one step, which saves lots of time.
> ![](4_Adverserial_Search.assets/image-20240209150421471.png)



# Integrated Examples
## Policy Iteration
> [!important]
> ![](Markov_Decision_Process.assets/image-20240215151033415.png)![](Markov_Decision_Process.assets/image-20240215151045123.png)


