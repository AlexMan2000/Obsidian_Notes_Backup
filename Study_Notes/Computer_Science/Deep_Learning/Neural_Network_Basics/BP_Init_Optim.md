# Autodifferentiation Algorithm
See [Backprogation_Autodifferentiation](Backprogation_Autodifferentiation.pdf)


# Computational Graphs
## Scalar Operations
> [!important]
> ![](BP_Init_Optim.assets/image-20240326124929463.png)




## Vanishing Gradient
> [!def]
> For the sigmoid activation function $$\sigma(z)=\frac{1}{1+e^{-z}}$$ the gradient of it at $z$ will be $\sigma'(z)=\sigma(z)(1-\sigma(z))$ which obtains its maximum at $z=0$ and quickly vanish to 0 when $z$ moves away from $z=0$.
> 
> In terms of the output $\sigma(z)$, if it approaches $0$ or $1$, the gradient $\sigma'(z)$ will be close to 0.





## CG Definition
> [!important] Notes
> ![](BP_Init_Optim.assets/image-20240319161937642.png)![](BP_Init_Optim.assets/image-20240319162255659.png)


## CG Examples
### Shallow Example 1
> [!example]
> ![](BP_Init_Optim.assets/image-20240326130133160.png)


### Shallow Example 2
> [!example] EECS182 Sp23 Disc02 P2
> ![](BP_Init_Optim.assets/image-20240319152128498.png)![](BP_Init_Optim.assets/image-20240319152135007.png)![](BP_Init_Optim.assets/image-20240319152140047.png)



### Logistic Regression (Batch = 1)
> [!example]
> ![](BP_Init_Optim.assets/image-20240326130442607.png)



### 2-Layer MLP(Batch Size = 3)
> [!overview]
> ![](BP_Init_Optim.assets/image-20240326133440790.png)


#### Forward
> [!example]
> ![](BP_Init_Optim.assets/image-20240326131551093.png)![](BP_Init_Optim.assets/image-20240326131558700.png)



#### Backward
> [!example]
> ![](BP_Init_Optim.assets/image-20240326131738385.png)![](BP_Init_Optim.assets/image-20240326132403435.png)![](BP_Init_Optim.assets/image-20240326132522601.png)











# Back Propagation Algorithm
## Definitions
> [!def]
> Assume a fully-connected 1-hidden-layer network. Denote the dimensionalities of the input, hidden, and output layers as $d^{(0)}, d^{(1)}$, and $d^{(2)}$. 
> 
> That is, the input (which we will denote with a superscript (0)) is a vector of the form $x_1^{(0)}, \ldots, x_{d^{(0)}}^{(0)}$. Let $g$ denote the activation function applied at each layer. We will let $S_j^{(l)}=\sum_{i=1}^{d^{(l-1)}} w_{i j}^{(l)} x_i^{(l-1)}$ be the weighted input(before activation) to node $j$ in layer $l$, and let $\delta_j^{(l)}=\frac{\partial \ell}{\partial S_j^{(l)}}$ be the partial derivative of the final loss $\ell$ with respect to $S_j^{(l)}$.
> 
> Here for $w_{ij}^{(l)}x_i^{(l-1)}$ we can understand it as follows:
> 1. $i$ is the index for input dimension.
> 2. $j$ is the index for output dimension.
> 
> Also we have $x^{l}=g(x^l)$ element wise.
> 
> For a 2-layered neural network, we have the following graphical representation:
> ![](BP_Init_Optim.assets/image-20240319170446376.png)





## Base Step
> [!important]
> $$\begin{aligned}\delta_j^{(l)}=\frac{\partial \mathbf{e}(\mathbf{w})}{\partial s_j^{(l)}} \quad \text { For the final layer } l & =L \text { and } j=1: \\\delta_1^{(L)} & =\frac{\partial \mathbf{l}(\mathbf{w})}{\partial s_1^{(L)}} \\\mathbf{l}(\mathbf{w}) & =\left(x_1^{(L)}-y_n\right)^2 \\x_1^{(L)} & =\theta\left(s_1^{(L)}\right)\end{aligned}$$
>


## Induction Step
> [!important]
> $$\begin{aligned} \delta_i^{(l-1)}&=\frac{\partial l(w)}{\partial S_i^{(l-1)}} \\&=\sum_{j}^{d(l)} \frac{\partial l(w)}{\partial S_j^{(l)}} \times \frac{\partial S_j}{\partial x_i^{(l-1)}} \times \frac{\partial x_i^{(l-1)}}{\partial S_i^{(l-1)}} \\&=\sum_{j}^{d(l)} \delta_j^{(l)} w_{i j}^{(l)} g^{\prime}\left(S_i^{(l-1)}\right) \\&=g^{\prime}\left(S_i^{(l-1)}\right) \sum_{j}^{d(l)} \omega_{i j}^{(l)} \delta_j^{(l)} \cdots\end{aligned}$$



## Iterative Algorithm
> [!algo]
> **Step 1**: Compute the partial derivative w.r.t $x$ for all layers. In other words, start from output layer and move backward by computing $\delta_i^{l}$ for all $l$ and $i\in d(l)$.
> 
> **Step 2**: Given the $\delta_i^{l}$ computed in step 1, use $$\frac{\partial l(w)}{\partial w_{ij}(l)}=\delta_j^{(l)}x_i^{l-1}$$ to compute the derivative w.r.t any weight $w_{ij}^{(l)}$.
> 
> In short:
> 1. Initialize all weights $w_{i j}^{(l)}$ for $t=0,1,2, \ldots$ do
> 
> 2. Pick $n \in\{1,2, \cdots, N\}$
> 3. Forward: Compute all $x_j^{(l)}$
> 4. Backward: Compute all $\delta_j^{(l)}$
> 5. Update the weights: $w_{i j}^{(l)} \leftarrow w_{i j}^{(l)}-\eta x_i^{(l-1)} \delta_j^{(l)}$
> 6. Iterate to the next step until it is time to stop
> 7. Return the final weights $w_{i j}^{(l)}$

> [!important]
> A note on weight updating:
> 
> We can evaluate $\frac{\partial \mathbf{l}(\mathbf{w})}{\partial w_{i j}^{(l)}}$ one by one: analytically or numerically
> 
> A trick for efficient computation:
> $$\frac{\partial \mathbf{l}(\mathbf{w})}{\partial w_{i j}^{(l)}}=\frac{\partial \mathbf{l}(\mathbf{w})}{\partial s_j^{(l)}} \times \frac{\partial s_j^{(l)}}{\partial w_{i j}^{(l)}}$$
> 
> We have $\frac{\partial s_j^{(l)}}{\partial w_{i j}^{(l)}}=x_i^{(l-1)} \quad$ We only need: $\frac{\partial \mathrm{l}(\mathrm{w})}{\partial s_j^{(l)}}=\delta_j^{(l)}$





## Examples
### Shallow Example 1
> [!example] EECS189 Fa23 Disc04 P2
> ![](BP_Init_Optim.assets/b86ed5bf85897a13f461b4c6cfa0b149_MD5.jpeg)![](BP_Init_Optim.assets/9bd1b552093db7b72792d08cb613d8a3_MD5.jpeg)![](BP_Init_Optim.assets/7ff42baabe4f82262f5576f5105c522a_MD5.jpeg)![](BP_Init_Optim.assets/9f80ba7f7a4676e674ff065c8f114575_MD5.jpeg)![](BP_Init_Optim.assets/dbd7caa2bf17af0669ce5e20d730bf81_MD5.jpeg)
> Note that for neural network, we are using numerator layout instead of denominator layout as in EECS127.
> 
> ![](BP_Init_Optim.assets/image-20240320180942367.png)![](BP_Init_Optim.assets/image-20240320180954707.png)![](BP_Init_Optim.assets/image-20240320181002393.png)![](BP_Init_Optim.assets/image-20240320181010563.png)



# Optimization for BP
## Descent Mechanisms
> [!example] EECS182 Disc01 P1
> ![](Descent_Mechanisms.assets/image-20240319125356923.png)![](Descent_Mechanisms.assets/image-20240319125409976.png)![](Descent_Mechanisms.assets/image-20240319125414581.png)![](Descent_Mechanisms.assets/image-20240319125451870.png)![](Descent_Mechanisms.assets/image-20240319125458122.png)



## Convergence and Optimal LR
> [!important]
> ![](BP_Init_Optim.assets/image-20240329104754314.png)![](BP_Init_Optim.assets/image-20240329104803942.png)![](BP_Init_Optim.assets/image-20240329104811920.png)![](BP_Init_Optim.assets/image-20240329104818157.png)![](BP_Init_Optim.assets/image-20240329104824570.png)![](BP_Init_Optim.assets/image-20240329104833888.png)
> The notion of optimal learning rate is detailed in this problem [Optimal Learning Rate of G.D.](../../Machine_Learning/EECS127AB/4_Descent_Methods/Gradient_Descent.md#Optimal%20Learning%20Rate%20of%20G.D.)


## Exponential Weighted Average
> [!def]
> The idea of momentum is finding a safe way to make the $η$ bigger.


### Exponentially Weighted Averages(EWA)
> [!def]
> Suppose we have a time series data, $\theta_1,\theta_{2,\cdots,}\theta_t$ where $v_i$ represents the temperature on day $i$.
> 
> The exponentially weighted average model for these temperatures are defined as the following recurrence function:
> $$v_{t}=\beta v_{t-1}+(1-\beta)\theta_{t}$$ where $v_t$ is the exponentially weighted average of the temperature up until time step $t$ and $\beta\in(0,1)$.
> - When $\beta$ is close to 1, the result is more oscillating since we put less weight on the older data points.
> - When $\beta$ is close to 0, the result is more smooth since we put more weight on the older data points.
> 
> We can think of $v_t$ as a smoothing operation over $\theta_t$, where $\theta_t$ is oscillating across $t$ while $v_t$ is trying to average the past and present information about the temperature.
> 
> To solve for this recurrence, we use recursion and could get:
> $$v_{t}=\beta^{t}v_0+\sum\limits_{i=1}^{t}(1-\beta)\beta^{t-i}\theta_{i}$$
> which can be viewed as an inner product between an exponential decaying function $f(x)=\beta^x$ and $\theta_i$.
> 
> Recall in calculus we have $\lim_{n\to \infty}(1+\frac{1}{n})^n=e$, if we replace $n$ by $\frac{1}{\epsilon}$ we have $\lim_{\epsilon\to 0}(1+\epsilon)^{\frac{1}{\epsilon}}=e$. Thus we have:
> $$\lim_{\epsilon\to 0}(1-\epsilon)^{\frac{1}{\epsilon}}=\frac{1}{e}$$ where the role $\epsilon$ plays can be viewed as the same as $1-\beta$. 
> 
> We can interpret it as if $\beta=0.9$, it will take $\frac{1}{1-0.9}=10$ steps away from the current step to make the weight to decay to $\frac{1}{e}\approx \frac{1}{3}$.
 


### Bias Correction of EWA
> [!property]



## GD with Momentum
### Theory
> [!example] EECS182 HW2 P2 - Least Square Example
> More on stability [Stability_Feedback_Control](../../Machine_Learning/Control_LA_Circuit/EECS16B/Module2_Robotic_Control/Stability_Feedback_Control.md)
> 
> Here the $1-2\eta X^{\top}X$ is the weight decay parameter, controlling how fast our parameters are converging to optimal point.
> ![](BP_Init_Optim.assets/image-20240330135451710.png)![](BP_Init_Optim.assets/image-20240330135458785.png)![](BP_Init_Optim.assets/image-20240330135504961.png)![](BP_Init_Optim.assets/image-20240330135514396.png)![](BP_Init_Optim.assets/image-20240330135522815.png)![](BP_Init_Optim.assets/image-20240330135531740.png)![](BP_Init_Optim.assets/image-20240330135541263.png)![](BP_Init_Optim.assets/image-20240330135549485.png)![](BP_Init_Optim.assets/image-20240330135558573.png)![](BP_Init_Optim.assets/image-20240330135615946.png)![](BP_Init_Optim.assets/image-20240330135630102.png)


### Coding
> [!code] Coding for part (g)
> **Dataset:**
> We generate a dataset of 2D datapoints from the gaussian distribution with a mean of $(-3, 0)$ and covariance matrix of $\begin{pmatrix}3 & 0 \\ 0 & 1\end{pmatrix}$. The binary labels $y$ indicate whether the second dimension is greater than 0 (positive) or not (negative). The data is visualized using a scatter plot with different colors representing the different labels.
```python
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(0)

# Generate Dataset
def gen_gaussian_points(n, mean, sigma):
    return np.random.normal(mean, sigma, [n, 2])

N = 500

X = gen_gaussian_points(N, [-3, 0], [3, 1])
y = (X[:,1]>0).astype(float)
y = np.expand_dims(y, axis=-1)

# Here X[y.squeeze()==0].T is (2, 500), *X[y.squeeze()==0].T is [x_coordinates], [y_coordinates], used for plt.scatter
plt.scatter(*X[y.squeeze()==0].T)
plt.scatter(*X[y.squeeze()==1].T)
plt.title("Visualization of Data")
plt.show()

```
``




#### Plain GD
> [!code]
> We will implement gradient descent *without* momentum below.
```python
def runGD(maxiter,stepsize):
    w = np.zeros((2, 1))
    grads = []
    ws = []
    losses = []
    for i in range(maxiter):
        grad = 2 * (X.T @ X @ w) - 2 * X.T @ y
        w = w - stepsize * grad
        grads.append(grad)
        ws.append(w)
        loss = np.linalg.norm(y - X @ w) ** 2
        losses.append(loss)
    print("Final loss =", loss)
    grads = np.array(grads).squeeze()
    ws = np.array(ws).squeeze()
    return grads, ws, losses

maxiter = 100
stepsize = 1e-4
grads, ws, losses = runGD(maxiter,stepsize)
```




#### GDM
> [!code]
> Implement the gradient descent with momentum algorithm. **Fill in the missing code** for updating the parameters. As a verification step, compare the final loss with the previous part to ensure it is reasonable and not significantly different.

```python
def runGDM(maxiter, stepsize, beta):
    w = np.zeros((2, 1))
    grads_m = []
    ws_m = []
    losses_m = []
    for i in range(maxiter):
        grad = 2 * (X.T @ X @ w) - 2 * X.T @ y
        if i == 0:
            smoothed_grad = grad
        ###############################################
        ###       TODO: YOUR CODE HERE              ###
        ###############################################
        smoothed_grad = (1 - beta) * smoothed_grad + beta * grad
        ###############################################
        ###       END OF YOUR CODE                  ###
        ###############################################
        w = w - stepsize * smoothed_grad
        grads_m.append(grad)
        ws_m.append(w)
        loss = np.linalg.norm(y - X @ w) ** 2
        losses_m.append(loss)
    print("Final loss =", loss)
    grads_m = np.array(grads_m).squeeze()
    ws_m = np.array(ws_m).squeeze()
    return grads_m, ws_m, losses_m

maxiter = 100
stepsize = 1e-4
beta = 0.6
grads_m, ws_m, losses_m = runGDM(maxiter, stepsize, beta)
```




### Visualization

#### Visualizing the Loss Landscape
> [!code] Very good example of meshgrid use
> The following contour plot visualizes the loss landscape of this optimization task. It's important to note that the data has been generated such that the correlation coefficient between dimension 0 and dimension 1 is zero, aligning dimension 0 and dimension 1 with the two singular vectors in the Singular Value Decomposition (SVD) of the data matrix.
> ![](BP_Init_Optim.assets/image-20240330155958780.png)
```python
# Create a 100x100 coordinate grid
w0_s, w1_s = np.meshgrid(np.linspace(-0.5, 0.5, 100), np.linspace(-0.5, 0.5, 100))
w_s = np.stack([w0_s.reshape(-1), w1_s.reshape(-1)], axis=1)

# Evaluate the loss function Xw at each point (w_xi, w_yi)
loss_s = ((X @ w_s.T - y) ** 2).sum(axis=0).reshape(100, 100)
from matplotlib import ticker, cm
plt.contourf(w0_s, w1_s, loss_s, cmap=cm.PuBu_r, levels=40)
plt.colorbar()
plt.xlabel("w0")
plt.ylabel("w1")
plt.show()
```



#### GD
> [!code] Compare Dimensions
> ![](BP_Init_Optim.assets/image-20240330160056860.png)![](BP_Init_Optim.assets/image-20240330160105666.png)
```python
plt.figure(figsize=(12, 4))
plt.plot(range(maxiter), np.abs(grads)[:,0], 'r', label="Dimension 0")
plt.plot(range(maxiter), np.abs(grads)[:,1], 'b', label="Dimension 1")
plt.title("Gradients")
plt.xlabel("Iterations")
plt.legend()
plt.show()

plt.figure(figsize=(12, 4))
plt.plot(range(maxiter), np.abs(ws)[:,0], 'r', label="Dimension 0")
plt.plot(range(maxiter), np.abs(ws)[:,1], 'b', label="Dimension 1")
plt.title("Parameters")
plt.xlabel("Iterations")
plt.legend()
plt.show()
```


#### GDM
> [!code] Compare Dimensions
> ![](BP_Init_Optim.assets/image-20240330160119603.png)![](BP_Init_Optim.assets/image-20240330160127427.png)
```python
plt.figure(figsize=(12, 4))
plt.plot(range(maxiter), np.abs(grads_m)[:,0], 'r', label="Dimension 0")
plt.plot(range(maxiter), np.abs(grads_m)[:,1], 'b', label="Dimension 1")
plt.title("Gradients")
plt.xlabel("Iterations")
plt.legend()
plt.show()

plt.figure(figsize=(12, 4))
plt.plot(range(maxiter), np.abs(ws_m)[:,0], 'r', label="Dimension 0")
plt.plot(range(maxiter), np.abs(ws_m)[:,1], 'b', label="Dimension 1")
plt.title("Parameters")
plt.xlabel("Iterations")
plt.legend()
plt.show()
```



#### Comparisons
> [!code] Compare Gradients
> ![](BP_Init_Optim.assets/image-20240330161420821.png)![](BP_Init_Optim.assets/image-20240330161425025.png)
```python
plt.figure(figsize=(12, 4))
plt.plot(range(maxiter), np.abs(grads)[:,0], 'r', label="GD")
plt.plot(range(maxiter), np.abs(grads_m)[:,0], 'b', label="momentum")
plt.title("Gradients of Dimension 0")
plt.xlabel("Iterations")
plt.legend()
plt.show()

plt.figure(figsize=(12, 4))
plt.plot(range(maxiter), np.abs(grads)[:,1], 'r', label="GD")
plt.plot(range(maxiter), np.abs(grads_m)[:,1], 'b', label="momentum")
plt.title("Gradients of Dimension 1")
plt.xlabel("Iterations")
plt.legend()
plt.show()
```

> [!code] Compare Parameters
> ![](BP_Init_Optim.assets/image-20240330161439735.png)![](BP_Init_Optim.assets/image-20240330161443239.png)
```python
plt.figure(figsize=(12, 4))
plt.plot(range(maxiter), np.abs(ws)[:,0], 'r', label="GD")
plt.plot(range(maxiter), np.abs(ws_m)[:,0], 'b', label="momentum")
plt.title("Parameters of Dimension 0")
plt.xlabel("Iterations")
plt.legend()
plt.show()

plt.figure(figsize=(12, 4))
plt.plot(range(maxiter), np.abs(ws)[:,1], 'r', label="GD")
plt.plot(range(maxiter), np.abs(ws_m)[:,1], 'b', label="momentum")
plt.title("Parameters of Dimension 1")
plt.xlabel("Iterations")
plt.legend()
plt.show()
```

> [!code] Compare Loss
> ![](BP_Init_Optim.assets/image-20240330161720955.png)
> 
```python
plt.figure(figsize=(12, 4))
plt.plot(range(maxiter), np.log(np.abs(losses)-losses[-1]), 'r', label="GD")
plt.plot(range(maxiter), np.log(np.abs(losses_m)-losses_m[-1]), 'b', label="momentum")
plt.title("Loss changes as iterations increase")
plt.legend()
plt.ylabel("Log(loss(at iteration $i$) - optimal loss)")
plt.xlabel("Iterations")
plt.show()
```



## RMSProp




## Adam






# Initialization for BP
## Problematic Initializations
### Constant Weight Init
> [!example] EECS189 Fa23 Disc04 P1
> Note that here we assume $h=XW+b$
> 
> In summary, initializing all weights to be constant will result in symmetry learning.
> ![](Initialization.assets/image-20240319130248258.png)![](BP_Init_Optim.assets/image-20240319130316823.png)![](BP_Init_Optim.assets/image-20240319130332758.png)![](BP_Init_Optim.assets/image-20240319172156358.png)![](BP_Init_Optim.assets/image-20240319172240886.png)



### Zero Initialization
> [!important]
> Actually a special case of constant weight initialization. 
> 
> Initializing all the weights with zeros leads the neurons to learn the same features during training.
> 
> In fact, any constant initialization scheme will perform very poorly. Consider a neural network with two hidden units, and assume we initialize all the biases to 0 and the weights with some constant $α$. 
> 
> If we forward propagate an input $(x_1,x_2)$ in this network, the output of both hidden units will be $relu(αx_1​+αx_2​)$. 
> 
> Thus, both hidden units will have identical influence on the cost, which will lead to identical gradients. Thus, both neurons will evolve symmetrically throughout training, effectively preventing different neurons from learning different things.

> [!quiz] Why is zero initialization bad?
> It's a bad idea because of 2 reasons:
> 1. If you have sigmoid activation, or anything where $g(0)≠0$ then it will cause weights to move "together", limiting the power of back-propagation to search the entire space to find the optimal weights which lower the loss/cost.
> 2. If you have tanh or ReLu activation, or anything where $g(0)=0$ then all the outputs will be 0, and the gradients for the weights will always be 0. Hence you will not have any learning at all.
> 
> Let's demonstrate this (for simplicity I assume a final output layer of 1 neuron, which is a special case in the last section where $j=1$).
> ![](BP_Init_Optim.assets/image-20240326163543967.png)![](BP_Init_Optim.assets/image-20240326163604972.png)![](BP_Init_Optim.assets/image-20240326163657908.png)![](BP_Init_Optim.assets/image-20240326163752228.png)![](BP_Init_Optim.assets/image-20240326163816727.png)



### Extreme Value Initialization
> [!important]
> ![](BP_Init_Optim.assets/image-20240326165203811.png)


### Too-Large Initialization
> [!def]
> ![](BP_Init_Optim.assets/image-20240326165339350.png)


### Too-Small Initialization
> [!def]
> ![](BP_Init_Optim.assets/image-20240326165345740.png)



## RELU Elbow Distribution
> [!important]
> ![](BP_Init_Optim.assets/image-20240331175851106.png)![](BP_Init_Optim.assets/image-20240331175900012.png)





## Proper Initialization Values
### Rules of Thumb
> [!important]
> To prevent the gradients of the network’s activations from vanishing or exploding, we will stick to the following rules of thumb:
> 1. The **mean** of the activations should be zero.
> 2. The **variance** of the activations should stay the same across every layer.
>  
> Under these two assumptions, the backpropagated gradient signal should not be multiplied by values too small or too large in any layer. It should travel to the input layer without exploding or vanishing.
> 
> More concretely, consider a layer $l$. Its forward propagation is:
> $$\begin{aligned}a^{[l-1\rfloor} & =g^{[l-1\rfloor}\left(z^{[l-1\rfloor}\right) \\z^{[l]} & =W^{[l]} a^{[l-1]}+b^{[l]} \\a^{[l]} & =g^{[l]}\left(z^{[l]}\right)\end{aligned}$$
> 
> We would like the following to hold ${ }^2$ :$$\begin{aligned}E\left[a^{[l-1]}\right] & =E\left[a^{[l]}\right] \\\operatorname{Var}\left(a^{[l-1]}\right) & =\operatorname{Var}\left(a^{[l]}\right)\end{aligned}$$



### Tanh - Xavier Normal Initialization
> [!def]
> ![](BP_Init_Optim.assets/image-20240331173731165.png)![](BP_Init_Optim.assets/image-20240331174014930.png)
> **Theory:**
> 
> The goal of Xavier Initialization is to initialize the weights such that the variance of the activations are the same across every layer. 
> 
> This constant variance helps prevent the gradient from exploding or vanishing.
> 
> The recommended initialization is Xavier initialization (or one of its derived methods), for every layer $l$:
> $$\begin{aligned}W^{[l]} & \sim \mathcal{N}\left(\mu=0, \sigma^2=\frac{1}{n^{[l-1]}}\right) \\b^{[l]} & =0\end{aligned}$$
> 
> In other words, all the **weights** of layer $l$ are picked randomly from a normal distribution with mean $\mu=0$ and variance $\sigma^2=\frac{1}{n^{[l-1]}}$ where $n^{[l-1]}$ is the number of neuron in layer $l-1$. 
> 
> **Biases are initialized with zeros.**

> [!proof] Proof Sketch
> In this section, we will show that Xavier Initialization ${ }^4$ keeps the variance the same across every layer. We will assume that our layer's activations are normally distributed around zero. Sometimes it helps to understand the mathematical justification to grasp the concept, but you can understand the fundamental idea without the math.
> 
> Let's work on the layerl described in part (III) and assume the activation function is tanh. The forward propagation is:$$
> \begin{aligned}
> & z^{[l]}=W^{[l]} a^{[l-1]}+b^{[l]} \\& a^{[l]}=\tanh \left(z^{[l]}\right)\end{aligned}$$
> 
> The goal is to derive a relationship between $\operatorname{Var}\left(a^{[l-1]}\right)$ and $\operatorname{Var}\left(a^{[l]}\right)$. We will then understand how we should initialize our weights such that: $\operatorname{Var}\left(a^{[l-1]}\right)=\operatorname{Var}\left(a^{[l]}\right)$.
> 
> Assume we initialized our network with appropriate values and the input is normalized. Early on in the training, we are in the linear regime of $\tanh$. Values are small enough and thus $\tanh \left(z^{[l]}\right) \approx z^{[l]}, 5$ meaning that:$$\operatorname{Var}\left(a^{[l]}\right)=\operatorname{Var}\left(z^{[l]}\right)$$
> 
> Moreover, $z^{[l]}=W^{[l]} a^{[l-1]}+b^{[l]}=\operatorname{vector}\left(z_1^{[l]}, z_2^{[l]}, \ldots, z_n^{[l]}\right)$ where $z_k^{[l]}=\sum_{j=1}^{n^{[l-1]}} w_{k j}^{[l]} a_j^{[l-1]}+b_k^{[l]}$. For simplicity, let's assume that $b^{[l]}=0$ (it will end up being true given the choice of initialization we will choose).
> 
> Thus, looking element-wise at the previous equation $\operatorname{Var}\left(a^{[l-1]}\right)=\operatorname{Var}\left(a^{[l]}\right)$ now gives:$$\operatorname{Var}\left(a_k^{[l]}\right)=\operatorname{Var}\left(z_k^{[l]}\right)=\operatorname{Var}\left(\sum_{j=1}^{n[l-1]} w_{k j}^{[l]} a_j^{[l-1]}\right)$$
> A common math trick is to extract the summation outside the variance. To do this, we must make the following three assumptions:
> 1. Weights are independent and identically distributed
> 2. Inputs are independent and identically distributed
> 3. Weights and inputs are mutually independent
> 
> Thus, now we have:$$\operatorname{Var}\left(a_k^{[l]}\right)=\operatorname{Var}\left(z_k^{[l]}\right)=\operatorname{Var}\left(\sum_{j=1}^{n[l-1]} w_{k j}^{[l]} a_j^{[l-1]}\right)=\sum_{j=1}^{n^{[l-1]}} \operatorname{Var}\left(w_{k j}^{[l]} j_j^{[l-1]}\right)$$
> 
> Another common math trick is to convert the variance of a product into a product of variances. Here is the formula for it:
> $$\operatorname{Var}(X Y)=E[X]^2 \operatorname{Var}(Y)+\operatorname{Var}(X) E[Y]^2+\operatorname{Var}(X) \operatorname{Var}(Y)$$
> 
> Using this formula with $X=w_{k j}^{[l]}$ and $Y=a_j^{[l-1]}$, we get:$$\operatorname{Var}\left(w_{k j}^{[l]} a_j^{[l-1]}\right)=E\left[w_{k j}^{[l]}\right]^2 \operatorname{Var}\left(a_j^{[l-1]}\right)+\operatorname{Var}\left(w_{k j}^{[l]}\right) E\left[a_j^{[l-1]}\right]^2+\operatorname{Var}\left(w_{k j}^{[l]}\right) \operatorname{Var}\left(a_j^{[l-1]}\right)$$
> 
> We're almost done! The first assumption leads to $E\left[w_{k j}^{[l]}\right]^2=0$ and the second assumption leads to $E\left[a_j^{[l-1]}\right]^2=0$ because weights are initialized with zero mean, and inputs are normalized. Thus:
> $$\operatorname{Var}\left(z_k^{[l]}\right)=\sum_{j=1}^{n^{[l-1]}} \operatorname{Var}\left(w_{k j}^{[l]}\right) \operatorname{Var}\left(a_j^{[l-1]}\right)=\sum_{j=1}^{n^{[l-1]}} \operatorname{Var}\left(W^{[l]}\right) \operatorname{Var}\left(a^{[l-1]}\right)=n^{[l-1]} \operatorname{Var}\left(W^{[l]}\right) \operatorname{Var}\left(a^{[l-1]}\right)$$
> 
> The equality above results from our first assumption stating that:
> $$\operatorname{Var}\left(w_{k j}^{[l]}\right)=\operatorname{Var}\left(w_{11}^{[l]}\right)=\operatorname{Var}\left(w_{12}^{[l]}\right)=\cdots=\operatorname{Var}\left(W^{[l]}\right)$$
> 
> Similarly the second assumption leads to:$$\operatorname{Var}\left(a_j^{[l-1]}\right)=\operatorname{Var}\left(a_1^{[l-1]}\right)=\operatorname{Var}\left(a_2^{[l-1]}\right)=\cdots=\operatorname{Var}\left(a^{[l-1]}\right)$$
> 
> With the same idea:$$\operatorname{Var}\left(z^{[l]}\right)=\operatorname{Var}\left(z_k^{[l]}\right)$$
> 
> Wrapping up everything, we have:$$\operatorname{Var}\left(a^{[l]}\right)=n^{[l-1]} \operatorname{Var}\left(W^{[l]}\right) \operatorname{Var}\left(a^{[l-1]}\right)$$
> 
> Voilà! If we want the variance to stay the same across layers $\left(\operatorname{Var}\left(a^{[l]}\right)=\operatorname{Var}\left(a^{[l-1]}\right)\right)$, we need $\operatorname{Var}\left(W^{[l]}\right)=\frac{1}{n^{[l-1]}}$. This justifies the choice of variance for Xavier initialization.
> 
> Notice that in the previous steps we did not choose a specific layer $l$. Thus, we have shown that this expression holds for every layer of our network. Let $L$ be the output layer of our network. Using this expression at every layer, we can link the output layer's variance to the input layer's variance:
> $$\begin{aligned}\operatorname{Var}\left(a^{[L]}\right) & =n^{[L-1]} \operatorname{Var}\left(W^{\lfloor L]}\right) \operatorname{Var}\left(a^{\lfloor L-1]}\right) \\& =n^{[L-1]} \operatorname{Var}\left(W^{[L]}\right) n^{[L-2]} \operatorname{Var}\left(W^{[L-1]}\right) \operatorname{Var}\left(a^{[L-2]}\right) \\& =\cdots \\& =\left[\prod_{l=1}^L n^{[l-1]} \operatorname{Var}\left(W^{[l]}\right)\right] \operatorname{Var}(x)\end{aligned}$$
> 
> Depending on how we initialize our weights, the relationship between the variance of our output and input will vary dramatically. Notice the following three cases.$$n^{[l-1]} \operatorname{Var}\left(W^{[l]}\right) \begin{cases}<1 & \Longrightarrow \text { Vanishing Signal } \\ =1 & \Longrightarrow \operatorname{Var}\left(a^{[L]}\right)=\operatorname{Var}(x) \\ >1 & \Longrightarrow \text { Exploding Signal }\end{cases}$$
> 
> Thus, in order to avoid the vanishing or exploding of the forward propagated signal, we must set $n^{[l-1]} \operatorname{Var}\left(W^{[l]}\right)=1$ by initializing $\operatorname{Var}\left(W^{[l]}\right)=\frac{1}{n^{[l-1]}} \cdot$
> 
> Throughout the justification, we worked on activations computed during the forward propagation. The same result can be derived for the backpropagated gradients. Doing so, you will see that in order to avoid the vanishing or exploding gradient problem, we must set $n^{[l]} \operatorname{Var}\left(W^{[l]}\right)=1$ by initializing $\operatorname{Var}\left(W^{[l]}\right)=\frac{1}{n[l]}$.



### Dead RELU Problem
> [!important]
> ![](BP_Init_Optim.assets/image-20240331175027675.png)![](BP_Init_Optim.assets/image-20240331175042534.png)
> More about Leaky RLU/ELU on [Activations&Features](Activations&Features.md)



### Relu - He Initialization
> [!def]
> ![](BP_Init_Optim.assets/image-20240331175138787.png)

> [!code] Implementation
```python


```



### Bias Initialization
> [!def]
> ![](BP_Init_Optim.assets/image-20240331175157919.png)


