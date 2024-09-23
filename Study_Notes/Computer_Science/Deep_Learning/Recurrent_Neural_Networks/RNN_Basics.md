
# RNN Forward
## Network Structure
> [!def]
> ![](RNN_Basics.assets/image-20240704230447907.png)

> [!quiz]
> ![](RNN_Basics.assets/image-20240705094259412.png)




## Computational Graph
> [!important]
> ![](RNN_Basics.assets/image-20240704225634407.png)![](RNN_Basics.assets/image-20240704225641566.png)
> Circle here represents functions and variables are represented by arrows(data stream).




# RNN Backpropagation
## Single Loss at Final Time Step
> [!important]
> **Tranditional Backpropagation:**
> Here $f$ means layer(could be sigmoid layer, linear layer)
> ![](RNN_Basics.assets/image-20240704224025961.png)
> **Backpropagation for RNN:**
> 
> ![](RNN_Basics.assets/image-20240704223940884.png)



## Loss at each time step
> [!important]
> ![](RNN_Basics.assets/image-20240704225954229.png)



# RNN Training
## Vanishing/Exploding Gradient
> [!important]
> **Why is vanishing gradient a problem?**
> ![](RNN_Basics.assets/image-20240704231032016.png)![](RNN_Basics.assets/image-20240922133314808.png)
> **Why is exploding gradient a problem?**
> 
> ![](RNN_Basics.assets/image-20240922133531610.png)
> Examples see [Analyzing RNN Gradients](RNN_Basics.md#Analyzing%20RNN%20Gradients)


> [!proof] Proof Sketch
> ![](RNN_Basics.assets/image-20240922133243764.png)![](RNN_Basics.assets/image-20240922133249438.png)![](RNN_Basics.assets/image-20240922133255320.png)

> [!proof] Proof
> ![](RNN_Basics.assets/image-20240922133124847.png)![](RNN_Basics.assets/image-20240922133131341.png)![](RNN_Basics.assets/image-20240922133141871.png)![](RNN_Basics.assets/image-20240922133148542.png)![](RNN_Basics.assets/image-20240922133154524.png)












## Better Gradient Flow
> [!def]
> ![](RNN_Basics.assets/image-20240705084319733.png)![](RNN_Basics.assets/image-20240705084329748.png)



## Dealing with Exploding Gradients
### Saturation Activation Functions
> [!important]
> ![](RNN_Basics.assets/image-20240705094425772.png)
> For example if the many-to-one RNN as follows:
> 
> ![](RNN_Basics.assets/image-20240705120957134.png)
> 
> has no linearities, and the forward pass looks like $$h_{t}=W^{h}h_{t-1} + W^{x}x_{t}+b$$ instead of $$h_{t}=g(W^{h}h_{t-1} + W^{x}x_{t}+b)$$ where $g$ is a non-linear function, then if the prediction output at time step $t$ is $\hat{y}_T=W^{f}h_{T}+b^{f}$ and the loss is MSE, the gradient w.r.t $W_{h}$ would be $$\frac{\partial \mathcal{L}}{\partial h_{t}}=2(\hat{y}_T-y_T)W^{f}(W^{h})^{T-t}$$
> If the magnitude of the largest eigenvalue of $W^h$ is much greater than 1, the gradient will explode, and if it’s much less than 1, the gradient will start to vanish. 
> 
> Gradients are only stable when the largest eigenvalue magnitude is close to 1.
> 
> Examples see [Analyzing RNN Gradients](RNN_Basics.md#Analyzing%20RNN%20Gradients)

### Gradient Clipping
> [!def]
> ![](RNN_Basics.assets/image-20240922133602411.png)



## Dealing with Dying Gradients
## Vertical Skips
> [!def]
> ![](RNN_Basics.assets/image-20240706105642436.png)





## Horizontal Skips
> [!def]
> ![](RNN_Basics.assets/image-20240706105649763.png)![](RNN_Basics.assets/image-20240706105659912.png)![](RNN_Basics.assets/image-20240706105705195.png)


# Bi-directional RNNs
## Motivations
> [!motiv]
> ![](RNN_Basics.assets/image-20240922175307363.png)


## Model Definition
> [!def]
> ![](RNN_Basics.assets/image-20240922175324345.png)![](RNN_Basics.assets/image-20240922175508666.png)![](RNN_Basics.assets/image-20240922175518015.png)

> [!bug] Caveats
> ![](RNN_Basics.assets/image-20240922175532565.png)




# LSTM - Fixing Vanishing Gradient
## Definition
> [!def]
> ![](RNN_Basics.assets/image-20240705085421376.png)![](RNN_Basics.assets/image-20240922174901787.png)
> Here the output $h_{t}$ of a hidden layer of RNN is obtained by element-wise product of $$h_{t}=\tilde{o}_{t}\odot tanh(a_{t})$$
> - $h_{t}$ is the hidden state
> - $a_{t}$ is the cell state, or candidate state($C_{t}$ in some literatures)
> 
> **Remarks:**
> Intuitively, we are **not** applying non-linearity to $a_{t}$ at every time step, we just want to control the amount of information of cell states to keep across different time steps. This makes the derivatives of $a_{t}$ every well-behaved. 
> $$a_{t} = a_{t-1}\odot \tilde{f}_{t} + \tilde{i}_{t}\odot \tilde{g}_{t}$$ this changes very little step to step(long term memory)
> $$h_{t}$$ changes all the time(multiplicative, short-term memory).





## Forget Gate
> [!def]
> ![](RNN_Basics.assets/image-20240705085819609.png)



## Input Gate
> [!def]
> ![](RNN_Basics.assets/image-20240705085826321.png)



## Candidate Cell State
> [!def]
> ![](RNN_Basics.assets/image-20240705085835458.png)




## Output Gate
> [!def]
> ![](RNN_Basics.assets/image-20240705085842703.png)



## Summary
> [!summary]
> ![](RNN_Basics.assets/image-20240922180111110.png)![](RNN_Basics.assets/image-20240922180146354.png)








# Implementations
## RNN Layers
> [!code]
> ![](RNN_Basics.assets/image-20240705103331628.png)
```python

import copy

# If you are not using colab you can delete these two lines
from google.colab import output
output.enable_custom_widget_manager()

import torch as th
from torch import nn
import torch.nn.functional as F
import torch.optim as optim
import numpy as np
import matplotlib.pyplot as plt
from ipywidgets import interactive, widgets, Layout



class RNNLayer(nn.Module):
  def __init__(self, input_size, hidden_size, nonlinearity=th.tanh):
    """
    Initialize a single RNN layer.

    Inputs:
    - input_size: Data input feature dimension
    - hidden_size: RNN hidden state size (also the output feature dimension)
    - nonlinearity: Nonlinearity applied to the rnn output
    """
    super().__init__()
    self.input_size = input_size
    self.hidden_size = hidden_size
    self.nonlinearity = nonlinearity
    
    # Initialize any parameters your class needs.             
    self.linear = nn.Linear(input_size + hidden_size, hidden_size, bias=True)

  def forward(self, x):
    """
    RNN forward pass

    Inputs:
    - x: input tensor (B, seq_len, input_size)

    Returns:
    - all_h: tensor of size (B, seq_len, hidden_size) containing hidden states
             produced for each timestep
    - last_h: hidden state from the last timestep (B, hidden_size)
    """
    h_list = []  # List to store the hidden states [h_1, ... h_T]
    # 1. Initialize h0 with zeros                                   
    # 2. Roll out the RNN over the sequence, storing hidden states 
    # 3. Return the appropriate outputs                             
    h0 = th.zeros(x.size(0), self.hidden_size)
    last_h = h0
    for t in range(x.size(1)):
      last_h = self.nonlinearity(self.linear(th.concat([x[:, t, :], last_h], dim = 1)))
      h_list.append(last_h)


    # h_list should now contain all hidden states, each of size (B, hidden_size)
    # We will store the hidden states so we can analyze their gradients later
    self.store_h_for_grad(h_list)
    all_h = th.stack(h_list, dim=1)
    return all_h, last_h

  def store_h_for_grad(self, h_list):
    """
    Store input list and allow gradient computation for all list elements
    """
    for h in h_list:
      h.retain_grad()
    self.h_list = h_list
```


> [!test]
```python
rnn = RNNLayer(1, 1)
# Overwrite initial parameters with fixed values.
# Should give deterministic results even with different implementations.
rnn.load_state_dict({k: v * 0 + .1 for k, v in rnn.state_dict().items()})
data = th.ones((1, 1, 1))
expected_out = th.FloatTensor([[[0.1973753273487091]]])
all_h, last_h = rnn(data)
assert all_h.shape == expected_out.shape
assert th.all(th.isclose(all_h, last_h))
print(f'Expected: {expected_out.item()}, got: {last_h.item()}, max error: {th.max(th.abs(expected_out - last_h)).item()}')

rnn = RNNLayer(2, 3, nonlinearity=lambda x: x)  # no nonlinearity

num_params = sum(p.numel() for p in rnn.parameters())
assert num_params == 18, f'expected 18 parameters but found {num_params}'

rnn.load_state_dict({k: v * 0 - .1 for k, v in rnn.state_dict().items()})
data = th.FloatTensor([[[.1, .15], [.2, .25], [.3, .35], [.4, .45]], [[-.1, -1.5], [-.2, -2.5], [-.3, -3.5], [-.4, -.45]]])
expected_all_h = th.FloatTensor([[[-0.1250, -0.1250, -0.1250],
         [-0.1075, -0.1075, -0.1075],
         [-0.1328, -0.1328, -0.1328],
         [-0.1452, -0.1452, -0.1452]],

        [[ 0.0600,  0.0600,  0.0600],
         [ 0.1520,  0.1520,  0.1520],
         [ 0.2344,  0.2344,  0.2344],
         [-0.0853, -0.0853, -0.0853]]])
expected_last_h = th.FloatTensor([[-0.1452, -0.1452, -0.1452],
        [-0.0853, -0.0853, -0.0853]])
all_h, last_h = rnn(data)
assert all_h.shape == expected_all_h.shape
assert last_h.shape == expected_last_h.shape
print(f'Max error all_h: {th.max(th.abs(expected_all_h - all_h)).item()}')
print(f'Max error last_h: {th.max(th.abs(expected_last_h - last_h)).item()}')
```
> [!test] Output
> ![](RNN_Basics.assets/image-20240705103000361.png)



## RNN Regression Model
> [!code]
> ![](RNN_Basics.assets/image-20240705103423876.png)
```python
class RecurrentRegressionModel(nn.Module):
  def __init__(self, recurrent_net, output_dim=1):
    """
    Initialize a simple RNN regression model

    Inputs:
    - recurrent_net: an RNN or LSTM (single or multi layer)
    - output_dim: feature dimension of the output
    """
    super().__init__()
    self.recurrent_net = recurrent_net
    self.output_dim = output_dim
    self.linear = nn.Linear(self.recurrent_net.hidden_size, self.output_dim)

  def forward(self, x):
    """
    Forward pass

    Inputs:
    - x: input tensor (B, seq_len, input_size)

    Returns:
    - out: predictions of shape (B, seq_len, self.output_dim).
    - all_h: tensor of size (B, seq_len, hidden_size) containing hidden states
             produced for each timestep.
    """
    all_h, _ = self.recurrent_net.forward(x)
    B, seq_len = x.size(0), x.size(1)

    # Apply the linear layer to the hidden states al at once
    out = self.linear(all_h.reshape(B * seq_len, -1)).reshape(B, seq_len, -1)

    return out, all_h
```

> [!test]
> ![](RNN_Basics.assets/image-20240705111306241.png)
```python
rnn = RecurrentRegressionModel(RNNLayer(2, 3), 4)

num_params = sum(p.numel() for p in rnn.parameters())
assert num_params == 34, f'expected 34 parameters but found {num_params}'

rnn.load_state_dict({k: v * 0 - .1 for k, v in rnn.state_dict().items()})
data = th.FloatTensor([[[.1, .15], [.2, .25], [.3, .35], [.4, .45]], [[-.1, -1.5], [-.2, -2.5], [-.3, -3.5], [-.4, -.45]]])
expected_preds = th.FloatTensor([[[-0.0627, -0.0627, -0.0627, -0.0627],
         [-0.0678, -0.0678, -0.0678, -0.0678],
         [-0.0604, -0.0604, -0.0604, -0.0604],
         [-0.0567, -0.0567, -0.0567, -0.0567]],

        [[-0.1180, -0.1180, -0.1180, -0.1180],
         [-0.1453, -0.1453, -0.1453, -0.1453],
         [-0.1692, -0.1692, -0.1692, -0.1692],
         [-0.0748, -0.0748, -0.0748, -0.0748]]])
expected_all_h = th.FloatTensor([[[-0.1244, -0.1244, -0.1244],
         [-0.1073, -0.1073, -0.1073],
         [-0.1320, -0.1320, -0.1320],
         [-0.1444, -0.1444, -0.1444]],

        [[ 0.0599,  0.0599,  0.0599],
         [ 0.1509,  0.1509,  0.1509],
         [ 0.2305,  0.2305,  0.2305],
         [-0.0840, -0.0840, -0.0840]]])
preds, all_h = rnn(data)
assert all_h.shape == expected_all_h.shape
assert preds.shape == expected_preds.shape
print(f'Max error all_h: {th.max(th.abs(expected_all_h - all_h)).item()}')
print(f'Max error last_h: {th.max(th.abs(expected_preds - preds)).item()}')
```


## Dataset and Loss Function
> [!code]
> ![](RNN_Basics.assets/image-20240705111929099.png)
```python
def generate_batch(seq_len=10, batch_size=1):
  data = th.randn(size=(batch_size, seq_len, 1))
  sums = th.cumsum(data, dim=1)
  div = (th.arange(seq_len) + 1).unsqueeze(0).unsqueeze(2)
  target = sums / div
  return data, target


# x, y torch.Size([4, 10, 1])
x, y = generate_batch(seq_len=10, batch_size=4)

def loss_fn(pred, y, last_timestep_only=False):
  """
  Inputs:
  - pred: model predictions of size (batch, seq_len, 1)
  - y: targets of size (batch, seq_len, 1)
  - last_timestep_only: boolean indicating whether to compute loss for all
    timesteps or only the lat

  Returns:
  - loss: scalar MSE loss between pred and true labels
  """
  if last_timestep_only:
    loss = F.mse_loss(pred[:, -1], y[:, -1])
  else:
    loss = F.mse_loss(pred, y)
  return loss

```

> [!test]
> ![](RNN_Basics.assets/image-20240705113329346.png)
```python
pred = th.FloatTensor([[.1, .2, .3], [.4, .5, .6]])
y = th.FloatTensor([[-1.1, -1.2, -1.3], [-1.4, -1.5, -1.6]])
loss_all = loss_fn(pred, y, last_timestep_only=False)
loss_last = loss_fn(pred, y, last_timestep_only=True)
assert loss_all.shape == loss_last.shape == th.Size([])
print(f'Max error loss_all: {th.abs(loss_all - th.tensor(3.0067)).item()}')
print(f'Max error loss_last: {th.abs(loss_last - th.tensor(3.7)).item()}')
```



## Analyzing RNN Gradients
> [!important]
> ![](RNN_Basics.assets/image-20240705113405441.png)![](RNN_Basics.assets/image-20240705113357508.png)


### When no linearity
> [!code] Exploding when weight scale is > 1
> ![](RNN_Basics.assets/image-20240705114641516.png)

> [!code] Vanishing when weight scale is < 1
> ![](RNN_Basics.assets/image-20240705114717542.png)



### With Relu 
> [!code] Results
> When weights are small, there is vanishing gradient.
> ![](RNN_Basics.assets/image-20240705121756085.png)
> 
> When weights are big, there is exploding hidden states norm and gradient magnitude.
> 
> ![](RNN_Basics.assets/image-20240705122051132.png)



### With Tanh
> [!code]
> When weight is small, there are more vanishing problems than Relu and linearity.
> ![](RNN_Basics.assets/image-20240705122153615.png)
> When weights are big, there are fewer exploding issues.
> 
> ![](RNN_Basics.assets/image-20240705122255782.png)



### With multiple output
> [!code]
> ![](RNN_Basics.assets/image-20240705122445123.png)



## Single LSTM Layer
> [!code]
> ![](RNN_Basics.assets/image-20240705122540360.png)![](RNN_Basics.assets/image-20240705122549259.png)
```python
class LSTMLayer(nn.Module):
  def __init__(self, input_size, hidden_size):
    """
    Initialize a single LSTM layer.

    Inputs:
    - input_size: Data input feature dimension
    - hidden_size: RNN hidden state size (also the output feature dimension)
    """
    super().__init__()
    self.input_size = input_size
    self.hidden_size = hidden_size

    self.Wfx = nn.Linear(input_size, hidden_size, bias = False)
    self.Wfh = nn.Linear(hidden_size, hidden_size, bias = True)
    self.Wix = nn.Linear(input_size, hidden_size, bias = False)
    self.Wih = nn.Linear(hidden_size, hidden_size, bias = True)
    self.Wox = nn.Linear(input_size, hidden_size, bias = False)
    self.Woh = nn.Linear(hidden_size, hidden_size, bias = True)
    self.Wgx = nn.Linear(input_size, hidden_size, bias = False)
    self.Wgh = nn.Linear(hidden_size, hidden_size, bias = True)

  def forward(self, x):
    """
    LSTM forward pass

    Inputs:
    - x: input tensor (B, seq_len, input_size)

    Returns:
    - all_h: tensor of size (B, seq_len, hidden_size) containing hidden states
             produced for each timestep
    - (h_last, c_last): hidden and cell states from the last timestep, each of
             size (B, hidden_size)
    """
    h_list = []
    B, seq_len = x.size(0), x.size(1)
    h_last = th.zeros(B, self.hidden_size)
    c_last = th.zeros(B, self.hidden_size)
    
    for t in range(seq_len):
      # 1. Compute forget Gate
      f = th.sigmoid(self.Wfx(x[:, t, :]) + self.Wfh(h_last))
    
      # 2. Compute Input Gate
      i = th.sigmoid(self.Wix(x[:, t, :]) + self.Wih(h_last))
      
      # 3. Compute Output Gate
      o = th.sigmoid(self.Wox(x[:, t, :]) + self.Woh(h_last))

      # 4. Compute Candidate states
      c_curr = th.tanh(self.Wgx(x[:, t, :]) + self.Wgh(h_last))

      # 5. Compute output Candidate states
      c_last = f * c_last + i * c_curr

      # 6. Compute output hidden states
      h_last = th.tanh(c_last) * o

      h_list.append(h_last)

    # h_list should now contain all hidden states, each of size (B, hidden_size)
    # We will store the hidden states so we can analyze their gradients later
    self.store_h_for_grad(h_list)
    all_h = th.stack(h_list, dim=1)

    return all_h, (h_last, c_last)

  def store_h_for_grad(self, h_list):
    """
    Store input list and allow gradient computation for all list elements
    """
    for h in h_list:
      h.retain_grad()
    self.h_list = h_list
```

> [!test]
> ![](RNN_Basics.assets/image-20240706103629511.png)
```python
lstm = LSTMLayer(2, 3)
lstm.load_state_dict({k: v * 0 - .1 for k, v in lstm.state_dict().items()})
data = th.FloatTensor([[[.1, .15], [.2, .25], [.3, .35], [.4, .45]], [[-.1, -1.5], [-.2, -2.5], [-.3, -3.5], [-.4, -.45]]])
expected_all_h = th.FloatTensor([[[-0.0273, -0.0273, -0.0273],
         [-0.0420, -0.0420, -0.0420],
         [-0.0514, -0.0514, -0.0514],
         [-0.0583, -0.0583, -0.0583]],

        [[ 0.0159,  0.0159,  0.0159],
         [ 0.0568,  0.0568,  0.0568],
         [ 0.1142,  0.1142,  0.1142],
         [ 0.0369,  0.0369,  0.0369]]])
expected_last_h = th.FloatTensor([[-0.0583, -0.0583, -0.0583],
        [ 0.0369,  0.0369,  0.0369]])
expected_last_c = th.FloatTensor([[-0.1280, -0.1280, -0.1280],
        [ 0.0759,  0.0759,  0.0759]])
all_h, (last_h, last_c) = lstm(data)
assert all_h.shape == (2, 4, 3)
assert last_h.shape == last_c.shape == (2, 3)
print(f'Max error all_h: {th.max(th.abs(expected_all_h - all_h)).item()}')
print(f'Max error last_h: {th.max(th.abs(expected_last_h - last_h)).item()}')
print(f'Max error last_h: {th.max(th.abs(expected_last_c - last_c)).item()}')
```



## Analyzing LSTM Gradients
> [!code]
> ![](RNN_Basics.assets/image-20240706104059671.png)![](RNN_Basics.assets/image-20240706104105066.png)
```python
hidden_size = 3
last_target_only = True
rnn = LSTMLayer(1, hidden_size)
gv = GradientVisualizer(rnn, last_target_only)
gv.create_visualization()
```



## Multiple-Layered RNN/LSTM
> [!code]
> ![](RNN_Basics.assets/image-20240706110226166.png)
> **Remarks:**
> 
> For multilayered RNN, each layer has its own weights, as shown below:
> 
> ![](RNN_Basics.assets/image-20240706111239032.png)
```python
class RNN(nn.Module):
  def __init__(self, input_size, hidden_size, num_layers):
    """
    Initialize a multilayer RNN

    Inputs:
    - input_size: Data input feature dimension
    - hidden_size: hidden state size (also the output feature dimension)
    - num_layers: number of layers
    """
    super().__init__()
    assert num_layers >= 1
    self.input_size = input_size
    self.hidden_size = hidden_size
    self.num_layers = num_layers

    self.layers = nn.ModuleList([
        RNNLayer(input_size, hidden_size),
        *[RNNLayer(hidden_size, hidden_size)
         for i in range(1, num_layers)]
    ])


  def forward(self, x):
    """
    Multilayer RNN forward pass

    Inputs:
    - x: input tensor (B, seq_len, input_size)

    Returns:
    - last_layer_h: tensor of size (B, seq_len, hidden_size) containing the
             outputs produced for each timestep from the last layer
    - last_step_h: all hidden states from the last step (num_layers, B, hidden_size)
    """

    last_step_h_list = []
    all_h = x
    for i in range(self.num_layers):
      all_h, last_h = self.layers[i].forward(all_h)
      last_step_h_list.append(last_h)

    last_layer_h = all_h
    last_step_h = th.stack(last_step_h_list, dim = 0)

    return last_layer_h, last_step_h


class LSTM(nn.Module):
  def __init__(self, input_size, hidden_size, num_layers):
    """
    Initialize a multilayer LSTM

    Inputs:
    - input_size: Data input feature dimension
    - hidden_size: hidden state size (also the output feature dimension)
    - num_layers: number of layers
    """
    super().__init__()
    assert num_layers >= 1
    self.input_size = input_size
    self.hidden_size = hidden_size
    self.num_layers = num_layers

    self.layers = nn.ModuleList([
        LSTMLayer(input_size, hidden_size),
        *[LSTMLayer(hidden_size, hidden_size)
         for i in range(1, num_layers)]
    ])


  def forward(self, x, hc0=None):
    """
    Multilayer LSTM forward pass

    Inputs:
    - x: input tensor (B, seq_len, input_size)

    Returns:
    - last_layer_h: tensor of size (B, seq_len, hidden_size) containing the
             outputs produced for each timestep from the last layer
    - (last_step_h, last_step_c): all hidden and cell states from the last step
            size (num_layers, B, hidden_size)
    """
    last_step_h_list = []
    last_step_c_list = []
    all_h = x
    for i in range(self.num_layers):
      all_h, (last_h, last_c) = self.layers[i].forward(all_h)
      last_step_h_list.append(last_h)
      last_step_c_list.append(last_c)

    last_layer_h = all_h
    last_step_h = th.stack(last_step_h_list, dim = 0)
    last_step_c = th.stack(last_step_c_list, dim = 0)
    return last_layer_h, (last_step_h, last_step_c)
```

> [!test]
> ![](RNN_Basics.assets/image-20240706113346078.png)
```python
rnn = RNN(2, 3, 1)
rnn.load_state_dict({k: v * 0 - .1 for k, v in rnn.state_dict().items()})
data = th.FloatTensor([[[.1, .15], [.2, .25], [.3, .35], [.4, .45]], [[-.1, -1.5], [-.2, -2.5], [-.3, -3.5], [-.4, -.45]]])
expected_all_h = th.FloatTensor([[[-0.1244, -0.1244, -0.1244],
         [-0.1073, -0.1073, -0.1073],
         [-0.1320, -0.1320, -0.1320],
         [-0.1444, -0.1444, -0.1444]],

        [[ 0.0599,  0.0599,  0.0599],
         [ 0.1509,  0.1509,  0.1509],
         [ 0.2305,  0.2305,  0.2305],
         [-0.0840, -0.0840, -0.0840]]])
expected_last_h = th.FloatTensor([[[-0.1444, -0.1444, -0.1444],
         [-0.0840, -0.0840, -0.0840]]])
all_h, last_h = rnn(data)
assert all_h.shape == expected_all_h.shape
assert last_h.shape == expected_last_h.shape
print(f'Max error all_h: {th.max(th.abs(expected_all_h - all_h)).item()}')
print(f'Max error last_h: {th.max(th.abs(expected_last_h - last_h)).item()}')

rnn = RNN(2, 3, 2)
rnn.load_state_dict({k: v * 0 - .1 for k, v in rnn.state_dict().items()})
data = th.FloatTensor([[[.1, .15], [.2, .25], [.3, .35], [.4, .45]], [[-.1, -1.5], [-.2, -2.5], [-.3, -3.5], [-.4, -.45]]])
expected_all_h = th.FloatTensor([[[-0.0626, -0.0626, -0.0626],
         [-0.0490, -0.0490, -0.0490],
         [-0.0457, -0.0457, -0.0457],
         [-0.0430, -0.0430, -0.0430]],
        [[-0.1174, -0.1174, -0.1174],
         [-0.1096, -0.1096, -0.1096],
         [-0.1354, -0.1354, -0.1354],
         [-0.0342, -0.0342, -0.0342]]])
expected_last_h = th.FloatTensor([[[-0.1444, -0.1444, -0.1444],
         [-0.0840, -0.0840, -0.0840]],
        [[-0.0430, -0.0430, -0.0430],
         [-0.0342, -0.0342, -0.0342]]])
all_h, last_h = rnn(data)
assert all_h.shape == (2, 4, 3)
assert last_h.shape == (2, 2, 3)
print(f'Max error all_h: {th.max(th.abs(expected_all_h - all_h)).item()}')
print(f'Max error last_h: {th.max(th.abs(expected_last_h - last_h)).item()}')


lstm = LSTM(2, 3, 1)
lstm.load_state_dict({k: v * 0 - .1 for k, v in lstm.state_dict().items()})
data = th.FloatTensor([[[.1, .15], [.2, .25], [.3, .35], [.4, .45]], [[-.1, -1.5], [-.2, -2.5], [-.3, -3.5], [-.4, -.45]]])
expected_all_h = th.FloatTensor([[[-0.0273, -0.0273, -0.0273],
         [-0.0420, -0.0420, -0.0420],
         [-0.0514, -0.0514, -0.0514],
         [-0.0583, -0.0583, -0.0583]],

        [[ 0.0159,  0.0159,  0.0159],
         [ 0.0568,  0.0568,  0.0568],
         [ 0.1142,  0.1142,  0.1142],
         [ 0.0369,  0.0369,  0.0369]]])
expected_last_h = th.FloatTensor([[[-0.0583, -0.0583, -0.0583],
         [ 0.0369,  0.0369,  0.0369]]])
expected_last_c = th.FloatTensor([[[-0.1280, -0.1280, -0.1280],
         [ 0.0759,  0.0759,  0.0759]]])
all_h, (last_h, last_c) = lstm(data)
assert all_h.shape == (2, 4, 3)
assert last_h.shape == last_c.shape == (1, 2, 3)
print(f'Max error all_h: {th.max(th.abs(expected_all_h - all_h)).item()}')
print(f'Max error last_h: {th.max(th.abs(expected_last_h - last_h)).item()}')
print(f'Max error last_c: {th.max(th.abs(expected_last_c - last_c)).item()}')


lstm = LSTM(2, 3, 3)
lstm.load_state_dict({k: v * 0 - .1 for k, v in lstm.state_dict().items()})
data = th.FloatTensor([[[.1, .15], [.2, .25], [.3, .35], [.4, .45]], [[-.1, -1.5], [-.2, -2.5], [-.3, -3.5], [-.4, -.45]]])
expected_all_h = th.FloatTensor([[[-0.0212, -0.0212, -0.0212],
         [-0.0296, -0.0296, -0.0296],
         [-0.0329, -0.0329, -0.0329],
         [-0.0343, -0.0343, -0.0343]],
        [[-0.0211, -0.0211, -0.0211],
         [-0.0291, -0.0291, -0.0291],
         [-0.0320, -0.0320, -0.0320],
         [-0.0332, -0.0332, -0.0332]]])
expected_last_h = th.FloatTensor([[[-0.0583, -0.0583, -0.0583],
         [ 0.0369,  0.0369,  0.0369]],
        [[-0.0320, -0.0320, -0.0320],
         [-0.0430, -0.0430, -0.0430]],
        [[-0.0343, -0.0343, -0.0343],
         [-0.0332, -0.0332, -0.0332]]])
expected_last_c = th.FloatTensor([[[-0.1280, -0.1280, -0.1280],
         [ 0.0759,  0.0759,  0.0759]],
        [[-0.0666, -0.0666, -0.0666],
         [-0.0907, -0.0907, -0.0907]],
        [[-0.0716, -0.0716, -0.0716],
         [-0.0693, -0.0693, -0.0693]]])
all_h, (last_h, last_c) = lstm(data)
assert all_h.shape == (2, 4, 3)
assert last_h.shape == last_c.shape == (3, 2, 3)

print(f'Max error all_h: {th.max(th.abs(expected_all_h - all_h)).item()}')
print(f'Max error last_h: {th.max(th.abs(expected_last_h - last_h)).item()}')
print(f'Max error last_c: {th.max(th.abs(expected_last_c - last_c)).item()}')
```


> [!test] Training
```python
def train(model, optimizer, num_batches, last_timestep_only, seq_len=10, batch_size=32):
  # model
  model.train()

  losses = []
  from tqdm import tqdm
  t = tqdm(range(0, num_batches))
  for i in t:
      data, labels = generate_batch(seq_len=seq_len, batch_size=batch_size)
      pred, h = model(data)
      loss = loss_fn(pred, labels, last_timestep_only)
      losses.append(loss.item())

      optimizer.zero_grad()
      loss.backward()
      optimizer.step()
      if i % 100 == 0:
          t.set_description(f"Batch: {i} Loss: {np.mean(losses[-10:])}")
  return losses


def train_all(hidden_size, lr, num_batches, last_timestep_only):
  input_size = 1
  rnn_1_layer = RecurrentRegressionModel(RNN(input_size, hidden_size, 1))
  lstm_1_layer = RecurrentRegressionModel(LSTM(input_size, hidden_size, 1))
  rnn_2_layer = RecurrentRegressionModel(RNN(input_size, hidden_size, 2))
  lstm_2_layer = RecurrentRegressionModel(LSTM(input_size, hidden_size, 2))
  models = [rnn_1_layer, lstm_1_layer, rnn_2_layer, lstm_2_layer]
  model_names = ['rnn_1_layer', 'lstm_1_layer', 'rnn_2_layer', 'lstm_2_layer']

  losses = []
  for model in models:
    optimizer = optim.Adam(model.parameters(), lr=lr)
    loss = train(model, optimizer, num_batches, last_timestep_only)
    losses.append(loss)

  # visualize the results
  fig, ax1 = plt.subplots(1)
  for loss in losses:
    ax1.plot(loss)
  ax1.legend(model_names)
  plt.show()

  batch_size = 4
  x, y = generate_batch(seq_len=10, batch_size=batch_size)
  preds_list = [model(x)[0] for model in models]
  for i in range(batch_size):
    fig, ax1 = plt.subplots(1)
    ax1.plot(x[i, :, 0])
    if last_timestep_only:
      ax1.plot(np.arange(10), [y[i, -1].item()] * 10, 'bo')
    else:
      ax1.plot(y[i, :, 0], 'bo')
    for pred in preds_list:
      if last_timestep_only:
        ax1.plot(np.arange(10), [pred[i, -1, 0].detach().cpu().numpy()] * 10)
      else:
        ax1.plot(pred[i, :, 0].detach().cpu().numpy())
    ax1.legend(['x', 'y'] + model_names)
    plt.show()
  return models, losses



def generate_batch(seq_len=10, batch_size=1):
  data = th.randn(size=(batch_size, seq_len, 1))
  sums = th.cumsum(data, dim=1)
  div = (th.arange(seq_len) + 1).unsqueeze(0).unsqueeze(2)
  target = sums / div
  return data, target


def loss_fn(pred, y, last_timestep_only=False):
  """
  Inputs:
  - pred: model predictions of size (batch, seq_len, 1)
  - y: targets of size (batch, seq_len, 1)
  - last_timestep_only: boolean indicating whether to compute loss for all
    timesteps or only the lat

  Returns:
  - loss: scalar MSE loss between pred and true labels
  """
  if last_timestep_only:
    loss = F.mse_loss(pred[:, -1], y[:, -1])
  else:
    loss = F.mse_loss(pred, y)
  return loss



hidden_size = 32
lr = 1e-4
num_batches = 5000
last_timestep_only = False

th.manual_seed(0)
predict_all_models, predict_all_losses = train_all(hidden_size, lr, num_batches, last_timestep_only)
last_timestep_only = True
predict_one_models, predict_one_losses = train_all(hidden_size, lr, num_batches, last_timestep_only)
```
> [!test] Training Output
> **Last Step Only = False**
> ![](RNN_Basics.assets/image-20240706114151683.png)![](RNN_Basics.assets/image-20240706114202926.png)
> **Last Step Only = True**
> 
> ![](RNN_Basics.assets/image-20240706114528532.png)![](RNN_Basics.assets/image-20240706114540738.png)



# Applications
## Name Classification
### Task Descriptions
> [!task]
> ![](RNN_Basics.assets/image-20240706115010520.png)![](RNN_Basics.assets/image-20240706115124157.png)
> Basically, we are building a model to predict a person's nationality/mother tongue based on his last name.


### Preprocess The Dataset
> [!code]
```python

```



### Model Definition
> [!code]
```python
class RecurrentClassifier(nn.Module):
    def __init__(
        self,
        vocab_size: int,
        rnn_size: int,
        n_categories: int,
        num_layers: int = 1,
        dropout: float = 0.0,
        model_type: str = 'lstm'
    ):
        super().__init__()
        self.rnn_size = rnn_size
        self.model_type = model_type

        self.embedding = nn.Embedding(vocab_size, rnn_size)


        # Create a RNN/LSTM model with [num_layers] layers, with a dropout between each layer stack, 
        # controlled by dropout parameter, help regularizing the model
        if model_type == 'lstm':
            self.rnn = nn.LSTM(rnn_size, rnn_size, num_layers, batch_first=True, dropout=dropout)
        elif model_type == 'rnn':
            self.rnn = nn.RNN(rnn_size, rnn_size, num_layers, batch_first=True, dropout=dropout)

        self.drop = nn.Dropout(dropout)
        self.output = nn.Linear(rnn_size, n_categories)

    def forward(self, x: torch.Tensor, last_pos: torch.Tensor) -> torch.Tensor:
        embeds = self.embedding(x)
        if self.model_type == 'lstm':
            rnn_out, _ = self.rnn(embeds)
        else:
            rnn_out, _ = self.rnn(embeds)

        # Advanced Index
        out = rnn_out[torch.arange(x.size(0)), last_pos]
        out = self.drop(out)
        logits = self.output(out)
        return logits
```




### Model Training/Tuning
> [!code] Using Multi-layered RNN
> This hyperparameter group gives eval accuracy of over 80% on our multi-layered RNN model.
> ![](RNN_Basics.assets/image-20240706174409739.png)![](RNN_Basics.assets/image-20240706174415047.png)
```python
hidden_size = 512
num_layers = 7
dropout = 0.6
optimizer_class = optim.Adam
lr = 1e-3
batch_size = 256
```
> [!test] Using Multi-layered LSTM
> With smaller `hidden_size` and `num_layers`, `LSTM` can even outperform RNN.
> ![](RNN_Basics.assets/image-20240706182040546.png)
```python
hidden_size = 256
num_layers = 3
dropout = 0.6
optimizer_class = optim.Adam
lr = 1e-3
batch_size = 256
```



### Ethic Considerations
> [!important]
> ![](RNN_Basics.assets/image-20240706160049550.png)





