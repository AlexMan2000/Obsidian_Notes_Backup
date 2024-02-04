[Note21.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1685266598199-184c950f-17fd-41cf-8dc8-0a97c8497d64.pdf)
[Note22.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1685198753708-e0424f6d-75f0-49de-9078-b551f4250d35.pdf)
[Written_Notes21.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1685266598203-be4278ca-24eb-4119-a394-ec268b67407a.pdf)
[Written_Notes22.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1685236322419-a7ef2a1c-fb93-465e-9dc2-22c452986aa3.pdf)

# Basic Concepts
## Inner Products
> **Algebraic Definition:**
> ![image.png](Correlation_GPS.assets/20230722_0954378214.png)
> **Geometric Definition:**
> ![image.png](Correlation_GPS.assets/20230722_0954373246.png)
> **Properties:**
> ![image.png](Correlation_GPS.assets/20230722_0954422794.png)![image.png](Correlation_GPS.assets/20230722_0954426522.png)![image.png](Correlation_GPS.assets/20230722_0954428646.png)
> **Cauchy-Schwarz Inequality:**
> ![image.png](Correlation_GPS.assets/20230722_0954425013.png)![image.png](Correlation_GPS.assets/20230722_0954424111.png)



## Customized Inner Products
> ![image.png](Correlation_GPS.assets/20230722_0954439741.png)

**Problem (a)**![image.png](Correlation_GPS.assets/20230722_0954439515.png)![image.png](Correlation_GPS.assets/20230722_0954433355.png)![image.png](Correlation_GPS.assets/20230722_0954432837.png)
**Problem (b)**![image.png](Correlation_GPS.assets/20230722_0954438062.png)
**Problem (c)**![image.png](Correlation_GPS.assets/20230722_0954438050.png)
> 上述三问我们通过观察矩阵的形式就可以判断`Inner Product`是否满足定义。
> 本质上只需要看矩阵是否满足`SPSD`(对称正定矩阵)，因为`Linearity`一定满足。

**Problem (d) Frobenius Inner Product **⭐⭐⭐⭐⭐![image.png](Correlation_GPS.assets/20230722_0954431523.png)![image.png](Correlation_GPS.assets/20230722_0954434328.png)


## Special Vector Operations
> ![image.png](Correlation_GPS.assets/20230722_0954437246.png)




## Norms
> ![image.png](Correlation_GPS.assets/20230722_0954438019.png)![image.png](Correlation_GPS.assets/20230722_0954432592.png)![image.png](Correlation_GPS.assets/20230722_0954438950.png)



## Projection⭐⭐⭐⭐⭐
> ![image.png](Correlation_GPS.assets/20230722_0954449237.png)![image.png](Correlation_GPS.assets/20230722_0954441087.png)
> 🔔: 本质上如果我们要计算$\vec{x}$在$\vec{y}$上的投影，我们只需要知道$\vec{x}$和$\vec{y}$的内积和$\vec{y}$的模，然后根据
> $proj_{\vec{y}}\vec{x}=\frac{\langle \vec{x},\vec{y}\rangle}{\|\vec{y}\|^2}\vec{y}$
> 求出投影向量。

**Proof - Geometric****Method 1: Using Pythagorean Theorem**
![image.png](Correlation_GPS.assets/20230722_0954442081.png)
**Method 2: Using Orthogonality**
$\begin{aligned}(\vec{b}-\beta\vec{a})^{\top}\vec{a}&=0 \\ \vec{b}^{\top}\vec{a}&=\beta\vec{a}^{\top}\vec{a}\\\beta&=\frac{\langle \vec{a},\vec{b}\rangle}{\|\vec{a}\|^2}\end{aligned}$
所以$\vec{z}=\beta\vec{a}=\frac{\langle\vec{a},\vec{b}\rangle}{\|\vec{a}\|^2}\vec{a}$
**Proof - Algebraic, Minimization Problem**![image.png](Correlation_GPS.assets/20230722_0954445848.png)
> ![image.png](Correlation_GPS.assets/20230722_0954448725.png)

**Problem (a)**![image.png](Correlation_GPS.assets/20230722_0954447185.png)![image.png](Correlation_GPS.assets/20230722_0954459292.png)
**Problem (b)**![image.png](Correlation_GPS.assets/20230722_0954459674.png)


# Cauchy-Shwarz Inequality
> ![image.png](Correlation_GPS.assets/20230722_0954458225.png)![image.png](Correlation_GPS.assets/20230722_0954451359.png)

**Problem (a)**![image.png](Correlation_GPS.assets/20230722_0954455316.png)![image.png](Correlation_GPS.assets/20230722_0954457727.png)
**Problem (b)**![image.png](Correlation_GPS.assets/20230722_0954452447.png)
**Problem (c)**![image.png](Correlation_GPS.assets/20230722_0954451751.png)
**Problem (d)**![image.png](Correlation_GPS.assets/20230722_0954461783.png)
**Problem (e)**![image.png](Correlation_GPS.assets/20230722_0954469152.png)


# Signal 
## Signal Definition
> ** A signal is a message that contains information as a function of time.** Signals can also be functions of other variables, such as space (like in an image). However, for simplicity we’ll define them as a function of time, while knowing that they can be used more generally. 
> - **Discrete Time Signal: **The signal is only defined at specific points in time (for example, every minute).
> - **Continuous Time Signal: **The signal that is defined over all time.


## Vector Representation
> 对于离散信号来说，我们使用向量来表示:
> ![image.png](Correlation_GPS.assets/20230722_0954465592.png)
> 数学记号为$\vec{s}$, 其中$\vec{s}[k]$表示第$k$个时间步的信号大小。



# Correlations
## Cross Correlation
> 定义$\vec{x}$和$\vec{y}$是两个信号，长度均为$N$。则`Cross Correlation`是一个向量，长度为$N$。
> 1. **Linear Correlation:**
> 
![image.png](Correlation_GPS.assets/20230722_0954464540.png)
> **Assumptions:**
>    1. $\vec{x}[n],\vec{y}[n]=\begin{cases} \vec{x}[n],\vec{y}[n]& 0\leq n\leq N\\0&otherwise\end{cases}$
>    2. 如果$\vec{x}$和$\vec{y}$的长度不一样，则我们假设短的向量最后为零。
> 
![image.png](Correlation_GPS.assets/20230722_0954462890.png)
> 2. **Circular Correlation:**
> 
![image.png](Correlation_GPS.assets/20230722_0954462769.png)![image.png](Correlation_GPS.assets/20230722_0954475251.png)![image.png](Correlation_GPS.assets/20230722_0954478192.png)
> 3. **Periodic Correlation:**
> 
![image.png](Correlation_GPS.assets/20230722_0954471139.png)
> **Assumptions:**
>    1. The signal is repeating with period $N$。Different from Linear Correlation where the values outside of the defined range are zero.
>    2. To avoid infinite sum, we define periodic Correlation to be over just one period from $0$ to $N-1$



## Auto Correlation
> ![image.png](Correlation_GPS.assets/20230722_0954471731.png)



## Circulant Matrix
> **Definition:**
> ![image.png](Correlation_GPS.assets/20230722_0954477377.png)
> **Properties: **$\|\mathbf{C}_{\vec{x}}\vec{y}\| = \|\mathbf{C}_{\vec{y}}\vec{x}\|$
> **Proof:**
> ![image.png](Correlation_GPS.assets/20230722_0954487155.png)



## Numpy Command
> ![image.png](Correlation_GPS.assets/20230722_0954481295.png)
> `numpy.correlate([1,2,3],[1,2])`, 仅仅返回`[5,8]`, 这表明它仅仅计算了信号从左侧对齐到右侧对齐的所有值。
> `numpy.correlate([1,2,3],[1,2],"full")`, 仅仅返回`[2,5,8,3]`, 这表明它计算了两个信号从有重叠开始的所有值。



# Signal Detection Basics
[Signal_Detection.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1685279250853-68a8481a-500a-48b5-b757-cc78512ab8c9.pdf)

## Method 1: Error Vector
> 假设我们的`Receiver`收到的信号是$\vec{r}\in \mathbb{R}^{n}$, 而`Sender`发送的信号可能是$\vec{s}_1\in \mathbb{R}^{n}$或者$\vec{s_2}\in \mathbb{R}^{n}$, **这个方法假设**`**Receiver**`**和**`**Sender**`**的信号长度一致。**
> 定义`Error Vector`$\vec{e_1}=\vec{r}-\vec{s_1}$, $\vec{e_2}=\vec{r}-\vec{s_2}$。我们希望$\vec{e}$越小，则$\vec{s}$更有可能与$\vec{r}$匹配(出现在$\vec{r}$中)。



## Method 2: Inner Product
### Algorithm
> 假设我们的`Receiver`收到的信号是$\vec{r}\in \mathbb{R}^{m}$, 而`Sender`发送的信号可能是$\vec{s}_1\in \mathbb{R}^{n_1}$或者$\vec{s_2}\in \mathbb{R}^{n_2}$, 且$m\geq n$。**这个方法不假设**`**Receiver**`**和**`**Sender**`**的信号长度一致。**
> 则我们可以通过计算`Linear Cross Correlation`得到$\vec{r}$中是否存在$\vec{s_1}$或者$\vec{s_2}$, 以及如果存在$\vec{s_1}$或者$\vec{s_2}$, 其`Transmission Delay`$\tau$是多少。计算步骤:
> 1. 计算$corr_{\vec{r}}(\vec{s_1})\in \mathbb{R}^{n_1+m+1}$, 其中$corr_{\vec{r}}(\vec{s_1})$的`index`范围是$[-n_1, m]$。代码为`numpy.correlate(r, s1, "full")`。寻找使得$corr_{\vec{r}}(\vec{s_1})[k]\approx\|s_1\|^2$的第一个$k$作为`Delay`$\tau_1$。
> 2. 计算$corr_{\vec{r}}(\vec{s_2})\in \mathbb{R}^{n_2+m+1}$, 其中$corr_{\vec{r}}(\vec{s_2})$的`index`范围是$[-n_2, m]$。代码为`numpy.correlate(r, s2, "full")`。寻找使得$corr_{\vec{r}}(\vec{s_2})[k]\approx\|s_2\|^2$的第一个$k$作为`Delay`$\tau_2$。



### Assumptions
> 假设我们有:
> $\vec{s_1}=\begin{bmatrix} 1 & 1&-1&-1&1&1\end{bmatrix}^{\top}$
> $\vec{s_2}=\begin{bmatrix} 4 & -4&-4&4&4&4\end{bmatrix}^{\top}$
> $\vec{r}=\begin{bmatrix} 1 & 1&-1&-1&1&1\end{bmatrix}^{\top}$
> 则$\|\vec{s_1}\|=\sqrt{6}, \|\vec{s_2}\|=4\sqrt{6}$
> 现在我们采用`Method 2`进行`Singal Detection`, 则:
> $\langle \vec{r},\vec{s_1}\rangle=6=\|\vec{s_1}\|^2$, $\langle \vec{r},\vec{s_2}\rangle=8>6$
> 所以我们看到，即便$\vec{r}$和$\vec{s_1}$明显更接近，但是`Inner Product`却比$\vec{r}$和$\vec{s_2}$的更小。
> 为了解决这个问题，我们需要一个**重要假设: **$\|\vec{s_1}\|=\|\vec{s_2}\|$



### Example
> ![image.png](Correlation_GPS.assets/20230722_0954488672.png)



#### Example 1
> ![image.png](Correlation_GPS.assets/20230722_0954482767.png)
> **计算步骤如下:**
> ![image.png](Correlation_GPS.assets/20230722_0954488564.png)![image.png](Correlation_GPS.assets/20230722_0954489372.png)



#### Example 2
> ![image.png](Correlation_GPS.assets/20230722_0954484555.png)![image.png](Correlation_GPS.assets/20230722_0954487934.png)![image.png](Correlation_GPS.assets/20230722_0954495491.png)



## Method 1 vs Method 2
> 上述两种`Signal Detection`算法之间是有联系的，我们做如下推导:
> $\begin{aligned} \|\vec{e}\|^2 &= \vec{e}^{\top}\vec{e}\\&= (\vec{r}-\vec{s})^{\top}(\vec{r}-\vec{s})\\&=(\vec{r}^{\top}-\vec{s}^{\top})(\vec{r}-\vec{s})\\&=\|\vec{r}\|^2-2\langle\vec{s},\vec{r}\rangle+\|\vec{s}\|^2\end{aligned}$
> 所以当$\langle\vec{s},\vec{r}\rangle$足够大时，$\|\vec{e}\|$就会趋近于零。

 


## Sending Multiple Signals
> 假设接收端收到了$\vec{r}=\vec{s_1}+\vec{s_2}+\vec{n}$, 其中$\vec{n}$是高斯噪声，且：
> 1. $\|\vec{s_1}\|=\|\vec{s_2}\|$
> 2.  $\langle  \vec{s_1} ,\vec{s_2}\rangle =0$
> 3. 在$\vec{s_i}$的向量的长度足够大时，有 $\langle  \vec{n} ,\vec{s_i}\rangle\to 0$。
> 
则我们使用`Method 2`进行检测:
> $\begin{aligned} \langle \vec{r}, \vec{s_1}\rangle &= \langle \vec{s_1}+\vec{s_2}+\vec{n}, \vec{s_1} \rangle \\&= \langle \vec{s_1},\vec{s_1}\rangle + \langle \vec{s_2},\vec{s_1}\rangle + \langle \vec{n},\vec{s_1}\rangle \\&=\|\vec{s_1}\|^2 + \langle \vec{s_2},\vec{s_1}\rangle + \langle \vec{n},\vec{s_1}\rangle \\&= \|\vec{s_1}\|^2+0+small\end{aligned}$
> 结果为:
> ![image.png](Correlation_GPS.assets/20230722_0954493922.png)



# AutoFile Matching - Correlation
> ![image.png](Correlation_GPS.assets/20230722_0954494457.png)![image.png](Correlation_GPS.assets/20230722_0954492025.png)![image.png](Correlation_GPS.assets/20230722_0954493024.png)

**Problem (a)**![image.png](Correlation_GPS.assets/20230722_0954494921.png)
**Problem (b)**![image.png](Correlation_GPS.assets/20230722_0954499480.png)
**Problem (c) Mistake**![image.png](Correlation_GPS.assets/20230722_0954499256.png)
**Problem (d) Normalized Cross Correlation**![image.png](Correlation_GPS.assets/20230722_0954495245.png)
长度一样了(`Normalized`)那么内积的大小就取决于向量之间的夹角，夹角越小内积越大。

# GPS Problem
[Written_Notes22_2.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1685317102408-75813ee6-1b57-4cc9-865d-1993d9380108.pdf)
[aps1.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1686227127900-e45900a2-2b4d-4c46-9d34-3dd3975cbd26.pdf)
[aps2.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1686227127891-bb72803b-c4b9-4d62-8f6a-e6c3e062e828.pdf)

## Basic Concepts
> ![image.png](Correlation_GPS.assets/20230722_0954506721.png)![image.png](Correlation_GPS.assets/20230722_0954504410.png)



## Problem Settings
**What GPS receiver knows?**

1. Database Signal Sequence: $\vec{s_1}, \vec{s_2}, \cdots$。
2. Which satellite sends which sequence?
3. The position of the satellite.
4. When the signals are transmitted.

**What GPS receiver doesn't knows?**

1. **Which signal are present in the received signal?**
2. How much is the **transmission delay **$\tau$ of the signal from the sending satellite to the receiver.
3. Our **position **$\vec{x}$ on the GPS.

## GPS Satellite Assumptions
> ![image.png](Correlation_GPS.assets/20230722_0954509802.png)![image.png](Correlation_GPS.assets/20230722_0954516795.png)


## Calculate Time Delay
> ![image.png](Correlation_GPS.assets/20230722_0954519979.png)
> 假设我们的接收端收到的信号是$\vec{r}=a_1\vec{s_1}+a_2\vec{s_2}+\cdots+a_n\vec{s_n}$, 其中$\vec{s_n}$满足`GPS Assumptions`, 则我们需要对每一个$\vec{s_i}$计算$\hat{k_i}=\argmax_{k}corr_{\vec{r}}(\vec{s_i})[k]$, 如果$corr_{\vec{r}}(\vec{s_i})[\hat{k_i}]\approx \|\vec{s_i}\|$, 则$\vec{s_i}$这个信号从发送端被发送至接收端。
> 对于那些满足$corr_{\vec{r}}(\vec{s_i})[\hat{k_i}]\approx \|\vec{s_i}\|$的信号$\vec{s_i}$来说，假设其`Sampling Frequency`是$F_{\vec{s_i}}$。我们求出的$\hat{k_i}$实际上是`How many samples it takes from the sender to receiver`, 所以通过$\frac{samples}{F_{\vec{s_i}}}=\frac{samples}{\frac{samples}{second}}=seconds$得到的秒数就是我们的`Time Delay`。


## Calculating Distance
> 有了`Time Delay`, 我们就可以很方便的计算发送端到接收端的`Distance`。
> ![image.png](Correlation_GPS.assets/20230722_0954519547.png)


## Calculate Locations
> 在通过上一步计算出`Delay`并继而得到$\vec{d_i}$之后，我们可以开始计算$\vec{x}$：
> ![image.png](Correlation_GPS.assets/20230722_0954511928.png)![image.png](Correlation_GPS.assets/20230722_0954511030.png)
> 这里$\|\vec{a_i}\| 和\|\vec{d_i}\|$都是已知量。所以本质上我们需要解一个线性方程组$A\vec{x}=\vec{b}$。但是这个线性方程组很可能无解，比如我们出现了一些`Noisy Measurements`得到了下图中的结果, 此时$\vec{x}$就没有唯一解了，此时我们需要使用最小二乘法进行估计。
> ![image.png](Correlation_GPS.assets/20230722_0954515138.png)



## Colinear Problem
### Definition of Colinearity
![image.png](Correlation_GPS.assets/20230722_0954518651.png)
![image.png](Correlation_GPS.assets/20230722_0954525516.png)

### Unique Solution
![image.png](Correlation_GPS.assets/20230722_0954529004.png)![image.png](Correlation_GPS.assets/20230722_0954529660.png)
![image.png](Correlation_GPS.assets/20230722_0954526510.png)

### Non-unique Solutions
![image.png](Correlation_GPS.assets/20230722_0954524553.png)![image.png](Correlation_GPS.assets/20230722_0954521414.png)
![image.png](Correlation_GPS.assets/20230722_0954528790.png)
![image.png](Correlation_GPS.assets/20230722_0954529899.png)



# Gold Codes
## Basic Concepts
> ![image.png](Correlation_GPS.assets/20230722_0954524826.png)


## Sender Gold Codes
> ![image.png](Correlation_GPS.assets/20230722_0954528954.png)![image.png](Correlation_GPS.assets/20230722_0954528080.png)

```python
%pylab inline
import numpy as np
import matplotlib.pyplot as plt
import scipy.io
import sys

## RUN THIS FUNCTION BEFORE YOU START THIS PROBLEM
## This function will generate the gold code associated with the satellite ID using linear shift registers
## The satellite_ID can be any integer between 1 and 24
def Gold_code_satellite(satellite_ID):
    codelength = 1023
    registerlength = 10
    
    # Defining the MLS for G1 generator
    register1 = -1*np.ones(registerlength)
    MLS1 = np.zeros(codelength)
    for i in range(codelength):
        MLS1[i] = register1[9]
        modulo = register1[2]*register1[9]
        register1 = np.roll(register1,1)
        register1[0] = modulo
    
    # Defining the MLS for G2 generator
    register2 = -1*np.ones(registerlength)
    MLS2 = np.zeros(codelength)
    for j in range(codelength):
        MLS2[j] = register2[9]
        modulo = register2[1]*register2[2]*register2[5]*register2[7]*register2[8]*register2[9]
        register2 = np.roll(register2,1)
        register2[0] = modulo
    
    delay = np.array([5,6,7,8,17,18,139,140,141,251,252,254,255,256,257,258,469,470,471,472,473,474,509,512,513,514,515,516,859,860,861,862])
    G1_out = MLS1;
    shamt = delay[satellite_ID - 1]
    G2_out = np.roll(MLS2,shamt)
    
    CA_code = G1_out * G2_out
    
    return CA_code
```

## Receiver Listening
> ![image.png](Correlation_GPS.assets/20230722_0954533783.png)



## Modulation of Signal
> ![image.png](Correlation_GPS.assets/20230722_0954531054.png)



## Problem Settings
> ![image.png](Correlation_GPS.assets/20230722_0954533283.png)![image.png](Correlation_GPS.assets/20230722_0954531526.png)![image.png](Correlation_GPS.assets/20230722_0954537408.png)![image.png](Correlation_GPS.assets/20230722_0954533018.png)

**(a) Auto-correlation of gold code**
```python
def array_correlation(array1,array2):
    """ This function should return two arrays or a matrix with one row corresponding to 
    the offset and other to the correlation value. array1 and array2 do not have to be
    arrays of equal length. array2 is the argument that is shifted (i.e. the signature of the statellite), 
    array1 is the argument that is stationary, (i.e the received signal).
    """
    ## Use np.correlate with "FULL". Check out the helper page for it 
    correlated_array = np.correlate(array1,array2,'full')
    length1 = len(array1)
    length2 = len(array2)
    min_ind = min(length1,length2)
    max_ind = max(length1,length2)
    indices = np.linspace(-min_ind + 1, max_ind - 1, min_ind + max_ind -1)
    return (indices, correlated_array)
    
# Plot the auto-correlation of satellite 10 with itself. Your signal should be centered
# at offset = 0.
# Use plt.plot or plt.stem to plot.

array_10 = Gold_code_satellite(10)
(ind_10, self_10) = array_correlation(array_10,array_10)
plt.figure(figsize=(16,4))
plt.stem(ind_10,self_10)
```
![image.png](Correlation_GPS.assets/20230722_0954531813.png)![image.png](Correlation_GPS.assets/20230722_0954537732.png)
**(b) Cross Correlation of Golde Codes**
```python
array_13 = Gold_code_satellite(13)
(ind_10_13, cross_10_13) = array_correlation(array_10, array_13)#insert first agument, #insert second argument
plt.figure(figsize=(16,4))
plt.stem(ind_10_13,cross_10_13)
```
![image.png](Correlation_GPS.assets/20230722_0954537057.png)![image.png](Correlation_GPS.assets/20230722_0954539110.png)![image.png](Correlation_GPS.assets/20230722_0954544804.png)
![image.png](Correlation_GPS.assets/20230722_0954548643.png)
**(c) Cross Correlation of Golde Code with Integer Noise**
```python
def integernoise_generator(length_of_noise):
    noise_array = np.random.randint(2, size = length_of_noise)
    noise_array = 2 * noise_array - np.ones(size(noise_array))
    return noise_array
```
![image.png](Correlation_GPS.assets/20230722_0954543413.png)![image.png](Correlation_GPS.assets/20230722_0954542530.png)
**(d) Cross Correlation of Golde Code with Gaussian Noise**
```python
def gaussiannoise_generator(length_of_noise):
    noise_array = np.random.normal(0,1,length_of_noise)
    return noise_array
```
![image.png](Correlation_GPS.assets/20230722_0954541927.png)![image.png](Correlation_GPS.assets/20230722_0954544296.png)
**(e) Singal Detection with Noise**
```python
## THIS IS A HELPER FUNCTION FOR PART E, F AND G

## This function returns a 1 if peak (greater than threshold or less than -threshold) is found else it returns a 0.
def find_peak(correlation,threshold):
    max_value = np.amax(correlation)
    min_value = np.amin(correlation)
    if max_value > threshold:
        ret_value = 1
    elif min_value < -1*threshold:
        ret_value = 1
    else:
        ret_value = 0
    return ret_value
```
```python
# Part E
## 'np.load' FUNCTION IS USED TO LOAD THE RECIEVED SIGNAL DATA
signal1 = np.load('data1.npy')
visible_sat_e = np.zeros(24) #this can be used to keep track of which satellites are visible
thresh = 800


# YOUR CODE HERE --- A skeleton that might be useful is provided, you may write this in any other way:
for sat_ID in np.arange(1,24):
    gold_code = Gold_code_satellite(sat_ID)
    #YOUR CODE HERE
    #find the correlation of the signal with the gold code of each satellite
    #then find if any of the correlations cross the threshold value using the find-peak function
    (ind, cross) = array_correlation(signal1, gold_code)
    print(find_peak(cross, thresh))
```
![image.png](Correlation_GPS.assets/20230722_0954541050.png)![image.png](Correlation_GPS.assets/20230722_0954544330.png)
**(f) Find the sender and decode the Message**![image.png](Correlation_GPS.assets/20230722_0954545495.png)![image.png](Correlation_GPS.assets/20230722_0954547991.png)
![image.png](Correlation_GPS.assets/20230722_0954548208.png)
**(g) Locate the Peak**![image.png](Correlation_GPS.assets/20230722_0954547654.png)
![image.png](Correlation_GPS.assets/20230722_0954554551.png)



# *Noise Cancellation Headphone
> 



