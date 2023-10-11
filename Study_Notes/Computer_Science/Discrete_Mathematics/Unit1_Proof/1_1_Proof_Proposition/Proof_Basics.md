> Mathematics for Computer Science Chapter 2

[lec-2-handout.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1677206621976-6217c156-5b2d-4470-9962-e1a7ac5a4254.pdf)
[Proofs.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1677206622008-367ad310-43e9-48b2-b281-4ec4345ebdf2.pdf)


# Notations 
## Set
> ![image.png](./Proof_Basics.assets/20230914_1455029263.png)


## Divides
> ![image.png](./Proof_Basics.assets/20230914_1455043407.png)
> 对于$a|b$来说，我们有$a\leq b$这个关系恒成立。



## Definition
> ![image.png](./Proof_Basics.assets/20230914_1455059780.png)


## Summary
> ![image.png](./Proof_Basics.assets/20230914_1455052061.png)


# The Axoimatic Method
## Theorems/Lemma/Corallary
> ![image.png](./Proof_Basics.assets/20230914_1455074201.png)


## ZFC Axioms⭐⭐⭐
> Zermelo-Fraenkel with Choice(ZFC) axioms. 
> ![image.png](./Proof_Basics.assets/20230914_1455106735.png)
> `Axioms are assumed to be true`:
> **Ex:** If a=b, b=c, then a=c



## Logical Deductions
> **Inference Rules&Modus Ponens:**
> ![image.png](./Proof_Basics.assets/20230914_1455118558.png)![image.png](./Proof_Basics.assets/20230914_1455138503.png)![image.png](./Proof_Basics.assets/20230914_1455156708.png)

**Examples of (not) sound inference rules**![image.png](./Proof_Basics.assets/20230914_1455177239.png)


# Patterns of Proof
## Direct Proof
> ![image.png](./Proof_Basics.assets/20230914_1455195836.png)


### Definition
> ![image.png](./Proof_Basics.assets/20230914_1455215509.png)



### Divide by 9 Example
> ![image.png](./Proof_Basics.assets/20230914_1455221181.png)

**Proof**![image.png](./Proof_Basics.assets/20230914_1455242572.png)
> ![image.png](./Proof_Basics.assets/20230914_1455262459.png)

**Proof**![image.png](./Proof_Basics.assets/20230914_1455272502.png)
> ![image.png](./Proof_Basics.assets/20230914_1455294432.png)



### Divide by 11 Example
> ![image.png](./Proof_Basics.assets/20230914_1455316213.png)

**Proof**![image.png](./Proof_Basics.assets/20230914_1455321173.png)
> ![image.png](./Proof_Basics.assets/20230914_1455336361.png)

**Proof**![image.png](./Proof_Basics.assets/20230914_1455358958.png)

> ![image.png](./Proof_Basics.assets/20230914_1455366505.png)


> ![image.png](./Proof_Basics.assets/20230914_1455396483.png)


## Proof By Cases
### Social Network Example
> ![image.png](./Proof_Basics.assets/20230914_1455407342.png)![image.png](./Proof_Basics.assets/20230914_1455422330.png)![image.png](./Proof_Basics.assets/20230914_1455447944.png)


### Irrational -> rational Example
> ![image.png](./Proof_Basics.assets/20230914_1455462294.png)

**Proof by cases**![image.png](./Proof_Basics.assets/20230914_1455472254.png)



### No rational solution
> ![image.png](./Proof_Basics.assets/20230914_1455484265.png)

**Proof by cases**![image.png](./Proof_Basics.assets/20230914_1455501225.png)


## Proof By Contradiction
> ![image.png](./Proof_Basics.assets/20230914_1455521360.png)


### Definition
> ![image.png](./Proof_Basics.assets/20230914_1455549726.png)
> **Remarks:**
> 1. 想要证明`If P holds, then Q holds`实际上就是在证明$P\implies Q$是`True`(因为`P`和`Q`都是`True`的, `holds`就是`True`的意思)。
> 2. 通过`Proof by contradiction`我们可以证明$\neg P\implies\neg R\land R=False$是`True`的, 即$True\implies P$是`True`的， 那么$P$只能是`True`了。
> 3. 这是因为`Implication`的`Non-consequences`性质(也叫`Modus Ponens Rule`)：对于一个`Implication`$p\implies q$来讲，如果$p$和$p\implies q$都是`True`的话，那么$q$就一定是`True`。



### Infinite prime numbers⭐⭐⭐⭐⭐
> ![image.png](./Proof_Basics.assets/20230914_1455551785.png)![image.png](./Proof_Basics.assets/20230914_1455578801.png)![image.png](./Proof_Basics.assets/20230914_1455596505.png)![image.png](./Proof_Basics.assets/20230914_1456002498.png)

**Proof**![image.png](./Proof_Basics.assets/20230914_1456027429.png)
> ![image.png](./Proof_Basics.assets/20230914_1456048664.png)



### Irrational number
> ![image.png](./Proof_Basics.assets/20230914_1456056194.png)

**Proof 1**![image.png](./Proof_Basics.assets/20230914_1456077375.png)
**Proof 2**![image.png](./Proof_Basics.assets/20230914_1456088785.png)


## Java Logical Expression
> ![image.png](./Proof_Basics.assets/20230914_1456105222.png)
> Prove by cases that this logic is equivalent to the following:
> ![image.png](./Proof_Basics.assets/20230914_1456123706.png)

**Proof by cases**![image.png](./Proof_Basics.assets/20230914_1456141915.png)![image.png](./Proof_Basics.assets/20230914_1456163281.png)

# Proving an Implication
> ![image.png](./Proof_Basics.assets/20230914_1456185707.png)



## Method 1-Direct Proof
> ![image.png](./Proof_Basics.assets/20230914_1456207620.png)

**Example**![image.png](./Proof_Basics.assets/20230914_1456216504.png)
**Logic Flow:**
![image.png](./Proof_Basics.assets/20230914_1456235300.png)
**Formal Proof:**
![image.png](./Proof_Basics.assets/20230914_1456249214.png)

## Method 2- Contrapositive
> ![image.png](./Proof_Basics.assets/20230914_1456264077.png)

**Example**![image.png](./Proof_Basics.assets/20230914_1456293106.png)

### Definition
> ![image.png](./Proof_Basics.assets/20230914_1456302291.png)



### Divide by odd Example
> ![image.png](./Proof_Basics.assets/20230914_1456326922.png)

**Proof by contrapositive**![image.png](./Proof_Basics.assets/20230914_1456346724.png)


### Lemma
> ![image.png](./Proof_Basics.assets/20230914_1456358703.png)

**Proof**![image.png](./Proof_Basics.assets/20230914_1456373243.png)



### Pigeonhole Principle
> ![image.png](./Proof_Basics.assets/20230914_1456387101.png)

**Proof by contrapositive**![image.png](./Proof_Basics.assets/20230914_1456399505.png)


## Method 3 - Contradiction
> 对于$P\implies Q$来说，他等价于$\neg P\lor Q$, 其`Contradiction`是$\neg(\neg P\lor Q)= P\land\neg Q$, 所以我们只需要在$P\land\neg Q$的基础上推演，推矛盾即可。
> 一旦$P\land\neg Q=F$, 则$\neg P\lor Q=T$, 则原`Implication`为`T`。


# Proving "If and only if"
## Method 1- Bi-directional
> ![image.png](./Proof_Basics.assets/20230914_1456417561.png)



## Method 2- Construct a Chian of Iffs
> ![image.png](./Proof_Basics.assets/20230914_1456436808.png)

**Example**![image.png](./Proof_Basics.assets/20230914_1456454325.png)![image.png](./Proof_Basics.assets/20230914_1456478205.png)![image.png](./Proof_Basics.assets/20230914_1456491184.png)


##  In-class Proofs
[In-Class Questions Session 1.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1673960544818-4dd9a8fc-d5b4-4378-93d8-d3d256fa4f99.pdf)

### Pythagorean Theorem - Proof By Picture
> ![image.png](./Proof_Basics.assets/20230914_1456507502.png)![image.png](./Proof_Basics.assets/20230914_1456521607.png)![image.png](./Proof_Basics.assets/20230914_1456532217.png)![image.png](./Proof_Basics.assets/20230914_1456553664.png)![image.png](./Proof_Basics.assets/20230914_1456564737.png)![image.png](./Proof_Basics.assets/20230914_1456587968.png)![image.png](./Proof_Basics.assets/20230914_1457003876.png)![image.png](./Proof_Basics.assets/20230914_1457016980.png)



### Ambiguity causes problems
> ![image.png](./Proof_Basics.assets/20230914_1457037877.png)
> (a):$\sqrt{-1}\sqrt{-1}=(\sqrt{-1})^2$不一定成立，因为我们知道$-1$有两个虚根$i,-i$, 即$\sqrt{-1}=i~~or~~-i$, 所以这里会造成歧义。
> (b): Consequence of $1=-1$, then $\frac{1}{2}=-\frac{1}{2}$, then $2=1$(亚里士多德的三段论)
> ![image.png](./Proof_Basics.assets/20230914_1457057379.png)



# Prove Logic Equivalence
> 假设我们要证明$n$个`Statements`: $P_1,P_2,\cdots, P_n$, 则: 我们只需要证明$P_1\implies P_2, P_2\implies P_2,\cdots, P_{n-1}\implies P_n, P_n\implies P_1$即可。


# Common errors in proof
## Lesson 1: Never assume the claim
> ![image.png](./Proof_Basics.assets/20230914_1457077045.png)



## Lesson 2: Divide by zero
> ![image.png](./Proof_Basics.assets/20230914_1457088259.png)


## Lesson 3: Negative numbers with inequality
> ![image.png](./Proof_Basics.assets/20230914_1457101996.png)




# ADT - Sets
[MIT6_042JS15_Sets.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674101624967-76b223a7-1c2a-4965-ad1d-635d1169f4e4.pdf)

## Definition
:::info
![image.png](./Proof_Basics.assets/20230914_1457127780.png)
![image.png](./Proof_Basics.assets/20230914_1457149196.png)
:::



## Some popular Sets
:::info
![image.png](./Proof_Basics.assets/20230914_1457165895.png)
:::


## Set Builder Notation
:::info
![image.png](./Proof_Basics.assets/20230914_1457179866.png)![image.png](./Proof_Basics.assets/20230914_1457188096.png)
![image.png](./Proof_Basics.assets/20230914_1457213503.png)
:::


## Set Relations
:::info
![image.png](./Proof_Basics.assets/20230914_1457222265.png)![image.png](./Proof_Basics.assets/20230914_1457248132.png)
:::

## Sets Operations
:::info
![image.png](./Proof_Basics.assets/20230914_1457255920.png)
:::
### Subset
:::info
![image.png](./Proof_Basics.assets/20230914_1457278943.png)![image.png](./Proof_Basics.assets/20230914_1457288550.png)![image.png](./Proof_Basics.assets/20230914_1457296925.png)
:::

### Proper/Strict Subset
:::info
![image.png](./Proof_Basics.assets/20230914_1457312186.png)
:::


### Union
:::info
![image.png](./Proof_Basics.assets/20230914_1457328635.png)![image.png](./Proof_Basics.assets/20230914_1457331517.png)
:::


### Intersection
:::info
![image.png](./Proof_Basics.assets/20230914_1457351337.png)![image.png](./Proof_Basics.assets/20230914_1457366881.png)
:::


### Set Difference
:::info
![image.png](./Proof_Basics.assets/20230914_1457377003.png)![image.png](./Proof_Basics.assets/20230914_1457396260.png)
:::


### Complements
:::info
![image.png](./Proof_Basics.assets/20230914_1457402462.png)![image.png](./Proof_Basics.assets/20230914_1457437531.png)
:::


### Cross Product
:::info
![image.png](./Proof_Basics.assets/20230914_1457454992.png)
:::


## Power Set
:::info
![image.png](./Proof_Basics.assets/20230914_1457464767.png)![image.png](./Proof_Basics.assets/20230914_1457481191.png)
:::


## Cardinality
:::info
![image.png](./Proof_Basics.assets/20230914_1457496489.png)
:::


## Sequences
:::info
![image.png](./Proof_Basics.assets/20230914_1457527306.png)
:::



## Quick Question
:::info
![image.png](./Proof_Basics.assets/20230914_1457524248.png)
:::



# Proof about Sets
## Prove Set Equalities
:::info
![image.png](./Proof_Basics.assets/20230914_1457544271.png)![image.png](./Proof_Basics.assets/20230914_1457564213.png)
:::
**Remarks**![image.png](./Proof_Basics.assets/20230914_1457584556.png)![image.png](./Proof_Basics.assets/20230914_1457591183.png)


## *Russell's Paradox and the Logic Sets


## *ZFC Axioms
