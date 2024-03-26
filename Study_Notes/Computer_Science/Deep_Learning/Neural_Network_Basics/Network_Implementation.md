# Structure and Terminology
> [!def]
> ![](Network_Implementation.assets/image-20240326120342844.png)![](Network_Implementation.assets/image-20240326120349338.png)![](Network_Implementation.assets/image-20240326120355637.png)![](Network_Implementation.assets/image-20240326120404304.png)




# Neural Network Implementation
> In this chapter, we implement the NN with pure numpy.





## Weight Initialization
### Xavier Initialization
> [!important]
> The goal of Xavier Initialization is to initialize the weights such that the variance of the activations are the same across every layer. 
> 
> This constant variance helps prevent the gradient from exploding or vanishing.





## Loss Function




## Fully-Connected Layers





## Activation Layers
### Relu Activation
> [!def]
> ![](Network_Implementation.assets/image-20240326120712302.png)![](Network_Implementation.assets/image-20240326115412549.png)![](Network_Implementation.assets/image-20240326115433374.png)

```python
class ReLU(Activation):
    def __init__(self):
        super().__init__()

    def forward(self, Z: np.ndarray) -> np.ndarray:
        """Forward pass for relu activation:
        f(z) = z if z >= 0
               0 otherwise
        
        Parameters
        ----------
        Z  input pre-activations (any shape), batch of data

        Returns
        -------
        f(z) as described above applied elementwise to `Z`
        """
        ### YOUR CODE HERE ###
        return np.maximum(Z, 0)

    def backward(self, Z: np.ndarray, dY: np.ndarray) -> np.ndarray:
        """Backward pass for relu activation.
        
        Parameters
        ----------
        Z   input to the `forward` method
        dY  derivative of loss w.r.t. the output of this layer
            (same shape as `Z`)

        Returns
        -------
        derivative of loss w.r.t. 'Z'
        """
        ### YOUR CODE HERE ###
        return dY * np.logical_and(np.ones(Z.shape), Z >= 0)
        # Here we can utilize the broadcasting, making it to be:
        # return dY * np.logical_and(1, Z >= 0)
```



### Sigmoid Activation
> [!code]
> For a sigmoid function $$\sigma(z)=\frac{1}{1+e^{-z}}$$, the gradient is just $$\frac{\partial \sigma(z)}{\partial z}=\sigma(z)(1-\sigma(z))$$
```python
class Sigmoid(Activation):
    def __init__(self):
        super().__init__()

    def forward(self, Z: np.ndarray) -> np.ndarray:
        """Forward pass for sigmoid function:
        f(z) = 1 / (1 + exp(-z))
        
        Parameters
        ----------
        Z  input pre-activations (any shape)

        Returns
        -------
        f(z) as described above applied elementwise to `Z`
        """
        ### YOUR CODE HERE ###
        return 1 / (1 + np.exp(-1 * Z))

    def backward(self, Z: np.ndarray, dY: np.ndarray) -> np.ndarray:
        """Backward pass for sigmoid. (Elementwise)
        
        Parameters
        ----------
        Z   input to the `forward` method
        dY  derivative of loss w.r.t. the output of this layer
            (same shape as `Z`)

        Returns
        -------
        derivative of loss w.r.t. 'Z'
        """
        ### YOUR CODE HERE ###
        output = self.forward(Z)
        return dY * output * (1- output)
```



### Softmax Activation
> [!def]
> ![](Network_Implementation.assets/image-20240326121502943.png)![](Network_Implementation.assets/image-20240326121511688.png)![](Network_Implementation.assets/image-20240326121517466.png)![](Network_Implementation.assets/image-20240326121523438.png)![](Network_Implementation.assets/image-20240326122713477.png)

```python
class SoftMax(Activation):
    def __init__(self):
        super().__init__()


    def forward(self, Z: np.ndarray) -> np.ndarray:
        """Forward pass for the softmax activation.
        Hint: The naive implementation might not be numerically stable.
        
        Parameters
        ----------
        Z  input pre-activations (batch size, num_activations)

        Returns
        -------
        f(z), which is the array resulting from applying the softmax function
        to each sample's activations (same shape as 'Z')， different across samples, so
        we cannot apply to the whole matrix Z.
        """
        ### YOUR CODE HERE ###
        shifted = Z - np.max(Z, axis=-1, keepdims=True)
		exp = np.exp(shifted)
		out = np.divide(exp, np.sum(exp, axis=-1, keepdims=True))
		return out

    def backward(self, Z: np.ndarray, dY: np.ndarray) -> np.ndarray:
        """Backward pass for softmax activation.
        
        Parameters
        ----------
        Z   input to the `forward` method
        dY  derivative of loss w.r.t. the output of this layer
            same shape as `Z`

        Returns
        -------
        derivative of loss w.r.t. Z
        """
        ### YOUR CODE HERE ###
        p = self.forward(Z)
        backward = []
        for i, example in enumerate(p):
            diag = np.diagflat(example)
            example = example.reshape((-1, 1))
            J = diag - np.dot(example, example.T)
            backward.append(dY[i] @ J)
        return np.array(backward)
```



## Optimizer 




