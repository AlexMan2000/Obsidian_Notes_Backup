> Ch 2.1~2.3: [http://composingprograms.com/pages/21-introduction.html](http://composingprograms.com/pages/21-introduction.html)

[released_assets_slides_11-Sequences_full.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1672545868991-9b5a855c-bf68-48d6-af96-3ae034d9eb84.pdf)
[released_assets_slides_12-Containers_full.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1672545869040-7f75a6a1-d3dd-4089-b9b3-4e71742b0c66.pdf)
[released_assets_slides_13-Data_Abstraction_full.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1672545869194-57004294-f137-4c58-b370-ac12bd9cfac1.pdf)

# 1 Sequences
## List Basics
### Common Operations
> List in python can have arbitrary length, most important functions are listed below:
> 1. Defining a list: `digits = [1,8,2,8]`
> 2. Length of a list: `len(digits)`
> 3. Indexing a list: `digits[i]`, will raise an error if `i >= len(digits)`
> 4. Mutate a list: `digits[i]=...`, will raise an error if `i >= len(digits)`
> 5. Concat lists: `[2,7]+[3,6]` => `[2,7,3,6]`, orders are kept.
> 6. Nested list/indexing: `a=[[10,20],[30,40]]`, `a[1][0] =>30`
> 7. Iterate through the list: `for item in list: suites`
> 8. **Sequence unpacking:** `pairs = [[1,2], [2,2], [2,3], [4,4]]`, `for x,y in pairs: suites`
> 
![image.png](./Lectures__Readings.assets/20230302_1013031500.png)
> 9. Ranges: Used for iterations.
> 10. **List constructor:** `list(range(5,8)) => [5,6,7]`, `list(range(4)) => [0,1,2,3]`
> 
**More operations:**
> ![image.png](./Lectures__Readings.assets/20230302_1013036532.png)



### Range Type
> ![image.png](./Lectures__Readings.assets/20230302_1013033144.png)


### For Statements - Sequence Iteration
> ![image.png](./Lectures__Readings.assets/20230302_1013034817.png)![image.png](./Lectures__Readings.assets/20230302_1013039569.png)




## Sequence Processing
### List Comprehensions
> ![image.png](./Lectures__Readings.assets/20230302_1013033587.png)
> `List Comprehension`的完整形式, 在本周的`Lab`中会用到。
>  `[<map exp1> if <bool exp> else <map exp2> for <name> in <iter exp> if <filter exp>]`

**Promoted Example**![image.png](./Lectures__Readings.assets/20230302_1013035811.png)
```python
def promoted(s, f):
    """Return a list with the same elements as s, but with all
    elements e for which f(e) is a true value placed first.

    >>> promoted(range(10), odd)  # odds in front
    [1, 3, 5, 7, 9, 0, 2, 4, 6, 8]
    """
    return [e for e in s if f(e)] + [e for e in s if not f(e)]
```


### Aggregation
> ![image.png](./Lectures__Readings.assets/20230302_1013032093.png)![image.png](./Lectures__Readings.assets/20230302_1013048846.png)

**Perfect Number Problem, Using List**![image.png](./Lectures__Readings.assets/20230302_1013048586.png)
**Minimum Perimeter Problem(最小周长问题)**![image.png](./Lectures__Readings.assets/20230302_1013048694.png)
```python
sum(odds)
sum({3:9, 5:25})
max(range(10))
max(range(10), key=lambda x: 7 - (x-2)*(x-4))
all([x < 5 for x in range(5)])
perfect_square = lambda x: x == round(x ** 0.5) ** 2
any([perfect_square(x) for x in range(50, 60)]) # Try ,65)
```


### Higher-Order Function
> ![image.png](./Lectures__Readings.assets/20230302_1013043033.png)![image.png](./Lectures__Readings.assets/20230302_1013041537.png)![image.png](./Lectures__Readings.assets/20230302_1013049321.png)![image.png](./Lectures__Readings.assets/20230302_1013041997.png)

**Perfect Number Problem**![image.png](./Lectures__Readings.assets/20230302_1013049900.png)


### Conventional Names
> 三个常用函数, `apply`, `filter`, `reduce`:
> ![image.png](./Lectures__Readings.assets/20230302_1013047962.png)



## Sequence Abstraction
### Membership
> ![image.png](./Lectures__Readings.assets/20230302_1013057315.png)


### Slicing
> ![image.png](./Lectures__Readings.assets/20230302_1013059088.png)

```python
odds = [3, 5, 7, 9, 11]
list(range(1, 3))
[odds[i] for i in range(1, 3)]
odds[1:3]
odds[1:]
odds[:3]
odds[:]
```

### Strings
> ![image.png](./Lectures__Readings.assets/20230302_1013054495.png)
> `exec('curry = lambda f: lambda x: lambda y: f(x,y)')`可以被`interpreter`解析并执行, 本质上`exec(string)`中的`string`如果是一个可执行的代码逻辑，那么就可以获得其执行结果。
> ![image.png](./Lectures__Readings.assets/20230302_1013054226.png)![image.png](./Lectures__Readings.assets/20230302_1013054174.png)



### Dictionary
> ![image.png](./Lectures__Readings.assets/20230302_1013057777.png)![image.png](./Lectures__Readings.assets/20230302_1013064493.png)

```python
def dict_demos():
    numerals = {'I': 1, 'V': 5, 'X': 10}
    numerals['X']
    # numerals['X-ray']   # KeyError
    # numerals[10]        # KeyError
    len(numerals)
    list(numerals)
    numerals.values()
    list(numerals.values())  # numerals.values() is a 'divt_values' class, should use list()
    sum(numerals.values())
    dict([[3, 9], [4, 16]] # => {3:9, 4:16}
    numerals.get('X', 0)   # 10
    numerals.get('X-ray', 0)  # KeyError
    {1: 2, 1: 3}              # The second value override the first one.
    {[1]: 2}				  # unhashable type 'list'
    {1: [2]}                  # Valid

```
**Indexing Example**![image.png](./Lectures__Readings.assets/20230302_1013061036.png)
```python
def index(keys, values, match):
    """Return a dictionary from keys k to a list of values v for which 
    match(k, v) is a true value.
    
    >>> index([7, 9, 11], range(30, 50), lambda k, v: v % k == 0)
    {7: [35, 42, 49], 9: [36, 45], 11: [33, 44]}
    """
    return {k: [v for v in values if match(k, v)] for k in keys}
```


## Box-and-Pointer Notation
> ![image.png](./Lectures__Readings.assets/20230302_1013065212.png)![image.png](./Lectures__Readings.assets/20230302_1013064957.png)



# 2 Data Abstraction
> ![image.png](./Lectures__Readings.assets/20230302_1013069344.png)




## Native Data Types
> **Native data types have the following properties:**
> 1. There are expressions that evaluate to values of native types, called _literals_.
> 2. There are built-in functions and operators to manipulate values of native types.
> 3. `int`,`float`, `complex`are built-in native numeric type and `boolean` are native non-numeric type.


## Pairs Abstraction
> ![image.png](./Lectures__Readings.assets/20230302_1013061023.png)



## Rational Numbers Abstraction
> ![image.png](./Lectures__Readings.assets/20230302_1013063389.png)

### Constructor and Selector
> ![image.png](./Lectures__Readings.assets/20230302_1013072670.png)![image.png](./Lectures__Readings.assets/20230302_1013074981.png)![image.png](./Lectures__Readings.assets/20230302_1013074243.png)

```python
from fractions import gcd
def rational(n, d):
    """A representation of the rational number N/D."""
    g = gcd(n, d)
    return [n//g, d//g]

def numer(x):
    """Return the numerator of rational number X in lowest terms and having
    the sign of X."""
    return x[0]

def denom(x):
    """Return the denominator of rational number X in lowest terms and positive."""
    return x[1]

```
```python
def rational(n, d):
    """A representation of the rational number N/D."""
    g = gcd(n, d)
    n, d = n//g, d//g
    def select(name):
        if name == 'n':
            return n
        elif name == 'd':
            return d
    return select

def numer(x):
    """Return the numerator of rational number X in lowest terms and having
    the sign of X."""
    return x('n')

def denom(x):
    """Return the denominator of rational number X in lowest terms and positive."""
    return x('d')
```
**Function Representation**![image.png](./Lectures__Readings.assets/20230302_1013074462.png)

### Arithmetics
**Rational Number Arithmetics**![image.png](./Lectures__Readings.assets/20230302_1013076029.png)![image.png](./Lectures__Readings.assets/20230302_1013074153.png)
```python
# Rational arithmetic
def add_rational(x, y):
    """The sum of rational numbers X and Y."""
    nx, dx = numer(x), denom(x)
    ny, dy = numer(y), denom(y)
    return rational(nx * dy + ny * dx, dx * dy)

def mul_rational(x, y):
    """The product of rational numbers X and Y."""
    return rational(numer(x) * numer(y), denom(x) * denom(y))

def rationals_are_equal(x, y):
    """True iff rational numbers X and Y are equal."""
    return numer(x) * denom(y) == numer(y) * denom(x)

def print_rational(x):
    """Print rational X."""
    print(numer(x), "/", denom(x))

```


### Abstraction Barrier
> ![image.png](./Lectures__Readings.assets/20230302_1013074765.png)
> We cannot cross the layers.
> 1. 当我们想用`Rational Numbers`计算时，我们应该将`rational number`看成一个整体，作为参数传入`add_rational, mul_rational`函数中。
> 2. 当我们想实现`Rational Number`计算过程的时候，我们的操作粒度应该在`rational number`的分子和分母。
> 3. 当我们想要构造`Rational Number`的时候（`Constructor`和`Selector`），我们应该将`rational number`看成二元列表。


### Violation of Abstraction Barriers
> ![image.png](./Lectures__Readings.assets/20230302_1013072018.png)
> 1. `add_rational`应该将`x`和`y`视为一个整体, 但是这里却直接下探到了`Constructor Layer`, 违反了`Abstraction Barrier`。
> 2. 函数体中实现这个`divide_rational`的计算过程的时候，我们应该把`x`和`y`看成是分子和分母，也就是`numer(x),numer(y),denom(x),denom(y)`, 图中`x[0]`属于`select`操作，这直接下探到了`Constructor Layer`, 违反了`Abstraction Barrier`。
> 
同时`return []`中还出现了`construct`操作，这直接下探到了`Constructor Layer`, 违反了`Abstraction Barrier`。



