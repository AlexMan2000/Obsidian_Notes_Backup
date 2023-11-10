[Lecture Note 3.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1662729962635-2540a918-91b5-4669-ab2d-fec1cc672a96.pdf)
# 
# 1 Ordered Set and Bound
## 1.1 Ordered Set
:::info
![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152414373.png)
常见的`Ordered Set`:
![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152424960.png)

- 导数第二个例子中，我们回顾一下笛卡尔积的定义:$\mathbb{Q}\times \mathbb{Q}=\{(a,b):a\in A,b\in B\}$
- 最后一个例子中，我们说$\mathcal{P}(\mathbb{N})$不是一个`Ordered Set`, 因为我们知道如果一个集合是一个有序集的话，必须满足`trichotomy`和`transitivity`两个性质，而对于$\{0\},\{1\}\in \mathcal{P}(\mathbb{N})$, 我们知道$\{0\}\neq \{1\}$, 于是我们期望有$\{0\}>\{1\}$或者$\{0\}<\{1\}$的关系存在，但是我们没有定义过这样的比较关系，所以$\mathcal{P}(\mathbb{N})$不是`Order Set`。
:::

## 1.2 (Least) Upper/Lower Bound
:::info
![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152427491.png)![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152428376.png)
注意，`upper bound`的定义只有在`ordered set`上才有意义。因为这时候不等式才有数学意义。
一个简单的例子就是$S:=\{a,b,c,d,e\}$, 且$E:=\{a,c\}$。
此时$c,d,e$都是$E$的`Upper Bounds`, 且$c$是$E$的`Least Upper Bound`, 也记作$sup E$(`Supremum of E`)
值得注意的是，**一个集合**$E$**的**$sup$**或者**$inf$**不一定要在集合**$E$**本身中，但是一定要在集合**$E$规定的定义域中, 也就是集合$S$中:

- 对于$E:=\{x\in \mathbb{Q}:x<1\}$, 此时$x$的定义域是有理数集$\mathbb{Q}$(因为$E\subset \mathbb{Q}$)，那么此时$sup E=1$, 但是$1$不在集合$E$中，但在定义域中。
- 对于$G:=\{x\in \mathbb{Q}:x\leq 1\}$来说，此时$sup G=1$, 且$1$在集合$G$中。

**一个集合**$E$**可能没有**$sup$**存在**，造成这种现象的原因有很多，比如

- $P:=\{x\in \mathbb{Q}:x\geq 0\}$没有`Least Upper Bound`, 因为首先$P\subset \mathbb{Q}$, 而且对于$\forall y\in Q,\exists x\in P, s.t. x>y$(而不是小于等于)。此时$P$是一个`Countably Infinite Set`。但幸运的是$P$有$inf P=0$。
- 也有可能这个上界不在我们的定义域内，比如集合$T=\{x\in Q:x^2<2\}$, $T\subset \mathbb{Q}$, 我们知道如果最小上界存在，那一定是$\sqrt{2}$, 但是很不幸，$\sqrt{2}\notin \mathbb{Q}$, 因此$T$没有最小上界。
:::
**Least Upper Bound Figure 1.1**![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152442794.png)


## 1.3 Well-Ordering Property of N
> 对于一个自然数集$\mathbb{N}$来说，其`Well-Ordering Property`说的是，$\forall E\subset \mathbb{N}$, 都存在一个`Least Element`$k\in \mathbb{E},s.t.\forall k_t\in \mathbb{E} ,~~k\leq k_t$。
> ![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152446937.png)


## 1.4 Least Upper Bound Property
:::info
![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152455826.png)
这个定理说的是对于一个有序集合$S$, 如果它有`Lease-Upper-Bound Property`, 则对于其任何非空子集$E$，如果$E$有上界，则$E$一定有一个最小上界存在。
几个例子:

1. 假设$S=\{0,1\}(0<1)$, 则对于$S$的非空子集，

$E_1=\{0\},sup E_1=0\in S$,
$E_2=\{1\}, sup E_2=1\in S$, 
$E_3=\{0,1\}, sup E_3=1\in S$, 所以$S$有`Least Upper Bound Property`

2. 假设$S=\{-1,-2,-3,-4,\cdots \}=-\mathbb{N}$, 我们知道$\forall E\subset S$, $E$的上界是$-1$, 所以所有$S$的非空子集都是`Bounded above by`$-1$。下面我们将证明所有$S$的非空子集都有其最小上界:

对于$\forall E\subset S$, 构造$-E=\{-x:x\in E\}\subset \mathbb{N}$(bijection from $E$to $-E$), 所以根据自然数集的`Well-Ordering Property`, $\exists m\in -E$, 使得$m\leq -x ,\forall x\in E$, 所以$\exists -m\in E$and$\forall x\in E,x\leq -m$, 所以$-m=supE$。所以$S$具有`LUBP`

3. $\mathbb{Z}$有`LUBP`
4. $\mathbb{Q}$没有`Least-upper-bound property`这个事实也是我们喜欢在$\mathbb{R}$上做实数分析的原因。这个性质的缺失导致很多的代数性质不能够被使用。
:::
> ![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152454995.png)
> 这个定理的意思是: 如果集合$\{q\in \mathbb{Q}|q>0,q^2<2\}$存在一个最小上界$sup=x$, 则这个最小上界$x$一定满足: $x>0~and ~x^2=2$
> ![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152452808.png)

**Proof of Theorem 14**![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152457721.png)![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152456378.png)
**Proof of Theorem 15**先证明$E$是`Bounded Above`的，因为$\forall q\in E, q^2<2<4$, 所以$\forall q\in E, q<2$, 于是$E$是`Bounded Above`的。
然后证明`Least Upper Bound`不存在。
![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152452600.png)



# 2 域和实数集
[Lecture Note 4.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1667013485653-5ecee2ad-4465-4e56-8cd9-fbaf7675ad67.pdf)
## 2.1 Field
### 2.1.1 Definitions 
:::info
我们喜欢在实数集上做分析的原因之一是实数集是因为一个`Field`，换句话说，实数集加法和数乘封闭。在线性代数线性算子视角下我们研究过这个问题: [multiplicative inverse](https://www.yuque.com/alexman/so5y8g/wal3n1#YWbtI)
![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152461062.png)
$A4$是`Zero Indentity`, $A5$是`Additive Inverse`
使用这些公理就可以用证明`Field`的很多其他运算性质。
:::
**整数集不是Field**![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152476867.png)
> 有些集合在加上一些外置条件之后也可以成为`Field`, 比如下面的两个例子:
> ![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152472509.png)



### 2.1.2 Properties
> ![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152471995.png)
> **证明:** $0=0x+(-0x)=(0+0)x+(-0x)=0x+0x-0x=0x$



## 2.2 Ordered Field
### 2.2.1 Definition
> 一个`Field`$F$称为`Ordered Field`如果$F$是一个满足下列条件的`Ordered Set`:
> 1. $\forall x,y,z\in F, x<y\Rightarrow x+z<y+z$
> 2. $\forall x,y\in F, x>0\space and\space y>0\Rightarrow xy>0$
> 
![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152479025.png)

**有理数集是Ordered Field**
**复数集不是Ordered Field**![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152498359.png)
**Z={0,1}不是Ordered Field**![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152495468.png)


### 2.2.2 Ordered Field 的性质
> ![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152498167.png)

**Proof**![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152519312.png)
**对于的证明:**

**对于的证明:**

**对于的证明:**
可以拆分成四种情况来看:

1. , 则, 所以, 于是
2. , 则
3. , 则
4. , 则

所以
:::info
![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152518565.png)
**我们可以从其逆否命题入手证明:**
![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152519371.png)![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152518184.png)
:::

## 2.3 Greatest Lower Bound Property
> ![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152529939.png)
> 对于一个`Ordered Field`而言，他不仅仅有`Least Upper Bound Property`也有`Greatest Lower Bound Property`

**Proof**![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152521334.png)


## 2.4 Uniqueness of Ordered Field
> ![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152527721.png)
> ![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152526182.png)

**Insights**![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152525752.png)
> ![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152521211.png)



# 3 Assignment/Recitations
[hw2.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1667285380014-ec73a985-b4e5-4c99-ba06-e6aa9e8cc604.pdf)
[Recitation 1.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1667527191762-027ad8fc-2caf-4b08-96a1-30c8011dcd5d.pdf)

## P1 Ordered Field Property
> ![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152532860.png)

**Proof**

## P2 Ordered Set
> ![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152531920.png)

**Proof**Suppose we have a set  of size , and we use the induction to prove the proposition:

1. When , the set has exactly one element, and let's denote it by , in this case the set is bounded by and 
2. Suppose when , the proposition is true such that is bounded and that 
3. Then when , we will introduce a new element called to the set , and we know that adding a single element to the set doesn't change the boundedness of  and there are three cases for :
   1. , then , 
   2. , then , 
   3. , then , 

Thus we can conclude the proof by induction.


## P3 Supremium
> ![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152537944.png)

**Proof**Since $b$is an upper bound for $A$, so $\forall a\in A$, we have $a\leq b$. Also, by the definition of the upper bound and the least upper bound, we know that $b\geq supA$.
Suppose $b>supA$, since the relationship $b>supA\geq a,\forall a$always holds. Since $b\in A$, this simply contradicts the definition of $supA$. Thus $b=supA$. The proof is finished.

## P4 Countability 
> ![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152539519.png)

**Proof**Suppose the largest element in $A$is $a_n$, then $a_n=supA\in A$. However, $supA\notin A$. So $a_n$isn't the largest element in $A$, which means there exists $a_{n+1}$such that $a_n<a_{n+1}<supA$. 
With this fact in mind, we can construct a set $A=\{a_n,n\in \mathbb{Z}\}$which is countably infinite.

## P5 AM-GM Inequality
> ![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152536527.png)

**Proof**因为, 欲证明, 我们只要证明。当时，, 所以。当时，, 此时。证毕。
:::info
**Prove the Generalized Version:**
![Screen Shot 2022-11-02 at 11.21.41 AM.png](./L3_L4__实数集和LUBP.assets/20231110_1152534565.png)
**Methodology:**
![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152548473.png)
:::
**Proof**![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152546242.png)![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152542852.png)![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152541076.png)


## P6 Addition of Sup/Inf
> ![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152546389.png)

**Proof of the first part**
1. 证明存在性: 因为都是有界的，所以, 所以, 所以是集合的上界。因为且具有`LUBP`, 所以存在。
2. 证明相等性: 首先证明, 因为, 有, 所以, 于是是的上界，于是, 于是, 于是时的上界，于是, 所以。

然后证明, 这个结论显然。
综上
**Proof of the second part**
1. **证明存在性:**

因为都是有界的，于是和均存在，于是, 所以, 所以是的`Lower Bound`, 因为且具有`LUBP`, 所以存在。

2. **证明相等性:**

首先证明, 因为
然后证明, 这个结论显然。
综上, 证毕。


## P7 Multiplication of Sup/Inf
### Positive Real Numbers
> ![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152546819.png)

**Proof**
1. **证明存在性:**

![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152554183.png)

2. **证明相等性:**

![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152558334.png)![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152553698.png)

### Nonnegative Real Numbers
:::info
![Screen Shot 2022-11-02 at 11.23.04 AM.png](./L3_L4__实数集和LUBP.assets/20231110_1152551058.png)
:::
 **Proof of the first part**
1. 首先证明有上界。因为都是非空且有界的集合，且, 因为具有`Least Upper Bound Property`, 所以和存在，且满足且, 因为均为非负实数，即, 所以, 所以, 因为,于是是的上界。因为, 且具有`LUBP`, 所以存在。
2. 证明是的最小上界。即。如果我们要证明等式的话其实等价于证明和同时成立。
   1. 首先证明, 此时我们知道。
      1. 如果或者, 则, 此时成立。
      2. 否则，, 我们按照`Positive Real Numbers`中的思路证明就能得到成立(只要取那些即可)
   2. 然后证明, 这个结论显然。

综上, 
**Proof of the second part**
1. **首先证明存在性:**

首先因为都是`Bounded Set`, 所以且, 于是对于, 于是是集合的`Lower Bound`, 因为且具有`Least Upper Bound Property/Ordered Field`，所以存在。

2. **然后证明相等性:**
   1. 证明,  
      1. 如果, 则, 此时成立。
      2. 因为, 所以我们取任意的使得, 于是
   2. 证明，这个结论显然。

综上，

## P8 Construction Methods
> ![image.png](./L3_L4__实数集和LUBP.assets/20231110_1152558825.png)

**(a)**因为, 所以, 于是is bounded above, 证毕。
**(b)**
1. 因为, 所以存在，因为, 因为, 则, 所以, 于是
2. 假设, 我们现在要证明, 于是我们可以转而证明和同时成立:
   1. 证明，使用反证法，假设, 我们想要找到矛盾点使得, 于是我们考虑构造一个, 使得, 这样就不是的`Upper Bound`了。怎么构造呢，我们可以反推。

因为, 我们令, 而且很显然我们有:, 并且这个不等式恒成立，所以。
于是
于是且, 于是, 矛盾。所以。

   2. 证明。还是一样使用反证法，假设, 我们想要构造出一个矛盾使得, 这样。怎么构造呢? 注意到要想成立(即)，需要是的一个上界。因为, 于是至少得大于, 于是我们得选取一个同时的使得。于是我们观察。换句话说，我们只需要找到使得且同时成立的即可。

于是，我们可以选取，这样根据假设， 所以, 		另外，我们可以验证，而这个不等式恒成立。所以:
, 所以。
所以, 于是, 矛盾，于是成立。
综上，我们有成立。证毕。
