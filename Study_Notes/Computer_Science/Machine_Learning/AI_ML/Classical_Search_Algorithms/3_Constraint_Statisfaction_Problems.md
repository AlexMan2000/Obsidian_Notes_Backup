> Chapter 6 Edition 3
# Constraint Satisfaction Problems
## Search and CSPs
> [!def] Motivation
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128124908032.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240128124933842.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240128124939779.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240128153458346.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240128153759963.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240128154048826.png)

> [!example] Map Coloring
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128153545630.png)

> [!example] N-Queens
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128153604074.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240128153612818.png)



## Constraint Graphs
> [!def]
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128153629838.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240128153735933.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240128153644953.png)

> [!example] Cryptarithmetic
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128153710136.png)

> [!example] Sudoku
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128153720670.png)


## Solving CSP - Backtracking
> [!algo]
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128154240425.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240128135445088.png)



# Speed up Backtracking
## Method 1: Filtering - Filter out Values
### Forward Checking
> [!def]
> Propagation ahead to see whether the current assignment is good.
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128143109091.png)

> [!bug] Limitation
> Forward checking only detects failure right in front of you. In other words, forward-checking ensures minimum-level filtering.



### Arc Consistency
> [!def]
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128141633915.png)
> **Note:** Tail is the non-arrow end while head is the arrow end.


#### AC-3 Algorithm
> [!algo]
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128142515222.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240128142638391.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240205134614074.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240213153116109.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240213153126124.png)
> The logic is that, once we find an arc that is inconsistent, we delete the value that causes inconsistency from the tail of that arc(call it node $x$) and treat that tail as new head and update all the arcs that treat node $x$ as head to remain arc consistency over the entire CSP. 
> 
> Suppose we have $A,B,C,D,E$, we should enforce arc consistency by choosing a starting node. Let's say we choose $A$, then we check the arc consistency by $A\to B,A\to C, A\to D, A\to E,B\to A, B\to C,\cdots$, along the way if there is any tail of the arc that has domain shrinked, for example during $A\to C$, we shrink $A$'s domain, tehn we should append all the arcs that **previously** treated $A$ as the head, any arcs that are already in the queue will not be re-appended.
> 
> **The termination condition** is when the queue is empty or we detect some inconsistency due to zero value domain in the tail of the arc.
> 
> **Note** that we only enforce arc consistency on those tails that have not been assigned any value yet.


> [!example] Map Coloring - Arc Consistency
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128141904681.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240128141911562.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240128141931386.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240128141939407.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240128141944842.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240128141950464.png)


#### Limitations
> [!important]
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128142707699.png)
> The top right corner graph contains multiple solutions after running `AC-3`. Since here each arc is consistent, which satisfies arc consistency, but overall the problem has multiple solutions even if we have enforced arc consistency.
> 
> The bottom right corner graph contains no solution after running `AC-3`. Since here each arc is consistent, which satisfies arc consistency, but overall the problem has no solution even if we have enforced arc consistency.
> 
> In other words, arc consistency only looks at pair of nodes myopically instead of looking at triple nodes or more.
> 
> The above problems are the reason why `AC-3` still need backtracking as a guarantee to find solution. 



### Modified AC-3 Algorithm
> [!algo]
>
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240213153539598.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240213153628321.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240213153633368.png)








### K-Consistency
> [!important]
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128153045922.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240128153050865.png)



## Method 2: Ordering Heuristics
> This method decides which variable to choose and what value to assign to that variable.
### Minimum Remaining Values(MRV)
> [!def]
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128140244206.png)
> When deciding **which variable** to assign value next, we can choose the next unassigned variable **in order.** The order is determined by our handpicked algorithm. MRV is one of them.
> 
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128140549170.png)
> **Why min rather max?**
> We want to fail fast. Once assignment causes problem, MRV will detect it fast and backtrack and use a different value to assign.
> 
> **Note:** This speed up is related to the choice of next unassigned variable.

 
### Least Constraining Value(LCV)
> [!def]
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128135853909.png)
> **Why MRV and LCV?**
> 
> Because it is a CSP. It is an identification problem where you have to assign value to every variable. So we want every variable to be assigned. In other words, we want to try more values that are part of the potential solution instead of failing fast.
> 
> **Note:** This speed up happens after we have chosen the variable and want to **choose the value** to be assigned to it.




## Method 3: Structure
> [!motiv] Motivation
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128154602121.png)
> Our original problem in the worst case requires traversing through each possible assignment of variables, which gives worst-case runtime of $O(d^n)$ where $d$ is the size of the domain and $n$ is the number of variables in our problem specification.
> 
> But we can split the problem into** independent subproblems**(if viable), then the runtime could be greatly optimized.
> 
> But in real life, independent subproblems are very rare since the whole point of CSP is to solve problems with variables that interact(i.e. not independent).



### Tree-Structured CSP
> [!algo]
> If we’re trying to solve a tree-structured CSP (**one that has no loops in its constraint graph**), we can reduce the runtime for finding a solution from $O(d^N)$ all the way to $O(n\cdot d^2$ ), linear in the number of variables. This can be done with the tree-structured CSP algorithm, outlined below:
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128155026131.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240128155033958.png)
> **Notes:**
> 
> 1. **How do we know during the backward pass, for each node in the DAG, there is no other arcs that are pointing to that node?** 
> 
> 	Tree property! For each node in a tree, it can only have one parent.
> 2. **Why is the runtime $O(nd^2)$?**
> 	$n$ means we iterate through node $1$ to node $n$, $d^2$ means we are checking the pair of values in the domain of tail and head of an arc. More importantly, every time you see $d^2$ as a factor in the runtime, very likely we are checking the consistency of an arc.
> 	
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240213153925736.png)


> [!proof] Proof Sketch
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128160742049.png)
>

> [!bug] Limitations
> 
> **Why doesn't this algorithm work with cycles in the constraint graph?**
> 
> Suppose we have an edge from C to F ad shown below:
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128161829110.png)
> Suppose after the backward pass step, we have 
> C:[green]
> D: [blue] 
> F:[green, blue] where arc CF and DF are both consistent. 
> 
> Then during the forward assignment, C got green and F have to be blue. but then we move onto D, and assign blue, F have no choice to pick. 
> 
> To sum up, for tree we only need 2-consistency(arc-consistency) but for graph we need higher-order consistency.



### Make it Tree-Structured
#### Cutset Conditioning
> [!algo]
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128162428183.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240128162451670.png)
> **Derivations on runtime:**
> 
> The initial assignment to a cutset of size c may leave the resulting tree-structured CSP(s) with no valid solution after pruning, so we may still need to backrack up to $d^c$ times. 
> 
> Since removal of the cutset leaves us with a tree-structured CSP with $(n − c)$ variables, we know this can be solved (or determined that no solution exists) in $O((n − c)\cdot d^2 )$. 
> 
> Hence, the runtime of cutset conditioning on a general CSP is $O(d^c\cdot (n−c)\cdot d^2)$, very good for small c. 


#### Tree Decomposition(Optional)
> [!algo]
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240128165756398.png)
> Generally we can solve the subproblems separately. But since subproblems are not guaranteed to be independent, the solution from the subproblems have to satisfy some constraints in order to be considered valid for the original CSP problem.


# CSP Properties
## Backtracking cannot be eliminated
> [!property] BT is the bottomline
> Even if we apply speeding up techniques like filtering and ordering, we still need backtracking to find the optimal solution. These techniques alone won't secure us even a solution. Consider the following example:
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240205125128281.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240205125139304.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240205141851853.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240205141903541.png)
> The lesson is that arc consistency may work well when we have binary constraints. In this case, we may eliminate lots of unnecessary expansion paths and narrow down the backtracking search procedure but we cannot throw backtracking away.
> 
> The same argument holds with forward checking, which eliminates even fewer unnecessary paths.
> 


## Forward Checking and Arc Consistency Diverges
> [!property] Forward Checking and Arc Consistency may diverge on solutions
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240205140027565.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240205140036175.png)


## Arc Consistency and CSP Solutions
> [!property]
> We are given **a CSP with only binary constraints**. Assume we run backtracking search with arc consistency as follows. 
> 
> Initially, when presented with the CSP, one round of arc consistency is enforced. This first round of arc consistency will typically result in variables having pruned domains. 
> 
> Then we start a backtracking search using the pruned domains. In this backtracking search we use filtering through enforcing arc consistency after every assignment in the search.
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240205142614763.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240205142625075.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240205142635137.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240205142645034.png)



# Local Search - Alternative to BT
> [!overview]
> Local Search works when the CSP is complete, and not necessarily optimal.
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240205093020310.png)



## Min-Conflicts Algorithm
> [!def]
> Local search works by iterative improvement.
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240213155819427.png)
> Also called min-conflicts algorithm, it attempts to solve CSPs iteratively. It starts by assigning some value to each of the variables, ignoring the constraints when doing so. Then, while at least one constraint is violated, it repeats the following: 
> - (1) Randomly choose a variable that is currenly violating a constraint.
> - (2) Assign to it the value in its domain such that after the assignment the total number of constraints violated is minimized (among all possible selections of values in its domain).
> 
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240205093222558.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240205090954007.png)
> 
> In this 4-queen example, I start with a state where all 5 constraints are violated, then the iterative improvement will start with this state, pick one of these violating constraints, adjust it to make it satisfy. In fact, local search appears to run in almost constant time and have a high probability of success not only for N-queens with arbitrarily large N, but also for any randomly generated CSP.
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240205091521938.png)
> From the graph we can see most of the CSP problems are easy(two-tailed):
> 
> - When the number of constraints is high and the number of variables is low(right tail), this technique can greatly boost CSP's performance. Since the number of variables of low, the solution space cannot be big.
> 
> - When the number of constraints is low and the number of variables is high(left tail), this technique can also greatly boost CSP's performance. Like the sodoku problem where we have few rules, we can do whatever we want to not violate the constraints.
> 
> - But in reality, the CSP that we solve tend to have lots of variables and lots of constraints(middle spike), which may require us to find alternatives to backtracking algorithm for performance improvement.
> 
> However, despite these advantages, local search is both** incomplete** and **suboptimal** and so won’t necessarily converge to an optimal solution.



## Hill-Climbing Search
> [!overview]
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240205093046665.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240205093108214.png)
> The hill-climbing search algorithm (or **steepest-ascent**) moves from the current state towards a neighboring state that increases the objective value. 
> 
> The algorithm does not maintain a search tree but only the states and the corresponding values of the objective. The “greediness" of hill-climbing makes it vulnerable to being trapped in local maxima as locally those points appear as global maxima to the algorithm, and plateaux.

> [!algo]
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240205093657439.png)
> Variants of hill-climbing:
> - **Stochastic hill-climbing** which selects an action randomly among the uphill moves, have been proposed and has been shown in practice to converge to higher maxima at the cost of more iterations.
> - **RandomRestart hill-climbing** which conducts a number of hill-climbing searches each time from a randomly chosen initial state, is trivially complete as at some point the randomly chosen initial state will coincide with the global maximum.

> [!example] 8-queen problem
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240205094649014.png)




## Simulated Annealing
> [!algo]
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240205093901608.png)
> Simulated annealing aims to **combine random walk (randomly moves to nearby states) and hill-climbing** to obtain a complete and efficient search algorithm. In simulated annealing we allow moves to states that can decrease the objective. 
> 
> More specifically, the algorithm **at each state chooses a random move**. 
> - If the move leads to higher objective it is always accepted. 
> - If on the other hand it leads to smaller objectives then the move is accepted with some probability. This probability is determined by the **temperature parameter**, which initially is high (more “bad" moves allowed) and gets decreased according to some schedule. When the temperature is high, you are doing random selection, when temperature is low you are doing hill climbing.
> - If temperature is decreased slowly enough then the simulated annealing algorithm will reach the global maximum with probability approaching 1.
> 
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240205094727069.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240205094838952.png)







## Local Beam Search
> [!def]
> Keeping just one node in memory might seem to be an extreme reaction to the problem of memory limitations. The local beam search algorithm keeps track of **k** states rather than 1. 
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240205094848907.png)
>  It begins with k randomly generated states. At each step, all the successors of all k states are generated. If any one is a goal, the algorithm halts. Otherwise, it selects the k best successors from the complete list and repeats.
>  
>  At first sight, a local beam search with k states might seem to be nothing more than running k random restarts in parallel instead of in sequence. In fact, the two algorithms are quite different. 
>  - In a random-restart search, each search process runs **independently** of the others. 
>  - In a local beam search, useful information is passed among the parallel search threads. In effect, the states that generate the best successors say to the others, the algorithm quickly abandons unfruitful searches and moves its resources to where the most progress is being made.
>  
>  ![](3_Constraint_Statisfaction_Problems.assets/image-20240205095114604.png)
>  In its simplest form, local beam search can **suffer from a lack of diversity** among the k states—they can quickly become concentrated in a small region of the state space, making the search little more than an expensive version of hill climbing. 
>  
>  A variant called **stochastic beam search**, analogous to stochastic hill climbing, helps alleviate this problem. Instead of choosing the best k from the the pool of candidate successors, stochastic beam search chooses k successors at random, with the probability of choosing a given successor being an increasing function of its value. Stochastic beam search bears some resemblance to the process of natural selection, whereby the “successors” (offspring) of a “state” (organism) populate the next generation according to its “value” (fitness).

> [!example]
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240205095150057.png)



## Genetic Algorithms
> [!overview]
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240205100206017.png)
> **Initital Step:** The algorithm begins with k randomly generated states. Eac state is called individual and they together form a population.
> 
> **Ranking Initial States:** The initial states should be ranked according to **fitness function**(for 8-queen problem it is the number of nonattacking pairs of queens).
> 
> **Choosing Next Generation:** We normalize the fitness score to obtain a probability for each individual, which is the probability of being choosed. For example, the probability of the first individual 24748552's probability of being chosen is $\frac{24}{24+23+20+11}\approx 31\%$。
> 
> **Pair the individuals:** After choosing the individual according to the probability, we may have some individual being discarded and some individuals being chosen multiple times. Then we pair up individuals at random.
> 
> **Merge the pair:** After pairing up, we **randomly choose a crossover point for each pair** and merge them according to the crossover point. The choice of crossover point could be made non-random and generally we want to choose in a way such that the result get the better half.
> 
> **Mutation:** Finally, each offspring is susceptible to some random mutation with independent probability.
> 

> [!algo]
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240205102050008.png)
> Genetic algorithms try to move uphill while exploring the state space and exchanging information between threads. Their main advantage is the use of crossovers since this allows for large blocks of letters, that have evolved and lead to high valuations, to be combined with other such blocks and produce a solution with high total score.




## Local Search in Continuous Space
> [!def]
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240205102257709.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240205102302134.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240205102309108.png)



# Design Examples
## Trapped Pacman: CSP
> [!example] Fa23 Disc03 P1
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240205144017938.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240205144031271.png)
> Remember when we are doing CSP procedure, we will always first enforce **unary constraints**, then the constraints that immediately relate to the current assignment(if we use forward checking).
> 1. Enforce unary constraints: $X_2,X_3,X_4$ cannot take $P$ now.
> 2. Enforce related constraints w.r.t current assignment(**forward checking**): $X_2$ and $X_6$ must be $P$ now. So $X_2$ cannot be $G$ or $E$, thus $X_2$ has empty domain.
> 3. We don't need any further checking since this is forward checking.
>
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240205145621289.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240205145714797.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240205145956694.png)

## Course Scheduling
> [!example] Fa23 Disc03 P1
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240205151227398.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240205151237404.png)
> For problem 1, unary constraints shrink the domain while the binary constraints enforce that a professor cannot split into two class at the same time.




## Air Traffic Control
> [!example] Fa23 Exam Prep 4 P1
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240213150427599.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240213150431958.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240213151624437.png)
> **Note** that we pick $A$ as our starting point, so we start to check the consistency of the arc by $A\to B, A\to C, B\to A, B\to C,C\to A$, $C\to B, C\to D,D\to C, D\to E, E\to D$, along the way if any nodes' domain is shrinked, we append the arc into the queue if it's not already there.
> 
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240213152416164.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240213152901698.png)



## Digit CSP 
> [!example] Fa23 Exam Prep 4 P2
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240213155907745.png)![](3_Constraint_Statisfaction_Problems.assets/image-20240213155913090.png)


## Complexity Analysis
> [!example] Fa23 Exam Prep 4 P2
> ![](3_Constraint_Statisfaction_Problems.assets/image-20240213160259047.png)











# Demo Website
> [!example]
> https://inst.eecs.berkeley.edu/~cs188/fa21/assets/demos/csp/csp_demos.html


