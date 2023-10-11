> Mathematics for Computer Science Chapter 3

[lec-3-handout.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1677206930276-dd93ab5f-7b26-452a-8fda-e67ab12487fc.pdf)
[Mathematical Induction.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1677206930276-e3912825-a856-47cb-a863-c9430de122d2.pdf)
# 1 Welling Ordering Principle
## Theorem Statement
> ![image.png](./Basic_Induction.assets/20230914_1451058275.png)
> In order to show that a set $S$is well-ordered, we can show that every subset of $S$has a minimum element.


## Prove Irrational
> 我们可以使用`Welling Ordering Property`来证明$\sqrt{2}$是无理数。
> ![image.png](./Basic_Induction.assets/20230914_1451079090.png)![image.png](./Basic_Induction.assets/20230914_1451093200.png)



## Proof Structure
> ![image.png](./Basic_Induction.assets/20230914_1451114405.png)


## Application of the proof structure
### Formula for summation
> ![image.png](./Basic_Induction.assets/20230914_1451136384.png)

**Proof By Well-ordering principle**![image.png](./Basic_Induction.assets/20230914_1451152537.png)![image.png](./Basic_Induction.assets/20230914_1451172240.png)


### Factors into primes
> ![image.png](./Basic_Induction.assets/20230914_1451182100.png)

**Proof by well ordering principle**![image.png](./Basic_Induction.assets/20230914_1451206124.png)![image.png](./Basic_Induction.assets/20230914_1451218237.png)


### Well Ordered Postage
> Available Stamps: stamps with value of$5$and $3$
> $n$is postal if can make $n+8$postage from $3$and $5$stamps
> **Thm: Every number **$n$**is postal.**

**Proof**Suppose that "every number is postal" is not true(这一步非常关键，这保证了的非空性，这样才能使用`Well Ordering Principle`). 假设, 则is not empty。根据`Well Ordering Principle`, 我们假设是`Least Element that is not postal`, 所以`is postal`。
因为时，, 时，且时，, 所以，于是, 所以。
所以是`Postal`, 所以是`Postal`, 这个`isn't postal`是矛盾的，于是得证。


### Geometric Sum
> **Thm:**$1+r+r^2+r^3+\cdots r^n=\frac{r^{n+1}-1}{r-1}$holds for $n\in \mathbb{N}$

**Proof**假设是我们的`Counterexample Set`，根据`Well-ordering principle`, 是最小的元素使得`Thm`不成立。
因为时，左侧, 右侧, 即左侧右侧。
所以, 所以, 且满足`Thm`的等式，也就是说:

然后等式两边加上, 所以: , 这表明也满足`Thm`, 这与我们开头的立论是矛盾的。所以得证。


## In-class Problems
[In-class problems session 3.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674124932399-d19f7924-18fb-4014-9dd1-aaedb00daf6d.pdf)

### P1 Fill in the Logic
> ![image.png](./Basic_Induction.assets/20230914_1451249536.png)

**Sample Solution(By showing that P(n) is a contradiction)**
1. 假设命题不成立，即is not empty.
2. 根据`Well-Ordering Property`, 我们知道是中最小的元素。
3. 因为时，, 所以, 且

 时，, 所以, 且

4. 如果成立，则成立。如果成立，则成立，所以推出矛盾。


### P2 Sum of square
> ![image.png](./Basic_Induction.assets/20230914_1451255324.png)

**Proof(By showing P(n) is a contradiction)****Claim:** 

1. 假设`Claim`不成立，则is not empty
2. 根据`Well Ordering Principle`, 
3. 因为时，`Claim`成立，所以, 于是, 于是时`Claim`成立。
4. 代入`Claim`中我们有: , 两边同时加上得到 , 这表明时`Claim`是成立的。而这和矛盾。


### P3 Lehman's Equation
> ![image.png](./Basic_Induction.assets/20230914_1451271472.png)

**Proof(Medium, by showing smaller contradiction)**![image.png](./Basic_Induction.assets/20230914_1451295301.png)![image.png](./Basic_Induction.assets/20230914_1451307293.png)

### P4 Bit Envelopes
> ![image.png](./Basic_Induction.assets/20230914_1451331502.png)

**Proof**![image.png](./Basic_Induction.assets/20230914_1451358400.png)


### P5 Sum of Integers
> ![image.png](./Basic_Induction.assets/20230914_1451375977.png)

**Proof**是最小的不能被表示成的线性组合的整数
因为, 所以, 所以
所以能被表示成的线性组合, 于是也能，即能，这推出矛盾。


## Exercises
### E1 Well Ordering Proof
> ![image.png](./Basic_Induction.assets/20230914_1451399276.png)



### E2 Well Ordered Set
> ![image.png](./Basic_Induction.assets/20230914_1451414672.png)

**Explanation**![image.png](./Basic_Induction.assets/20230914_1451435075.png)


### E3 Fibonacci Sequence
> ![image.png](./Basic_Induction.assets/20230914_1451458327.png)![image.png](./Basic_Induction.assets/20230914_1451478632.png)

**Explanation**![image.png](./Basic_Induction.assets/20230914_1451482049.png)



# 2 Ordinary Induction
## Rule for ordinary Induction
:::info
![image.png](./Basic_Induction.assets/20230914_1451504566.png)
:::


## Inference Rule for Induction
:::info
![image.png](./Basic_Induction.assets/20230914_1451518864.png)
:::



## Proof Structure
:::info
![image.png](./Basic_Induction.assets/20230914_1451535931.png)![image.png](./Basic_Induction.assets/20230914_1451563987.png)
:::


## Simple Induction Example
:::info
![image.png](./Basic_Induction.assets/20230914_1451572261.png)![image.png](./Basic_Induction.assets/20230914_1451582896.png)
根据`Inference Rule`, 我们只要证明:
![image.png](./Basic_Induction.assets/20230914_1452006251.png)
:::
**Analysis**![image.png](./Basic_Induction.assets/20230914_1452026279.png)
**Complete Proof**![image.png](./Basic_Induction.assets/20230914_1452036201.png)


## Induction vs Welling Ordering Principle
:::info
![image.png](./Basic_Induction.assets/20230914_1452059098.png)
:::



# 3 Strengthening Induction⭐⭐⭐⭐⭐
## Simple Example 1
> ![image.png](./Basic_Induction.assets/20230914_1452075174.png)

**Weak Hypothesis**![image.png](./Basic_Induction.assets/20230914_1452097388.png)
**Strong Hypothesis**![image.png](./Basic_Induction.assets/20230914_1452113927.png)

## Simple Example 2
> ![image.png](./Basic_Induction.assets/20230914_1452129112.png)

**Failed Induction**![image.png](./Basic_Induction.assets/20230914_1452146429.png)
$\sum_{i=1}^k\frac{1}{i^2}=1+\sum_{i=2}^k \frac{1}{i^2}<1+\sum_{i=2}^k\frac{1}{i(i-1)}=2-\frac{1}{k}<2$, 所以$\sum_{i=1}^k\frac{1}{i^2}$其实根本不会等于$2$。
此时$\sum_{i=1}^k\frac{1}{i^2}+\frac{1}{(k+1)^2}<2-\frac{1}{k}+\frac{1}{(k+1)^2}<2$
所以我们的`Inductive Hypothesis`其实也是有点问题的。
**Successful Induction**![image.png](./Basic_Induction.assets/20230914_1452161974.png)
`Exercise`:两边同乘以$k+1$后，得到 $-1-\frac{1}{k}+\frac{1}{k+1}\leq -1$, 成立。

## Coutyard Tiles
:::info
下面的例子非常重要，他阐释了我们可以通过`Induction analysis`来`Strengthen Induction`, 能够在得到一个更强的结论的同时证明原来的结论。
:::
**Problem Settings**![image.png](./Basic_Induction.assets/20230914_1452186832.png)![image.png](./Basic_Induction.assets/20230914_1452205326.png)

**Doomed Induction - Too Weak Induction**![image.png](./Basic_Induction.assets/20230914_1452214725.png)![image.png](./Basic_Induction.assets/20230914_1452243044.png)
**Successful Induction - Stronger Induction**![image.png](./Basic_Induction.assets/20230914_1452255676.png)![image.png](./Basic_Induction.assets/20230914_1452276186.png)![image.png](./Basic_Induction.assets/20230914_1452297429.png)![image.png](./Basic_Induction.assets/20230914_1452316882.png)


## When and Why to Use?
> ![image.png](./Basic_Induction.assets/20230914_1452331461.png)


# 4 Invariants⭐⭐⭐
## What are invariants?
:::info
One of the most important uses of induction in computer science involves proving that a program or process preserves one or more desirable properties as it proceeds. **A property that is preserved through a series of operations or steps is known as an invariant. **
Examples of desirable invariants include:

- A variable **never exceeding** a certain value
- The altitude of a plane **never dropping below** 1,000 feet without the wingflaps and landing gear being deployed
- The temperature of a nuclear reactor n**ever exceeding the threshold** for a meltdown.

**We typically use induction to prove that a proposition is an invariant.**
In particular, we show that the proposition is true at the beginning (this is the base case) and that if it is true after `t` steps have been taken, it will also be true after step t+1 (this is the inductive step). We can then use the induction principle to conclude that the proposition is indeed an invariant, namely, that it will always hold.  
:::


## Diagonally-Moving Robot Example
:::info
![image.png](./Basic_Induction.assets/20230914_1452358767.png)
:::
**Induction Analysis - Figuring out the predicate**![image.png](./Basic_Induction.assets/20230914_1452364088.png)
**Inductive Proof**![image.png](./Basic_Induction.assets/20230914_1452387050.png)![image.png](./Basic_Induction.assets/20230914_1452409488.png)


## The Invariant Method
:::info
![image.png](./Basic_Induction.assets/20230914_1452422088.png)
:::


## Puzzle Problems
### Problem Settings
:::info
![image.png](./Basic_Induction.assets/20230914_1452449544.png)![image.png](./Basic_Induction.assets/20230914_1452458676.png)![image.png](./Basic_Induction.assets/20230914_1452476661.png)
:::
**Graphic Interpretations**![image.png](./Basic_Induction.assets/20230914_1452499101.png)


### 8-puzzle
:::info
![image.png](./Basic_Induction.assets/20230914_1452511185.png)![image.png](./Basic_Induction.assets/20230914_1452539978.png)![image.png](./Basic_Induction.assets/20230914_1452549222.png)
:::



## Proof for puzzle problem
### Goal theorem
:::info
![image.png](./Basic_Induction.assets/20230914_1452565305.png)
:::


### Lemma 3.3.4 Row Move
:::info
![image.png](./Basic_Induction.assets/20230914_1452573256.png)
:::


### Lemma 3.3.5 Column Move
:::info
![image.png](./Basic_Induction.assets/20230914_1452595296.png)
:::


### Definition of inversion pair
:::info
![image.png](./Basic_Induction.assets/20230914_1453011218.png)
:::
**Examples**![image.png](./Basic_Induction.assets/20230914_1453026455.png)![image.png](./Basic_Induction.assets/20230914_1453031196.png)


### Lemma 3.3.7 # of inversion pairs
:::info
![image.png](./Basic_Induction.assets/20230914_1453058979.png)
:::



### Corollary 3.3.8 Unchangeable Parity
:::info
![image.png](./Basic_Induction.assets/20230914_1453076912.png)
:::


### Lemma 3.3.9 Odd parity of inversion
:::info
![image.png](./Basic_Induction.assets/20230914_1453088955.png)
:::
**Proof**![image.png](./Basic_Induction.assets/20230914_1453105255.png)



### Proof of the goal theorem
:::info
![image.png](./Basic_Induction.assets/20230914_1453127407.png)
:::



# 5 Strong Induction⭐⭐⭐⭐⭐
## Strong vs Ordinary Induction
:::info
![image.png](./Basic_Induction.assets/20230914_1453139519.png)![image.png](./Basic_Induction.assets/20230914_1453159404.png)![image.png](./Basic_Induction.assets/20230914_1453171001.png)
:::


## Rule for Strong Induction
:::info
![image.png](./Basic_Induction.assets/20230914_1453186091.png)
:::
**Remarks**![image.png](./Basic_Induction.assets/20230914_1453201035.png)


## Examples
:::info
本质上我们要在$P(k)(0\leq k\leq n)$的假设上验证$P(n+1)$的正确性，通常我们可以`Proof by Cases`, 在下面的例子中可以看到。
:::
### Product of Primes
:::info
![image.png](./Basic_Induction.assets/20230914_1453229149.png)
:::
**Proof**![image.png](./Basic_Induction.assets/20230914_1453243402.png)![image.png](./Basic_Induction.assets/20230914_1453267133.png)
> ![image.png](./Basic_Induction.assets/20230914_1453275252.png)
> 如果使用`Simple Induction`的话，我们手上的条件只有$P(41)$: 41 is a product of primes。因为$42$是合数且$42=6\times 7$, 所以$41\times 42 = 41\times 6\times 7$, 但是我们不知道$6$和$7$是不是Product of primes.



### Making Change
:::info
![image.png](./Basic_Induction.assets/20230914_1453297608.png)
:::
**Proof**![image.png](./Basic_Induction.assets/20230914_1453312332.png)![image.png](./Basic_Induction.assets/20230914_1453334304.png)


### The Stacking Game
:::info
![image.png](./Basic_Induction.assets/20230914_1453362160.png)![image.png](./Basic_Induction.assets/20230914_1453379231.png)
:::
**Theorem and Proof**![image.png](./Basic_Induction.assets/20230914_1453393995.png)![image.png](./Basic_Induction.assets/20230914_1453415695.png)


# 6 False Proofs
## A Bogus Proof⭐⭐⭐⭐⭐
:::info
![image.png](./Basic_Induction.assets/20230914_1453434063.png)![image.png](./Basic_Induction.assets/20230914_1453441324.png)
:::
**Bogus Proof**![image.png](./Basic_Induction.assets/20230914_1453466297.png)![image.png](./Basic_Induction.assets/20230914_1453487143.png)![image.png](./Basic_Induction.assets/20230914_1453509642.png)![image.png](./Basic_Induction.assets/20230914_1453518240.png)![image.png](./Basic_Induction.assets/20230914_1453539239.png)



