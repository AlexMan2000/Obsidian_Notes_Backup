> Fa20

[lab01.zip](https://www.yuque.com/attachments/yuque/0/2023/zip/12393765/1673579836785-cd409ec8-7275-4a90-8699-6afbfdffb0a8.zip)

# Q1 Prerequisites
## Q1a summation
> ![image.png](./Lab_01__Prerequisite_Coding.assets/20230302_2122065406.png)



## Q1b zip
> ![image.png](./Lab_01__Prerequisite_Coding.assets/20230302_2122062125.png)

```python
def elementwise_list_sum(list_1, list_2):
    """Compute x^2 + y^3 for each x, y in list_1, list_2. 
    
    Assume list_1 and list_2 have the same length.
    """
    assert len(list_1) == len(list_2), "both args must have the same number of elements"
    return [pow(x,2) + pow(y,3) for x,y in zip(list_1,list_2)]
    ...
```


## Q1c variance
> ![image.png](./Lab_01__Prerequisite_Coding.assets/20230302_2122069469.png)

```python
def mean(population):
    """
    Returns the mean of population (mu)
    
    Keyword arguments:
    population -- a numpy array of numbers
    """
    # Calculate the mean of a population
    return sum(population) / len(population)
    ...

def variance(population):
    """
    Returns the variance of population (sigma squared)
    
    Keyword arguments:
    population -- a numpy array of numbers
    """
    # Calculate the variance of a population
    N = len(population)
    return sum([pow(x_i - mean(population),2) for x_i in population]) / N
    ...
```



# Q2 Numpy
> ![image.png](./Lab_01__Prerequisite_Coding.assets/20230302_2122066694.png)![image.png](./Lab_01__Prerequisite_Coding.assets/20230302_2122071273.png)



# Q3 Numpy Arrays
[NumpyReview.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1673581003284-78f85217-9632-42dc-8289-ba3058f9a821.pdf)
## Q3a Boolean Indexing
> ![image.png](./Lab_01__Prerequisite_Coding.assets/20230302_2122075875.png)

```python
np.random.seed(42)
random_arr = np.random.rand(60)
valid_values = random_arr[2 * random_arr ** 4 > 1]
```

## Q3b Numpy Operations
> ![image.png](./Lab_01__Prerequisite_Coding.assets/20230302_2122077341.png)

```python
def elementwise_array_sum(list_1, list_2):
    """Compute x^2 + y^3 for each x, y in list_1, list_2. 
    
    Assume list_1 and list_2 have the same length.
    
    Return a NumPy array.
    """
    assert len(list_1) == len(list_2), "both args must have the same number of elements"
    return np.power(np.array(list_1), 2) + np.power(np.array(list_2), 3)
```
> ![image.png](./Lab_01__Prerequisite_Coding.assets/20230302_2122074267.png)




# Q4 Plotting
> ![image.png](./Lab_01__Prerequisite_Coding.assets/20230302_2122071478.png)![image.png](./Lab_01__Prerequisite_Coding.assets/20230302_2122073344.png)

**Solution to Q4a and Q4b**![image.png](./Lab_01__Prerequisite_Coding.assets/20230302_2122083982.png)
```python
def f(x):
    return np.square(np.array(x))
    
def df(x):
    return 16 * np.array(x) - 64

def plot(f, df):              
    x_axis = np.arange(-15,16)
    y_axis = np.arange(-100, 300)
    plt.figure(figsize=(4,4))
    plt.plot(x_axis, f(x_axis), color = 'blue')
    plt.plot(x_axis, df(x_axis), color = 'yellow')
    plt.xlim(-15,15)
    plt.ylim([-100,300])
    plt.grid(b='True')
    plt.axhline(y = 0, color = "orange")
    plt.show()

plot(f, df)
```


# Q5 Random Sampling
## Q5a Coin Toss
> ![image.png](./Lab_01__Prerequisite_Coding.assets/20230302_2122086877.png)

**Solution**![image.png](./Lab_01__Prerequisite_Coding.assets/20230302_2122081825.png)



## Q5b MLE
> ![image.png](./Lab_01__Prerequisite_Coding.assets/20230302_2122081667.png)

```python
p_hat = 0.4  # From the graph
p_hat
```


# Q6 Comments
> ![image.png](./Lab_01__Prerequisite_Coding.assets/20230302_2122085689.png)
> [add_subplots](https://blog.csdn.net/You_are_my_dream/article/details/53439518)(...), 第一个参数是几行，第二个参数是几列，第三个参数是第几个子图。

**Solution**![image.png](./Lab_01__Prerequisite_Coding.assets/20230302_2122097101.png)

# Q7 Open Question(Skipped)
> ![image.png](./Lab_01__Prerequisite_Coding.assets/20230302_2122092545.png)



# Q8 Trignometric Waves
> ![image.png](./Lab_01__Prerequisite_Coding.assets/20230302_2122095623.png)![image.png](./Lab_01__Prerequisite_Coding.assets/20230302_2122091827.png)
> 如果有版本冲突导致`axes.set_xticks(ticks, labels)`的`labels`参数无效时，可以尝试下面的两行代码解决:
> `pip install --upgrade matplotlib`
> `pip install matplotlib --force-reinstall --user`

```python
import itertools

# Higher-Order Functions
def function_factory(a, f):
    def func(t):
         return a * np.sin(2 * np.pi * f * t)  
    func.a = str(a)
    func.f = str(f)
    return func
        
# Draw a single plot on the given subplot
def plot(f, ax):
    x_axis = np.arange(0, np.pi, 0.001)
    ax.plot(x_axis, f(x_axis), color="blue", linewidth = 4)
    ax.set_xlim(0, np.pi)
    ax.set_ylim(-10, 10)
    ax.set_xticks([0, np.pi/2, np.pi], labels=["0", "π/2", "π"])
    ax.set_yticks([-10, -5, 0, 5, 10])
    ax.set_xlabel(f'a: {f.a}')
    ax.set_ylabel(f'f: {f.f}')
    return
 

# Draw the 2 x 2 plot on the same canvas
def main_plot(row, column, param_list):
    """
    row: number of rows on the canvas
    column: number of columns on the canvas
    """
    assert row * column >= len(param_list), "Insufficient number of subplots"
    # Create a canvas
    fig = plt.figure(figsize = (12, 12))
    fig.suptitle(f'Sine waves with varying a={str(param_list[0])}, f={str(param_list[1])}')
    param_list = list(itertools.product(param_list[0], param_list[1]))
    for i in range(len(param_list)):
        param_int = (i + 1) + column * 10 + row * 100
        a, f = param_list[i]
        func = function_factory(a,f)
        ax = fig.add_subplot(param_int)
        plot(func, ax)
        
    plt.subplots_adjust()
    plt.show()
    return 0
    
main_plot(2, 2, [[2, 8], [2, 8]])
```
