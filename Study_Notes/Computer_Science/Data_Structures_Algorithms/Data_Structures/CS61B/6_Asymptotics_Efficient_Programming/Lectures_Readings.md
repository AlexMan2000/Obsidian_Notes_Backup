:::info
Reading: 8.1 ~ 8.4
:::


# 1 Encapsulation&API&ADT(Skipped)
[cs61b lec16 2018 APIs, ADTs, views.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674723130689-5c5912b5-ce59-44d9-ab24-a78e922bcd7f.pdf)

# 2 Asymtotics I - Big Theta
[cs61b 2018 lec17 asymptotics1.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674723571549-b56456c3-003c-4ffb-85be-3a2d3f3b4313.pdf)
## Algorithm Cost
> ![image.png](Lectures_Readings.assets/20230302_0948237049.png)![image.png](Lectures_Readings.assets/20230302_0948236951.png)


## How to measure execution cost?
> ![image.png](Lectures_Readings.assets/20230302_0948232826.png)

**Technique 1: Measure the time it takes for execution (Simulation)**![image.png](Lectures_Readings.assets/20230302_0948243223.png)![image.png](Lectures_Readings.assets/20230302_0948246106.png)![image.png](Lectures_Readings.assets/20230302_0948244057.png)
**Technique 2: Count the total operations (Building a Model)**![image.png](Lectures_Readings.assets/20230302_0948246793.png)![image.png](Lectures_Readings.assets/20230302_0948243192.png)
**Exercise 1: Symbolic Model**![image.png](Lectures_Readings.assets/20230302_0948245621.png)
![image.png](Lectures_Readings.assets/20230302_0948247981.png)
**Exercise 2: Comparing Algorithms**![image.png](Lectures_Readings.assets/20230302_0948241217.png)![image.png](Lectures_Readings.assets/20230302_0948252984.png)


## Asymptotic Behaviors
> ![image.png](Lectures_Readings.assets/20230302_0948258087.png)![image.png](Lectures_Readings.assets/20230302_0948252123.png)![image.png](Lectures_Readings.assets/20230302_0948251253.png)



## Duplicate Finding Analysis⭐⭐⭐⭐⭐
> ![image.png](Lectures_Readings.assets/20230302_0948257357.png)

**Simplification 1: Consider Only the Worst Case**![image.png](Lectures_Readings.assets/20230302_0948258427.png)![image.png](Lectures_Readings.assets/20230302_0948253301.png)
**Exercise**![image.png](Lectures_Readings.assets/20230302_0948265411.png)![image.png](Lectures_Readings.assets/20230302_0948264113.png)
**Simplification 2: Restrict Attention to One Operation (Pick representative operation)**![image.png](Lectures_Readings.assets/20230302_0948262975.png)
**Simplification 3: Eliminate low order terms**![image.png](Lectures_Readings.assets/20230302_0948268733.png)
**Simplification 4: Eliminate multiplicative constants**![image.png](Lectures_Readings.assets/20230302_0948266728.png)

> ![image.png](Lectures_Readings.assets/20230302_0948261601.png)

**Repeat the above process for dup2**![image.png](Lectures_Readings.assets/20230302_0948269890.png)
> ![image.png](Lectures_Readings.assets/20230302_0948272566.png)

**Simplified Analysis Process Example**![image.png](Lectures_Readings.assets/20230302_0948276960.png)![image.png](Lectures_Readings.assets/20230302_0948277157.png)![image.png](Lectures_Readings.assets/20230302_0948273928.png)


## Big-Theta
### Definition
> ![image.png](Lectures_Readings.assets/20230302_0948278217.png)![image.png](Lectures_Readings.assets/20230302_0948278566.png)
> 注意这里的不等关系仅仅在$N$很大的时候成立。

**Exercise**![image.png](Lectures_Readings.assets/20230302_0948276885.png)![image.png](Lectures_Readings.assets/20230302_0948272581.png)![image.png](Lectures_Readings.assets/20230302_0948285574.png)
> ![image.png](Lectures_Readings.assets/20230302_0948287335.png)



### Properties
> ![image.png](Lectures_Readings.assets/20230302_0948289924.png)



## Summary
> ![image.png](Lectures_Readings.assets/20230302_0948289820.png)



## Study Guide Exercises
[Asymptotics I Study Guide _ CS 61B Spring 2018.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1675493120342-ecf58b41-9137-4e07-b61e-7a0f0035c10e.pdf)
> ![image.png](Lectures_Readings.assets/20230302_0948285461.png)

**Solution**只有第四个是对的。其他都没有限定$N$的大小。$N$必须很大才可以。

# 3 Asymtotics II - Sorting
[cs61b 2018 lec18 asymptotics2.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674723571653-5d2b4150-facc-4c30-90cd-646ea1be6ccb.pdf)

## Warmup Exercise⭐⭐⭐⭐
> ![image.png](Lectures_Readings.assets/20230302_0948284769.png)

**Solution**![image.png](Lectures_Readings.assets/20230302_0948284164.png)![image.png](Lectures_Readings.assets/20230302_0948283694.png)![image.png](Lectures_Readings.assets/20230302_0948292566.png)![image.png](Lectures_Readings.assets/20230302_0948291868.png)
计算过程: $1+2+4+\cdots+N=\frac{1\cdot (1-2^{log_2(N)+1})}{1-2}=2N-1$


## Recursion
> ![image.png](Lectures_Readings.assets/20230302_0948293344.png)

**Intuitive Solution**![image.png](Lectures_Readings.assets/20230302_0948295467.png)
**Exact Solution - Induction**![image.png](Lectures_Readings.assets/20230302_0948292740.png)![image.png](Lectures_Readings.assets/20230302_0948293203.png)
**Formal Approach - Recurrence Relation**![image.png](Lectures_Readings.assets/20230302_0948298846.png)![image.png](Lectures_Readings.assets/20230302_0948291059.png)![image.png](Lectures_Readings.assets/20230302_0948296327.png)


## Binary Search
> ![image.png](Lectures_Readings.assets/20230302_0948301937.png)

**Intuitive Solution**![image.png](Lectures_Readings.assets/20230302_0948303729.png)
**Exact Number of Calls**![image.png](Lectures_Readings.assets/20230302_0948304509.png)![image.png](Lectures_Readings.assets/20230302_0948307992.png)![image.png](Lectures_Readings.assets/20230302_0948301686.png)![image.png](Lectures_Readings.assets/20230302_0948305385.png)![image.png](Lectures_Readings.assets/20230302_0948305527.png)
**Recurrence Relation**![image.png](Lectures_Readings.assets/20230302_0948307918.png)


## Selection Sort
> ![image.png](Lectures_Readings.assets/20230302_0948319280.png)![image.png](Lectures_Readings.assets/20230302_0948317857.png)



## Merge Sort
### Merging Operations
> ![image.png](Lectures_Readings.assets/20230302_0948311994.png)![image.png](Lectures_Readings.assets/20230302_0948316513.png)
> 注意本小节的所有`Cost Model`都是`Array Writes`, 我们也完全可以选择其他的`Cost Model`，比如`Comparison`




### Selection Sort with Merging
> ![image.png](Lectures_Readings.assets/20230302_0948316233.png)![image.png](Lectures_Readings.assets/20230302_0948316804.png)



### Pure Merge Sort
> ![image.png](Lectures_Readings.assets/20230302_0948317389.png)


### Runtime analysis of PMS
> ![image.png](Lectures_Readings.assets/20230302_0948316389.png)

**Exact Count**![image.png](Lectures_Readings.assets/20230302_0948322056.png)
**Recurrence Relations**![image.png](Lectures_Readings.assets/20230302_0948322822.png)



## Summary
> ![image.png](Lectures_Readings.assets/20230302_0948323554.png)![image.png](Lectures_Readings.assets/20230302_0948326898.png)




## Study Guide Exercises
[Asymptotics II Study Guide _ CS 61B Spring 2018.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1675493120352-52647ec5-e952-4578-882d-65535148def5.pdf)


# 4 Asymtotics III - BigO&Omega
[cs61b 2018 lec19 asymptotics3.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674723571689-1eb436ce-7a4c-441e-b48d-5890957681f0.pdf)

## Warmup Tricks
### Tricky Question 1
> ![image.png](Lectures_Readings.assets/20230302_0948329968.png)

**Solution**![image.png](Lectures_Readings.assets/20230302_0948324621.png)
循环执行第一次的时候就会返回`true`。

### Tricky Question 2
> ![image.png](Lectures_Readings.assets/20230302_0948321607.png)

**Solution**![image.png](Lectures_Readings.assets/20230302_0948338314.png)![image.png](Lectures_Readings.assets/20230302_0948339174.png)


### Limitation of Big Theta
> ![image.png](Lectures_Readings.assets/20230302_0948339232.png)



## Big-O ⭐⭐⭐
> ![image.png](Lectures_Readings.assets/20230302_0948334684.png)

**Exercises**![image.png](Lectures_Readings.assets/20230302_0948339741.png)![image.png](Lectures_Readings.assets/20230302_0948335710.png)![image.png](Lectures_Readings.assets/20230302_0948338790.png)![image.png](Lectures_Readings.assets/20230302_0948337902.png)![image.png](Lectures_Readings.assets/20230302_0948336102.png)![image.png](Lectures_Readings.assets/20230302_0948335315.png)

## Big Omega
> ![image.png](Lectures_Readings.assets/20230302_0948349516.png)![image.png](Lectures_Readings.assets/20230302_0948347612.png)


## Comparison ⭐⭐⭐⭐⭐
> ![image.png](Lectures_Readings.assets/20230302_0948346552.png)![image.png](Lectures_Readings.assets/20230302_0948349901.png)![image.png](Lectures_Readings.assets/20230302_0948347197.png)



## Amortized Analysis⭐⭐⭐⭐⭐
### Grigometh's Tribute⭐⭐
> ![image.png](Lectures_Readings.assets/20230302_0948346060.png)

**Solution**![image.png](Lectures_Readings.assets/20230302_0948344270.png)



### Array Geometric Resizing
> ![image.png](Lectures_Readings.assets/20230302_0948343796.png)


### Intuitive Analysis
> ![image.png](Lectures_Readings.assets/20230302_0948351778.png)
> `Worst Case` 就是我们`Resize`操作的时候需要的`N`次`Array Copy`操作。
> `Average Case`可以这么理解, 假设我们将`N`个`items`依次`append`到`array[N]`里面，则总共的`Array Write`操作数量是$1\times N + N(copy) = 2N$, 而此时我们有$N$个元素在`array`中，则均摊到每一个元素上我们的`Array Write`操作数量就是$\frac{2N}{N}=2=\Theta(1)$



### Rigorous Analysis⭐⭐⭐⭐⭐
> ![image.png](Lectures_Readings.assets/20230302_0948353038.png)



#### Cost Model: Array Access
> ![image.png](Lectures_Readings.assets/20230302_0948357999.png)![image.png](Lectures_Readings.assets/20230302_0948351209.png)


#### Amortization of Runtime
> ![image.png](Lectures_Readings.assets/20230302_0948354406.png)
> 这个`Array Resizing`的例子中我们的`Amortized Cost`是`3.14`
> ![image.png](Lectures_Readings.assets/20230302_0948359093.png)
> 表格中的$\Phi_i$是`Self-maked up`的
> 假设我们的`Grigometh's Tribute`中我们每天都将$5$单位的`hay`放在`urn`之上，即`amortized cost = 5`(可以任意选取)。 `total cost`就是`actual cost`, 也被称为`withdrawal`, `amortized cost`也被称为`deposit`
> ![image.png](Lectures_Readings.assets/20230302_0948352706.png)![image.png](Lectures_Readings.assets/20230302_0948357415.png)



## Summary
> ![image.png](Lectures_Readings.assets/20230302_0948367705.png)


## Study Guide Exercises
[Asymptotics III Study Guide _ CS 61B Spring 2018.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1675493120342-8f3f10c2-19b1-44b7-b447-64371c50b869.pdf)

