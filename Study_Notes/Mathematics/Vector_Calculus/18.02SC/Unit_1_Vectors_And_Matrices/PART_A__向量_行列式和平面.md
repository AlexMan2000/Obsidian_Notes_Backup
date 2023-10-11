# 2 矢量分解和投影
[Components and Projection.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1658713065749-3e538d8a-ad50-4db5-b2a3-2a7c961671ab.pdf)
## 2.1 矢量分量
### 定义
:::success
`**Vector Component**`**: 是一个**`**Scalar**`**, 描述一个非单位向量在其他向量方向上的投影长度**
`**Orthogonal Projection**`: 正交投影，非常重要的概念, 本质就是将一个向量投影到一个单位向量方向上的长度
**标准定义:**
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038069760.png)
**图解:**
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038064443.png)
**重要性质:**
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038064875.png)
:::


### 快速求解方法
:::info
给定向量$\bf a,b$, 我们要求$\bf{a}$在$\bf{b}$方向上的`Vector Components`, 我们可以直接$\frac{\bf a\cdot b}{\bf |b|}$求得
:::

### 示例1: 求投影
:::success
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038079784.png)
:::
:::info

1. **通过**$|\vec{A}||\vec{B}|cos(\theta)$**求投影**

![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038076915.png)

2. **通过向量点乘求投影**

![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038078679.png)

3. **投影值可以负数，因为投影本质上只是一个标量，标量可正可负，取决于向量和投影方向的张角的**$cos$**值大小**

![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038078803.png)
:::



### 示例2: 物理系统
:::info
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038076168.png)
:::


## 2.2 Problems 
### P1: 求投影
:::info
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038071105.png)
:::
Keys![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038073852.png)


### P2: 根据投影求向量
:::info
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038076180.png)
:::
Key![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038079184.png)

### P3：投影为零的情况
:::info
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038082081.png)
:::
Key![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038085285.png)



# 3 行列式与面积
## 3.1 定义加例子**⭐⭐**
:::info
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038086722.png)
我们想求$\bf \frac{1}{2}|\vec{A}| |\vec{B}|sin(\theta)$, 并且想转换成点乘的形式，也就是$\vec{A'}\cdot \vec{B'}$的形式
:::
> 我们可以使用三角等式中的$sin(\theta)=cos(\frac{\pi}{2}-\theta)$进行转换， 最终转换成一个向量点积的形式
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038087157.png)
> 我们得到了一个类似于行列式的表达式

:::success
我们可以定义$det(\vec{A},\vec{B})=\begin{vmatrix} a_1 & a_2 \\ b_1 & b_2 \end{vmatrix}$, 其中$\vec{A}=<a_1,a_2>$,$\vec{B}=<b_1,b_2>$
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038082954.png)
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038089986.png)
这个行列式描述了一个平行四边形的面积，这个性质非常重要
其实$det(\vec{A},\vec{B})=\begin{vmatrix} a_1 & a_2 \\ b_1 & b_2 \end{vmatrix}$的结果就是**我们后续要讲的向量叉乘的**`**k component**`**的值**, 表示的都是平行四边形的面积
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038081764.png)
:::

## 

## 3.2 向量的行列式
[Volumes and Determinants in Space.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1658715376841-3f1405c0-fa56-4c49-8834-8956d4e8642a.pdf)

### 二维平面的定义
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038083717.png)
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038087297.png)


### 行列式的重要性质**⭐⭐⭐**
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038084696.png)
> **注意：**
> - $D-3$中的性质，对行列式乘以$c$只能改变**某一行或列**的所有值为原来的$c$倍
> - $D-4$性质是我们进行高斯消元的基础，也是为什么**高斯消元不会改变矩阵是否可逆**的原因



### 代数余子式**⭐⭐⭐**
> #### `ij-entry`：描述行列式中的第$i$行第$j$列中的元素
> `**ij-minor**`: **余子式， **描述行列式中去掉含有$a_{ij}$的行和列之后的**行列式**
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038099961.png)
> `**ij-cofactor**`**: 代数余子式，**$A_{ij}=(-1)^{i+j}|A_{ij}|$**, 是余子式乘上正负系数之后的结果(不包括诸如**$a_{11},a_{12},a_{13}$**的系数), 是一个数值**
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038094995.png)![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038096104.png)



### 行列式的Laplace Expansion
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038094941.png)
> **本质上是按照某一行或者某一列展开**
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038097976.png)
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038097493.png)
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038091863.png)





## 3.3 行列式的几何含义
[Geometric Interpretations.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1658716200469-5c845d8a-6ed5-4c35-90fb-362029f45813.pdf)
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038099420.png)
> **关于**$(1)$**的证明:**
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038103394.png)

> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038102010.png)
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038101171.png)












## 3.4 Problems
### P1: 计算行列式
:::info
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038105204.png)
:::
Keys![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038108771.png)


### P2: 计算行列式
:::info
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038105355.png)
:::
Key![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038101044.png)


### P3: 计算多边形面积
:::info
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038104328.png)
:::
Key![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038104998.png)


### P4: 计算多边形面积
:::info
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038108935.png)
:::
Key![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038111284.png)


### P5: 计算多边形面积 
:::info
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038114442.png)
:::
Key![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038111612.png)


### P6: 其他行列式计算
[Extra Exercises.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1658716917629-92a997fe-783e-4f74-a31c-e6092b3a372c.pdf)

# 4 向量叉乘
## Lecture Notes**⭐⭐⭐**
### How to Calculate?
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038112028.png)
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038111002.png)

### 基本性质**⭐⭐⭐**
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038115316.png)
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038114491.png)
:::info

- 用于获得一个平面的法向量$\vec{N}=\vec{A}\times \vec{B}$
- 用于计算平行四边形面积$area=|\vec{A}\times \vec{B}|$
- 尤其注意$\bf \vec{A}\times \vec{B} = -\bf \vec{B}\times \vec{A}$, 这由右手定则可以得到
- 将$\bf \vec{B}$替换成$\bf \vec{A}$, 可以得到$\bf \vec{A}\times \vec{A} = -\bf \vec{A}\times \vec{A}$, 所以$\bf \vec{A}\times \vec{A}=0$
:::


### 右手定则
:::info
确定$\vec{A}\times \vec{B}$的方向
:::
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038128737.png)

### 表示体积**⭐⭐⭐**
:::info
$\vec{A}\cdot \hat{n}$就是$\vec{A}$在$\hat{n}$方向上的投影，因为$\hat{n}$是单位向量，所以投影的大小就是这个平行六面体的高
:::
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038121121.png)
> $\bf det(\vec{A},\vec{B},\vec{C})=\bf \vec{A}\cdot (\vec{B}\times \vec{C})=|\vec{A}||\vec{B}\times\vec{C}|\times cos(\theta)$, $\theta$是$\vec{B}\times\vec{C}$和$\vec{A}$的张角
> 而$|\vec{A}|\times cos(\theta)$是$\vec{A}$在$\vec{B}\times\vec{C}$方向上的`Vector Component`， 也就是投影
> 由第二小节中的投影相关理论我们知道, $|\vec{A}|\times cos(\theta)=\bf \vec{A}\cdot \hat{n}=\bf \vec{A}\cdot \frac{\vec{B}\times \vec {C}}{|\vec{B}\times \vec{C}|}$
> **于是就有了一个非常重要的公式: **$det(\vec{A},\vec{B},\vec{C})= \vec{A}\cdot \frac{\vec{B}\times \vec {C}}{|\vec{B}\times \vec{C}|}=(\bf \vec{A}\cdot \frac{\vec{B}\times \vec {C}}{|\vec{B}\times \vec{C}|})|\vec{B}\times\vec{C}| \newline =|\vec{B}\times\vec{C}|(\bf \vec{A}\cdot \frac{\vec{B}\times \vec {C}}{|\vec{B}\times \vec{C}|})=Volume \space of \space Parallelepiped$
> 将行列式和平行六面体的体积结合起来



### 和行列式的关系**⭐⭐⭐**
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038127036.png)
> 这个性质不是很显然，我们给出一定的说明:
> 首先我们有: $\bf det(\vec{A},\vec{B},\vec{C})=\begin{vmatrix} a_1 & a_2 & a_3\\ b_1 & b_2 &b_3 \\c_1 &c_2 & c_3 \end{vmatrix}$
> 由行列式的第一行的拉普拉斯展开可得: $\bf det(\vec{A},\vec{B},\vec{C})=a_1\begin{vmatrix}  b_2 &b_3 \\c_2 & c_3 \end{vmatrix}-a_2\begin{vmatrix} b_1  &b_3 \\c_1 & c_3 \end{vmatrix}+a_3\begin{vmatrix}  b_1 & b_2  \\c_1 &c_2\end{vmatrix}$
> 而$\bf \vec{B}\times \vec{C}=\begin{vmatrix} i & j & k\\ b_1 & b_2 &b_3 \\c_1 &c_2 & c_3 \end{vmatrix}=\begin{vmatrix}  b_2 &b_3 \\c_2 & c_3 \end{vmatrix}-\begin{vmatrix} b_1  &b_3 \\c_1 & c_3 \end{vmatrix}+\begin{vmatrix}  b_1 & b_2  \\c_1 &c_2\end{vmatrix}$
> 于是$\bf \vec{A}\cdot (\vec{B}\times \vec{C})=a_1\begin{vmatrix}  b_2 &b_3 \\c_2 & c_3 \end{vmatrix}-a_2\begin{vmatrix} b_1  &b_3 \\c_1 & c_3 \end{vmatrix}+a_3\begin{vmatrix}  b_1 & b_2  \\c_1 &c_2\end{vmatrix}$
> 所以$\bf det(\vec{A},\vec{B},\vec{C})=\bf \vec{A}\cdot (\vec{B}\times \vec{C})$证毕



## Cross Product Basics
[Cross Product.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1658489185785-5bf24ea6-44a8-4a6b-b5c3-f8cb510f6776.pdf)
:::info
相乘的结果是另一个向量
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038129970.png)
:::

### Definition
:::info
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038126620.png)
其中，$\bf i=(1,0,0),j=(0,1,0),k=(0,0,1)$, 都是`Unit Vector`
:::


### Algebraic Properties**⭐⭐⭐**
:::info
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038127961.png)
:::
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038123742.png)
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038122071.png)



### Geometric Interpretations**⭐⭐**
#### Theorem
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038131126.png)
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038138540.png)



#### Lagrange Identity**⭐⭐**
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038134016.png)

:::info
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038136912.png)
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038138928.png)
:::



## 

### Examples
#### Example 1
:::info
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038131828.png)
:::

#### Example 2
:::info
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038131391.png)
:::


## Problems
### P1: 计算叉乘
:::info
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038131010.png)
:::
**Key**![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038133720.png)

### P2: 计算平行四边形面积
:::info
![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038137616.png)
:::
**Key**![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038148195.png)

## 注意点
> 我们说的向量叉乘一般是对于两个三维空间内的向量的运算
> 一般我们会将一个向量$\vec {r}$写成`Position Vector`(`Unit 1C`中提到)的形式$\bf{r(t)}=x(t)\bf{i}+y(t)\bf{j}+z(t)k$, 如果向量在一个二维平面内，比如$xy-plane$,那么$z(t)=0,\forall\space t$
> 但是在叉乘的时候还是要把$z(t)$带上出现在行列式中, 只是以$0$的大小出现, 不能不写



# 5 平面方程**⭐⭐**
> 可以通过向量叉乘获得平面方程: 几何意义就是**，这三个向量在同一平面内，所以这三个向量组成的平行六面体的体积是**`**0**`
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038144792.png)
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038144064.png)
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038149861.png)



## Problems
### P1: 求平面方程
> ![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038148800.png)

Key![image.png](./PART_A__向量_行列式和平面.assets/20230302_1038156057.png)
