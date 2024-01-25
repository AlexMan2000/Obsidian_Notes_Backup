# Op-Amps
## Node Symbol
> ![](1_Op_Amps.assets/image-20230411104205009.png)
> 🔔：总的来说，我们的输入是$V_-$ 和 $V_+$ , 输出是$V_{out}$。且$V_{out}$的值取决于$V_{DD}$和$V_{SS}$。且$V_{out}$在$[V_{SS}, V_{DD}]$之间取值。
> 其中，$V_+$和$V_-$都是我们用户自定义的输入，$V_{DD}$和$V_{SS}$是用户设置的超参数(也是驱动电压, 是`必须提供`的)，用于规定$V_{out}$可能的取值，然后$V_{out}$是这个系统的输出。
> $V_{DD}$和$V_{SS}$被称为`Rails`。



## Curcuit Model
> 🔔: `Op-Amp`(Operation Amplifier, 运算放大器)电路能够把一个电压信号$V_{+}-V_-$转换成另一个电压信号$V_{out}-V_{SS}$, 下图中就是将$V_+-V_-$放大$A$ 倍成$V_{out}-0=A(V_{+}-V_{-})$。对于任意一个设计较好的`Op-amp`来说，$A\to \infty$, 也就是说，如果不对`Op-amp`所在的电路做一些设计，那么`Op-amp`就只能用于`Comparator`，也就是
> ![](1_Op_Amps.assets/image-20230412121001980.png)![](1_Op_Amps.assets/image-20230524124157273.png)
> 🔔: 对于任意的理想的`Op-amp`来说，此时$A\to \infty$, 那么:
> - 当 $V_+ < V_− (也就是V_+ −V_− < 0$ ，即$A(V_+-V_-)\to -\infty$时，) , 我们有$V_{out} =  \max\{V_{SS},-\infty\}=V_{SS}$ 。
> - 当 $V_+ > V_− (也就是V_+ −V_− > 0$ ，即$A(V_+-V_-)\to \infty$时，) , 我们有$V_{out} =  \min\{V_{DD},\infty\}=V_{DD}$ 。
> - 如果我们将$V_+-V_-=0$附近的区域放大一百万倍, 实际上从点$(0,V_{SS})$到$(0,V_{DD})$之间并不是`Vertical`的，而是有`finite slope`的。
> - `Rail-Determined Offset`是由`Supply Voltages`决定的，本质上是当$V_+=V_-$时，$V_{out}$应该取$V_{DD}$和$V_{SS}$的均值。
> ![](1_Op_Amps.assets/image-20230524123932356.png)![](1_Op_Amps.assets/image-20230524124103889.png)


## Circuit Symbol
> 🔔下面是`Op-amp`的完整结构:
> 1. `Comparator（Railing）`: 当`Op-amp`用于`Comparator`目的时，我们一般需要将`Supply Voltage`($V_{DD}$和$V_{SS}$)标注出来。我们可以用这个`Comparator`对输入电压进行大小判断，如果输出为$V_{DD}$则$V_+>V_-$。
> ![](1_Op_Amps.assets/image-20230412121139105.png)
> 2. `Not Railing`: 当`Op-amp`处在一个`Negative Feedback Loop`中时，我们一般会省略`Supply Voltage`, 因为此时我们的目的就是不让输出电压超过$[V_{SS}, V_{DD}]$这个区间。
> ![](1_Op_Amps.assets/image-20230523233352414.png)![](1_Op_Amps.assets/image-20230523233424507.png)



# Audio System 
## DAC
> A `digital to analog converter` (DAC) is a component that **translates digital signals into output analog voltages**. 
> Say we have a song stored digitally on our computer and we’d like to convert it to a voltage with a DAC and then play it on a speaker.



## Amplifying
> ![](1_Op_Amps.assets/image-20230411110258651.png)
> The DAC takes in digital bits and converts them into an analog signal. Then this signal is fed into a speaker, as illustrated on the right. The maximum voltage the DAC can produce is 3.3V, and the minimum voltage the DAC can produce is 0V. 
> However, you want the input voltage to the speaker to be between 0V and 10V (in order to make the speaker loud enough). So somehow you want to be able to **map voltages from 0 to 3.3V to voltages from 0 to 10V.** 
> 🔔: 所以我们的目标是将`DAC`的$[0V,3.3V]$映射到$[0V,10V]$, 从而使得`Speaker`能够输出较大的音量。更具体的来说，我们想要`Gain is roughly 3`。


# Audio Syatem Circuit Modeling
## ⚠️Attempt 1: Direct Connection
> 我们可以将`Speaker`抽象为一个 $8\Omega$的电阻，然后将`DAC`抽象为其`Thevenin Equivalent`， 其中$V_{TH}$可以理解为$V_+-V_-$。
> 💡: 如果我们直接将`DAC`和`Speaker`相连的话，我们会得到如下电路:
> ![](1_Op_Amps.assets/image-20230412134657192.png)
> 🔔: 注意到这个电路就是比较经典的`Voltage Divider`, 所以$V_{speaker}=\frac{8}{8+1000}\times V_{TH}$, 注意到$V_{speaker}$比$V_{TH}$小很多, 而我们的目标是使得$V_{speaker}$是$V_{TH}$的$(\frac{10}{3.3})$倍。所以这个电路建模并不能满足我们的要求。
> ⭐: 这种电路会导致所谓的`Loading Effect`的情况的发生，也就是说我们将`Speaker`接入电路后会导致其两端电压变得非常小，使得其没有办法被驱动。


## ⚠️Attempt 2: Buffer Layer
> ![](1_Op_Amps.assets/image-20230412140947010.png)
> 🔔: 所以首先我们意识到，我们不能直接将`DAC`与`Speaker`连接，这样得到的是一个`Voltage Divider`电路，所以我们需要在`DAC`和`Speaker`之间添置一个类似于`Op-amp`的结构，但是也不能直接添置，因为`Op-amp`中的$A\to \infty$, 所以此时`Op-amp`默认会作为一个`Comparator`, 其输出将不会是连续的，而是只有$V_{DD}=10V$和$V_{SS}=0V$两个离散的数值。所以这种设计也不完整。
> ![](1_Op_Amps.assets/image-20230412150212847.png)![](1_Op_Amps.assets/image-20230412150223831.png)
> 可以看到，此时我们的$V_{output}$仍然是离散的，原因还是我们的$A\to \infty$导致的`Op-amp Railing`的发生。





## ✔️Attempt 3: Negative Feedback
> Negative feedback is used just about everywhere, including electronics, biology, mechanics, robotics, and more. 
> **Negative feedback occurs when some function of the output of a system is fed back into the input, in a way to keep the output at some finite value.** 
> 💡: `We want` to get **a certain known gain(e.g. 3)** out of our op amp. 
> 📗: `We have` an op-amp with some very large uncertain `internal gain`(e.g. $A$). 
> We can describe this problem using a `block diagram`; a collection of drawings (mathematical in nature) that operate on quantities of interest using simplified representations.
> ![](1_Op_Amps.assets/image-20230412142301494.png)![](1_Op_Amps.assets/image-20230412142655349.png)
> ⭐: 简单来说，这个`Negative Feedback`的作用就是将`Output`控制在一个合理的范围内。
> 上图中有几个公式需要注意:
> - $error = input-feedback$
> - $feedback = f\times output$, 这里$f$ 是非常重要的一个变量，用于控制我们最终输出的范围。
> - $output = A\times error$, 这里$error$其实在$A\to \infty$时是零，后面的部分会介绍。
> 💡：简单推导之后我们可以得到：$output = \frac{A}{1+Af}\times input$。所以当$A\to \infty$时，我们有：$\lim_{A\to \infty}output=\lim_{A\to \infty}\frac{A}{1+A\cdot f}\times input=\frac{input}{f}$. 可以看到，我们可以控制`output`的大小了。比如我们可以选取$f=\frac{1}{3}$, 这样我们就可以精确地控制`output`是`input`的三倍了。
> ![](1_Op_Amps.assets/image-20230412153737352.png)



## Loading and Buffering
> ![](1_Op_Amps.assets/image-20230413120644769.png)![](1_Op_Amps.assets/image-20230413120653259.png)![](1_Op_Amps.assets/image-20230413120659970.png)![](1_Op_Amps.assets/image-20230413120705843.png)![](1_Op_Amps.assets/image-20230524140925886.png)
> 🔔: 本质上说，`Op-Amp`不会改变和其连接的电路中的电压(`No Loading Effect`), 是因为`OpAmp`本质上是一个`Open Circuit`，没有电流，也不会造成电势下降的结果。 





# Op-amp with Negative Feedback

## Negative Feedback Loops
> ![](1_Op_Amps.assets/image-20230412142733608.png)
> 如果$R_1=2R_2$, 则$V_{fb}$(输入端的负极, 也就是`feedback`的电压) = $\frac{R_2}{R_1+R_2}\cdot V_{out}=\frac{1}{3}\cdot V_{out}$(根据`Voltage Divider`的性质)。也就是$feedback = \frac{1}{3}\times output$。
> 因为我们有$feedback = f\times output$, 所以$f=\frac{R_2}{R_1+R_2}=\frac{1}{3}$。
> 同时我们知道$output=\frac{1}{f}\times input$ when $A\to\infty$, 所以$V_{out}=\frac{V_{in}}{f}=\frac{R_1+R_2}{R_2}\times V_{in}=(1+\frac{R_1}{R_2})\cdot V_{in}$
> 🔔: 其中$\frac{1}{f}$称为`Gain with NFB`, 用$A_V$表示，数值上等于$1+\frac{R_1}{R_2}$。
> ![](1_Op_Amps.assets/image-20230412154335118.png)
> 🔔总结一下:
> 1. 对于整个电路系统来说，输入信号用$U_+$ 表示，`Feedback Loop`的输出信号用$U_-$表示。对于`Op-Amp`来说，输入信号是$U_+-U_-$，$A$是放大倍数。对于理想的`OpAmp`来说这个$A\to \infty$。
> 2. $A_v=\frac{A}{1+A\cdot f}$, 其中$U_-=\frac{U_{out}}{f}$。
> 3. $f$的大小可以通过`Voltage Divider`来实现。




## Golden Rules⭐⭐⭐⭐⭐

### Rule 1: No Current(Always True)
> ![](1_Op_Amps.assets/image-20230412153622156.png)
> ⭐: 这条`Rule`对于`Op-amp`(不管有没有`Negative Feedback`都成立)。



### Rule 2: No Error(Only with Negative Feedback)
> ![](1_Op_Amps.assets/image-20230412154444416.png)
> 🔔: 尽管我们的$U_+$和$U_-$没有直接用导线相连，$U_+=U_-$在$A\to \infty$且当`Op-amp`接入了`Negative Feedback`这个`Rule`才生效。

> [!info] Proof
> ![](1_Op_Amps.assets/image-20230412153849465.png)



## Check the negative feedback
### Checking Procedure
> 🔔: 前文说明，只有当`Negative Feedback`存在于`Op-amp`周围时，我们的`Rule Two`才生效。于是现在问题的关键就在于我们如何确定`Op-amp`周围是否存在`Negative Feedback`。
> ![](1_Op_Amps.assets/image-20230412161548122.png)
> 另一种说法：
> ![](1_Op_Amps.assets/image-20230412161626765.png)
> 🔔: `Step 1`比较好理解，我们只需要按照[Equivalence](../1_Resistive_Touchscreen/5_Superposition_and_Equivalence.md#Equivalence)中的`Zero-Out Policy`即可。
> `Step 2`其实说的是，我们给`Output`端施加一个扰动，然后看看这个扰动在经过了整个`Negative Feedback`之后是否有被抵消掉的趋势
> - 如果有就说明`Negative Feedback`存在。
> - 如果没有就是`Positive Feedback`。


### Example Circuit 1
> ![](1_Op_Amps.assets/image-20230412162147196.png)![](1_Op_Amps.assets/image-20230412162154006.png)![](1_Op_Amps.assets/image-20230412162202722.png)![](1_Op_Amps.assets/image-20230412162209266.png)




### Example Circuit 2: Trans-Resistance Amplifier
> ![](1_Op_Amps.assets/image-20230412162231622.png)![](1_Op_Amps.assets/image-20230412162237691.png)



### Example Circuit 3
> ![](1_Op_Amps.assets/image-20230412162249630.png)![](1_Op_Amps.assets/image-20230412162254360.png)



# (Non)-Inverting Amplifers

## Non-inverting Amplifers
> ![](1_Op_Amps.assets/image-20230412160413792.png)![](1_Op_Amps.assets/image-20230412160425716.png)
> 🔔: 注意在我们没有`Attach Negative Feedback`的时候，我们的`Gain`就是`Op-amp`的`Gain`, 用$A$ 表示。当我们接入`Negative Feedback`的时候，我们的`Gain`就是$A_V$, 因为$R_{top}$和$R_{bottom}$都大于零，所以$A_V>1$。
> ⭐:电阻$R_{DAC}$有没有都不会影响我们的电路分析，因为根据`Golden Rule 1`, 我们知道$I_+=0$。
> `Non-inverting`就是说输出电压和输入电压是同号的。



## Inverting Amplifiers
> ![](1_Op_Amps.assets/image-20230412163036186.png)
> `Inverting`就是说输出电压和输入电压是异号的。


## Interactive Example
> ![](1_Op_Amps.assets/image-20230412164046734.png)



# Artificial Neuron
## Definition
> ![](1_Op_Amps.assets/image-20230413115630276.png)


## Inverting Summing Amplifiers
> ![](1_Op_Amps.assets/image-20230413115503175.png)![](1_Op_Amps.assets/image-20230413115610989.png)
> 🔔: 观察$v_{out}$ 和 $v_1$  and $v_2$ 之间的关系(也就是公式11中的$x_1$ 和$x_2$), 我们有 $a_1 = \frac{R_3}{R_1}$ 以及 $a_2 = \frac{R_3}{R_2}$ . This circuit is named "inverting summing amplifier" — since R1,R2,R3 are resistors and all have positive values, the coefficients $a_1$ and $a_2$  are all negative.



## Making Coefficients Positive
> How do we make $a_1$ and $a_2$  positive instead? By adding another inverter amplifier circuit at vout, we can get positive coefficients.
> ![](1_Op_Amps.assets/image-20230413120029722.png)



# Thinking in Block Diagram⭐⭐⭐⭐⭐
## Blocks(Module Thinking)
> ![](1_Op_Amps.assets/image-20230413120944970.png)


## Cascading Block
### Safe Way(Safe Isolation)
> ![](1_Op_Amps.assets/image-20230413121017947.png)


### Unsafe Way(Loading Effect)
> ![](1_Op_Amps.assets/image-20230524154626931.png)![](1_Op_Amps.assets/image-20230524152153680.png)
> 所以理想状况下:
> - 从`Block f()`的视角来看，`Block g()`相当于一个`Open Circuit`, 因为$R_{thg}=\infty$。
> - 从`Block g()`的视角来看，`Block f()`相当于一个`Voltage Source`, 因为我们需要$V_{in}$被原封不动地传导到`Block g()`。因为$R_{thf}=0$(`Wire`)。



# Resources
> [Note17](../2_Capacitive_Touchscreen/Typed_Notes/Note17.pdf)
> [Note18](Typed_Notes/Note18.pdf)
> [Note19](Typed_Notes/Note19.pdf)
> [Written_Notes18](Typed_Notes/Written_Notes18.pdf)
> [Written_Notes19](Typed_Notes/Written_Notes19.pdf)
> [Written_Notes20](Typed_Notes/Written_Notes20.pdf)


