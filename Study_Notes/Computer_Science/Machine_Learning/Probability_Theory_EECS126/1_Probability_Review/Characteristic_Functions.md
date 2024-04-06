# Characteristic Function Definition
> [!def]
> ![](Characteristic_Functions.assets/image-20240315231507475.png)



# Character Function Examples
## Rademacher RV
> [!example]
> ![](Characteristic_Functions.assets/image-20240316101129126.png)![](Characteristic_Functions.assets/image-20240316101141253.png)



## Uniform RV
> [!example]
> ![](Characteristic_Functions.assets/image-20240316101151380.png)![](Characteristic_Functions.assets/image-20240316101259852.png)




# Properties of CF
## Complex Conjugate
> [!important]
> ![](Characteristic_Functions.assets/image-20240316104027848.png)![](Characteristic_Functions.assets/image-20240316104036601.png)
> Here $\varphi_{-X}(t)=\varphi_X(-t)$ is by the change of variable in integral.


## Derivatives are Moments
> [!important]
> ![](Characteristic_Functions.assets/image-20240316105851388.png)
> $$\begin{aligned}\varphi_x(t) & =E\left[e^{i t X}\right] \\& =E\left[\sum_{m=0}^{\infty} \frac{(i X)^m t^m}{m !}\right] \\\varphi_X^{(k)}(t) & =E\left[\sum_{m=0}^{k=1} \cdot 0+\frac{(i X)^k t^0}{k !} \cdot k !+\sum_{m=k+1}^{\infty} p(t)\right] \\\left.\varphi_X^{(k)}(t)\right|_{t=0} & =E\left[(i X)^k\right] \\& =i^k E\left[X^k\right]\end{aligned}$$ where $p(t)$ is a polynomial of $t$ and $p(t)=0$ at $t=0$.


## Independence
> [!def]
> ![](Characteristic_Functions.assets/image-20240316110023203.png)![](Characteristic_Functions.assets/image-20240316110044670.png)



# Rotationally Invariant R.V.
## Definition
> [!def]
> ![](Characteristic_Functions.assets/image-20240316110347961.png)![](Characteristic_Functions.assets/image-20240316110415777.png)![](Characteristic_Functions.assets/image-20240316134856722.png)


## Properties
> [!property]
> For a random variable $X$, we have the following properties that come in handy in proof:
> 1. $\varphi_{cX}(t)=\varphi_X(ct)$
> 2. $\varphi_{X+Y}(t)=\varphi_X(t)\varphi_Y(t)$ given that $X\perp Y$.


## Gaussian Example
> [!example] Fa21 HW6 P4
> ![](Characteristic_Functions.assets/image-20240316132824386.png)![](Characteristic_Functions.assets/image-20240316154600667.png)
> In question (a), the rotation matrix that we choose could be $$\begin{bmatrix}\frac{1}{\sqrt{n}}&-\frac{\sqrt{n-1}}{\sqrt{n}}\\\frac{\sqrt{n-1}}{\sqrt{n}}&\frac{1}{\sqrt{n}} \end{bmatrix}$$, then we can prove using mathematical induction.
> 
> In question (c), we encounter the concept of [P1 Density of R Q](../../../../Mathematics/Analysis/18_100A_Real_Analysis/L5_L6__Properties_of_Real_Numbers__Sequence_and_Limits__Basic_Topology.md#P1%20Density%20of%20R%20Q), which intuitively means:
> 
> ![](Characteristic_Functions.assets/image-20240316160722736.png)![](Characteristic_Functions.assets/image-20240316155555469.png)
> The reason $\{t:t^{2}\in\mathbb{Q}\}$ is dense is as follows:
> 
> ![](Characteristic_Functions.assets/image-20240316160342568.png)
> The reason why the last sentence holds is that:
> 
> ![](Characteristic_Functions.assets/image-20240316160916100.png)![](Characteristic_Functions.assets/image-20240316160924254.png)














