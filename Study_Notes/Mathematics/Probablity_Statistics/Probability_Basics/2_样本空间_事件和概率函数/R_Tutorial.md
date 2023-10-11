# 1 Basics
[R Tutorial 1A: Basics](https://ocw.mit.edu/courses/18-05-introduction-to-probability-and-statistics-spring-2014/pages/r-tutorial-1a-basics/)
## 1.1 基本计算
> 包含加减乘除，注意`/`除法不是整数除法

```r
> 2+3
[1] 5
> 2*3
[1] 6
> 2/3
[1] 0.6666667
> 2^3
[1] 8
> 2*(3+1)^2
[1] 32
```

## 1.2 变量声明
> 两种方式: `=`和`<-`

```r
> x = 2+3
# When you assign a value to a variable, 
# it does not echo the answer to the screen.
# You can see the value of x by just using x as a command.
>x
[1] 5
> y = 1+2
> x*y
[1] 15
> z = x^y
> z
[1] 125


# R has another notation for assignment: the arrow: <- . 
# Many R programmers use this. 
# It may seem odd to programmers coming from other languages.
> x <- 3
> x
[1] 3
> x <- 5.412
> x
[1] 5.412
```

## 1.3 向量声明**⭐⭐⭐**
> 1. 使用`c(1,2,3,4)`创建向量$\begin{bmatrix} 1\\2\\3\\4\end{bmatrix}$
> 2. 使用`1:4`创建向量$\begin{bmatrix} 1\\2\\3\\4\end{bmatrix}$

```r
# A vector with 4 entries
> c(1, 2, 3, 4)
[1] 1 2 3 4
# You can store vectors in variables.
> x = c(1.1, 0.0, 3.14, 2.718)
> x
[1] 1.100 0.000 3.140 2.718

# Of course using the arrow instead of equal sign works here.
> x <- c(2,4,6)
> x
[1] 2 4 6

# Sequences of integers are so common that 
# there is a shortcut for making them.
> 1:4
[1] 1 2 3 4
> 3:10
[1]  3  4  5  6  7  8  9 10
> 9:2
[1] 9 8 7 6 5 4 3 2

# A long vector will be displayed over several lines. At
# the start of each line in brackets is the index of the first entry 
# on that line.
> x = 1:40
> x
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 
 [15] 15 16 17 18 19 20 21 22 23 24 25 26 27 28 
 [29] 29 30 31 32 33 34 35 36 37 38 39 40
```

## 1.4 向量计算**⭐⭐⭐⭐**
> 和`numpy`中的向量对象一样，都有传播机制。

```r
> x = c(1,3,5)
> x + 7.1
[1]  8.1 10.1 12.1

# Subtraction, multiplication, division and powers work the same way.
> x = c(1,3,5)
> 7*x
[1]  7 21 35
> x/7
[1] 0.1428571 0.4285714 0.7142857
> 7/x
[1] 7.000000 2.333333 1.400000
> x^6
[1]     1   729 15625
> x^7
[1]     1  2187 78125
> 7^x
[1]     7   343 16807
```


## 1.5 获取向量分量
> 假设$\bf x$是向量$\bf x=\begin{bmatrix} x_1\\x_2\\x_3\\x_4 \end{bmatrix}$
> 1. 通过`**x[i]**`访问向量$\bf x$的第$i$个分量$\bf x_i$
> 2. 通过`**x[c(1,2,3)]/x[1:3]**`访问向量$\bf x$的第$1,2,3$个分量的切片向量$\bf x'=\begin{bmatrix} x_1\\x_2\\x_3 \end{bmatrix}$
> 3. 通过`**x[c(2,2,2,1)]**`重复访问向量$\bf x$的分量切片$\bf x'=\begin{bmatrix} x_2\\x_2\\x_2\\x_1 \end{bmatrix}$

```r
# 获取一个分量
# Entries in vectors are found with the notation x[j]
> x = c(2,4,6,8,10)
> x[1]
[1] 2
> x[2]
[1] 4
> x[3]
[1] 6
> x[4]
[1] 8


# 一次获取多个分量
# R allows you to access more than one entry at a time
# x has 8 elements
> x = 2*c(1,2,3,4,5,6,7,8)
> x
[1]  2  4  6  8 10 12 14 16

# Notice that we have to put a vector of indices inside 
# the brackets to access the first and second entries in x
> x[c(1,2)]
[1] 2 4
> x[c(1,3,5)]
[1]  2  6 10
# We can access the same entry multiple times.
> x[c(2,2,2,1)]
[1] 4 4 4 2
# Using the colon method of creating vectors is useful here.
> x[2:5]
[1]  4  6  8 10
```

## 1.6 向量操作函数
> `sin(x)/cos(x)/exp(x)/sum(x)/mean(x)`都很直观,都有广播机制

```r
# We'll start with functions numbers
> sin(1)
[1] 0.841471

> sin(1.4)
[1] 0.9854497

> sin(3)
[1] 0.14112

# R knows about pi
> pi
[1] 3.141593

> sin(pi/2)
[1] 1
> sin(pi/2)

# The exponential function is given by 'exp'.
> exp(0)
[1] 1

> exp(1)
[1] 2.718282

# Sin acts on vectors by taking the sin of each element.
> x = c(1,2,3,4)
> x
[1] 1 2 3 4
> sin(x)
[1]  0.8414710  0.9092974  0.1411200 -0.7568025

# exp also acts on vectors.
> x = c(1,2,3,4)
> exp(x)
[1]  2.718282  7.389056 20.085537 54.598150

# In 18.05 we will use the sum and mean functions on vectors. They take the sum and average respectively of the vectors entries
> x = 1:6
> x
[1] 1 2 3 4 5 6
> sum(x)
[1] 21
> mean(x)
[1] 3.5

# Example: find the sum of the integers from 1 to 1024.
> x = 1:1024
> sum(x)
[1] 524800

# This can be done in one command.
> sum(1:1024)
[1] 524800

# Example: find the sum of the squares of the integers from 1 to 1024.
> x = 1:1024
> sum(x^2)
[1] 358438400

# This can be done in one command.
> sum((1:1024)^2)
[1] 358438400
```

## 1.7 矩阵声明
> $R$语言创建矩阵有一些复杂, 创建步骤如下:
> 1. 创建一个向量$\bf x=[1,2,...,10]$
> 2. 本质是调用`matrix(x,nrow=2,ncol=5,byrow=True)`
> 
整个过程类似于`numpy`中将一个一维向量`reshape`之后得到二维矩阵

```r
# A vector of length 10 can be arranged as
a 2x5 or a 5x2 matrix
# Again the syntax is clunky but very clear
> x = 1:10
> x
 [1]  1  2  3  4  5  6  7  8  9 10
> y = matrix(x,nrow=2,ncol=5)
> y
     [,1] [,2] [,3] [,4] [,5]
[1,]    1    3    5    7    9
[2,]    2    4    6    8   10
> z = matrix(x,nrow=5,ncol=2)
> z
     [,1] [,2]
[1,]    1    6
[2,]    2    7
[3,]    3    8
[4,]    4    9
[5,]    5   10

# Notice in the examples above that R builds the matrices
# one column at a time. That is, our vector 1 to 10 runs in
# sequence down the columns. For 18.05 this is usually fine. 

# However the matrix() function, like most R functions, 
# has a lot of optional parameters that allow you to control 
# its behavior. Here's how to make it buid a matrix by rows
> z = matrix(x,nrow=2,ncol=5, byrow = TRUE)
> z
     [,1] [,2] [,3] [,4] [,5]
[1,]    1    2    3    4    5
[2,]    6    7    8    9   10
```

## 1.8 获取矩阵元素
> 获取矩阵元素`matrix[i,j]`

```r
> x = 1:10
> y = matrix(x,nrow=2,ncol=5)
> y
     [,1] [,2] [,3] [,4] [,5]
[1,]    1    3    5    7    9
[2,]    2    4    6    8   10
> y[1,1]
[1] 1
> y[2,3]
[1] 6
```


## 1.9 矩阵求和与平均
> `sum(m)`求矩阵所有元素的和
> `colSums(m)/colMeans(m)`: 按列求和，返回一个向量
> `rowSums(m)/rowMeans(m)`: 按行求和，返回一个向量

```r
# Start by creating a matrix to practice on.
> x = 1:10
> y = matrix(x,nrow=2,ncol=5)
> y
     [,1] [,2] [,3] [,4] [,5]
[1,]    1    3    5    7    9
[2,]    2    4    6    8   10

# To sum each of the columns we use the colSums function. 
> y
     [,1] [,2] [,3] [,4] [,5]
[1,]    1    3    5    7    9
[2,]    2    4    6    8   10

# y has five columns so colSums(y) produces 5 numbers.
> colSums(y)
[1]  3  7 11 15 19

# y has two rows so rowSums(y) produces 2 numbers.
> rowSums(y)
[1] 25 30


# Likewise rowMeans(y) and colMeans(y):
> rowMeans(y)
[1] 5 6
> colMeans(y)
[1] 1.5 3.5 5.5 7.5 9.5
```

## 1.10 帮助文档
```r
# R and RStudio have complete documentation on all R functions. 
# The lower right window in RStudio has a help tab you can use. 
# The help contains a lot of information, 
# so you will have to learn to filter out what you don't need.

# It's often faster to ask for help from the command line 
# using a question mark.
> ?mean
# Try it, the result will appear in the help window.
```


# 2 Random Numbers
[R Tutorial 1B: Random Numbers](https://ocw.mit.edu/courses/18-05-introduction-to-probability-and-statistics-spring-2014/pages/r-tutorial-1b-random-numbers/)
## 2.1 dim 函数**⭐⭐**
```r
# The dim() function   
# We can always check that x has 4 rows and 1000 columns 
# using the dim() function.   
> dim(x)   
[1]    4 1000
```
## 2.2 sample 函数**⭐⭐⭐⭐**
> `sample(x, k, replace = FALSE)`: 从`x`中随机抽取`k`个不重复元素, 且`k<=length(x)`，默认行为
> `sample(x, k, replace = TRUE)`: 从`x`中随机抽取`k`个元素, 允许重复

```r
# start with a vector x with 5 elements. 
> x = 1:5 
> x 
[1] 1 2 3 4 5

# randomly sample 3 of the elements of x.
> sample(x,3) 
[1] 2 5 1 
> sample(x,3) 
[1] 3 1 4 
> sample(x,3) 
[1] 1 2 5 
# Note every element is chosen at most once.

# randomly sampling 5 elements of x is a permutation of all 5 elements.
> sample(x,5) 
[1] 1 3 2 5 4 
> sample(x,5) 
[1] 2 3 1 4 5

# You can't pick more than 5 different elements from a set of 5 things, 
# so R gives an error.&nbsp; 
> sample(x,6) 
Error in sample.int(length(x), size, replace, prob) :&nbsp;&nbsp; 
 cannot take a sample larger than the population when 'replace = FALSE'
```

```r
# Note that we get can get repeated values&nbsp; 
> sample(x,3,replace=TRUE) 
[1] 3 1 4 
> sample(x,3,replace=TRUE) 
[1] 4 5 4 
> sample(x,3,replace=TRUE) 
[1] 2 1 5 
> sample(x,5,replace=TRUE) 
[1] 5 1 5 1 4 
> sample(x,5,replace=TRUE) 
[1] 3 5 5 2 1 
> sample(x,5,replace=TRUE) 
[1] 4 2 3 2 1


# Now there is no problem asking for more than 5 things from a set of 5 elements.&nbsp; 
> sample(x,12,replace=TRUE) 
[1] 1 1 2 1 4 2 3 4 1 2 4 5 
> sample(x,12,replace=TRUE) 
[1] 3 2 5 1 4 2 4 1 4 5 3 1


# Generate a 3 x 4 array of random dice rolls.
> y = sample(1:6, 12, replace=TRUE) 
> matrix(y,nrow=3,ncol=4) 
     [,1] [,2] [,3] [,4] 
[1,]    1    3    6    1
[2,]    2    2    3    6
[3,]    2    1    4    3


# Or we could make it a 2 x 6 array.   
> matrix(y,nrow=2,ncol=6)  
     [,1] [,2] [,3] [,4] [,5] [,6]
[1,]    1    2    2    6    4    6
[2,]    2    3    1    3    1    3
```
## 
## 2.3 Simulation**⭐⭐⭐⭐⭐**
### 2.3.1 模拟掷骰子3次
> 模拟掷骰子3次, 并验证是否有某一次投掷点数为`6`

```r
# First we use sample to generate 3 samples from 1:6   
> x = sample(1:6,3, replace=TRUE)  
> x  
[1] 6 4 1

# To check if any of the 3 rolls are 6 we use the following command. It returns a vector of TRUE or FALSE depending on whether that entry of x is 6 or not. Note the use of the double equal sign. We can't use a single equal sign because that would mean 'set the value of x to 6'. Compare the result with the value of x above.   
> x == 6  
[1] TRUE FALSE FALSE
```
### 
### 2.3.2 平均点数
> 模拟掷骰子`1000`次:
> - 验证投掷点数为`6`的次数$\approx \frac{5000}{6}$
> - 验证投掷点数为`6`的概率$\approx \frac{1}{6}$
> 
`R`和脚本语言`Python`, `Javascript`一样，`Boolean`的变量在做数值运算的时候会隐式转换成`1/0`

```r
# Simulate 1000 rolls   
> x = sample(1:6,1000, replace=TRUE)

# x == 6 gives a vector of TRUE or FALSE. 
# R is clever, when we sum the vector: 
# each TRUE counts as 1 and each FALSE counts as 0. 
# So the sum is the number of TRUE's. 
# In this case that means the number of 6's, which happens to be 168.    
> sum(x == 6)   
[1] 168


# Divide by 1000 to get the fraction of 6's.   
> sum(x == 6)/1000   
[1] 0.168


# Compare that with the theoretical value of 1/6.   
> 1/6   
[1] 0.1666667   
# Not bad!
```

### 2.3.3 统计1
> **模拟**: 掷骰子$4$次至少一次点数为$6$的概率，将其抽象为事件$\bf A$. 使用统计思想估算概率
> **下面是每行代码的解释: **
> `**Command 1**`: 生成一个$4\times10$的矩阵，每一列代表一次试验，也就是事件$\bf A$
> ** **`**Command 2**`: 打印`x`
> `**Command 3**`: 查看哪些`Entries`是点数为`6`的
> `**Command 4**`: 打印`y`
> `**Command 5**`: 按列求和，得到一个`Boolean`向量，代表每次实验中是否出现了`6`的次数
> `**Command 6**`: 打印`z`
> `**Command 7**`: 出现过$6$的实验都转化为`True`
> `**Command 8**`: 统计$10$次实验中有几次出现了$6$
> `**Command 9**`: 取平均 $5/10 = 0.5$.得到事件$\bf A$的概率。
> 总体逻辑是: 我模拟进行$n$次试验，然后统计$n$次实验中有多少次试验满足事件$\bf A$,求出这个数值即为事件$\bf A$发生的概率

```r
> x = matrix(sample(1:6, 4*10, replace=TRUE), nrow=4, ncol=10)   
> x   
> y = (x==6)   
> y   
> z = colSums(y)   
> z   
> z > 0   
> sum(z > 0)   
> mean(z > 0)   
```
```r
# Let's repeat this but with 1000 trials instead of 10.
# Without all the comments it's pretty short.   
> x = matrix(sample(1:6, 4*1000, replace=TRUE), nrow=4, ncol=1000)   
> y = (x==6)   
> z = colSums(y)   
> sum(z > 0)   
[1] 525   
> mean(z>0)   
[1] 0.525
```

### 2.3.4 统计2
```r
# Goal: estimate the probability of getting a sum   
# of 7 when rolling two dice.   
> ntrials = 10000   
> x = matrix(sample(1:6, 2*ntrials, replace=TRUE), nrow=2, ncol=ntrials)   
> y = colSums(x)   
> mean(y == 7)   
[1] 0.1658
```

## 2.4 练习
> 统计: 估算事件$\bf P$: 扔两次骰子，两次都是$6$的概率。

```r
ntrials = 1000
x = matrix(sample(1:6,2*ntrials,replace=TRUE),nrow=2,ncol=ntrials)
y = colSums(x==6)
z = (y==2)
p = mean(z)
```

# 3 Run For Loops**⭐⭐**
[R Tutorial: Run For Loops](https://ocw.mit.edu/ans7870/18/18.05/s14/html/r-tut-forloop.html)
## 3.1 rep 函数
> 一般用于初始化$\bf 0$向量

```r
rep()
# Often we want to start with a vector of 
# 0's and then modify the entries in later code. 
# R makes this easy with the replicate function rep()

# rep(0, 10) makes a vector of of 10 zeros.
x = rep(0,10)
x
[1] 0 0 0 0 0 0 0 0 0 0

# rep() will replicate almost anything
x = rep(2,6)
x
[1] 2 2 2 2 2 2

x = rep('abc',5)
x
[1] "abc" "abc" "abc" "abc" "abc"


# 重复一个向量
x = rep(1:4,5)
x
[1] 1 2 3 4 1 2 3 4 1 2 3 4 1 2 3 4 1 2 3 4

```


## 3.2 for loop
```r
# 'for loops' let us repeat (loop) 
# through the elements in a vector and run the same code on each element

# We will illustrate with examples 

# Loop through the sequence 1 to 5 printing the square of each number
for (j in 1:5)
{
  print(j^2)
}
 class='r'>[1] 1
[1] 4
[1] 9
[1] 16
[1] 25

# We can capture the results of our loop in a list
# First we create a vector and then we fill in its values
n = 5
x = rep(0,n)
for (j in 1:n)
{
  x[j] = j^2
}
x
 class='r'>[1]  1  4  9 16 25

# You always wanted to know the sum of the first 100 squares.
n = 100
x = rep(0,n)
for (j in 1:n)
{
  x[j] = j^2
}
sum(x)
 class='r'>[1] 338350

# Let's use a for loop to estimate the average of squaring the result of a roll of a die.
nsides = 6
ntrials = 1000
trials = rep(0,ntrials)
for (j in 1:ntrials)
{
  trials[j] = sample(1:nsides,1)  # We get one sample at a time
}
mean(trials^2)
[1] 15.207

# Of course we could have done this simulation without a loop.

# for loops are truly valuable when the calculation is more complicated and we can't do it exactly or with built in R functions.

# Let's estimate the probability of a derangement in a permutation of 9 objects. (A derangement is a permutation where no element ends up in its original position.)
n = 9
x = 1:n
ntrials = 10000
trials = rep(0,ntrials)
for (j in 1:ntrials)
{
    y = sample(x,n)
    s = sum(y == x)  # s = number of people in their original seat
    trials[j] = (s == 0) # 1 if a derangement, 0 if not
}
mean(trials)  # mean(trials) = fraction that are 1's
[1] 0.3697

```

# 4 Run Length Encoding**⭐⭐⭐**
[R Tutorial: Run Length Encoding](https://math.mit.edu/~dav/05.dir/r-tut-rle.html)
## 4.1 术语
> `run`: 代表一组重复连续的数字, 对于向量`1,1,2,2,3,3,3`来说:
> - 序列`1,1`是一个`run`
> - 序列`2,2`是一个`run`
> - 序列`3,3,3`是一个`run`


## 4.2 rle 函数
> `**rle(vec)**`**: 接收一个序列，或者向量，返回一个**`**rle**`**对象， 包含对这个序列中的**`**runs**`**的统计结果，可以通过**`**对象$属性**`**获取**`**rle**`**对象上的属性**
> `rle对象`:
> - `lengths`属性: 分段连续统计结果，一个向量
> - `values`属性: 分段连续统计的对象，一个向量

```r
# rle(x) stands for 'run length encoding'. 
# It will be easiest to explain what this means through examples. 
# It will help with pset 2 in the question that asks you to estimate 
# the probability of runs in a sequence of Bernoulli (coin flips) trials.  
# A run means a streak of repeats of the same number.  

# First let's make a small sequence where we can see the runs
> x = c(1,1,1,2,3,3,3,1,1)
# We can describe this sequence as: three 1's, then one 2, 
# then three 3's and two 1's.

# This is exactly what rle(x) shows us
> y = rle(x)
> y
Run Length Encoding
  lengths: int [1:4] 3 1 3 2
  values : num [1:4] 1 2 3 1
# The values vector shows the values in the order they appeared. In this case the values of x are: 1, 2, 3, 1.

# The lengths vector shows the lengths of the runs of each value. In this case,
# three 1's, one 2, three 3's and two 1's.

# To pick out just the lengths vector you use the syntax y$lengths
> y$lengths
[1] 3 1 3 2

# Let's look for streaks in a sequence of Bernoulli trials
# We simulate 20 Bernoulli(.5) trials using rbinom(20,1,.5).
> set.seed(1)
> y = rbinom(20,1,.5)  

# y is a vector of 0's and 1's of length 20. 
# We can use rle() to find the length of the longest run in y
> max(rle(y)$lengths)

# We can count the number of runs of more than 3.
> sum(rle(y)$lengths > 3)

# We can count the number of runs of exactly length 3.
> sum(rle(y)$lengths == 3)
```
