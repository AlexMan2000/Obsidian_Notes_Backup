# Capacitor Analysis⭐⭐⭐⭐⭐
> **HW01 Sp23 P2~P6**
> **计算一个电容的两端的：**
> 1. 电压随时间变化的曲线: $V_C(t) = V_C(0)+\int_0^t\frac{I(t')}{C}dt'$。
> 2. `Power`随时间变化的曲线: 如果我们有$I(t)$和$V_C(t)$的图像，则$P_C(t)$的图像也就呼之欲出了，就只需要把$I(t)$和$V_C(t)$的图像`Pointwise`相乘即可。
> 3. `Stored Energy`: 
>    1. 对于**某一时刻电容**储存的能量，我们可以永远相信$E_C(t)=\frac{1}{2}C(V_C(t))^2$。
>    2. 一般而言对于**稳定状态下的电子元件**储存的能量我们可以使用$E(t)=\int_0^{\infty} V(t)I(t)dt$进行积分求解。



## Charging Process  
> 对于一个电容来说，我们有$Q=CV$关系成立，其中$Q$和$V$是对时间而变化的函数，$Q(t)$和$V(t)$, 于是我们有以下定义:
> $Q(t)=C V(t)$
> ![image.png](Capacitors&Inductors&OpAmp.assets/2ce9a87a630b8d2d86dc5ed7d1387ed5_MD5.png)
> 电流源恒定时，$V_C(t)-V_C(0)=\frac{I_St}{C}$


## Capacitor I
> ![image.png](Capacitors&Inductors&OpAmp.assets/b2d9dae887a1ced9e0be131b9eeb6648_MD5.png)

**Voltage**![image.png](Capacitors&Inductors&OpAmp.assets/31dbb30619140f2219c39890785060f1_MD5.png)
首先注意这里的$\int_{0}^t i(t')dt'$的单位是$mA\cdot ms$, 所以在将$100$和$-100$带入求积分之后我们需要对得到的值乘以$10^{-3}\times 10^{-3}=10^{-6}$, 所以图像的斜率应该是$\frac{1}{3}\times 10^6\times 100\times 10^{-3}\times 10^{-3}=33.3$。
![image.png](Capacitors&Inductors&OpAmp.assets/75a9d3d517fa2862a12d48dbf28b1220_MD5.png)
**Power**$V_C(t)=10+33.3t$, $I_C(t)=\begin{cases} 0.1A&0~s<t<0.001~s\\-0.1A&0.001s<t<0.002s\end{cases}$
所以$W_C(t)=V_C(t)I_C(t)=(10+33.3t)I_C(t)=\begin{cases} 1+3.33t&0~s<t<0.001~s\\-1-3.33t&0.001s<t<0.002s\end{cases}$
![image.png](Capacitors&Inductors&OpAmp.assets/6fb0731f33cb21c44bb324dfce095a1e_MD5.png)
**Stored Energy**![image.png](Capacitors&Inductors&OpAmp.assets/f8e43003a7299adbb9d8fa5987a25188_MD5.png)

## Capacitor II: Circuit Equivalence
> ![image.png](Capacitors&Inductors&OpAmp.assets/96bf00d08172048831270b6f0b77b785_MD5.png)

**Solution (a)**$\begin{aligned}100V-\frac{dV_C(t)}{dt}\cdot CR&=V_C(t)\\\frac{dV_C(t)}{dt}&=-\frac{1}{CR}V_C(t)+\frac{100}{CR}\end{aligned}$
所以$V_C(t)=100(1-e^{-\frac{t}{10^{-3}}})$
![image.png](Capacitors&Inductors&OpAmp.assets/b3ecf0286ae9922e2381b238893ce0bf_MD5.png)
> ![image.png](Capacitors&Inductors&OpAmp.assets/5e1b5cf629c630b89b78fb6bfaef3afa_MD5.png)

**Solution (b)**![image.png](Capacitors&Inductors&OpAmp.assets/4777cd6157e56d0689170a83ef39dab7_MD5.png)

## Capacitor III
> ![image.png](Capacitors&Inductors&OpAmp.assets/ee784176e31f170324308bb1730148f1_MD5.png)

**Solution**根据`KVL`定律我们有$V_C(t)-V_R(t)=0$
电流方向是从电容的正极流向负极，所以$V_R(t)=-I_C(t)R$
因为$I_C(t)=\frac{dV_C(t)}{dt}\cdot C$, 所以$V_C(t)+\frac{dV_C(t)}{dt}\cdot CR=0$。
所以$\frac{dV_C(t)}{dt}=-\frac{1}{CR}V_C(t)$, 这里$CR=0.02\times 10^{-6}\cdot 1\times 10^6=0.02$。
所以$\frac{dV_C(t)}{dt}=-\frac{1}{0.02}V_C(t)$, 得到$V_C(t)=V_C(0)e^{-\frac{1}{0.02}t}=50e^{-\frac{t}{0.02}}$
综合来看，我们有: $V_C(t)=\begin{cases} 50&t\leq0\\ 50e^{-\frac{t}{0.02}}&t>0\end{cases}$, $V_R(t)=\begin{cases} 50&t\leq0\\ 50e^{-\frac{t}{0.02}}&t>0\end{cases}$
> ![image.png](Capacitors&Inductors&OpAmp.assets/3fd426bc55d2c81edf756dc07d984805_MD5.png)

**Solution**$I_C(t)=\frac{dV_C(t)}{dt}\cdot C=\begin{cases}0&t\leq 0\\-2500e^{-50t}&t>0 \end{cases}\times 0.02\times 10^{-6}=\begin{cases} 0&t\leq 0\\-50e^{-50t}\times 10^{-6}&t>0\end{cases}$
$\begin{aligned}W_R(t)&=V_{R}(t)I_R(t)=V_R(t)\cdot (-I_C(t))\\&=\begin{cases} 50&t\leq0\\ 50e^{-\frac{t}{0.02}}&t>0\end{cases}\times (-\begin{cases} 0&t\leq 0\\-5e^{-50t}\times 10^{-6}&t>0\end{cases})\\&=\begin{cases}0&t\leq 0\\2500e^{-100t}\times 10^{-6}&t>0 \end{cases}=\begin{cases}0&t\leq 0\\2.5e^{-100t}\times 10^{-3}&t>0 \end{cases}\end{aligned}$
> ![image.png](Capacitors&Inductors&OpAmp.assets/2bebdd1e42030153e9c644b529ad5bce_MD5.png)

**Solution**本题主要运用公式即可$\int_0^{\infty}V_R(t)I_R(t)dt$:
$\begin{aligned}\int_0^{\infty}V_R(t)I_R(t)dt&=\int_0^{\infty}50e^{-50t}\times -2500e^{-50t}\times 0.02\times 10^{-6}dt\\&=2.5\times 10^{-3}\times (-\frac{1}{100}e^{-100t}\big|_0^{\infty})\\&=25\times 10^{-6}\\&=25uJ\end{aligned}$
> ![image.png](Capacitors&Inductors&OpAmp.assets/669cb4dccec0059b0a6811595e351122_MD5.png)

**Solution**![image.png](Capacitors&Inductors&OpAmp.assets/a0784f576fff496a3738bc551c613e6a_MD5.png)
可以发现，电容中储存的能量最终都流向了电阻。


## Capacitor IV
> **EECS16B sp23 HW1 P4**
> ![image.png](Capacitors&Inductors&OpAmp.assets/043196332789b3603519b6312624aab8_MD5.png)

**Solution (a)**假设$v(t)$是电容两端的电压，$V$是电压源的电压则我们根据`RC`电路微分方程可知，$\frac{dv(t)}{dt}+\frac{v(t)}{RC}=\frac{V}{RC}$, 其解为$v(t)=V(1-e^{-\frac{t}{RC}}),t\geq 0$, 所以$\frac{dv(t)}{dt}=(-\frac{1}{RC})\cdot (-e^{-\frac{t}{RC}})=\frac{1}{RC}e^{-\frac{t}{RC}}$
于是根据能量公式: 
$\begin{aligned}w_s&=\int_0^{\infty}v(t)i(t)dt\\&=\int_0^{\infty}v(t)\cdot\frac{dv(t)}{dt}Cdt\\&=C\int_0^{\infty}V(1-e^{-\frac{t}{RC}})\frac{d(V(1-e^{-\frac{t}{RC}}))}{dt}dt\\&=C\int_0^{\infty}V(1-e^{-\frac{t}{RC}})\frac{V}{RC}e^{-\frac{t}{RC}}dt\\&=\frac{CV^2}{RC}\int_0^{\infty}(1-e^{-\frac{t}{RC}})e^{-\frac{t}{RC}}dt\\&=\frac{CV^2}{RC}(-RC)(-1+\frac{1}{2})\\&=\frac{1}{2}CV^2\end{aligned}$
**Solution (b)**![image.png](Capacitors&Inductors&OpAmp.assets/aac062642a5b2ec2c85e57dc3ee8b94a_MD5.png)
**Solution (c)**![image.png](Capacitors&Inductors&OpAmp.assets/bd414c1cff0dec30255bc2e3a1dccc83_MD5.png)
**Solution (d)**![image.png](Capacitors&Inductors&OpAmp.assets/5bef61ee04a12fc674b583847a353470_MD5.png)


# Inductors
## Definition
> ![image.png](Capacitors&Inductors&OpAmp.assets/26a1f5fdccc1d377efef0582c659870c_MD5.png)
> 🔔: 这里要注意$I_{L}$不会突变，因为如果$I_L$突变，也就是说$\frac{dI_L(t)}{dt}\to \infty$, 那么$V_L(t)\to \infty$, 这也是不符合实际的。


## Physics Behind
> 电容因为电荷的正负极会产生电场$\vec{E}$, 电场能够储存电容的能量。
> 电导因为有电流流经会产生电磁场$\vec{B}$，磁场能够储存电导的能量。
> ![image.png](Capacitors&Inductors&OpAmp.assets/e237c60654a8d792d0a2b01cb47bb1b4_MD5.png)



## Magnetic Flux
> ![image.png](Capacitors&Inductors&OpAmp.assets/7a4c75e6beff072732ece12803d2175a_MD5.png)


## Stored Energy
> ![image.png](Capacitors&Inductors&OpAmp.assets/f041ce363750e2153032d492966bdd5c_MD5.png)

**Proof**![image.png](Capacitors&Inductors&OpAmp.assets/6f39eece7b4880b3f8e475b0f7b0e9f2_MD5.png)



# Mutual Inductance
> ![image.png](Capacitors&Inductors&OpAmp.assets/7ff2cd6650a1a252e6a693fa913f050a_MD5.png)
> **总的来说，我们有:**
> $\begin{aligned}& v_1(t)=L_1 \frac{\mathrm{d} i_1}{\mathrm{~d} t} \pm M \frac{\mathrm{d} i_2}{\mathrm{~d} t} \\& v_2(t)= \pm M \frac{\mathrm{d} i_1}{\mathrm{~d} t}+L_2 \frac{\mathrm{d} i_2}{\mathrm{~d} t}\end{aligned}$

**Proof**![image.png](Capacitors&Inductors&OpAmp.assets/6812258fa602370b907b47a9405f258e_MD5.png)

# Inductor Equivalence
## Series Equivalence
> ![image.png](Capacitors&Inductors&OpAmp.assets/e8c3487a381544aeffc0d491397eb1af_MD5.png)




## Parallel Equivalence
> ![image.png](Capacitors&Inductors&OpAmp.assets/824df77b984d6cef47362a56926f7311_MD5.png)



## RL Circuit
> ![image.png](Capacitors&Inductors&OpAmp.assets/576ca91dfe87e12024562624130fa1c2_MD5.png)
> $\begin{aligned}V_R(t) & =V_S-V_L(t) \\R I_L(t) & =V_S-L \frac{\mathrm{d}}{\mathrm{d} t} I_L(t)\\\frac{\mathrm{d}}{\mathrm{d} t} I_L(t)&=-\frac{R}{L} I_L(t)+\frac{V_S}{L}\\
I_L(t) &=-\frac{V_S}{R} \mathrm{e}^{-\frac{R}{L} t}+\frac{V_S}{R} \\
&=\frac{V_S}{R}\left(1-\mathrm{e}^{-\frac{R}{L} t}\right)\\V_L(t)&=V_S \mathrm{e}^{-\frac{R}{L} t}
\end{aligned}$
> 其中$\frac{L}{R}$的单位是$s$, 决定了时间轴上的`Time Scale`。
> 假设 $R=500 \Omega, L=1 \mathrm{mH}, V_S=5 \mathrm{~V}$, 我们有$\tau=\frac{L}{R}=0.2\times 10^6s=2us$, 于是:
> ![image.png](Capacitors&Inductors&OpAmp.assets/834a8c2ab51dde50e7aa1062a3f2f57a_MD5.png)


# Inductor Analysis
## Charging Process
> **Disc 02B Sp23 P1(a)**
> ![image.png](Capacitors&Inductors&OpAmp.assets/d793df682b718b13b9637468296b7ec2_MD5.png)
> 1. 假设$I_L(0)=0A$, 两端有一个恒定电压源$V_S$，则$\frac{dI_L(t)}{dt}\cdot L=V_S$, 两边积分得到$\int_0^{t}dI_L(t)=\int_0^{t}\frac{V_S}{L}$, 于是$I_L(t)-I_L(0)=V_S$, 所以$I_L(t)=\frac{V_S t}{L}$。



## Power Properties
> **HW03 Sp23 P2**
> ![image.png](Capacitors&Inductors&OpAmp.assets/e488c08628fae4a1d4fe81589dd50653_MD5.png)

**Voltage**![image.png](Capacitors&Inductors&OpAmp.assets/ad4161244694bc08271d99f0ebfe1ab5_MD5.png)
**Power**![image.png](Capacitors&Inductors&OpAmp.assets/86df60e8fb718354209cac312c73d7c9_MD5.png)
**Stored Energy**![image.png](Capacitors&Inductors&OpAmp.assets/a6a86d5932ba2cf1a4a6c9622978f91f_MD5.png)


## Inductance Extremities
> **HW03 Sp23 P3**
> ![image.png](Capacitors&Inductors&OpAmp.assets/fd0e34f5a210122e8d1df3f79f42f50f_MD5.png)
> `Open Circuit`对应的条件是$I_L(t)=0$, 因为$V_L(t)=\frac{dI_L(t)}{dt}\times L$, 所以:
> $\frac{V_L(t)}{L}=\frac{dI_L(t)}{dt}$, 两边取积分得到$I_L(t)-I_L(t_0)=\frac{1}{L}\int_{t_0}^tV_L(\tau)d\tau$, 因为$I_L(t)=I_L(t_0)=0$
> 所以$\frac{1}{L}\int_{t_0}^tV_L(\tau)d\tau=0$, 因为$\int_{t_0}^tV_L(\tau)d\tau\neq 0$, 所以$L\to \infty$。
> `Short Circuit`对应的条件是$V_L(t)=0$, 因为$\frac{dI_L(t)}{dt}\neq 0$, 所以$L=0$。



## Mutual Inductance
> **HW03 Sp23 P4**
> ![image.png](Capacitors&Inductors&OpAmp.assets/c892adc4272452a26841c0d0b3128c7f_MD5.png)






# OpAmp
## Op-Amp Stability Part 1
> **HW02 Fa21 P5**
> ![image.png](Capacitors&Inductors&OpAmp.assets/fd9b9b88ecaf06418e09b409a427b45d_MD5.png)

**(a) OpAmp Circuit in Detail**![image.png](Capacitors&Inductors&OpAmp.assets/f08885f88e726975ea625319ca591752_MD5.png)
**(b) OpAmp Differential Equation - Negative Feedback Loop**![image.png](Capacitors&Inductors&OpAmp.assets/8ed9af9e0ce2156e999d9c634f49495f_MD5.png)
**(c) OpAmp Differential Equation - Positive Feedback Loop**![image.png](Capacitors&Inductors&OpAmp.assets/4ffe9fe9ba3d4d9fb5dc68756a73efc4_MD5.png)
**(d) Limiting Behaviors**![image.png](Capacitors&Inductors&OpAmp.assets/355b2ecbf58f6584b465d8fa1eb6bb62_MD5.png)
**(e) Vector Differential Equations**![image.png](Capacitors&Inductors&OpAmp.assets/a211708e1de5152c58c962174ad3e72f_MD5.png)
> **本题要注意:**
> 在画一个`Detailed OpAmp`电路的时候，左侧的`Terminal`和`OpAmp`本体之间永远是`Open Circuit`, 无论有没有`Feedback Loop`, 左侧的$V_+$和$V_-$端都是裸露在电路之外的。如下图中的的绿色端，电流都是零，流经`Feeback Loop`的电流也是零。
> ![image.png](Capacitors&Inductors&OpAmp.assets/a14f55bd36ccecf6f29a8a3f0c4b5f05_MD5.png)
> 即$(a)$中的输入端是$V_{in}-V_{out}$, $(b)$中的输入端是$V_{out}-V_{in}$。


## Op-Amp Stability Part 2
> **HW03 Fa21 P6**
> ![image.png](Capacitors&Inductors&OpAmp.assets/608b9327c4e9db6c219b7e164c542378_MD5.png)

**(a) Eigenvalues**![image.png](Capacitors&Inductors&OpAmp.assets/4819e739ec9a9d5e83de014196147f98_MD5.png)
**(b) Approximation**![image.png](Capacitors&Inductors&OpAmp.assets/001cced28a1531abf3933f638c160613_MD5.png)



# Summary
## Capacitors&Inductors
> ![image.png](Capacitors&Inductors&OpAmp.assets/6c8b3c84cbaa45dcb2d4931d64e2c213_MD5.png)

