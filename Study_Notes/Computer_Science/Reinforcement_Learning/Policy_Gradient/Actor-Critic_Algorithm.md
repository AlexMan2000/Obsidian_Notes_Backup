# Review on some Definitions
> [!important]
> ![](Actor-Critic_Algorithm.assets/6a95f9e0d97e92321560d61c620af99b_MD5.jpeg)![](Actor-Critic_Algorithm.assets/ec3bd8e210224a16753e3c6b047def68_MD5.jpeg)



# Improving PPO -> Actor Critic
## Motivations
> [!important]
> ![](Actor-Critic_Algorithm.assets/2f03c89d0b55674f512d251e9d064a13_MD5.jpeg)![](Actor-Critic_Algorithm.assets/5a2a33a9756d6768367c55bf1487d815_MD5.jpeg)



## Advantage Term
> [!def]
> ![](Actor-Critic_Algorithm.assets/96d147800b66b7bc6cfb640e61e82f7b_MD5.jpeg)

> [!code] How to estimate Advantage Term
> ![](Actor-Critic_Algorithm.assets/a5ea79426d43b9e8e36d8fbdf40b532f_MD5.jpeg)


## Valuing Function Fitting
> [!def]
> ![](Actor-Critic_Algorithm.assets/9705b10fccc9f5931652ddca5288f036_MD5.jpeg)![](Actor-Critic_Algorithm.assets/770fd0831c1ca8bd3dee8ab89c3f3009_MD5.jpeg)![](Actor-Critic_Algorithm.assets/e2f07cece3f881c5af7d87f2a2ebc207_MD5.jpeg)![](Actor-Critic_Algorithm.assets/7960e6e8be2c5f13ebe12693bacee76f_MD5.jpeg)


### Policy Evaluation
> [!def]
> ![](Actor-Critic_Algorithm.assets/21a106de55e9b957aeaff661aec05c54_MD5.jpeg)


### Monte Carlo Evaluation
> [!important]
> ![](Actor-Critic_Algorithm.assets/2b5d06f06e80d2a1d7b50186c75bafb3_MD5.jpeg)![](Actor-Critic_Algorithm.assets/b8dee530e46328445ce87648f7ddfb15_MD5.jpeg)![](Actor-Critic_Algorithm.assets/34e8042bf7347c788fac9293d423a847_MD5.jpeg)![](Actor-Critic_Algorithm.assets/4587b74d25ca6266674149a1ba7c1bff_MD5.jpeg)







## Discount Factors
> [!important]
> ![](Actor-Critic_Algorithm.assets/256c766247b71eae00d99a8a46b38542_MD5.jpeg)![](Actor-Critic_Algorithm.assets/8a96f695ee96f8dfb38a9ffd00a72634_MD5.jpeg)



 


# Actor-Critic Algorithm
## Motivations
> [!motiv]
> ![](Actor-Critic_Algorithm.assets/2974fc36103bdf79286f22400d997a8b_MD5.jpeg)




## Batch AC Algorithm
> [!algo]
> ![](Actor-Critic_Algorithm.assets/1ad87d6c10a517358f3e81ef4ef4ce60_MD5.jpeg)




## Online AC Algorithm
> [!algo]
> ![](Actor-Critic_Algorithm.assets/43085d2bcd07736bdf6d81e1494eb9c4_MD5.jpeg)

> [!proof]
> ![](Actor-Critic_Algorithm.assets/ee28404cd190c8687e70bcc14f68efe3_MD5.jpeg)![](Actor-Critic_Algorithm.assets/ce4e0f18887cfbd6be00e96bfed22771_MD5.jpeg)![](Actor-Critic_Algorithm.assets/9db63bedd01a6761b36e379cb9a10a70_MD5.jpeg)![](Actor-Critic_Algorithm.assets/3a7655c2c1e321d2923bf0a28eaa6d38_MD5.jpeg)



## Architecture Design
> [!important]
> ![](Actor-Critic_Algorithm.assets/27366899868156de8eac582506c61b19_MD5.jpeg)


### Actor
> [!important]
> A network $\pi_{\theta}(a|s)$ that takes a state, and return a distribution over actions at this state, i.e. $p(a_{t}|s_{t})$
> - **Purpose:** Represents the policy $\pi_{\theta}(a|s)$, where the actor predicts the probability distribution over actions given a state.
> - **Role:** It is updated to maximize the objective function (surrogate loss) while adhering to a clipped constraint to prevent large policy updates.
> - **Output:** Action probabilities (for discrete action spaces) or parameters of the action distribution (mean and standard deviation for continuous action spaces).
```python
class Actor(nn.Module):  
  
    def __init__(self, state_dim, action_dim, hidden_dim=256):  
        super().__init__()  
        self.fc1 = nn.Linear(state_dim, hidden_dim)  
        self.fc2 = nn.Linear(hidden_dim, hidden_dim)  
        self.fc_mean = nn.Linear(hidden_dim, action_dim)  
        self.fc_std = nn.Linear(hidden_dim, action_dim)  
        self.relu = nn.ReLU()  
        self.tanh = nn.Tanh()  
        self.softplus = nn.Softplus()  
  
    def forward(self, x):  
        x = self.relu(self.fc1(x))  
        x = self.relu(self.fc2(x))  
        mean = self.tanh(self.fc_mean(x)) * 2  
        std = self.softplus(self.fc_std(x)) + 1e-3  
  
        return mean, std  
  
  
    def select_action(self, s):  
        with torch.no_grad():  
            mu, sigma = self.forward(s)  
            normal_dist = Normal(mu, sigma)  # p(a_{t}|s_{t}) is N(mu(s), sigma(s))  
            action = normal_dist.sample()  
            action = action.clamp(-2.0, 2.0)  
        return action
```




### Critic
> [!important]
> - **Purpose:** Represents the value function $V_\phi(s)$, which estimates the expected return from a given state.
> - **Role:** Provides a baseline to reduce variance in the policy gradient and evaluates how good a state is.
```python
class Critic(nn.Module):  
    """  
    Value network, which takes an observation and outputs a value for that observation.    输出的是一个一维数值  
    """    def __init__(self, state_dim, action_dim, hidden_dim=256):  
        super().__init__()  
        self.fc1 = nn.Linear(state_dim, hidden_dim)  
        self.fc2 = nn.Linear(hidden_dim, hidden_dim)  
        self.fc3 = nn.Linear(hidden_dim, 1)  
        self.relu = nn.ReLU  
  
    def forward(self, s):  
        s = self.relu(self.fc1(s))  
        s = self.relu(self.fc2(s))  
        s = self.fc(s)  
        return s
```



### Reward Model
> [!important]


### Reference Model
> [!def]
> ![](Actor-Critic_Algorithm.assets/59d6405bb3518692f473252fa47e68b3_MD5.jpeg)






### ReplayMemory
> [!def]
> - **Purpose:** Stores trajectories of states, actions, rewards, and log probabilities for use during training.
> - **Role:** Collects data from interactions with the environment and processes it for mini-batch updates.
```python


```

 



# Policy Gradient vs Actor Critic
> [!important]
> ![](Actor-Critic_Algorithm.assets/c5d2b67520bab5efc640255d8021086b_MD5.jpeg)







# Trust-Region Methods
## Motivations
> [!motiv]
> ![](Actor-Critic_Algorithm.assets/47067339cff479c4b6aa6bf13280f321_MD5.jpeg)




## Proximal Policy Optimization
> [!algo]
> ![](Actor-Critic_Algorithm.assets/c890148a59d3f6a3f4d6d6d505b5ff3d_MD5.jpeg)

> [!important]
> ![](Policy_Gradient_Optimization.assets/b721c3e8295a10996d62c0e1ede216a1_MD5.jpeg)







