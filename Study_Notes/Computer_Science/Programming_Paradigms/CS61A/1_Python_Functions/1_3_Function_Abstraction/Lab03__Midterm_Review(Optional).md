[released_lab_lab03_lab03.zip](https://www.yuque.com/attachments/yuque/0/2022/zip/12393765/1672407408058-8993637a-1e75-4a1d-8600-8564b645c4fa.zip)
[released_lab_sol-lab03_lab03.zip](https://www.yuque.com/attachments/yuque/0/2022/zip/12393765/1672407408125-c591c157-77b8-4d7e-96bf-b52943f3d220.zip)


# Control
## Q1 Ordered Digits
> ![image.png](./Lab03__Midterm_Review(Optional).assets/20230302_1006371370.png)

```python
def ordered_digits(x):
    prev = x % 10
    while x // 10:
        x //= 10
        curr = x % 10
        if curr > prev:
            return False
        prev = curr
    return True
```
```python
def ordered_digits(x):
    last = x % 10
    x = x // 10
    while x > 0 and last >= x % 10:
        last = x % 10
        x = x // 10
    # 导致循环退出有两种情况，一种是遍历完了，对于x>0, 一种是不严格递增，对应 last >= x % 10
    return x == 0  

```

## Q2 K Runner⭐⭐
> ![image.png](./Lab03__Midterm_Review(Optional).assets/20230302_1006375698.png)

```python

def get_k_run_starter(n, k):
    i = 0
    final = None
    while n > 0 and i <= k:
        while n > 10 and ((n // 10) % 10) < (n % 10):
            n //= 10
        final = n % 10
        i = i + 1
        n = n // 10
    return final
```
```python
def get_k_run_starter(n, k):
    i = 0
    final = None
    while i <= k:
        # Pay attention here, n > 10
        while n > 10 and (n % 10 > (n // 10) % 10):
            n = n // 10
        final = n % 10
        i = i + 1
        n = n // 10
    return final
```


# Higher Order Function
## Q3 Repeated Call⭐⭐⭐⭐
> ![image.png](./Lab03__Midterm_Review(Optional).assets/20230302_1006377901.png)

```python
def make_repeater(func, n):
    def repeater(init_value):
    	
        if n == 0:
            return init_value
    	# make_repeater()函数最终返回的是一个会call func n-1次的函数
        # repeater(x)返回的是最终的值，于是这里的return statement需要通过make_repeater()()调用
        # 确保其返回值和repeater函数的返回值行为一致
        return make_repeater(func,n-1)(func(init_value))

    return repeater
```
```python
def composer(func1, func2):
    """Return a function f, such that f(x) = func1(func2(x))."""
    def f(x):
        return func1(func2(x))
    return f


def make_repeater(func, n):
    g = identity
    while n > 0:
        g = composer(func, g)
        n = n - 1
    return g


# Alternate
def make_repeater2(func, n):
    def inner_func(x):
        k = 0
        while k < n:
            x, k = func(x), k + 1
        return x
    return inner_func
```


## Q4 Apply Twice
> ![image.png](./Lab03__Midterm_Review(Optional).assets/20230302_1006377593.png)

```python
def apply_twice(func):
    def repeat(x):
        return make_repeater(func, 2)(x)
    return repeat
```
```python
def apply_twice(func):
    return make_repeater(func, 2)
```


## Q5 It's Always a Good Prime⭐⭐⭐
> ![image.png](./Lab03__Midterm_Review(Optional).assets/20230302_1006371102.png)![image.png](./Lab03__Midterm_Review(Optional).assets/20230302_1006385798.png)
> 本题非常的巧妙，核心代码段是`checker = (lambda f, i: lambda x: x % i == 0 or f(x))(checker, i)`。运用离散数学中的语言，我们假设代表`x % i == 0`这个`proposition`, 则上面代码等价于。而这个命题实际上就表示能否被所有`2`到`n`之间的`prime numbers`整除，实际上运用了`short circuiting`的知识店，非常值得复习。

```python
def div_by_primes_under(n):
    checker = lambda x: False
    i = 2
    while i <= n:
        if not checker(i):
            checker = (lambda f, i: lambda x: x % i == 0 or f(x))(checker, i)
        i = i + 1
    return checker


def div_by_primes_under_no_lambda(n):
    def checker(x):
        return False
    i = 2
    while i <= n:
        if not checker(i):
            def outer(f, i):
                def inner(x):
                    return x % i == 0 or f(x)
                return inner
            checker = outer(checker, i)
        i = i + 1
    return checker
```


## Q6 Church numerals⭐⭐⭐⭐⭐
### Lambda Calculus
#### Basics
> [https://www.youtube.com/watch?v=3VQ382QG-y4](https://www.youtube.com/watch?v=3VQ382QG-y4)
> **Basic Syntax:**
> ![image.png](./Lab03__Midterm_Review(Optional).assets/20230302_1006382221.png)
> **Application(Javascript):**
> -   = `f(a)`, invoke `f`with `a`
> -  = `f(a)(b)`, function must be unary in lambda calculus
> -  = `f(a(b))`
> - : `a => b`
> - : `a => b(x)`
> - : `a =>( b(x))`, greedy
> - : `(a => b)(x)`
> - : `a => b => a`
> - : `a => (b => a)`, useless parentheses
> 
**:**
> ![image.png](./Lab03__Midterm_Review(Optional).assets/20230302_1006388452.png)



#### Self-Application
>  : `M = f => f(f)`
> `M(I)=I`, since `M(I)=I(I)=I`
> `M(M)=M(M)=M(M)=...`, which blows up the stack.



#### Nested Lambda
> : `a => b => c => b`



### Supplementals
[Notes_ Lambda Calculus.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1672477177440-bf352162-4a00-4abb-b14a-92a85d1d0401.pdf)
[church.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1672477177376-05329e50-2292-481d-b75a-f030cac35733.pdf)
[supplemental.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1672474674806-81db1a89-29e0-47b0-8c7b-00424c8e3a61.pdf)
> **参考:** [https://www.cnblogs.com/ZHDreamer/p/15929157.html](https://www.cnblogs.com/ZHDreamer/p/15929157.html)


### Problem
**Problems**![image.png](./Lab03__Midterm_Review(Optional).assets/20230302_1006382873.png)![image.png](./Lab03__Midterm_Review(Optional).assets/20230302_1006382730.png)
> **Church numerals** are a way to represent non-negative integers via repeated function application.
> 邱奇编码是把数据和运算符嵌入到`lambda`演算内的一种方式，最常见的形式即邱奇数，它使用`lambda`符号表示自然数。
> 本题首先我们要搞清楚`successor(zero)`和`successor(successor(zero))`在干什么。
> 首先, `successor(zero)`最终`evaluate`的结果是一个函数`lambda f: lambda x: f(n(f)(x))`, 其中根据闭包的性质可知`n=zero`, 而`zero(f)`是一个`identity function`, 于是`lambda f: lambda x: f(n(f)(x))` 等价于`lambda f: lambda x: f(x)`, 于是`successor(zero) = one(f) = lambda f: lambda x:f(x)`, 于是`one(f)`的函数体中就应该写`lambda x: f(x)`。
> 类似的，`successor(successor(zero))`等价于`successor(one)`, 即`lambda f: lambda x: f(one(f)(x))`, 所以`two`的函数体中应该写`lambda x: f(one(f)(x))`
> 于是我们知道，在`Church`发明的`lambda`体系中:
> - `zero := x=>x`, 是一个`Identity Function`
> - `one := x => f(x)`
> - `two := x => f(one(f)(x)) := x => f(f(x))`, 因为`one(f)`返回的是`x => f(x)`函数, 然后`one(f)(x)`相当于就是`(x => f(x))(x)`, 结果就是`f(x)`
> - 所以`one(f) := x => f(x)`, `two(f) := x => f(f(x))`

```python
def zero(f):
    return lambda x: x


def successor(n):
    return lambda f: lambda x: f(n(f)(x))


def one(f):
    """Church numeral 1: same as successor(zero)"""
    "*** YOUR CODE HERE ***"
    return lambda x: f(x)



def two(f):
    """Church numeral 2: same as successor(successor(zero))"""
    "*** YOUR CODE HERE ***"
    return lambda x: f(f(x))

three = successor(two)
```
> `chruch_to_int`的实现可以从`one => 1`开始考虑， 因为`one`作为一个函数, 我们在调用它`one(f)`的时候返回一个`lambda x: f(x)`, 然后`one(f)(x)`就是在执行`f(x)`, 所以问题就在与这个`f`怎么设计和这个参数`x`传什么。
> 然后我们关注`zero => 0`，`zero`也是一个函数，调用`zero(f)`之后返回一个`identity`函数`x => x`, 所以我们可以令`x=0`, 此时`zero(f) =0`(`f`可以任意取值)，所以参数必须传递`x=0`。
> 然后就是找`f`, 在`x=0`的情况下，我们要求`one(f)(0)=1`, 即`f(0)=1`, 所以`f=lambda x:x+1`, 求解完毕。

```python
def church_to_int(n):
    """Convert the Church numeral n to a Python integer.

    >>> church_to_int(zero)
    0
    >>> church_to_int(one)
    1
    >>> church_to_int(two)
    2
    >>> church_to_int(three)
    3
    """
    "*** YOUR CODE HERE ***"
    return n(lambda x: x+1)(0)
```
> 解决这些操作之前我们首先要明白符合的概念，以及如何用程序思维来表达。
> **首先是加法:**
> 我们先从简单的情况入手：`one(f) := x => f(x)`, `two(f) := x => f(f(x))`, 如果我们要用`one(f)`和`two(f)`表示`three(f)`应该如何做到呢?
> 我们知道`three(f) := x => f(f(f(x))) := x => f(two(f)(x)) := x => one(f)(two(f)(x))`, 所以对于任意的整数`n`和`m`, 我们有:
> ![image.png](./Lab03__Midterm_Review(Optional).assets/20230302_1006387797.png)

```python
def add_church(m, n):
    """Return the Church numeral for m + n, for Church numerals m and n.

    >>> church_to_int(add_church(two, three))
    5
    """
    "*** YOUR CODE HERE ***"
    return lambda f: lambda x: n(f)(m(f)(x))  # Order doesn't matter

```
> **然后是乘法:**
> 我们先从简单的情况入手：`two(f) := x => f(f(x))`, `three(f) := x => f(f(f(x)))`, 如果我们要用`two(f)`和`three(f)`表示`six(f)`应该如何做到呢?
> 其实我们只要理解了`f`在其中的作用即可，我们注意到`two(f)`中有两个`f`，而`three`中有三个，所以我们实际上可以把`two(f)`写成`two(f2) := x => f2(f2(x))`, 同时将`three(f)`作为参数传递进去使得`f2=three(f)`, 这样就可以构造出来了。
> ![image.png](./Lab03__Midterm_Review(Optional).assets/20230302_1006392713.png)

```python
def mul_church(m, n):
    """Return the Church numeral for m * n, for Church numerals m and n.

    >>> four = successor(three)
    >>> church_to_int(mul_church(two, three))
    6
    >>> church_to_int(mul_church(three, four))
    12
    """
    "*** YOUR CODE HERE ***"
    return lambda f: n(m(f))  # Order doesn't matter
```
> 最后是乘方，较难:
> ![image.png](./Lab03__Midterm_Review(Optional).assets/20230302_1006399655.png)

```python
def pow_church(m, n):
    """Return the Church numeral m ** n, for Church numerals m and n.

    >>> church_to_int(pow_church(two, three))
    8
    >>> church_to_int(pow_church(three, two))
    9
    """
    "*** YOUR CODE HERE ***"
    return n(m)   # Order matters
```


# Environment Diagrams
## Q7 Doge
> ![image.png](./Lab03__Midterm_Review(Optional).assets/20230302_1006396232.png)

**Solution**![image.png](./Lab03__Midterm_Review(Optional).assets/20230302_1006398875.png)



## Q8 Diagram - Challenge 1
> ![image.png](./Lab03__Midterm_Review(Optional).assets/20230302_1006393804.png)

**Solution**[https://pythontutor.com/visualize.html#mode=edit](https://pythontutor.com/visualize.html#mode=edit)


## Q9 Diagram - Challenge 2
> ![image.png](./Lab03__Midterm_Review(Optional).assets/20230302_1006396259.png)

**Solution**[https://pythontutor.com/visualize.html#mode=edit](https://pythontutor.com/visualize.html#mode=edit)
