[released_disc_disc02_disc02.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1672407465916-dd7284a4-20fa-47da-9cd1-a679afef11af.pdf)
[released_disc_sol-disc02_disc02.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1672407465883-fe9e2d53-de11-4552-8ade-c98180f156af.pdf)


# Q1 Call Diagram
> ![image.png](Disc02__Environment_Diagrams__High-Order_Functions.assets/20230302_1006315960.png)

**Solution**![image.png](Disc02__Environment_Diagrams__High-Order_Functions.assets/20230302_1006315744.png)


# Q2 Nested Calls Diagrams
> ![image.png](Disc02__Environment_Diagrams__High-Order_Functions.assets/20230302_1006313934.png)

**Solution**![image.png](Disc02__Environment_Diagrams__High-Order_Functions.assets/20230302_1006315874.png)

# Q3 Lambda the Environment Diagram
> ![image.png](Disc02__Environment_Diagrams__High-Order_Functions.assets/20230302_1006316493.png)

**Solution**![image.png](Disc02__Environment_Diagrams__High-Order_Functions.assets/20230302_1006315030.png)


# Q4 Make Adder
> ![image.png](Disc02__Environment_Diagrams__High-Order_Functions.assets/20230302_1006316010.png)
> 注意`parent`后面写的一定是`frame`的名字而不是函数的名字。比如`parent=Global`或者`parent=f1`(`f1`是函数执行的时候创建出来的`frame`).
> ![image.png](Disc02__Environment_Diagrams__High-Order_Functions.assets/20230302_1006328318.png)

**Solution Environment Diagram**![image.png](Disc02__Environment_Diagrams__High-Order_Functions.assets/20230302_1006329339.png)


# Q5 Make Keeper
> ![image.png](Disc02__Environment_Diagrams__High-Order_Functions.assets/20230302_1006323182.png)

**Solution**![image.png](Disc02__Environment_Diagrams__High-Order_Functions.assets/20230302_1006321725.png)


# Q6 Make Your Own Lambdas
> ![image.png](Disc02__Environment_Diagrams__High-Order_Functions.assets/20230302_1006328004.png)
> 注意这里可能有些规律: 函数有几个括号，`lambda`的个数就是括号数量`-1`

**Solution**![image.png](Disc02__Environment_Diagrams__High-Order_Functions.assets/20230302_1006324189.png)


# Q7 Curry2 Diagram
> ![image.png](Disc02__Environment_Diagrams__High-Order_Functions.assets/20230302_1006323338.png)

**Solution**![image.png](Disc02__Environment_Diagrams__High-Order_Functions.assets/20230302_1006327847.png)



# Q8 Match Maker(Challenge)⭐⭐
> ![image.png](Disc02__Environment_Diagrams__High-Order_Functions.assets/20230302_1006321636.png)
> 不要想太复杂, 可以不用递归的。直接隔项比较即可。

```python
# Neat and smart
def match_k_alt(k):
    def check(x):
        while x // (10 ** k):
            if (x % 10) != (x // (10 ** k)) % 10:
                return False
            x //= 10
        return True
    return check

# Solution 2
def match_k(k):
    def check(x):
        i = 0
        while 10 ** (i + k) < x:
            if (x // 10**i) % 10 != (x // 10 ** (i + k)) % 10:
                return False
            i = i + 1
        return True
    return check
```
