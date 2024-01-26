# Poisson Process



# Galton-Watson Branching Process
> [!def]
> The **Galton-Watson branching process** is a mathematical model used to describe the **dynamics of populations**, particularly in contexts where members of the **population reproduce independently** of each other.
> We use:
> - $\{X_n\}_{n\geq 0}$ to represent this random process where $X_n$ means the total population at $n$-th generation. 
> - $\epsilon^{n,k}$ is a random variable that denotes the number of people the $k$-th individual of $n$-th generate gave birth to. 
> - $\epsilon^{n,k}$ are assumed to have the same distribution as $\epsilon$
> 
> Then this process can be modeled as follows(if we start with 1 individual):
> 1. At the 0-th generation, we have $X_0=1$, we start with 1 person.
> 2. At the 1st generation, we have $X_1=\epsilon^{0,1}$, since we want to know how many people are born by the 0-th generation guys.
> 3. At the 2nd generation, we have $X_2=\sum\limits_{i=1}^{X_1}\epsilon^{1,i}$
> 4. Generally, for any $n$, we have the following recurrence: $$X_{n+1}=\sum\limits_{j=1}^{X_n}\epsilon^{n,j}$$
>

> [!example] Fa23 Disc03 P2
> ![](Random_Process.assets/image-20240125231255199.png)![](Random_Process.assets/image-20240125231302892.png)![](Random_Process.assets/image-20240125231310048.png)
> Calculation Details:
> $$\begin{aligned}\operatorname{Var}\left[X_n \mid X_{n-1}\right] & =E\left[\left(X_n-E\left[X_n \mid X_{n-1}\right]\right)^2 \mid X_{n-1}\right] \\& =E\left[\left(X_n-\mu X_{n-1}\right)^2 \mid X_{n-1}\right] \\& =E\left[X_n^2 \mid X_{n-1}\right]-2 E\left[X_n \mid X_{n-1}\right] \cdot X_{n-1} \cdot\mu \\&+\mu^2 X_{n-1}^2\\&=E\left[(\sum\limits_{j=1}^{X_{n-1}}\epsilon^j)^2 \mid X_{n-1}\right]-\mu^2 X_{n-1}^2\\&=E\left[\sum\limits_{j=1}^{X_{n-1}}(\epsilon^j)^2 \mid X_{n-1}\right]-\mu^2 X_{n-1}^2\\&=X_{n-1}E\left[\sum\limits_{j=1}^{X_{n-1}}(\epsilon^j)^2 \mid X_{n-1}\right]-\mu^2 X_{n-1}^2\\&=X_{n-1}E\left[\sum\limits_{j=1}^{X_{n-1}}(\epsilon^j)^2\right]-\mu^2 X_{n-1}^2 \\&=X_{n-1}(\sigma^2+\mu^2-\mu^2)\\&=\sigma^2X_{n-1}\end{aligned}$$








