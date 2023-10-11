> **Ch 3.2:** [http://composingprograms.com/pages/32-functional-programming.html](http://composingprograms.com/pages/32-functional-programming.html)
> **Ch 3.3: **[http://composingprograms.com/pages/33-exceptions.html](http://composingprograms.com/pages/33-exceptions.html)
> **Ch 3.4:** [http://composingprograms.com/pages/34-interpreters-for-languages-with-combination.html](http://composingprograms.com/pages/34-interpreters-for-languages-with-combination.html)
> **Ch 3.5:** [http://composingprograms.com/pages/35-interpreters-for-languages-with-abstraction.html#structure](http://composingprograms.com/pages/35-interpreters-for-languages-with-abstraction.html#structure)
> **Online Scheme Interpreter: **[https://inst.eecs.berkeley.edu/~cs61a/fa14/assets/interpreter/scheme.html](https://inst.eecs.berkeley.edu/~cs61a/fa14/assets/interpreter/scheme.html)

[released_assets_slides_29-Calculator_full.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1673186100040-0fea8a60-dd04-4ec9-9e72-ba764232d5cf.pdf)
[released_assets_slides_30-Interpreters_full.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1673186099876-96a8994c-2463-4004-b32a-5898fff9c43a.pdf)

# 1 Scheme Lists
## Defining& Drawing Lists
> ![image.png](./Lectures__Readings.assets/20230302_1021262126.png)

**Demo**![image.png](./Lectures__Readings.assets/20230302_1021261016.png)![image.png](./Lectures__Readings.assets/20230302_1021264047.png)

## Built-in List Functions
Demo![image.png](./Lectures__Readings.assets/20230302_1021269209.png)![image.png](./Lectures__Readings.assets/20230302_1021275854.png)![image.png](./Lectures__Readings.assets/20230302_1021276580.png)


## Symbolic Programming
> ![image.png](./Lectures__Readings.assets/20230302_1021273690.png)
> 即便我们不知道`a`具体是什么值，我们仍然可以`quote a`，或者`'a`, 之后赋值也是可以的。先用后付。

**Demo**![image.png](./Lectures__Readings.assets/20230302_1021273457.png)![image.png](./Lectures__Readings.assets/20230302_1021285327.png)![image.png](./Lectures__Readings.assets/20230302_1021286968.png)![image.png](./Lectures__Readings.assets/20230302_1021287137.png)
上面的两个例子中，`cdr`会返回一个`list`, 而`car`返回的是一个`list`中的第一个元素。


## List Processing Procedures
> ![image.png](./Lectures__Readings.assets/20230302_1021283281.png)

**Demo**![image.png](./Lectures__Readings.assets/20230302_1021295321.png)


## Even Subsets⭐⭐⭐⭐⭐
> ![image.png](./Lectures__Readings.assets/20230302_1021292007.png)

**Scheme**![image.png](./Lectures__Readings.assets/20230302_1021299477.png)![image.png](./Lectures__Readings.assets/20230302_1021308841.png)![image.png](./Lectures__Readings.assets/20230302_1021309651.png)

```python
# Non-empty subsets of integer list that have an even sum
def even_subsets(lst):
    if len(lst) == 0:
        return []

    res = even_subsets(lst[1:])
    if lst[0] % 2 == 1:
        res.extend(list(map(lambda x: [lst[0]] + x, odd_subsets(lst[1:]) )))
    else:
        res.extend(list(map(lambda x:  [lst[0]] + x, even_subsets(lst[1:]))))
        res.append([lst[0]])
    return res[:]



    # Non-empty subsets og integer list that have an odd sum
def odd_subsets(lst):
    if len(lst) == 0:
        return []

    res = odd_subsets(lst[1:])
    if lst[0] % 2 == 1:
        res.extend(list(map(lambda x: [lst[0]] + x, even_subsets(lst[1:]))))
        res.append([lst[0]])
    else:
        res.extend(list(map(lambda x:  [lst[0]] + x, odd_subsets(lst[1:]))))

    return res[:]
```
```python
# Higher-Order Function
# Non-empty subsets of integer list that have an even sum
def even_subsets(lst):
    if len(lst) == 0:
        return []

    res = even_subsets(lst[1:])
    helper = subset_helper(lambda x: x % 2 == 0, lst)
    res = helper + res

    return res[:]

# Non-empty subsets og integer list that have an odd sum
def odd_subsets(lst):
    if len(lst) == 0:
        return []

    res = odd_subsets(lst[1:])
    helper = subset_helper(lambda x: x % 2 == 1, lst)
    res = helper + res

    return res[:]


def subset_helper(f, lst):
    res = []
    if f(lst[0]):
        res.extend(list(map(lambda x: [lst[0]] + x, even_subsets(lst[1:]))))
    else:
        res.extend(list(map(lambda x:  [lst[0]] + x, odd_subsets(lst[1:]))))
    if f(lst[0]):
        res.append([lst[0]])

    return res[:]
```


## Even Subsets: Concise⭐⭐⭐⭐⭐
> ![image.png](./Lectures__Readings.assets/20230302_1021305559.png)![image.png](./Lectures__Readings.assets/20230302_1021311190.png)

**Scheme Solution**![image.png](./Lectures__Readings.assets/20230302_1021313109.png)
```python
# Alternate Version - First figure out all the subset, then filter out the even ones
def non_empty_subset(lst):
    if len(lst) == 0:
        return []

    res = non_empty_subset(lst[1:])
    res.extend((list(map(lambda x: [lst[0]] + x, non_empty_subset(lst[1:])))))
    res.append([lst[0]])

    return res[:]


def filter_even_sum(lst):
    return list(filter(lambda x: sum(x) % 2 == 0, lst))
```


# 2 Exceptions
## Raise Exceptions
> ![image.png](./Lectures__Readings.assets/20230302_1021313018.png)

```python
def errors():
    abs('hello') # TypeError
    hello # NameError
    {}['hello'] # KeyError
    def f(): f()
    f() # RecursionError

def double(x):
    if isinstance(x, str):
        raise TypeError('double takes only numbers')
    return 2 * x
```

## Try Statements⭐⭐⭐⭐⭐
> ![image.png](./Lectures__Readings.assets/20230302_1021311628.png)![image.png](./Lectures__Readings.assets/20230302_1021322197.png)

```python
def invert(x):
    """Return 1/x

    >>> invert(2)
    Never printed if x is 0
    0.5
    """
    result = 1/x  # Raises a ZeroDivisionError if x is 0
    print('Never printed if x is 0')
    return result

def invert_safe(x):
    """Return 1/x, or the string 'divison by zero' if x is 0.

    >>> invert_safe(2)
    Never printed if x is 0
    0.5
    >>> invert_safe(0)
    'division by zero'
    """
    try:
        return invert(x)
    except ZeroDivisionError as e:
        return str(e)
```
**Output**![image.png](./Lectures__Readings.assets/20230302_1021326521.png)![image.png](./Lectures__Readings.assets/20230302_1021323632.png)


## Reduce
> ![image.png](./Lectures__Readings.assets/20230302_1021326520.png)

```python
from operator import add, mul, truediv
def reduce(f, s, initial):
    """Combine elements of s pairwise using f, starting with initial.

    >>> reduce(mul, [2, 4, 8], 1)
    64
    >>> reduce(pow, [1, 2, 3, 4], 2)
    16777216
    """
    for x in s:
        initial = f(initial, x)
    return initial

def divide_all(n, ds):
    """Divide n by every d in ds.

    >>> divide_all(1024, [2, 4, 8])
    16.0
    >>> divide_all(1024, [2, 4, 0, 8])
    inf
    """
    try:
        return reduce(truediv, ds, n)
    except ZeroDivisionError:
        return float('inf')
```


# 3 Interpreters&Programming Languages
:::info
**Study Guide:** [https://cs61a.org/study-guide/interpreters/#counting-calls](https://cs61a.org/study-guide/interpreters/#counting-calls)
:::
## Programming Languages
> ![image.png](./Lectures__Readings.assets/20230302_1021322091.png)



## Metalinguistic Abstraction
> ![image.png](./Lectures__Readings.assets/20230302_1021335933.png)



## Parsing - Details in Lab 11
> ![image.png](./Lectures__Readings.assets/20230302_1021332409.png)![image.png](./Lectures__Readings.assets/20230302_1021339052.png)

```python
# Details in lab 11
class Pair:
    """
    A pair has two instance attributes: first and rest. rest is a Pair or nil
    Like a linked list structure
    """
	pass


class nil:
    """The empty list"""
    pass
```


## Syntactic Analysis
> ![image.png](./Lectures__Readings.assets/20230302_1021338450.png)



# 4 Calculator Example
## Calculator Syntax
> ![image.png](./Lectures__Readings.assets/20230302_1021337122.png)



## Calculator Semantics
> ![image.png](./Lectures__Readings.assets/20230302_1021333956.png)



## The Eval Function
> ![image.png](./Lectures__Readings.assets/20230302_1021347504.png)

```python
def calc_eval(exp):
    """Evaluate a Calculator expression."""
    if type(exp) in (int, float):
        return simplify(exp)
    elif isinstance(exp, Pair):
        arguments = exp.second.map(calc_eval)
        return simplify(calc_apply(exp.first, arguments))
    else:
        raise TypeError(exp + ' is not a number or call expression')
```

## Applying Built-in Operators
> ![image.png](./Lectures__Readings.assets/20230302_1021346777.png)

```python
 def calc_apply(operator, args):
    """Apply the named operator to a list of args."""
    if not isinstance(operator, str):
        raise TypeError(str(operator) + ' is not a symbol')
    if operator == '+':
        return reduce(add, args, 0)
    elif operator == '-':
        if len(args) == 0:
            raise TypeError(operator + ' requires at least 1 argument')
        elif len(args) == 1:
            return -args.first
        else:
            return reduce(sub, args.second, args.first)
    elif operator == '*':
        return reduce(mul, args, 1)
    elif operator == '/':
        if len(args) == 0:
            raise TypeError(operator + ' requires at least 1 argument')
        elif len(args) == 1:
            return 1/args.first
        else:
            return reduce(truediv, args.second, args.first)
    else:
        raise TypeError(operator + ' is an unknown operator')
```


## Interactive Interpreters
> ![image.png](./Lectures__Readings.assets/20230302_1021347676.png)

**Demo Codes**![image.png](./Lectures__Readings.assets/20230302_1021345115.png)


## Raise Exceptions
> ![image.png](./Lectures__Readings.assets/20230302_1021348557.png)

**Output**![image.png](./Lectures__Readings.assets/20230302_1021341314.png)



## Handling Exceptions
> ![image.png](./Lectures__Readings.assets/20230302_1021349635.png)

**Demo Codes**![image.png](./Lectures__Readings.assets/20230302_1021353114.png)
直到`KeyboardInterrupt`或者`EOFError`(文件读完了)才停止`while loop`


# 5 Interpreting Scheme - More in Scheme Project
## Structure of Interpreter
> ![image.png](./Lectures__Readings.assets/20230302_1021358374.png)



## Special Forms
### Scheme Evaluation of special forms
> ![image.png](./Lectures__Readings.assets/20230302_1021354989.png)
> Each recursive call create a new environment, until we reach the base cases.

**Demo Codes**![image.png](./Lectures__Readings.assets/20230302_1021352699.png)
**Demo Output**![image.png](./Lectures__Readings.assets/20230302_1021363608.png)

### Logical Special Forms
> ![image.png](./Lectures__Readings.assets/20230302_1021362467.png)

**Demo Output**![image.png](./Lectures__Readings.assets/20230302_1021368123.png)

### Quotation - scheme_reader
> ![image.png](./Lectures__Readings.assets/20230302_1021361227.png)

**Demo Output**![image.png](./Lectures__Readings.assets/20230302_1021364214.png)


### Lambda Expression
> ![image.png](./Lectures__Readings.assets/20230302_1021369657.png)



## Frames and Environments
> ![image.png](./Lectures__Readings.assets/20230302_1021375727.png)
> `lookup()`method look up in the local frame and then in the global frame.

**Demo Output**![image.png](./Lectures__Readings.assets/20230302_1021371199.png)


## Define Expression
> ![image.png](./Lectures__Readings.assets/20230302_1021377381.png)



## Applying User-defined procedures
> ![image.png](./Lectures__Readings.assets/20230302_1021375195.png)

**Pseudocode**![image.png](./Lectures__Readings.assets/20230302_1021372538.png)



