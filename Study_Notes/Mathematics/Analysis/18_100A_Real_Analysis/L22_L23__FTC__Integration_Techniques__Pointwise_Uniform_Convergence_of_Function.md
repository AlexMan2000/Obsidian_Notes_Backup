[Lecture Note 22.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1670315259596-fb668a01-cfa5-4eab-ad4d-857be08e3693.pdf)
[Lecture Note 23.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1670315259456-bc1604c5-f87a-451c-95ea-d4277dafc37c.pdf)
# 1 Proproties of Riemann Integrals
## Linearity
> ![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509341154.png)





## Additivity
> ![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509349819.png)

**Proof of Theorem 1(Easy, Using the definition of Riemann Sum)**![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509342083.png)
![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509343536.png)


## Inf and Sup
> ![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509343383.png)

**Proof of Theorem 2(Easy)**![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509351069.png)![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509358244.png)


## Triangle Inequality
> ![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509352924.png)![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509355404.png)

**Proof of Theorem 3(Easy)**![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509359989.png)![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509355498.png)


# 2 Foundamental Theorem of Calculus
> ![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509363406.png)
> 第一部分实际上是为了计算积分，第二部分实际上是为了求解微分方程。

**Proof of Theorem 5(Medium)**![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509366688.png)![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509362418.png)![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509367429.png)


# 3 Integrating Techniques
## Integral by Parts(IBP)
> ![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509362266.png)

**Proof of Theorem 7(Medium)**![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509367760.png)


## Change of Variables
> ![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509361371.png)

**Proof of Theorem 11(Easy)**![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509375704.png)


# 4 Sequence of Functions
## Power Series
> ![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509378016.png)



## Radius of Convergence
> ![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509378482.png)

**Proof of Theorem 3(Easy, by root test)**![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509373344.png)
> ![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509371524.png)![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509377606.png)

**Examples**比如$a_j=\frac{1}{j!},x_0=0$, 则$f_n(x)=\sum_{j=0}^n a_j(x-x_0)^j$, 此时$R=\lim_{j\to \infty}|a_j|^{\frac{1}{j}}=0$, 所以`Radius of Convergence`$p=\infty$, 此时我们定义$e^x=\sum_{n=1}^{\infty} \frac{x^n}{n!}$。
![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509386235.png)
> ![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509387578.png)




## Fourier Series
> ![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509383048.png)

**Proof of Lemma 9(Easy)**![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509387789.png)


# 5 Pointwise/Uniform Convergence
## Pointwise Convergence
> ![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509389424.png)![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509385149.png)

**Examples**![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509388139.png)![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509391497.png)
**Graphical Explanations**![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509391572.png)![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509399337.png)![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509391690.png)![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509403986.png)



## Uniform Convergence
> ![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509404616.png)![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509406046.png)![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509404432.png)

**Proof of Theorem 9(Easy)**![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509405975.png)
**Graphical Explanations(Distance)**

## Difference between them
> $f_n\to f$`is pointwise convergent if` $\forall \epsilon>0, \forall x\in E, \exists N\in \mathbb{Z}^{+}， s.t. |f_n(x)-f(x)|<\epsilon$
> $f_n\to f$`is uniformly convergent if` $\forall \epsilon>0, \exists N\in \mathbb{Z}^{+}~~s.t.~~\forall n>N,~\forall x\in E，  |f_n(x)-f(x)|<\epsilon$
> 二者的区别就在于`Pointwise Convergence`中$f_n(x)$收敛于$f(x)$的速度会受到$x$取值的具体影响， 而`Uniform Convergence`中$f_n(x)$收敛于$f(x)$的速度对所有$x$都一样，是一个更为苛刻的条件。
> **所以: **`Uniform Convergence`**意味着**`**Pointwise Convergence**`**。**



# 6 Assignment
[hw12.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1670463515411-96ac64b7-fe65-4cea-b53d-471a899dcd26.pdf)


## P1
> ![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509402088.png)


## P2
> ![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509409118.png)



## P3
> ![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509418356.png)

## P4
> ![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509412298.png)


## P5
> ![image.png](L22_L23__FTC__Integration_Techniques__Pointwise_Uniform_Convergence_of_Function.assets/20230302_1509419569.png)

