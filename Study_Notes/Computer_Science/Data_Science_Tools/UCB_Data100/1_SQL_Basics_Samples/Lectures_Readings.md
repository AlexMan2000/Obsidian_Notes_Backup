# Lecture 1: Course Overview
> **Video:** [https://www.youtube.com/watch?v=_6sIND3jOYg](https://www.youtube.com/watch?v=_6sIND3jOYg)
> **Reading: **[Chapter 1](https://learningds.org/ch/01/lifecycle_intro.html)

[1. Course Overview, Data Science Lifecycle.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1673397267041-a201535a-33e6-4162-aa99-96f726cd8947.pdf)


## Data Science Lifecycle
> ![image.png](./Lectures_Readings.assets/20230302_2122118397.png)


### Asking Questions
> ![image.png](./Lectures_Readings.assets/20230302_2122112986.png)



### Data Acquisition and Cleaning
> ![image.png](./Lectures_Readings.assets/20230302_2122112728.png)



### Exploratory Data Analysis
> ![image.png](./Lectures_Readings.assets/20230302_2122111051.png)



### Prediction and Inference
> ![image.png](./Lectures_Readings.assets/20230302_2122124822.png)



## Demo with Codes
[lec01.zip](https://www.yuque.com/attachments/yuque/0/2023/zip/12393765/1673427408876-c90c570d-a874-4fc2-8494-ef9d0790e05d.zip)



# Lecture 2: Data Sampling & Probability 
> **Reading:** [Chapter 2](https://learningds.org/ch/02/data_scope_intro.html)

[2. Data Sampling and Probability.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1673397493283-642726d1-01a2-4a7d-968f-838a55c8638d.pdf)

## 2.1 Censuses and Surveys
### US Census
> ![image.png](./Lectures_Readings.assets/20230302_2122124142.png)![image.png](./Lectures_Readings.assets/20230302_2122125179.png)




### Surveys
> ![image.png](./Lectures_Readings.assets/20230302_2122127072.png)




### Quick Check
> ![image.png](./Lectures_Readings.assets/20230302_2122128617.png)



## 2.2 Samples
### What is sample?
> ![image.png](./Lectures_Readings.assets/20230302_2122121678.png)
> **Chance Error:** Every time we sample a subset, we get a different sample that may look significantly different from the population. It happens just due to our random choice of the data points.
> **Bias: **Constantly overestimate or underestimate the quantities.



### Convenience Samples
> ![image.png](./Lectures_Readings.assets/20230302_2122126707.png)



### Quota Samples(按比例抽样)
> ![image.png](./Lectures_Readings.assets/20230302_2122129845.png)



### Quality, Not Quantity
> ![image.png](./Lectures_Readings.assets/20230302_2122134797.png)




### Quick Check
> ![image.png](./Lectures_Readings.assets/20230302_2122134484.png)




## 2.3 Case Study in sampling bias
### 1936 Presidential Election
> ![image.png](./Lectures_Readings.assets/20230302_2122136433.png)![image.png](./Lectures_Readings.assets/20230302_2122138905.png)![image.png](./Lectures_Readings.assets/20230302_2122135256.png)




### Gallup's Poll
> ![image.png](./Lectures_Readings.assets/20230302_2122139915.png)![image.png](./Lectures_Readings.assets/20230302_2122136561.png)



## 2.4 Sampling Frame
### Population& Samples & Sampling Frame
> ![image.png](./Lectures_Readings.assets/20230302_2122147576.png)
> Sampling Frame isn't always equal to the population, and is typically smaller than the population.
> Sampling Frame will change depending on how you are trying to collect the samples.
> Those poeple that are in your sample, which are certainly in the sampling frame, may not be also in the population, which may induce bias.



### Common Bias
> ![image.png](./Lectures_Readings.assets/20230302_2122143348.png)
> **Selection Bias:** 样本有倾向性。
> **Response Bias:** 样本中有些人的回答不诚实。Depending on how you design your survey questions, people's response may cloud their real thoughts. For example, if you ask whether someone consume opium, lots of them won't be telling the truth.
> **Non-response Bias: **People who didn't fill in the survey.  我们不能假设那些没有填问卷的人和那些填问卷的人的脑回路是一致的，也就是说不能对那些没填问卷的人的最终的行为做任何看似合理的假设。Course Evaluation 可能会出现一种`Non-response Bias`。Barrier to fill up the survey should be low enough.



### Quick Check
#### Q1
> ![image.png](./Lectures_Readings.assets/20230302_2122142987.png)
> 因为我们的`Target Population`和`Sampling Frame`是一样的。


#### Q2
> ![image.png](./Lectures_Readings.assets/20230302_2122145467.png)



#### Q3
> ![image.png](./Lectures_Readings.assets/20230302_2122143482.png)
> **Selection bias: **样本倾向于选择支持民主党的人
> **Non-response bias:** 样本中有很多人没有完成问卷。




## 2.5 Probability Samples
### What is Probability Samples
> ![image.png](./Lectures_Readings.assets/20230302_2122146846.png)![image.png](./Lectures_Readings.assets/20230302_2122141709.png)


### (Simple) Random Samples
> ![image.png](./Lectures_Readings.assets/20230302_2122147692.png)![image.png](./Lectures_Readings.assets/20230302_2122155013.png)



### A very common approximation
> ![image.png](./Lectures_Readings.assets/20230302_2122153255.png)
> Probabilities of sampling with replacement(Not simple random sampling) is an approximation of simple random sampling when the population size is huge compared with sample size.



### Quick Check
#### Q1 Random Sampling
> ![image.png](./Lectures_Readings.assets/20230302_2122158793.png)
> The probability of getting a random sample of 20 students are the sample doesn't mean the probability of getting each student is the same.



#### Q2 Bayesian Formula
> ![image.png](./Lectures_Readings.assets/20230302_2122158631.png)
> 一个简单的贝叶斯公式的运用，条件概率。
> 假设事件$A$: 来自`Class A`, 事件$GA$: 获得A等第
> 假设事件$B$: 来自`Class B`, 事件$GB$: 获得B等第
> 根据贝叶斯公式: $\mathbb{P}(A|GA)=\frac{\mathbb{P}(GA|A)\mathbb{P}(A)}{\mathbb{P}(GA|A)P(A)+\mathbb{P}(GB|B)\mathbb{P}(B)}=\frac{30\%\times \frac{1}{5}}{30\%\times \frac{1}{5}+20\%\times \frac{4}{5}}=\frac{60}{60+160}=27\%$




## 2.6 Binomial& Multinomial Probability
### Basics
> ![image.png](./Lectures_Readings.assets/20230302_2122153248.png)![image.png](./Lectures_Readings.assets/20230302_2122155678.png)


### Binomial Probability
> ![image.png](./Lectures_Readings.assets/20230302_2122151663.png)





### Multinomial Probability
> ![image.png](./Lectures_Readings.assets/20230302_2122169925.png)



### Quick Check
#### Q1
:::info
![image.png](./Lectures_Readings.assets/20230302_2122163046.png)
:::


#### Q2
:::info
![image.png](./Lectures_Readings.assets/20230302_2122168110.png)
:::



## 2.7 Generalizing Bino&Multi-nomial Probability
### Binomial Probability 
> ![image.png](./Lectures_Readings.assets/20230302_2122165779.png)



### Multinomial Probability
> ![image.png](./Lectures_Readings.assets/20230302_2122168588.png)


### Quick Check
#### Q1
:::info
![image.png](./Lectures_Readings.assets/20230302_2122169091.png)
$\frac{3}{9}\times \frac{3}{9} \times \frac{3}{9}=(\frac{1}{3})^3$
:::


#### Q2
:::info
![image.png](./Lectures_Readings.assets/20230302_2122164027.png)
$\frac{3}{9}\times \frac{3}{9}\times \frac{3}{9}\times 3=(\frac{1}{3})^2$
:::

#### Q3
:::info
![image.png](./Lectures_Readings.assets/20230302_2122168127.png)
$C_3^1\frac{3}{9}\times C_2^1\frac{3}{9} \times C_1^1\frac{3}{9}=\frac{3!}{1!\times 1! \times 1!}(\frac{3}{9})^3=\frac{3!}{1!\times 1! \times 1!}(\frac{1}{3})^3$
:::

## 2.8 Permutations& Combinations
### Permutations
:::info
![image.png](./Lectures_Readings.assets/20230302_2122172958.png)![image.png](./Lectures_Readings.assets/20230302_2122178250.png)![image.png](./Lectures_Readings.assets/20230302_2122171511.png)
:::


###  Combinations
:::info
![image.png](./Lectures_Readings.assets/20230302_2122178913.png)![image.png](./Lectures_Readings.assets/20230302_2122173188.png)![image.png](./Lectures_Readings.assets/20230302_2122173419.png)
:::


### Quick Check
:::info
![image.png](./Lectures_Readings.assets/20230302_2122173484.png)
最后一题`Order Matters`
:::



## 2.9 Usage of Binomial Coefficients
### Order Doesn't Matter for Combinations
:::info
![image.png](./Lectures_Readings.assets/20230302_2122177758.png)![image.png](./Lectures_Readings.assets/20230302_2122187684.png)![image.png](./Lectures_Readings.assets/20230302_2122185570.png)![image.png](./Lectures_Readings.assets/20230302_2122184942.png)![image.png](./Lectures_Readings.assets/20230302_2122181774.png)
:::

### Quick Check
:::info
![image.png](./Lectures_Readings.assets/20230302_2122182900.png)
:::


# Lecture 3: Random Variables(Skipped)
[3. Random Variables.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1673440337779-31659d3d-c2b6-42eb-8b38-3beb49534133.pdf)


# Lecture 4: SQL
:::info
**Prereq:** CS61A
**Reading:** [Chapter 7](https://learningds.org/ch/07/sql_intro.html)
:::
[4. SQL.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1673440327222-2400e14a-24ae-4237-97ef-7f8726a54217.pdf)
[SQL-Cheat-Sheet-websitesetup.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1673568552559-5ebac6bb-02a8-40e9-a67f-cdc4670b201b.pdf)
[sqlReview.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1673568552562-cd89558d-8328-4640-aea4-d7bc03e03b47.pdf)
[sqlReviewSol.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1673568552554-a2da2536-d2d6-4642-808c-22fc3c467132.pdf)


## 4.1 Databases & DBMses
### Advantage of DBMS
:::info
![image.png](./Lectures_Readings.assets/20230302_2122187249.png)
:::

### Quick Check
:::info
![image.png](./Lectures_Readings.assets/20230302_2122185319.png)
:::


## 4.2 Database Schemas
### Terminology& Relation Schema
:::info
![image.png](./Lectures_Readings.assets/20230302_2122185190.png)![image.png](./Lectures_Readings.assets/20230302_2122186823.png)
:::


### Database Schema
:::info
![image.png](./Lectures_Readings.assets/20230302_2122191419.png)![image.png](./Lectures_Readings.assets/20230302_2122192244.png)
:::


### Database Implementations
:::info
![image.png](./Lectures_Readings.assets/20230302_2122191849.png)
:::

### Quick Check
:::info
![image.png](./Lectures_Readings.assets/20230302_2122191322.png)
:::

## 4.3 SQL Overview
### Basic Syntax
:::info
![image.png](./Lectures_Readings.assets/20230302_2122196998.png)
:::


### Distinct Syntax
> ![image.png](./Lectures_Readings.assets/20230302_2122196245.png)



### Quick Check
#### Q1
> ![image.png](./Lectures_Readings.assets/20230302_2122198157.png)
> 可以使用`from`和`where`来`Join Tables`, 后面会详细讲到。



#### Q2
> ![image.png](./Lectures_Readings.assets/20230302_2122203135.png)




## 4.4 Type of Joins
### Cross-Join(Cartesian Product)
> ![image.png](./Lectures_Readings.assets/20230302_2122203625.png)![image.png](./Lectures_Readings.assets/20230302_2122205953.png)




### Inner Join
> ![image.png](./Lectures_Readings.assets/20230302_2122205374.png)
> `JOIN = INNER JOIN` 




### Cross&Inner Join
> ![image.png](./Lectures_Readings.assets/20230302_2122205035.png)![image.png](./Lectures_Readings.assets/20230302_2122204162.png)



### Left Outer Join
> ![image.png](./Lectures_Readings.assets/20230302_2122207740.png)


### Right Outer Join
> ![image.png](./Lectures_Readings.assets/20230302_2122206923.png)


### Full Outer Join
> ![image.png](./Lectures_Readings.assets/20230302_2122211268.png)
> 很像是`I have something but you don't have, then I give you a NULL row to compensate that.`



### SQL Join Summary
> ![image.png](./Lectures_Readings.assets/20230302_2122219081.png)



### Quick Check
#### Q1
> ![image.png](./Lectures_Readings.assets/20230302_2122212906.png)




#### Q2
> ![image.png](./Lectures_Readings.assets/20230302_2122216060.png)![image.png](./Lectures_Readings.assets/20230302_2122218570.png)






## 4.5 NULL Values⭐⭐⭐⭐⭐
### Basics
> ![image.png](./Lectures_Readings.assets/20230302_2122215981.png)



### NULL in comparators
> ![image.png](./Lectures_Readings.assets/20230302_2122211204.png)



### Explicit NULL check - IS/IS NOT
> ![image.png](./Lectures_Readings.assets/20230302_2122219876.png)



### Aggregates Ignores NULLs⭐⭐⭐
> ![image.png](./Lectures_Readings.assets/20230302_2122218674.png)

**Solutions**![image.png](./Lectures_Readings.assets/20230302_2122221329.png)

### Quick Check
> ![image.png](./Lectures_Readings.assets/20230302_2122221303.png)





## 4.6 SQL Predicates&Casting
### SQL Predicates
> ![image.png](./Lectures_Readings.assets/20230302_2122225975.png)
> `like`可以看做是一种正则表达式的运用。`%`表示匹配任何字符。

 


### Type Casting
> ![image.png](./Lectures_Readings.assets/20230302_2122228402.png)




### Quick Check
#### Q1 Concept Check
> ![image.png](./Lectures_Readings.assets/20230302_2122223833.png)




#### Q2 Like Keyword 1
> ![image.png](./Lectures_Readings.assets/20230302_2122222271.png)



#### Q3 Like Keyword 2
> ![image.png](./Lectures_Readings.assets/20230302_2122225961.png)



## 4.7 SQL Sampling, Subqueries, and CTEs
### Sampling with LIMIT?
> ![image.png](./Lectures_Readings.assets/20230302_2122227908.png)
> 是一个`Probability Sample`, 前五行的概率是$1$, 其他的每一行的概率都是$0$。



### Random Sampling - SRS
> ![image.png](./Lectures_Readings.assets/20230302_2122233373.png)![image.png](./Lectures_Readings.assets/20230302_2122237738.png)



### Subqueries
> ![image.png](./Lectures_Readings.assets/20230302_2122233334.png)


### CTE - Temporary Tables
> ![image.png](./Lectures_Readings.assets/20230302_2122238671.png)



### Quick Check
#### Q1 SRS
> ![image.png](./Lectures_Readings.assets/20230302_2122238488.png)
> 这是一个`SRS`, 因为我们的样本大小是`5`, 对于每一次抽样所得的大小为`5`的样本，`Each pair/triple/so on`的概率都是一样的。



#### Q2 Subqueries
> ![image.png](./Lectures_Readings.assets/20230302_2122237443.png)


#### 
#### Q3 CTE
> ![image.png](./Lectures_Readings.assets/20230302_2122237193.png)



## 4.8 SQL CASE Expressions
### Case Expressions
> ![image.png](./Lectures_Readings.assets/20230302_2122241814.png)



### SUBSTR
> ![image.png](./Lectures_Readings.assets/20230302_2122242185.png)



### Quick Check
> ![image.png](./Lectures_Readings.assets/20230302_2122249748.png)



## 4.9 Summary
### Summary
> ![image.png](./Lectures_Readings.assets/20230302_2122247665.png)



### Quick Check
> ![image.png](./Lectures_Readings.assets/20230302_2122243536.png)



## 4.10 Code Walkthrough
[lec04.zip](https://www.yuque.com/attachments/yuque/0/2023/zip/12393765/1673578069543-87b401d4-6437-485e-8d07-3a520dd60f2c.zip)


