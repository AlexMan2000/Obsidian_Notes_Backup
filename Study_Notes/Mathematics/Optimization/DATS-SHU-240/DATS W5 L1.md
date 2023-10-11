# DATS W5 L1

Have to convert the maximization problem into minimization problem with KKT conditions.



## Sufficient Condition

也就是我们通过KKT condition解出来的x并不是全部的minimum points. 有的minimum point满足KKT, 有的不满足。

比如下面的凸优化问题:
$$
min~~x\\
s.t.
\\x^2 \leq 0
$$
首先这是一个凸优化问题，因为`Inequality constraint` 中的$g(x)=x^2$是一个`Convex Function`, 同时它也是连续可微的

但是

Convex Problem的判断准则:

1. 不等式约束是`Convex function`, 且是`continuously differentiable`的。



## Necessary Condition

如果g(x)(不等式约束)满足Slater Constaint Qualification，则KKT是necessary and sufficient的。所有的minimum points满足KKT conditions.

## Force Field

$$
\frac{\partial E_p}{\partial h}=F_G
$$

势能函数对于距离的偏导数就是力的大小。





## Graphical Explanations

对于如下的KKT Condition:
$$
\nabla f(\mathbf{x^*})+\lambda\sum_{i=1}^m\nabla h_i(\mathbf{x}^*) +\mu\sum_{j=1}^n \nabla g_i(\mathbf{x}^*)=0\\
h_i(\mathbf{x}^*)=0,i=1,2,\cdots, m\\
g_j(\mathbf{x}^*)\leq 0, j=1,2,\cdots, n\\
u_i \geq 0, j=1,2,\cdots, n\\
\mu_jg_j(\mathbf{x}^*)=0, j=1,2,.\cdots,n\\
$$
$\nabla g_i(\mathbf{x}^*)$ 相当于力的方向，$\mu_i$ 就相当于力的大小。

我们在解`slackness conditions`的时候，一般采用分类讨论，$\mu_i$ 只有等于零和大于零两种情况:

- 如果$\mu_i>0$, 表明minimum point受到了来自constraint boundary的力的作用，所以一般而言$g_j(\mathbf{x}^*)=0$, 表示$x^*$接触到了boundary, 因为$g(\mathbf{x}^*)=0$就表示$\mathbf{x}^*$在$g(\cdot)$的函数图像上。
- 如果$\mu_i=0$, 表明minimum point没有受到了来自constraint boundary的力的作用，所以一般而言$g_j(\mathbf{x}^*)<0$, 表示$x^*$没有接触到boundary。

更一般的，如果我们有$n$个不等式约束，我们需对每一组可能的$(\mu_1,\mu_2,\cdots, \mu_n)$的取值进行讨论。





## Solving Constrained Minimization

### Iterative Descent Approach

- The search **direction** has to point to a direction in which at least some feasible points lie.
- **Step size** should not cause infeasibility.







