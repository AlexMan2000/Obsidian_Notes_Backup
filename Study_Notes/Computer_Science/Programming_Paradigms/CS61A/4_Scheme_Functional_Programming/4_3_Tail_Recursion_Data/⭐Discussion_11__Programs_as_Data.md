[released_disc_disc11_disc11.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1673000889203-d917ef44-1355-4115-bf2e-3395a0e0b4f9.pdf)
[released_disc_sol-disc11_disc11.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1673000889195-c188ec13-322c-4913-a203-db0d14cfc6cd.pdf)

# Programs as Data
## Changing Evaluation Order - f string
> ![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022523429.png)![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022521648.png)![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022526517.png)
> 总的来说，`program as data`可以改变我们`evaluate program`的先后顺序。



## Q1 If Program Python
> ![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022522747.png)![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022524867.png)

```python
def if_program(condition, true_result, false_result):
    """
    >>> eval(if_program("True", "3", "4"))
    3
    >>> eval(if_program("0", "'if true'", "'if false'"))
    'if false'
    >>> eval(if_program("1", "print('true')", "print('false')"))
    true
    >>> eval(if_program("print('condition')", "print('true_result')", "print('false_result')"))
    condition
    false_result
    """
    "*** YOUR CODE HERE ***"

```
```python
def if_program(condition, true_result, false_result):
    """
    >>> eval(if_program("True", "3", "4"))
    3
    >>> eval(if_program("0", "'if true'", "'if false'"))
    'if false'
    >>> eval(if_program("1", "print('true')", "print('false')"))
    true
    >>> eval(if_program("print('condition')", "print('true_result')", "print('false_result')"))
    condition
    false_result
    """
    "*** YOUR CODE HERE ***"
    return f"{true_result} if {condition} else {false_result}"
```
**Solution**![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022535164.png)


# Scheme Programs as Data
## Basics - Using Scheme List
> ![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022531284.png)




## Quasiquotation
> ![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022536424.png)



## Q2 Writing Quasiquote Expressions⭐⭐
> ![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022531048.png)![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022532232.png)

**Solution**![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022536617.png)![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022535155.png)![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022537041.png)


## Q3 If Program Scheme
### Part 1: WWPD
> ![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022545110.png)

**Solution**![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022549333.png)


### Part 2: Code Writing
> ![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022545479.png)

```python
(define (if-program condition if-true if-false)
  'YOUR-CODE-HERE
)
```
**Solution**![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022544982.png)


# Program as Data Practice
## Q4 Exponential Powers
> ![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022543059.png)

**Solutions**![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022547434.png)

## Q5 Swap⭐⭐⭐⭐⭐
> ![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022548616.png)
> 注意: `(list ...)`就等同于`'(...)`, 只有`eval(list)`才能获得结果。
> 比如一个`list s`是`'(+ 1 (- 1 3))`, `(car (cdr s))`就是`1`, `(car (cdr (cdr s)))`就是`-1`

**Solutions - let keyword**![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022547767.png)

## Q6 Make Or ⭐⭐⭐
> ![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022559021.png)

**Solutions**![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022556508.png)


## Q7 Make "Make Or"⭐⭐⭐⭐⭐
> ![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022551971.png)
> 参考: [Generating Codes](https://www.yuque.com/alexman/ac5oth/bzd86lbwg957s3g7#dpkyK)

**Solutions**![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022559844.png)![image.png](./⭐Discussion_11__Programs_as_Data.assets/20230302_1022552121.png)
