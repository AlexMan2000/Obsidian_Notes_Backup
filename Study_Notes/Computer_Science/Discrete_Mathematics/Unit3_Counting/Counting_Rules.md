[10 Counting.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1693226199102-a277a97d-ff1e-4c47-b5b5-b83977928ee0.pdf)
[MIT6_042JF10_chap11.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1693226194998-1117923e-1800-47d3-b949-5f93ec316b4d.pdf)



# Bijection Rule - Zero Rule of Counting
> ![image.png](./Counting_Rules.assets/20231109_1115046101.png)![image.png](./Counting_Rules.assets/20231109_1115063813.png)

**Example - 插板法**![image.png](./Counting_Rules.assets/20231109_1115081631.png)![image.png](./Counting_Rules.assets/20231109_1115104137.png)


# Counting Sequences
## Product Rule
> ![image.png](./Counting_Rules.assets/20231109_1115115236.png)
> **一般形式:**
> ![image.png](./Counting_Rules.assets/20231109_1115114242.png)![image.png](./Counting_Rules.assets/20231109_1115133804.png)
> **Permutation:**
> ![image.png](./Counting_Rules.assets/20231109_1115159508.png)

**Example - Counting Subsets Using Bijection**![image.png](./Counting_Rules.assets/20231109_1115171184.png)![image.png](./Counting_Rules.assets/20231109_1115182648.png)


## Sum Rule
> ![image.png](./Counting_Rules.assets/20231109_1115201118.png)

**Example - Counting Passwords Using Sum Rule and Product Rule**![image.png](./Counting_Rules.assets/20231109_1115223702.png)



## Division Rule - Second Rule of Counting
> ![image.png](./Counting_Rules.assets/20231109_1115244201.png)![image.png](./Counting_Rules.assets/20231109_1115262367.png)

**Example - Chess Problem**![image.png](./Counting_Rules.assets/20231109_1115289558.png)![image.png](./Counting_Rules.assets/20231109_1115292816.png)
**Example - Knights of the Round Table**![image.png](./Counting_Rules.assets/20231109_1115315344.png)![image.png](./Counting_Rules.assets/20231109_1115337737.png)


# Counting Subsets
## Subset Rule
> ![image.png](./Counting_Rules.assets/20231109_1115357965.png)

**Proof**![image.png](./Counting_Rules.assets/20231109_1115374117.png)
比如说$\{3,1,2,5,4,6\}$和$\{1,2,3,4,6,5\}$都会被映射到$\{1,2,3\}$这个集合。


## Bit Sequence
> ![image.png](./Counting_Rules.assets/20231109_1115398797.png)![image.png](./Counting_Rules.assets/20231109_1115403478.png)




# Sequences with Repetitions
## Subset Split Rule
> ![image.png](./Counting_Rules.assets/20231109_1115424258.png)![image.png](./Counting_Rules.assets/20231109_1115437452.png)

**Proof**![image.png](./Counting_Rules.assets/20231109_1115466653.png)



## Bookkeeper Rule
> ![image.png](./Counting_Rules.assets/20231109_1115483589.png)

**Example 1- Bookkeeper**![image.png](./Counting_Rules.assets/20231109_1115498877.png)![image.png](./Counting_Rules.assets/20231109_1115527348.png)
**Example 2- Ordering Strings**![image.png](./Counting_Rules.assets/20231109_1115549578.png)
**Example 3- String - CS70 Fa20 Disc06a**![image.png](./Counting_Rules.assets/20231109_1115554022.png)![image.png](./Counting_Rules.assets/20231109_1115565368.png)
**Example 4 - Assigning Tasks - MIT Reci15**![image.png](./Counting_Rules.assets/20231109_1115588644.png)![image.png](./Counting_Rules.assets/20231109_1116009850.png)
**Example 5 - Mixing Pokers**![image.png](./Counting_Rules.assets/20231109_1116012915.png)


## Exercises
### Socks - Medium
> For the following problem, we will use 1,2,3,4,5 to denote 5 friends.
> ![image.png](./Counting_Rules.assets/20231109_1116037303.png)
> There is a bijection from {(1, sock pair 1), (2,  sock pair 2), (3,  sock pair 3), (4,  sock pair 4), (5,  sock pair 5)} to the number of roommate-sock combinations.
> Thus the problem is equal to count the permutation of sock pair, which is $10\times 9\times 8\times 7\times 6=30240$
> ![image.png](./Counting_Rules.assets/20231109_1116043918.png)
> There is a bijection from the bit sequence 0010101011(where 1 denote the color that is choosed) to the number of combinations, which is $(^{10}_5)=252$.
> ![image.png](./Counting_Rules.assets/20231109_1116063653.png)
> The probability is just equal to $\frac{1}{252}\approx 0.00397$, where the sequence is 0000011111(For example).
> ![image.png](./Counting_Rules.assets/20231109_1116086887.png)
> We could break into two cases. If the jealous roommate choose any one of pink, red, or teal socks, then there are 7 choices left to the rest of the roommates, thus there are $3\times 7\times 6\times 5\times 4$ways. If the jealous roommate choose any one of the socks other than pink, red, or teal(7 ways to choose), then there are 6 choices left to the rest of the roommates, thus there are $7\times (6\times 5\times 4\times 3)$, and we add them up to get $5040$。
> ![image.png](./Counting_Rules.assets/20231109_1116115752.png)
> This is a situation where the jealous roommate and the rest are choosing socks from two disjoint sets, one has size 3 and the other has size 7. Thus we have $3\times 7\times 6\times 5\times 4=2520$
> ![image.png](./Counting_Rules.assets/20231109_1116122259.png)
> There is a bijection from {(jealous, color he choose), (0010101)} to the number of combinations, thus we have $3\times (^7_3)=105$



### SUPERMAN - Medium
> ![image.png](./Counting_Rules.assets/20231109_1116146426.png)![image.png](./Counting_Rules.assets/20231109_1116165507.png)![image.png](./Counting_Rules.assets/20231109_1116184758.png)
> 标答是210。



### Digit Sequence
> ![image.png](./Counting_Rules.assets/20231109_1116187091.png)

**Solution (a)**$(^{10}_5)=252$
**Solution (b)**![image.png](./Counting_Rules.assets/20231109_1116208645.png)

# Combinatorial Proofs
## Binomial Theorem
### Main Theorem
> ![image.png](./Counting_Rules.assets/20231109_1116205159.png)

**Rigorous Proof**![image.png](./Counting_Rules.assets/20231109_1116227793.png)
**Proof by Bookkeeper Rule**![image.png](./Counting_Rules.assets/20231109_1116254686.png)![image.png](./Counting_Rules.assets/20231109_1116269523.png)


### Properties of Coefficient
> ![image.png](./Counting_Rules.assets/20231109_1116263390.png)

**Solution**![image.png](./Counting_Rules.assets/20231109_1116286627.png)


### Corollaries
> ![image.png](./Counting_Rules.assets/20231109_1116285279.png)

> ![image.png](./Counting_Rules.assets/20231109_1116285373.png)

**Proof**![image.png](./Counting_Rules.assets/20231109_1116304447.png)


## Multinomial Theorem
> ![image.png](./Counting_Rules.assets/20231109_1116305873.png)

**Proof by Bookkeeper Rule**![image.png](./Counting_Rules.assets/20231109_1116324329.png)


## Useful Combinatorial Identities
### Proof Techniques⭐⭐⭐⭐⭐
> ![image.png](./Counting_Rules.assets/20231109_1116346964.png)


### Split Pairs
> ![image.png](./Counting_Rules.assets/20231109_1116348128.png)



### Pascal Identity
> ![image.png](./Counting_Rules.assets/20231109_1116358352.png)

**Proof by Geometry**![image.png](./Counting_Rules.assets/20231109_1116378170.png)
**Proof by Reasoning**![image.png](./Counting_Rules.assets/20231109_1116386910.png)


### Recurrence
> ![image.png](./Counting_Rules.assets/20231109_1116389440.png)



## Hocky-Stick Identity
> ![image.png](./Counting_Rules.assets/20231109_1116383039.png)

**Proof**![image.png](./Counting_Rules.assets/20231109_1116406711.png)



## Exercises
### Identities Proof
> ![image.png](./Counting_Rules.assets/20231109_1116403075.png)

**Proof**![image.png](./Counting_Rules.assets/20231109_1116423123.png)
> ![image.png](./Counting_Rules.assets/20231109_1116442434.png)


# Sampling Procedure
## Without Replacement
> ![image.png](./Counting_Rules.assets/20231109_1116454234.png)



## With Replacement
### Order Matters
> ![image.png](./Counting_Rules.assets/20231109_1116456547.png)


### Order Doesn't Matter⭐⭐⭐⭐⭐
> ![image.png](./Counting_Rules.assets/20231109_1116473948.png)![image.png](./Counting_Rules.assets/20231109_1116489928.png)



### Stars and Bars⭐⭐⭐
> ![image.png](./Counting_Rules.assets/20231109_1116481416.png)

**Sum of Integers - CS70 Fa20 Disc06B**![image.png](./Counting_Rules.assets/20231109_1116484768.png)![image.png](./Counting_Rules.assets/20231109_1116481195.png)![image.png](./Counting_Rules.assets/20231109_1116483573.png)
**Fruit Distribution - MIT18.042J Recitation 15**![image.png](./Counting_Rules.assets/20231109_1116495679.png)![image.png](./Counting_Rules.assets/20231109_1116509646.png)


## Balls and Bins Problems
### Balls and Bins
> ![image.png](./Counting_Rules.assets/20231109_1116521634.png)![image.png](./Counting_Rules.assets/20231109_1116541216.png)



### Processors and Servers
> ![image.png](./Counting_Rules.assets/20231109_1116557306.png)



## Summary
> ![image.png](./Counting_Rules.assets/20231109_1116572478.png)





# Inclusion-Exclusion
## Main Theorem
> ![image.png](./Counting_Rules.assets/20231109_1116571026.png)![image.png](./Counting_Rules.assets/20231109_1116595693.png)

**Proof - Hard**![image.png](./Counting_Rules.assets/20231109_1117012521.png)![image.png](./Counting_Rules.assets/20231109_1117022239.png)


## Computing Examples
### Example 1: Phone Numbers
> ![image.png](./Counting_Rules.assets/20231109_1117046104.png)


### Example 2: Word Permutations
> ![image.png](./Counting_Rules.assets/20231109_1117061268.png)![image.png](./Counting_Rules.assets/20231109_1117065108.png)

**Solution - 1**![image.png](./Counting_Rules.assets/20231109_1117082748.png)
**Solution - 2**![image.png](./Counting_Rules.assets/20231109_1117099085.png)
**Solution - 3**![image.png](./Counting_Rules.assets/20231109_1117111336.png)
**Solution - 4**![image.png](./Counting_Rules.assets/20231109_1117131815.png)
**Solution - 5**![image.png](./Counting_Rules.assets/20231109_1117153143.png)
**Solution - 6**![image.png](./Counting_Rules.assets/20231109_1117161116.png)


### Example 3: Strings
> ![image.png](./Counting_Rules.assets/20231109_1117175715.png)
> 长度为`5`的。
> 题目的意思是，我的`string`中至少含有`A,B,C`各一次及以上，那我们可以考虑问题的反面，即`string`中不含有`A`或者`B`或者`C`。类似于$(A\cap B\cap C)^c=(A\cap B)^c\cup C^c=A^c\cup B^c\cup C^c$

**Solution**![image.png](./Counting_Rules.assets/20231109_1117188199.png)


### Example 4: Palindromes
> ![image.png](./Counting_Rules.assets/20231109_1117182316.png)

**Solution**![image.png](./Counting_Rules.assets/20231109_1117192472.png)


# Famous Counting Problems
## Poker Hands
### Five Card Draw
> ![image.png](./Counting_Rules.assets/20231109_1117221432.png)![image.png](./Counting_Rules.assets/20231109_1117231077.png)




### Four-of-a-Kind
> ![image.png](./Counting_Rules.assets/20231109_1117257995.png)




### Full House
> ![image.png](./Counting_Rules.assets/20231109_1117275602.png)




### Two Pairs⭐⭐⭐⭐⭐
> ![image.png](./Counting_Rules.assets/20231109_1117305448.png)![image.png](./Counting_Rules.assets/20231109_1117329218.png)![image.png](./Counting_Rules.assets/20231109_1117337733.png)

**Another Approach**![image.png](./Counting_Rules.assets/20231109_1117351805.png)


### Hands with Every Suit
> ![image.png](./Counting_Rules.assets/20231109_1117372989.png)![image.png](./Counting_Rules.assets/20231109_1117396281.png)



## Derangement⭐⭐⭐⭐⭐
### Motivation
> ![image.png](./Counting_Rules.assets/20231109_1117403652.png)![image.png](./Counting_Rules.assets/20231109_1117428578.png)



### Definition
> ![image.png](./Counting_Rules.assets/20231109_1117436242.png)![image.png](./Counting_Rules.assets/20231109_1117441934.png)

**Proof**![image.png](./Counting_Rules.assets/20231109_1117464866.png)![image.png](./Counting_Rules.assets/20231109_1117487461.png)
![image.png](./Counting_Rules.assets/20231109_1117509869.png)
> ![image.png](./Counting_Rules.assets/20231109_1117527163.png)

**Proof of Boundary Conditions**$D_1$本质上就是一个元素的重排，但是一个元素不能`Derange`，所以$D_1=0$。
$D_2$本质上是两个元素的重排，有一种情况, 就是交换顺序，所以$D_2=1$。



# Applications
## Graph 
### Graph Path⭐⭐⭐⭐⭐
> ![image.png](./Counting_Rules.assets/20231109_1117539494.png)![image.png](./Counting_Rules.assets/20231109_1117541904.png)
> 本题涉及到`Hypercube`的代数性质，就是我在`Hypercube`上的`Edge`移动相当于`Flip One Bit`。

**(a)**![image.png](./Counting_Rules.assets/20231109_1117551284.png)
最短路径可以理解为我每次都`Flip one bit from 0 to 1`, 且从来不`Flip the bit from 1 to 0`。因为假设我们已经`Flip`了`i`次，则我们的序列中已经有了`i`个`1`的存在，那么下一次我们只能`Flip``n-i`个剩余的`0`。这也就意味着在`Step i`时我们只有`n-i`个选择，所以我们有$n\cdot (n-1)\cdot (n-2)\cdots1=n!$种路径。
**(b)⭐⭐⭐**我们考虑一个较为简单的问题，比如说我们有一个`3-bit Hypercube`, 则根据第一问的描述，我们从`0`到$2^3-1$的最短路径长度是$3$，比如`000->001->101->111`, 每次`Flip`一个`bit`。
但是现在我们要求长度为$5$的路径个数，其实就是在最短路径的基础上我们在某一个`step`的时候将`1 flips back to 0`了，表现在图上就是我们走了一条回头路。
所以问题可以拆解成三部分:

1. 我先走到`Step i`(保证路径最短，有$n\times (n-1)\times \cdots\times (n-i+1)=\frac{n!}{(n-i)!}$种)，
2. 然后因为在`Step i`的时我们走了回头路，但是我们不知道走了哪一条回头路，但是回头路有`i`种选择(因为走了`Step i`的时候我们的序列中已经有`i`个`1`了，所以我们有`i`种将`1 flip backs to 0`的方法)。有$i$中回头路。
3. 在走完回头路之后我们的序列中有`n-i+1`个`0`, 此时我们开始`Flip 0 to 1`并且取最短路径，有$(n-i+1)!$种路径

三个部分乘起来得到$\frac{n!}{(n-i)!}\times i\times (n-i+1)!$, 但这只针对$i$的情况，我们需要考虑$i=1,2,\cdots, n$的所有情况，于是结果为: $\begin{aligned}\sum_{i=1}^n \frac{n!}{(n-i)!}\times i\times (n-i+1)!&=\sum_{i=1}^n \frac{n!}{(n-i)!\times i!}\times i!\times i\times (n-i+1)!\\&=\sum_{i=1}^n (^n_i)\times i!\times i\times (n-i+1)!\end{aligned}$
![image.png](./Counting_Rules.assets/20231109_1117574030.png)
**(c)**我们写成二进制会好理解一些:
$3_{2}=00000011$, $19_2=00010011$, $63_2=00111111$
从$0\to 3$我们需要`Flip 2 bits`, 有$2!$种。
从$3\to 19$我们需要`Flip 1 bit`, 有$1$种。
从$19\to 63$我们需要`Flip 3 bits`, 有$3!$种。
总共$2\times 3!$种。


### Random Graph
> ![image.png](./Counting_Rules.assets/20231109_1117587994.png)



