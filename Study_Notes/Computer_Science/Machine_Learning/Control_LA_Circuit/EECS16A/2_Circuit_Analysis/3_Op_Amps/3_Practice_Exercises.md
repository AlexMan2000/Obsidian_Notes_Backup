# Example Circuits
> ![](3_Practice_Exercises.assets/image-20230526092044904.png)


## Voltage Summer
> [dis5C](Exercise_Folder/dis5C.pdf)
> ![](3_Practice_Exercises.assets/image-20230526233346512.png)![](3_Practice_Exercises.assets/image-20230526233419184.png)



## Current Summer
> [dis5C](Exercise_Folder/dis5C.pdf)
> ![](3_Practice_Exercises.assets/image-20230526233714813.png)![](3_Practice_Exercises.assets/image-20230526233718135.png)




## Signal Summer
> Disc 5A Problem 1
> ![](3_Practice_Exercises.assets/image-20230526093710539.png)

> [!info] Problem (a)
> ![](3_Practice_Exercises.assets/image-20230526093809897.png)![](3_Practice_Exercises.assets/image-20230526093818244.png)

> [!info] Problem (b)
> ![](3_Practice_Exercises.assets/image-20230526093836626.png)


## Modular Circuits
> Disc 5A Problem 2
> ![](3_Practice_Exercises.assets/image-20230526093916971.png)

> [!info] Problem (a)
> 注意到对于一个`OpAmp with Negative Feedback`, 我们的`Gain`是$1+\frac{R_{top}}{R_{bottom}}>1$。
> 所以图中的$\frac{1}{2}$和$\frac{1}{3}$是不能通过`Opamp`来实现的，所以仍然需要`Voltage Divider`来实现。
> 但是为了$V_x$接入电路后不发生`Loaing Effect`, 如下所示:
> ![](../1_Resistive_Touchscreen/6_Practice_Exercises.assets/image-20230318093028155.png)
> 所以我们需要在中间加入一个`Unity Gain Buffer`, 如下所示:
> ![](3_Practice_Exercises.assets/image-20230526100853194.png)![](3_Practice_Exercises.assets/image-20230526100858203.png)


> [!info] Problem (b)
> ![](3_Practice_Exercises.assets/image-20230526101553187.png)![](3_Practice_Exercises.assets/image-20230526101602301.png)![](3_Practice_Exercises.assets/image-20230526101609955.png)


## Trans-Resistance Amplifier
> Disc 5A Problem 3
> ![](3_Practice_Exercises.assets/image-20230526101650779.png)

> [!info] Problem (a)
> ![](3_Practice_Exercises.assets/image-20230526101823381.png)

> [!info] Problem (b)
> ![](3_Practice_Exercises.assets/image-20230526102746906.png)



## Inverting Amplifiers
> Disc 4D Problem 2
> ![](3_Practice_Exercises.assets/image-20230524095913945.png)

> [!info] Problem (a)
> ![](3_Practice_Exercises.assets/image-20230524100922439.png)
> 首先我们注意到这个`Op-amp`中很可能处于`Negative Feedback Loop`, 我们来验证一下:
> 1. 将电压源$V_s$`Zero Out`为一个导线。
> 2. 我们对$u_{out}$(也就是$u_-$)施加一个微小的扰动, 使其减小一些，则`Op-amp`的输入$u_+-u_-$增大，然后经过`Op-amp`之后输出为$u_{out}=A(u_+-u_-)$增大，和原来的扰动方向相反，所以`Op-amp`处于`Negative Feedback Loop`中。
> 有了这个条件，我们根据`Golden Rules`可知:
> - $I_-=I_+=0$, 所以图中的$I_-$实际上是一个`Open Circuit`, 所以根据`KCL`有$I_{R_1}=I_{R_2}$。
> - $u_+=u_-=0V$(因为$U_+$端口接地)。
> 所以根据`KVL`我们有$\begin{cases}V_s-I_{R_1}R_1-I_{R_2}R_2&=U_{out}\\ V_s-0=I_{R_1}R_1\end{cases}$
> 所以解得$V_{out}=V_s-\frac{V_s}{R_1}R_1-\frac{V_s}{R_1}R_2=-\frac{R_2}{R_1}V_s$, 记$A_V=-\frac{R_2}{R_1}<0$(称为`Gain With Negative Feedback Loop`)。

>[!info] Numerical Example
>![](3_Practice_Exercises.assets/image-20230524144842087.png)
>![](3_Practice_Exercises.assets/image-20230524144850272.png)
>![](3_Practice_Exercises.assets/image-20230524144859494.png)

> ![](3_Practice_Exercises.assets/image-20230524123009220.png)





# Op-Amp
## Op-Amp Rules
> Disc 4D Problem 1
> ![](3_Practice_Exercises.assets/image-20230523230222425.png)

> [!info] Problem (a)
> ![](3_Practice_Exercises.assets/image-20230523232314077.png)

>[!info] Problem(b)
>![](3_Practice_Exercises.assets/image-20230523233628589.png)


## Unity Gain Buffer
> Disc 4D Problem 1
> ![](3_Practice_Exercises.assets/image-20230524093113390.png)
> 🔔: Key Formula Used, $V_{out}=\frac{A}{1+A\cdot f}V_{in}$，其中$f$ 是`Feedback Loop`对$V_{out}$的缩小/放大倍数。
> 本题中我们将见到$f=1$时的情形。我们称此时的电路为`Unity Gain Buffer`。
> `Buffer is the thing that goes in between circuits and helps connect/moderate`。
> 🔔: What's the purpose of the unity gain buffer?
> ✔️: It prevents loading, connect different circuits without affecting each other.

> [!info] Problem (c)
> ![](3_Practice_Exercises.assets/image-20230524092246796.png)

>[!info] Problem (d)
>![](3_Practice_Exercises.assets/image-20230524095723020.png)


# Negative Feedback
## Swapping Terminals
> ![](3_Practice_Exercises.assets/image-20230524142930888.png)![](3_Practice_Exercises.assets/image-20230524143024243.png)

> [!info] Answer
> ![](3_Practice_Exercises.assets/image-20230524142959984.png)


## Identifying NFB
> ![](3_Practice_Exercises.assets/image-20230524143438803.png)![](3_Practice_Exercises.assets/image-20230524143442528.png)

> [!info] Answer
> ![](3_Practice_Exercises.assets/image-20230524143456780.png)



# Buffer&Loading
> ![](3_Practice_Exercises.assets/image-20230524145334493.png)

> [!info] With Unity Buffering
> ![](3_Practice_Exercises.assets/image-20230524150539358.png)

> [!info] Without Buffering(Just using Wires)
> ![](3_Practice_Exercises.assets/image-20230524150600239.png)
 ![](3_Practice_Exercises.assets/image-20230524150553262.png)
 ![](3_Practice_Exercises.assets/image-20230524150648154.png)



# Industrial Circuit Design
## Noise Cancelling Headphones⭐⭐⭐⭐⭐
### Problem Solving
> Disc 5B Problem 1
> 降噪耳机的基本目标是让用户只听到所需的音频信号，而不是来自外部的任何声音。任何其他来自外部的声音。为了实现这一目标，降噪耳机包括至少一个麦克风，用于监听你可能从外部来源听到的声音，然后将一个信号输入到你的扬声器中，取消（减去）外部产生的声音。

> [!info] Problem (a) Power Supply Signal
> ![](3_Practice_Exercises.assets/image-20230526114720924.png)![](3_Practice_Exercises.assets/image-20230526114730735.png)![](3_Practice_Exercises.assets/image-20230526114843836.png)![](3_Practice_Exercises.assets/image-20230526114851726.png)![](3_Practice_Exercises.assets/image-20230526114913547.png)![](3_Practice_Exercises.assets/image-20230526114922490.png)![](3_Practice_Exercises.assets/image-20230526115105519.png)

> [!info] Problem (b) Noise Cancellation
> ![](3_Practice_Exercises.assets/image-20230526115228704.png)![](3_Practice_Exercises.assets/image-20230526115236909.png)![](3_Practice_Exercises.assets/image-20230526211117292.png)![](3_Practice_Exercises.assets/image-20230526211340813.png)![](3_Practice_Exercises.assets/image-20230526211349686.png)![](3_Practice_Exercises.assets/image-20230526211358128.png)![](3_Practice_Exercises.assets/image-20230526211516510.png)![](3_Practice_Exercises.assets/image-20230526211523729.png)![](3_Practice_Exercises.assets/image-20230526211532722.png)


### Circuit Building
> ![](3_Practice_Exercises.assets/image-20230526233900043.png)



## Timer Circuit
> [dis5C](Exercise_Folder/dis5C.pdf)
> ![](3_Practice_Exercises.assets/image-20230526224646146.png)

> [!info] Problem (a)
> ![](3_Practice_Exercises.assets/image-20230526230208928.png)


> [!info] Problem (b)
> ![](3_Practice_Exercises.assets/image-20230526230217405.png)![](3_Practice_Exercises.assets/image-20230526230234484.png)

> [!info] Problem (c)
> ![](3_Practice_Exercises.assets/image-20230526230257688.png)

> [!info] Problem (d)
> ![](3_Practice_Exercises.assets/image-20230526230318357.png)

> [!info] Problem (e)
> ![](3_Practice_Exercises.assets/image-20230526230325957.png)

> [!info] Problem (f)
> 本题的核心公式就是$v_2=\frac{R_3}{R_2}\cdot \frac{V_3}{R_1\cdot C_1}t$. 同时我们需要注意，在`Op-amp`上方的`Supply Voltage`永远是$V_{DD}$, 下方的`Supply Voltage`永远是$V_{SS}$。我们做差比较的时候永远是拿`Op-amp`正极减去负极之后来进一步做判断的。
> ![](3_Practice_Exercises.assets/image-20230526230341548.png)

> [!info] Problem (g)
> ![](3_Practice_Exercises.assets/image-20230526232616724.png)![](3_Practice_Exercises.assets/image-20230526232622795.png)
> 🔔: 总的来说，`Period of wave is determined by` $R_1C_1$


# Circuit Intuitions
## KVL
> [dis5D](Exercise_Folder/dis5D.pdf)
> ![](3_Practice_Exercises.assets/image-20230526235514568.png)


## KCL
> ![](3_Practice_Exercises.assets/image-20230526235518745.png)


## Equivalent Resistance
> ![](3_Practice_Exercises.assets/image-20230526235528988.png)![](3_Practice_Exercises.assets/image-20230526235550042.png)![](3_Practice_Exercises.assets/image-20230526235829991.png)![](3_Practice_Exercises.assets/image-20230526235836016.png)![](3_Practice_Exercises.assets/image-20230526235843897.png)


## Current Divider
> ![](3_Practice_Exercises.assets/image-20230526235947868.png)![](3_Practice_Exercises.assets/image-20230526235953159.png)


## Nodal Analysis
> ![](3_Practice_Exercises.assets/image-20230527001809538.png)![](3_Practice_Exercises.assets/image-20230527001818924.png)



## Equivalence I
> [dis5D](Exercise_Folder/dis5D.pdf)
> ![](3_Practice_Exercises.assets/image-20230527001959877.png)

> [!info] Answer
> ![](3_Practice_Exercises.assets/image-20230527074804765.png)


## Equivalence II: Transistor Equivalent⭐⭐⭐⭐⭐
> ![](3_Practice_Exercises.assets/image-20230527161132939.png)![](3_Practice_Exercises.assets/image-20230527161140239.png)

> [!info] Question (a)
> ![](3_Practice_Exercises.assets/image-20230527161232264.png)


> [!info] Question (b)
> ![](3_Practice_Exercises.assets/image-20230527161248293.png)![](3_Practice_Exercises.assets/image-20230527161305727.png)

> [!info] Question (c)
> ![](3_Practice_Exercises.assets/image-20230527161320219.png)![](3_Practice_Exercises.assets/image-20230527161328329.png)


> [!info] Question (d)
> ![](3_Practice_Exercises.assets/image-20230527161336812.png)


> [!info] Question (e)
> ![](3_Practice_Exercises.assets/image-20230527164305452.png)![](3_Practice_Exercises.assets/image-20230527164313190.png)




## Equivalence III: R-2R DAC⭐⭐⭐⭐⭐
> ![](3_Practice_Exercises.assets/image-20230527170349602.png)![](3_Practice_Exercises.assets/image-20230527170355663.png)![](3_Practice_Exercises.assets/image-20230527171116058.png)

> [!info] Answer
> ![](3_Practice_Exercises.assets/image-20230527171126779.png)![](3_Practice_Exercises.assets/image-20230527171137358.png)![](3_Practice_Exercises.assets/image-20230527171147285.png)![](3_Practice_Exercises.assets/image-20230527171156116.png)![](3_Practice_Exercises.assets/image-20230527171201942.png)![](3_Practice_Exercises.assets/image-20230527171209022.png)





# Summary
## Gain Buffer
> 1. $A_V$和$A$有什么不同?
> $A_V$和$A$表示的都是`Op-amp`的`Gain Magnitude`(定义为$\frac{V_{out}}{V_{in}}$), 但是$A_V$表示的是处于`Negative Feedback Loop`中的`Op Amp`的`Gain`, 而$A$表示的是所有`Op Amp`都具有的`Gain`。




# Resources
> [dis4D](Exercise_Folder/dis4D.pdf)
> [dis5A](Exercise_Folder/dis5A.pdf)
> [dis5B](Exercise_Folder/dis5B.pdf)
> [dis5C](Exercise_Folder/dis5C.pdf)
> [dis5D](Exercise_Folder/dis5D.pdf)
> [Sp23 prob11](Exercise_Folder/prob11.pdf)
> [Sp23 prob12](Exercise_Folder/prob12.pdf) 没做