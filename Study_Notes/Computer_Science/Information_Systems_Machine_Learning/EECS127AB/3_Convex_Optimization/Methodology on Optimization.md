# Unconstrained Optimization Problem
> [!important]
> We first address the unconstrained optimization problem:
> $$\min_{\vec{x}\in \mathbb{R}^n}f_0(\vec{x})$$
> For such problem, we first need to set its gradient to zero, and compute the Hessian at this point.
> - If the hessian turns out not to be PSD/NSD, then the point is not a local minimum, it is called the saddle point.
> - Otherwise, it is a local minimum/maximum.
> 
> Then we compute the objective at these local optima and see which one delivers the minimum objective and that will be our global minimum and thus a solution to our optimization problem.





# Constrained Optimization Problem
## General Framework
> [!important] 
> For a problem like this:
> $$\begin{align}min_{\vec{x}\in\mathbb{R}^n}&f_0(\vec{x})\\&g_i(\vec{x})\leq 0,\forall i=1,2,\cdots, m\\& h_i(\vec{x})=0,\forall i=1,2,\cdots, p\end{align}$$
> where we don't have any assumptions on the convexity of our constraints. In other words, $g_{i}(\vec{x})\forall i$ don't have to be all convex and $h_i(\vec{x})$ don't have to be all affine.
> 
> We will denote our feasible region to be $$\Omega=\{\vec{x}\in \mathbb{R}^n|\begin{aligned}&g_i(\vec{x})\leq 0,\forall i=1,2,\cdots, m\\& h_i(\vec{x})=0,\forall i=1,2,\cdots, p\end{aligned}\}$$
> 
> In this case, we just need to check all the critical points:
> 
> The first step is to check the feasibility of gradient zero points that satisfy $\nabla f_0(\vec{x})=0$. If it is not in the feasible region, then we drop it from the candidates for optimal solutions.
> 
> The second step is to check the objective value on the boundary points, which are: $$\mathcal{B}=\{\vec{x}\in \mathbb{R}^n|\begin{aligned}&g_i(\vec{x})= 0,\forall i=1,2,\cdots, m\\& h_i(\vec{x})=0,\forall i=1,2,\cdots, p\end{aligned}\}$$ 
> 
> Finally, we will compare the candidates that we find from the zero gradient point and the boundary points and see which ones deliver the minimum objective value.


## LICQ Framework
> [!def]
> Sometimes our feasible regions are complicated and it will be difficult to use the general framework, then we will opt to the following optimality condition:
> ![](Methodology%20on%20Optimization.assets/image-20231215150812149.png)![](Methodology%20on%20Optimization.assets/image-20231215140957427.png)
> The above theorem can be rewritten into formal KKT representation:
> 
> ![](Methodology%20on%20Optimization.assets/image-20231215143351490.png)
> 
> $LICQ$ eliminates the possibility that some gradient vectors can be expressed in terms of other gradient vectors. It turns out that $LICQ$ is non-trivial since it guarantees necessity of KKT for optimality. Note that we only requires those active constraints to be linearly independent for reasons seen later on.
> 
> This theorem says that if $\vec{x}$ is one of the optimal solutions and satisfy $LICQ$(regularity condition) to the constrained optimization problem, then it has to satisfy this optimality condition but not the other way around. In other words, if $\vec{x}$ is a solution and satisfies $LICQ$(regular condition), then KKT condition is necessary condition for optimality.
> 
> Note that for any optimization problem, First Order Optimality Condition(KKT Conditions actually) is ==neither a necessary condition nor a sufficient condition for optimality==, which means if we solve for it we still cannot have any idea of whether they are optimal.
> 
> Also note that we can construct KKT conditions for all optimization problems(convex or not, strong duality or not). It is just that the solution to KKT conditions will have different interpretations depending on the formulation of our optimization problem.
> 
> So under this framework, the best thing we can do is to check if $LICQ$ holds for $\vec{x}$ that we solve from the KKT conditions, if it holds, then necessity is met, then we still have to check whether these points are local minima/maxima and compare their objective values to get the global solutions since KKT is only necessary for optimality, which means the solutions that we get may contain other points that are not optimal points.

> [!proof] Proof for optimality condition $m=1,p=0$ case
> Suppose we have an optimal solution for the optimization problem, denote it by $\vec{x}^*$, we want to show that it satisfy $\nabla  f(\vec{x}^*)+\lambda\nabla g(\vec{x}^*)=0$
> Suppose for the sake of contradiction this doesn't hold, then geometrically we know that $\nabla f(\vec{x}^*)$ is not on the same line as $\nabla  g(\vec{x}^*)$, as shown in the graph below:
> ![](Methodology%20on%20Optimization.assets/image-20231215142053897.png)
> Then we can always find a direction $\vec{\delta_x}$, that has an obtuse angle with both $\nabla f(\vec{x}^*)$ and $\nabla g(\vec{x}^*)$ such that if we move towards this direction we will have $\nabla g(\vec{x}^*)^{\top}\vec{\delta_x}<0$ and $\nabla f(\vec{x}^*)^{\top}\vec{\delta_x}<0$. 
> 
> This delivers $g(\vec{x}^*+\vec{\delta_{x}})\approx g(\vec{x}^*)+\nabla g(\vec{x}^*)\vec{\delta_x}<g(\vec{x}^*)\leq0$ and $f(\vec{x}^*+\vec{\delta_x})\approx f(\vec{x}^*)+\nabla f(\vec{x}^*)\vec{\delta_x}<f(\vec{x}^*)$.
> 
> This means that we can always find $\vec{x}^*+\vec{\delta_x}\neq\vec{x}^*$ such that $\vec{x}^*+\vec{\delta_x}$ is feasible and $\vec{x}^*+\vec{\delta_x}$ is optimal, which is a contradiction.
> 
> The intuition behind the proof is that we want to find some points in the interior of our feasible region(not on the boundary) such that the objective value is smaller.

> [!proof] Proof for Optimality Condition - General Case
> First, notice that an equality constraint can always be rewritten into two inequality constraints, thus without generality we can just prove the case when $p=0$, which is deferred to next section.
> 


## Formal Proof of KKT Conditions
> [!overview]
> 
### Feasible Descent Directions
> [!important]
> ![](Methodology%20on%20Optimization.assets/image-20231215144151773.png)
> From the definition above one can quickly derive that if $\vec{d}$ is a feasible direction at $\vec{x}\in C$ then $\exists\epsilon>0,f(\vec{x}+td)<f(\vec{x}),\forall t\in [0,\epsilon]$

### The Basic Necessary Condition - No Feasible Descent Directions
> [!important]
> ![](Methodology%20on%20Optimization.assets/image-20231215144306394.png)![](Methodology%20on%20Optimization.assets/image-20231215144403731.png)![](Methodology%20on%20Optimization.assets/image-20231215145501693.png)
> Point-wise continuity here is enough, since we just want the non-oscillation at this particular point.


### The Fritz-John Necessary Condition
> [!thm]
> ![](Methodology%20on%20Optimization.assets/image-20231215150253463.png)![](Methodology%20on%20Optimization.assets/image-20231215150318711.png)
> We will not spend too much time on this theorem and we will utilize the result and build KKT on top of it with some regularity conditions.


### KKT for Inequality Constrained Problems
> [!thm]
> ![](Methodology%20on%20Optimization.assets/image-20231215150402334.png)
> The regularity condition here is just what have been mentioned above, the $LICQ$ condition. This ensures that $\lambda_0$ in the previous theorem cannot be zero.
> 
> ![](Methodology%20on%20Optimization.assets/image-20231215150414409.png)
> Here is one line where the reader may find confusing:
> $$\sum_{i \in I\left(\mathbf{x}^*\right)} \tilde{\lambda}_i \nabla g_i\left(\mathbf{x}^*\right)=\mathbf{0}$$.
> This holds because, initially we have $$\begin{align}\sum_{i=1}^m \tilde{\lambda}_i \nabla g_i\left(\mathbf{x}^*\right)&=\sum_{i \in I\left(\mathbf{x}^*\right)} \tilde{\lambda}_i \nabla g_i\left(\mathbf{x}^*\right)\\&+\sum_{i \notin I\left(\mathbf{x}^*\right)} \tilde{\lambda}_i \nabla g_i\left(\mathbf{x}^*\right)=\mathbf{0}\end{align}$$
> and for all non-active constraints $g_i(\vec{x})<0$ in order for the above equality to hold(equal to 0), the lagrangian multipliers have to be zero. That is, $\lambda_i=0\forall i\notin I(\vec{x})$ and we get the desired results.


### KKT for Inequality/Equality Constrained Problems
> [!thm]
> ![](Methodology%20on%20Optimization.assets/image-20231215150450408.png)


### KKT Points
> [!def]
> ![](Methodology%20on%20Optimization.assets/image-20231215151519952.png)
> Simply put, KKT points are just those points that are the solutions from KKT conditions.


## Convex Framework
> [!important]
> For a convex problem as follows:
> $$\begin{align}min_{\vec{x}\in\mathbb{R}^n}&f_0(\vec{x})\\&g_i(\vec{x})\leq 0,\forall i=1,2,\cdots, m\\& h_i(\vec{x})=0,\forall i=1,2,\cdots, p\end{align}$$
> where $g_{i}(\vec{x})\forall i$  have to be all convex function of $\vec{x}$ and $h_i(\vec{x})$ have to be all affine function of $\vec{x}$.
> 
> We will denote our feasible region to be $$\Omega=\{\vec{x}\in \mathbb{R}^n|\begin{aligned}&g_i(\vec{x})\leq 0,\forall i=1,2,\cdots, m\\& h_i(\vec{x})=0,\forall i=1,2,\cdots, p\end{aligned}\}$$
> 
> In this case: we will proceed as follows:
> 
> The first step is to check if the ==slater's condition== is met. This means whether there exists some $\vec{x}$ that 
> - Fulfill all the convex inequality constraints with strict order.
> - Fulfill affine inequality constraints with partial order.
> - Fulfill all the affine equality constraints.
> 
> The second step is to ==solve the KKT conditions== and all the solutions that we get from it should be optimal points since under convexity, KKT conditions is sufficient condition for Optimality.
> ![](Methodology%20on%20Optimization.assets/image-20231215162217800.png)





## Duality Framework
> [!important]
> If the problem is not convex, but has strong duality. (Notice that one can easily check strong duality under convex framework, but for general framework, strong duality cannot be easily checked. Unless someone told you so.)
> 
> Then we proceed as follows:
> The first step is to check the 


## Sufficiency and Necessity
> [!important]
> ![](Methodology%20on%20Optimization.assets/image-20231215154024803.png)



# Concrete Examples
## When there is no KKT Points
> [!example]
> ![](Methodology%20on%20Optimization.assets/image-20231215162546102.png)
> Since the LICQ is satisfied, The KKT Condition is as follows:
> 1. Primal Feasibility: $x_1^2+x_2^2=1$
> 2. Dual Feasibility: $\lambda\geq 0$
> 3. Complementary Slackness: $\lambda(x_1^2+x_2^2-1)=0$
> 4. Stationary Conditions: $\begin{bmatrix}1\\1\end{bmatrix}+\lambda\begin{bmatrix}2x_1(x_1^2+x_2^2-1)\\2x_2(x_1^2+x_2^2-1)\end{bmatrix}=\begin{bmatrix}0\\0\end{bmatrix}$
> 
> Combining 1 and 4 we know that there is no KKT points. Thus can transform the problem into its equivalent formulation below, which has two KKT points, one of them is the optimal solution.
> ![](Methodology%20on%20Optimization.assets/image-20231215162746267.png)


## When KKT is Necessary for Optimality
> [!important]
> When KKT condition is necessary, for example strong duality holds or regularity condition holds, not all the solutions from KKT condition is really optimal points.

### LICQ Holds
> [!example]
> Consider the following example:
> $$\begin{align}\min&x_1^2+x_2^2\\s.t.&x_1^2+x_2^2=1\end{align}$$
> 
> Note that the objective function is affine and thus convex, but the equality constraint is not affine(convex actually), so it is not convex. Since there is only when equality constraint, and LICQ is satisfied for all $\vec{x}$ and thus $\vec{x}^*$, so we move to the LICQ framework to solve KKT conditions.
> 1. Primal Feasibility: $x_1^2+x_2^2=1$
> 2. Dual Feasibility: $\lambda\geq 0$
> 3. Complementary Slackness: $\lambda(x_1^2+x_2^2-1)=0$
> 4. Stationary Conditions: $\begin{bmatrix}1\\1\end{bmatrix}+\lambda\begin{bmatrix}2x_1\\2x_2\end{bmatrix}=\begin{bmatrix}0\\0\end{bmatrix}$
> 
> Solve for it we could get $\lambda=\pm\frac{1}{\sqrt{2}}$.
> Note that LICQ only ensures necessity, we have to check the optimality of each solution.
> 1. $x_1=x_2=-\frac{\sqrt{2}}{2},\lambda=\frac{1}{\sqrt{2}}$
> 2. $x_1=x_2=\frac{\sqrt{2}}{2},\lambda=-\frac{1}{\sqrt{2}}$
> 
> The hessian at both points are PSD so they are both candidates for global minima, then we evaluate the value and verify that the second one is the optimal solution. Indeed, not all KKT points are optimal solution.


## When KKT is Both N and S
> [!example]
> ![](Methodology%20on%20Optimization.assets/image-20231215162941859.png)
> Note that this is a convex optimization problem in $(x_1,x_2)$ since the objective function $\vec{x}^{\top}\begin{bmatrix} 1&0\\0&0\end{bmatrix}\vec{x}+\begin{bmatrix} 0&-1\end{bmatrix}\begin{bmatrix} x_1\\x_2\end{bmatrix}$ is convex and the equality constraint is $\begin{bmatrix} 0&1\end{bmatrix}\begin{bmatrix} x_1\\x_2\end{bmatrix}=0$ affine.
> 
> Since the Slater's Condition holds, strong duality holds, thus we solve for KKT conditions to get:
> 1. Primal Feasibility: $x_2=0$
> 2. Dual Feasibility: None
> 3. Complementary Slackness: None
> 4. Stationary Conditions: $\begin{bmatrix}2x_1\\-1\end{bmatrix}+\lambda\begin{bmatrix}0\\1\end{bmatrix}=\begin{bmatrix}0\\0\end{bmatrix}$
> 
> We could get $(\vec{x}^*,\lambda^*)=(\begin{bmatrix}0\\0 \end{bmatrix},1)$ and it is the optimal solution.
> 

> [!example ]
> ![](Methodology%20on%20Optimization.assets/image-20231215165112569.png)


## When KKT is only Sufficient
> [!important]
> When we only have sufficiency, for example convex program. Solutions to KKT conditions cannot capture all the optimal solutions.


> [!example]
> 
> ![](Methodology%20on%20Optimization.assets/image-20231215163555554.png)
> This is a convex program, but the slater's condition is not met since the only feasible points for $x_2$ is $x_2=0$, which is on the boundary. But the sufficiency is always met. Thus we solve for KKT conditions to get:
> 1. Primal Feasibility: $x_2^2\leq0$
> 2. Dual Feasibility: $\lambda\geq 0$
> 3. Complementary Slackness: $\lambda(x_2^2)=0$
> 4. Stationary Conditions: $\begin{bmatrix}2x_1\\-1\end{bmatrix}+\lambda\begin{bmatrix}0\\2x_2\end{bmatrix}=\begin{bmatrix}0\\0\end{bmatrix}$
> 
> From 4 we know $\lambda\neq 0$, then from 3 we know $x_2=0$ which contradicts with 1, so we don't have KKT points. Since here we only have sufficiency, we can only get those optimal points that satisfy the KKT, but those optimal points that don't satisfy the KKT will be missing here, which is $(0,0)$.
> 
> Also we see $(0,0)$ doesn't satisfy regularity condition, since $x_2=0$ is not linear independent(any set containing zero vector is not linearly independent), so necessity doesn't hold.


> [!example] Ridge Regression
> ![](Methodology%20on%20Optimization.assets/image-20231215170309109.png)![](Methodology%20on%20Optimization.assets/image-20231215170320822.png)


## Solving for eigenvalues
> 

