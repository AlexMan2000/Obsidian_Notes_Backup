# Change of Basis
## Tracking Terry
> **HW03 Fa21 P3**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687269728412-a7ec9b56-d9c3-417a-a10c-19bf22695942.png#averageHue=%23f9f7f5&clientId=u0328a585-7e84-4&from=paste&id=ufc63db17&originHeight=1069&originWidth=1214&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=297505&status=done&style=none&taskId=ucbda2408-ea8e-42ec-94bf-0ac300e3bc8&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687270825082-85e91d18-2701-46a5-9b4d-88969aa90505.png#averageHue=%23fbfbfb&clientId=u0328a585-7e84-4&from=paste&height=301&id=u11306b81&originHeight=452&originWidth=703&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=14031&status=done&style=none&taskId=ue5b2d43f-8edd-428e-a684-26f68470ff3&title=&width=468.6666666666667)

**(a)**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687270039295-1ebc7728-3e5d-46c6-a8d3-4b057452cd84.png#averageHue=%23ffffff&clientId=u0328a585-7e84-4&from=paste&id=u83671a1d&originHeight=131&originWidth=1387&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=44799&status=done&style=none&taskId=u11682dd0-be69-4d7d-b53f-58e3b82bbd0&title=)
**(b)**本质上我们要求解这样一个线性方程组: $\begin{bmatrix} x_1&x_2\\x_3&x_4\end{bmatrix}\begin{bmatrix}2\\3 \end{bmatrix} =\begin{bmatrix} 4\\2\end{bmatrix}$, 所以我们有四个未知量，但是只有两个方程，所以不存在唯一的解。
**(c)**本质上我们可以将以$V$和$P$作为`Basis`的向量转换到`Standard Basis`中，也就是说我们有: $V\vec{x}_v=P\vec{x}_p$, 所以$\vec{x}_p=P^{-1}V\vec{x}_v$, $P=\begin{bmatrix} 1&0\\4&1\end{bmatrix}$, $P^{-1}=\begin{bmatrix} 1&0\\-4&1\end{bmatrix}$, 所以$P^{-1}V=\begin{bmatrix} 1&0\\-4&1\end{bmatrix} \begin{bmatrix} 1&0\\1&2\end{bmatrix}=\begin{bmatrix}1&0\\-3&2\end{bmatrix}$, 所以$T=\begin{bmatrix}1&0\\-3&2\end{bmatrix}$。
**(d)**我们要求的是使得$P\vec{x}_p=\vec{x}$和$V\vec{x}_v=\vec{x}$的$\vec{x}_p$和$\vec{x}_v$。
所以$\vec{x}_p=P^{-1}\vec{x}=\begin{bmatrix} 1&0\\-4&1\end{bmatrix}\begin{bmatrix}1\\3 \end{bmatrix}=\begin{bmatrix} 1\\-1\end{bmatrix}$, $\vec{x}_v=V^{-1}\vec{x}=\begin{bmatrix} 1&0\\-\frac{1}{2}&\frac{1}{2}\end{bmatrix}\begin{bmatrix}1\\3 \end{bmatrix}=\begin{bmatrix} 1\\1\end{bmatrix}$
![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687744563874-13c6ca0d-f69b-4654-a039-5e844e871e02.png#averageHue=%23fcfcfc&clientId=ucf4951c4-f4a0-4&from=paste&id=u6fb1adc6&originHeight=919&originWidth=1422&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=42059&status=done&style=none&taskId=u6521460e-428b-4024-92e3-b7dc6ce1c07&title=)


## Eigenvectors and Diagonalization
> **HW03 Fa21 P4**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687271259482-520daaec-2c74-4dee-a418-36cf07bb69cb.png#averageHue=%23f9f7f6&clientId=u0328a585-7e84-4&from=paste&id=uf1550dbb&originHeight=969&originWidth=1059&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=275759&status=done&style=none&taskId=u1bb90409-1139-459f-970f-369c47fae53&title=)

**(a)**根据特征向量的定义，我们有$A\vec{v_1}=\lambda \vec{v_1}\cdots,A\vec{v_n}=\lambda \vec{v_n}$, 将$\vec{v_i}$按列组成矩阵$V$我们有$AV= V\Lambda$
**(b)**因为$\vec{v_1},\cdots, \vec{v_n}$是线性无关的，所以$a_1\vec{v_1}+\cdots+a_n\vec{v_n}=\vec{0}$只有$a_1=a_2=\cdots=a_n=0$的解，也就是说如果$V=\begin{bmatrix} \vec{v_1}&\cdots&\vec{v_n}\end{bmatrix}$，则$V\vec{a}=\vec{0}$只有零解，也就是$V$的零空间只有$\{\vec{0}\}$, 所以$V$可逆。
因为$AV=V\Lambda$, 所以$A=V\Lambda V^{-1}$。
**(c)**$\Lambda=V^{-1}AV$。
**(d)**因为$A=UDU^{-1}$, 所以$U$可逆(因为能够表示成$U^{-1}$)，所以$AU=UD$, 令$U=\begin{bmatrix} \vec{u_1}&\vec{u_2}\cdots&\vec{u_n}\end{bmatrix}$ , $D=\begin{bmatrix} \lambda_1&\cdots&0\\\vdots&\ddots&\vdots\\0&\cdots&\lambda_n\end{bmatrix}$, 所以我们有$A\vec{u_i}=\lambda_i\vec{u_i}$，所以$\vec{u_i}$就是`Eigenvectors`。$D$的对角线上的元素就是`Eigenvalues`。
**(e)**因为$A\vec{v_i}=\lambda_i\vec{v_i}$, 所以$A^k\vec{v_i}=\lambda_i^k\vec{v_i}$, 于是$A^k$的特征值是$\lambda_i^k$, 特征向量是$\vec{v_i}$。
所以$A^kV=VD^k$, 即$A^k=VD^kV^{-1}$, 所以$A^k$是`Diagonalizable`的。

## Vector Differential Equations
> **HW03 Fa21 P5**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687272239907-7497622a-b5d7-4bdd-8ce2-9b67994aa837.png#averageHue=%23f9f7f5&clientId=u0328a585-7e84-4&from=paste&id=uc4370394&originHeight=1126&originWidth=935&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=333076&status=done&style=none&taskId=u8031c6f8-29c5-4883-84d7-1d360db1f97&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687272247523-01813e1e-9d4f-479d-90f0-7f436ea4124d.png#averageHue=%23f6f4f3&clientId=u0328a585-7e84-4&from=paste&height=286&id=u18d09fdb&originHeight=429&originWidth=1653&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=156349&status=done&style=none&taskId=u38ff4c1b-207c-4519-bba3-baf5f9becbf&title=&width=1102)

**(a)**$\begin{bmatrix}\frac{dx_1(t)}{dt}\\\frac{dx_2(t)}{dt} \end{bmatrix}=\begin{bmatrix}7&-8\\4&-5 \end{bmatrix}\begin{bmatrix}x_1(t)\\x_2(t) \end{bmatrix}$
我们对$A=\begin{bmatrix} 7&-8\\4&-5\end{bmatrix}$求解特征值：
$(7-\lambda)(-5-\lambda)+32=0$, 所以$\lambda_1=-1,\lambda_2=3$
**(b)**$\lambda_1=-1$, 对应的特征向量是$\begin{bmatrix} 1\\1  \end{bmatrix}$。
$\lambda_2 = 3$，对应的特征向量是$\begin{bmatrix} 2\\1\end{bmatrix}$。
所以`Column Eigenvectors`是$\begin{bmatrix} 1&2\\1&1\end{bmatrix}$。
**(c)**我们只需使用$B=\begin{bmatrix} 1&2\\1&1\end{bmatrix}$作为我们的`New Basis`, 也就是`Eigen Basis`, 此时$D=\begin{bmatrix} -1&0\\0&3\end{bmatrix}$
$\frac{d\vec{z}(t)}{dt}=D\vec{z}(t)$。
**(d)**首先我们需要求出$\vec{z}(0)=B^{-1}\vec{x}(0)=\begin{bmatrix} -1&2\\1&-1\end{bmatrix}\begin{bmatrix} 1\\-1\end{bmatrix}=\begin{bmatrix} -3\\2\end{bmatrix}$
根据一阶线性常系数齐次微分方程，我们有$\vec{z}(t)=\begin{bmatrix} -3e^{-t}\\2e^{3t}\end{bmatrix}$
**(e)**所以$\vec{x}(t)=B\vec{z}(t)=\begin{bmatrix} 1&2\\1&1\end{bmatrix}\begin{bmatrix} -3e^{-t}\\2e^{3t}\end{bmatrix}=\begin{bmatrix}-3e^{-t}+4e^{3t}\\-3e^{-t}+2e^{3t}\end{bmatrix}$
**(f)**既然要消除二阶项，我们不妨令$x(t)=\frac{dy(t)}{dt}$, 则$\frac{dx(t)}{dt}=\frac{d^2y(t)}{dt^2}$, 所以我们有:
$\frac{dx(t)}{dt}-5x(t)+6y(t)=0$和$\frac{dy(t)}{dt}=x(t)$。
也就是: $\begin{cases} \frac{dx(t)}{dt}=5x(t)-6y(t) \\ \frac{dy(t)}{dt}=x(t)\end{cases}$。
**(g)**因为$x(t)=\frac{dy(t)}{dt}$, 所以我们知道$\begin{cases} x(0)=1\\y(0)=1\end{cases}$
我们知道$A=\begin{bmatrix} 5&-6\\1&0\end{bmatrix}$, 特征值为$\lambda_1=2, \lambda_2=3$。
根据上述公式我们有$c_0e^{\lambda_1t}+c_1e^{\lambda_2 t}=\lambda_1c_2e^{\lambda_1t}+\lambda_2c_3e^{\lambda_2t}$。令$t=0$我们有$c_0+c_1=2c_2+3c_3$
因为$\frac{dx(t)}{dt}=5x(t)-6y(t)$, 我们有$c_0\lambda_1e^{\lambda_1 t}+c_1\lambda_2 e^{\lambda_2 t}=5c_0e^{\lambda_1t}+5c_1e^{\lambda_2 t}-6c_2e^{\lambda_1 t}-6c_3e^{\lambda_2 t}$。令$t=0$我们有
$2c_0+3c_1=5c_0+5c_1-6c_2-6c_3$, 即$3c_0+2c_1=6c_2+6c_3\tag{2}$
所以根据上述公式我们有: $c_0+c_1=1$, $c_2+c_3=1$
整理之后我们有: $\begin{cases} 2c_2+3c_3=1\\c_2+c_3=1\end{cases}$, 所以$c_2=2,c_3=-1$
带入$(2)$式中我们有$\begin{cases} 3c_0+2c_1=6\\c_0+c_1=1\end{cases}$, 所以$c_0=4, c_1=-3$
所以我们可以解出$c_0,c_1,c_2,c_3$。


# OpAmp Stability
> **HW03 Fa21 P6**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687308876436-c51a491e-cc14-4e38-b4dc-0f65fb9bb82d.png#averageHue=%23fbfbfb&clientId=u515e199f-53e0-4&from=paste&id=ueded1b74&originHeight=1211&originWidth=1051&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=124788&status=done&style=none&taskId=u026ae8ef-1bc6-4e7b-9f42-71dc2752654&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687309096897-bb539c7d-9bbf-412d-9b01-8cff8efa1ac3.png#averageHue=%23f3f1ef&clientId=u515e199f-53e0-4&from=paste&id=u550b178c&originHeight=1129&originWidth=1648&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=467573&status=done&style=none&taskId=u61e3843b-61f0-4b6b-b4be-c2eeb94ea20&title=)

**(a) Eigenvalues**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687356911721-53bdcaf4-dbc5-4982-8b89-0fa6121ac5e7.png#averageHue=%23ffffff&clientId=u515e199f-53e0-4&from=paste&id=u89d67286&originHeight=930&originWidth=1402&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=120690&status=done&style=none&taskId=u81bf5610-d288-4426-91f8-0692483bc54&title=)
**(b) Approximation**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687393375244-96d395b4-96cb-478e-ae9a-dec9df535cde.png#averageHue=%23ffffff&clientId=u497894ac-0f06-4&from=paste&id=uda3fd1dc&originHeight=1047&originWidth=1349&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=136047&status=done&style=none&taskId=ue19ebcb7-f698-45fc-b689-7480ba0ed94&title=)




# Solar Cell(Optional)
> **HW03 Fa21 P7**



# *Proof Practice
> **HW03 Fa21 P8**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687396848180-6a757e0a-cb15-4b81-8583-544ec96bc829.png#averageHue=%23f6f3f1&clientId=u68f50cc1-0a08-4&from=paste&id=ud30693f9&originHeight=860&originWidth=1413&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=422858&status=done&style=none&taskId=u17ec42f3-b8d3-4d5a-9a42-4be193aab13&title=)

**(a)**根据题意，令$\alpha_i$代表是否选择$\sigma_i$, 即$\alpha_i\in \{0,1\}$，则$\sum_{i=1}^n\alpha_i\sigma_i$表示选择的$\sigma$'s的和。
因为我们要从$n$个里面选择$k$个，所以$\sum_{i=1}^n \alpha_i=k$, 所以本质上我们要求的是:
$\argmax_{\vec{\alpha}} \sum_{i=1}^n \alpha_i \sigma_i,~~~s.t.~~\sum_{i=1}^n\alpha_i=k$
**证明:**
现在假设$\alpha_1=\alpha_2=\cdots=\alpha_k=1, \alpha_{k+1}=\cdots=\alpha_n=0$，并证明任何其他的`Encoding`都不是最大的。
假设$\vec{\alpha}$满足$\alpha_1=\alpha_2=\cdots=\alpha_k=1, \alpha_{k+1}=\cdots=\alpha_n=0$，并假设$\vec{\beta}\neq \vec{\alpha}$, 则$\exists i\in [1,k], ~~s.t.~~a_i=0$且$\exists j\in [k+1, n], ~~s.t.~~a_j=1$。因为$\sigma_1>\sigma_2>\cdots>\sigma_n\geq 0$, 则$\sum_{i=1}^n \alpha_i\sigma_i >\sum_{i=1}^n \beta_i\sigma_i$, 这说明任何其他的选择方式$\vec{\beta}$都不是最优的，于是$\vec{\alpha}$一定是最优的。
**(b)**





# Resources
> **HW03/04 Fa21/Sp23**

