# CNN Properties
## Translational Invariance
> [!important]






# CNN and MLP
> [!example] EECS182 Sp23 DISC04 P2
> Why does CNN perform better than MLP (Multilayer Perceptron) in various modalities? The three most distinct features that differentiate CNN from MLP are as follows:
> 1. **Sparse interactions** : Unlike the MLP model, which had to calculate the interactions between all neurons using matrix multiplication, CNN has sparse interactions. This is achieved by using smaller kernels in comparison to the resolution of the input image. This means that CNN can greatly reduce the amount of computation and memory requirements and improve statistical efficiency. This is also called sparse connectivity or sparse weights. 
> 2. **Parameter sharing** : Parameter sharing means using the same parameters more than once within a model. In the case of MLP, all parameters are used only once when calculating the output within one layer. This reduces the memory used to store parameters. More see [Weight Sharing](Convolution_Operation.md#Weight%20Sharing).
> 3. **Translational equivariance** : Parameter sharing in convolution operation makes the convolution layer equivariant to translation of given input. When a function is equivariant to some operation, it means that when the input changes as much as the given operation, the output of the function also changes in the same way. To explain it more formally, if a function $f(x)$ is equivariant to a transformation $g(x)$, then $f(g(x)) = g(f(x))$. In the case of convolution, $g(x)$ is the translation of the input $x$. While **convolution is equivariant to translation**, it is not equivariant to other transformations such as rotation, scale, or warping. Therefore, various regularizations such as data augmentations are used to obtain CNN functions that are robust to such transformations during training. 


## Setup
> [!code]

```python
# As usual, a bit of setup

import IPython
from IPython.display import display, HTML

import torch
import torch.nn as nn
import torch.optim as optim
import torch.nn.functional as F
from torch.utils.data import DataLoader
from torch.utils.data import sampler

import torchvision.datasets as dset
import torchvision.transforms as T

import matplotlib.pyplot as plt
import numpy as np
import random 

seed = 7
torch.manual_seed(seed)
random.seed(seed)
np.random.seed(seed)

# for auto-reloading external modules
# see http://stackoverflow.com/questions/1907993/autoreload-of-modules-in-ipython
%load_ext autoreload
%autoreload 2
```



## Loading Dataset
> [!code]
```python
NUM_TRAIN = 49000

# The torchvision.transforms package provides tools for preprocessing data
# and for performing data augmentation; here we set up a transform to
# preprocess the data by subtracting the mean RGB value and dividing by the
# standard deviation of each RGB value; we've hardcoded the mean and std.
# If we want to add data augmentations, torchvision also offers different 
# transformations that we can compose in here, though we would need to be sure
# to have two sets of transformations: one with data augmentation for the 
# training loaders, and one without for the test and validation sets.
transform = T.Compose([
                T.ToTensor(),
                T.Normalize((0.4914, 0.4822, 0.4465), (0.2023, 0.1994, 0.2010))
            ])

# We set up a Dataset object for each split (train / val / test); Datasets load
# training examples one at a time, so we wrap each Dataset in a DataLoader which
# iterates through the Dataset and forms minibatches. We divide the CIFAR-10
# training set into train and val sets by passing a Sampler object to the
# DataLoader telling how it should sample from the underlying Dataset.
cifar10_train = dset.CIFAR10('./deeplearning/datasets', train=True, download=True,
                             transform=transform)
loader_train = DataLoader(cifar10_train, batch_size=64, 
                          sampler=sampler.SubsetRandomSampler(range(NUM_TRAIN)))

cifar10_val = dset.CIFAR10('./deeplearning/datasets', train=True, download=True,
                           transform=transform)
loader_val = DataLoader(cifar10_val, batch_size=64, 
                        sampler=sampler.SubsetRandomSampler(range(NUM_TRAIN, 50000)))

cifar10_test = dset.CIFAR10('./deeplearning/datasets', train=False, download=True, 
                            transform=transform)
loader_test = DataLoader(cifar10_test, batch_size=64)
```


## Training Trigger
> [!code]
```python
def check_valid_accuracy(loader, model):
    # print('Checking accuracy on validation set')
    if not loader.dataset.train:
        print('Checking accuracy on test set')   
    num_correct = 0
    num_samples = 0
    model.eval()  # set model to evaluation mode
    with torch.no_grad():
        for x, y in loader:
            x = x.to(device=device, dtype=dtype)  # move to device, e.g. GPU
            y = y.to(device=device, dtype=torch.long)
            scores = model(x)
            _, preds = scores.max(1)
            num_correct += (preds == y).sum()
            num_samples += preds.size(0)
        acc = float(num_correct) / num_samples
        # print('Got %d / %d correct (%.2f)' % (num_correct, num_samples, 100 * acc))
    return acc

def train_model(model, optimizer, epochs=1):
    """
    Train a model on CIFAR-10 using the PyTorch Module API and prints model 
    accuracies during training.
    
    Inputs:
    - model: A PyTorch Module giving the model to train.
    - optimizer: An Optimizer object we will use to train the model
    - epochs: (Optional) A Python integer giving the number of epochs to train for
    
    Returns: Lists of validation accuracies at the end of each epoch.
    """
    model = model.to(device=device)  # move the model parameters to CPU/GPU
    train_accs = []
    val_accs = []
    for e in range(epochs):
        for t, (x, y) in enumerate(loader_train):
            model.train()  # put model to training mode
            x = x.to(device=device, dtype=dtype)  # move to device, e.g. GPU
            y = y.to(device=device, dtype=torch.long)

            scores = model(x)
            loss = F.cross_entropy(scores, y)

            # Zero out all of the gradients for the variables which the optimizer
            # will update.
            optimizer.zero_grad()

            # This is the backwards pass: compute the gradient of the loss with
            # respect to each trainable parameter of the model.
            loss.backward()

            # Actually update the parameters of the model using the gradients
            # computed by the backwards pass.
            optimizer.step()

            if t % print_every == 0:
                acc = check_valid_accuracy(loader_val, model)
                print(f"Epoch [{e}/{epochs}]: Iter {t}, loss = {round(loss.item(), 4)}, validation accuracy = {100*acc}%")
        val_accs.append(check_valid_accuracy(loader_val, model))
    return val_accs
```


## Define MLP and CNN
> [!code]
```python
class ThreeLayerConvNet(nn.Module):
    def __init__(self, in_channel, channel_1, channel_2, num_classes):
        super().__init__()
        # Same Padding, 32 -> (32 - 5 + 2 * 2)/1 + 1 = 32
        self.conv1 = nn.Conv2d(in_channel, channel_1, 5, stride=1, padding=2)
	    # Same Padding, 32 -> (32 - 3 + 1 * 2)/1 + 1 = 32
        self.conv2 = nn.Conv2d(channel_1, channel_2, 3, stride=1, padding=1)
        self.classifier = nn.Linear(channel_2 * 32 * 32, num_classes)

    def forward(self, x):
        x = self.conv1(x)
        x = F.relu(x)
        x = self.conv2(x)
        x = F.relu(x)
		# (N, C, H, W) -> (N, C*H*W)
        x = x.flatten(start_dim=1)
        x = self.classifier(x)

        return x

class ThreeLayerMLP(nn.Module):
    def __init__(self, input_size, hidden_size, num_classes):
        super().__init__()
        self.fc1 = nn.Linear(input_size, hidden_size)
        self.fc2 = nn.Linear(hidden_size, hidden_size)
        self.classifier = nn.Linear(hidden_size, num_classes)

    def forward(self, x):
        x = x.flatten(start_dim=1)
        x = self.fc1(x)
        x=  F.relu(x)
        x = self.fc2(x)
        x = F.relu(x)
        x = self.classifier(x)

        return x

```



## Training Model
> [!code]
```python
learning_rate = 3e-3

mlp_optimizer = optim.SGD(mlp_model.parameters(), lr=learning_rate)
cnn_optimizer = optim.SGD(cnn_model.parameters(), lr=learning_rate)

total_epochs = 2
# total_epochs = 5

print("Start MLP training...")
mlp_accuracy = train_model(mlp_model, mlp_optimizer, total_epochs)
print("Start CNN training...")
cnn_accuracy = train_model(cnn_model, cnn_optimizer, total_epochs)
```
> [!code] Output
> ![](Convolutional_Neural_Network.assets/image-20240401151258129.png)![](Convolutional_Neural_Network.assets/image-20240401151321004.png)



