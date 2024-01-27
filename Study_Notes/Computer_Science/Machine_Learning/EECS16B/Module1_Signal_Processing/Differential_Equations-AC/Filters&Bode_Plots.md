# Basic Filters
## Frequency Independent Filter
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687501411012-af979b19-4dfd-47c1-90e4-7ca8e418e770.png#averageHue=%23faf9f9&clientId=ubb32db90-495a-4&from=paste&id=u375ace80&originHeight=481&originWidth=1781&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=94970&status=done&style=none&taskId=ued755686-a8bd-4d91-94a8-1d8eb53441f&title=)
> 1. $R-R$:$H(jw)=\frac{R_2}{R_1+R_2}$, 和$w$无关。 
> 2. $L-L$: $H(jw)=\frac{Z_{L_2}}{Z_{L_1}+Z_{L_2}}=\frac{jwL_2}{jwL_1+jwL_2}=\frac{L_2}{L_1+L_2}$,和$w$无关。 
> 3. $C-C$: $H(jw)=\frac{Z_{C_2}}{Z_{C_1}+Z_{C_2}}=\frac{\frac{1}{jwC_1}}{\frac{1}{jwC_1}+\frac{1}{jwC_2}}=\frac{C_1}{C_1+C_2}$,和$w$无关。$w=0$时，我们的输入$V_{in}(t)$就变成一个恒定的值了，假设为$V_{in}$。
> 
使用`Charge Sharing Argument`可以证明$V_{out}=\frac{C_1}{C_1+C_2}$:
> 因为一开始两个电容都没有充上电，所以`Floating Node`(导线交叉处，$C_1$的右板和$C_2$的上板)的电荷量为零。在接入恒定电压源$V_{in}$之后，交叉处的电荷量总和应该还是零，假设此时$C_1$所携带的电荷量为$Q_1$, $C_2$携带的电荷量为$Q_2$, 所以$Q_1+(-Q_2)=0$, 所以$Q_1=Q_2=Q$, 因为$V_{C_1}=\frac{Q_1}{C_1}, V_{C_2}=\frac{Q_2}{C_2}$, 于是$V_{C_1}+V_{C_2}=V_{in}$, 即$\frac{Q}{C_1}+\frac{Q}{C_2}=V_{in}$, 于是$Q=\frac{C_1C_2V_{in}}{C_1+C_2}$, 所以$V_{C_2}=V_{out}=\frac{C_1}{C_1+C_2}V_{in}$, 所以$H(jw)=\frac{C_1}{C_1+C_2}$仍然成立。




## Low Pass Filter
### Definition
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687502316951-12c78d0d-e678-4808-8be5-7b0b9254cdf9.png#averageHue=%23fcfbfb&clientId=ubb32db90-495a-4&from=paste&height=281&id=ua2186c89&originHeight=422&originWidth=1717&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=44222&status=done&style=none&taskId=udc35b5a5-beec-445c-b120-e40b3a5c7b5&title=&width=1144.6666666666667)
> $H_{\mathrm{LP}}(\mathrm{j} \omega)=\frac{\frac{1}{\mathrm{j} \omega C}}{R+\frac{1}{\mathrm{j} \omega C}}=\frac{1}{1+\mathrm{j} \omega R C}$
> 我们选取$w_c=\frac{1}{RC}$作为基准频率，为什么呢? 因为我们知道$RC$的单位是$s$, 所以$\frac{1}{RC}$的单位是$s^{-1}$(也就是$Hz$), 所以可以作为频率。所以$H_{\mathrm{LP}}(jw)=\frac{1}{1+j\frac{w}{w_c}}$。
> 除了使用`R-C Circuit(测量C的电压)`, 我们还可以使用`L-R Circuit(测量R的电压)`:
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688262908683-3fca7ab7-aab7-4584-ba9c-b3b0c67af961.png#averageHue=%23fefefe&clientId=uf7f5e83e-3c11-4&from=paste&id=u0f7d5591&originHeight=361&originWidth=1268&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=37948&status=done&style=none&taskId=u05104937-8c90-4239-80b7-e85408bc228&title=)
> $H(jw)=\frac{R}{R+jwL}=\frac{1}{1+jw\frac{L}{R}}=\frac{1}{1+j\frac{w}{w_c}}$, 其中$w_c=\frac{R}{L}$。



### Asymptotic Analysis
> 下面我们探究$|H(jw)|$随着$w$变化的变化情况:
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687590536731-03c4c4d9-5315-429b-be0c-52f5e24f69db.png#averageHue=%23fcfbfa&clientId=u649ab3c2-cd35-4&from=paste&id=nvcP0&originHeight=335&originWidth=1350&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=74079&status=done&style=none&taskId=u602699e0-b09c-4016-96a5-bea1c9ddfd5&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688135829742-55a3ad41-3981-4b20-aed6-6fafdcaf6427.png#averageHue=%23edebe9&clientId=uc62dd94c-34d9-4&from=paste&id=VpsYo&originHeight=66&originWidth=2054&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=35193&status=done&style=none&taskId=ub18531e4-faec-422e-8af0-3c2d3d8068f&title=)
> $\begin{array}{cccc}\hline \omega & H(\mathrm{j} \omega) & |H(\mathrm{j} \omega)| & \measuredangle H(\mathrm{j} \omega) \\ \hline w\ll w_c & \approx 1 & \approx 1 & \approx 0^{\circ}\\ \hline 0.1 \omega_c & \frac{1}{1+\mathrm{j} 0.1} & 0.995 & -6^{\circ} \\ \hline \omega_c & \frac{1}{1+\mathrm{j}} & 0.71 & -45^{\circ} \\ \hline 10 \omega_c & \frac{1}{1+\mathrm{j} 10} & 0.1 & -84^{\circ} \\ \hline w\gg w_c & -j\frac{w_c}{w} & \frac{w_c}{w} & -90^{\circ} \\ \hline \end{array}$  
> 
> 1. 当$w\to 0$时(`Low Frequency`$w\ll w_c$), $\frac{1}{1+\mathrm{j} \frac{\omega}{\omega_c}}\approx \frac{1}{1+0}=1+0j$
> 
$\lim_{w\to 0}H_{LP}(jw)=\lim_{w\to 0}\frac{1}{1+\mathrm{j} \frac{\omega}{\omega_c} }=\frac{1}{1+0}=1=1+0j$, 使得频率为$\omega$的信号能够基本都能通过。
> $\lim_{w\to 0}|H_{LP}(jw)|=\lim_{w\to 0}\frac{1}{\sqrt{1+w^2R^2C^2}}=1$
> $\angle H_{\text{HP}}(jw)\approx arctan(\frac{0}{1})\approx arctan(\infty)\approx 0^{\degree}$
> 2. 当$w\to \infty$时(`High Frequency`$w\gg w_c$), $\frac{1}{1+j\frac{w}{w_c}}\approx \frac{1}{j\frac{w}{w_c}}=-j\frac{w_c}{w}\to 0$, 注意$\frac{w_c}{w}>0$且很小。
> 
$\lim_{w\to \infty}H_{LP}(jw)=\lim_{w\to \infty}\frac{1}{1+\mathrm{j} \frac{\omega}{\omega_c}}=0$ 
> $\lim_{w\to \infty}|H_{\mathrm{LP}}(jw)|=\frac{w_c}{w}\to 0$, 使得频率为$w$的信号无法通过。
> $\angle H_{\text{HP}}(jw)\approx arctan(-\frac{\frac{w_c}{w}}{0})\approx arctan(-\infty)\approx -90^{\degree}$


### Transfer Function Plot
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687566249799-8ba72827-675a-4c7f-b350-e1a9a1d69931.png#averageHue=%23f9f8f8&clientId=ubed7ee59-ef23-4&from=paste&id=Q99FG&originHeight=475&originWidth=1299&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=54589&status=done&style=none&taskId=ue49d90bf-9179-41e7-b34f-98f6b51ee54&title=)
> 在绘制`Transfer Fucntion Plot`的时候，我们一般会选取`Log-log Scale`, 则$log|H_{\mathrm{LP}}(jw)|=log(\frac{w_c}{w})=log(w_c)-log(w)$, 可以看见$log(w)$的斜率是$-1$。换句话说，当$w\gg w_c$时，当$w\to 10w$时，$|H_{\mathrm{LP}}(jw)|\to \frac{1}{10}|H_{\mathrm{LP}}(jw)|$, 对应图像的下降段。
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687566393989-e4f330a5-d47d-492f-b9ec-6152b28adf0d.png#averageHue=%23f9f8f8&clientId=ubed7ee59-ef23-4&from=paste&id=PbrLp&originHeight=462&originWidth=1282&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=53082&status=done&style=none&taskId=ub2256afb-1972-4dcc-adf3-3995f00039a&title=)
> 所以，这样的电路称为`Low-Pass Filter`, 使得低频信号能够通过，高频信号被拦截。


### Bode Plots
#### Magnitude
> `Bode Plot`旨在对`Transfer Function Plot`进行`Linear Approximation`, 图像的突变点就是我们的`Cutoff Frequency`$w_c$。
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687768224051-f2f0f506-d966-4031-894a-af4d0dd70073.png#averageHue=%23f9f8f8&clientId=u03d087a8-da6e-4&from=paste&id=u78f5df5c&originHeight=789&originWidth=1617&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=129935&status=done&style=none&taskId=ud6a2479e-f66c-49b8-8964-3328fe482f1&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687767997282-079e0f20-4f19-4dba-9ae8-d9af05d521c7.png#averageHue=%23faf9f9&clientId=u03d087a8-da6e-4&from=paste&id=u08f1749b&originHeight=805&originWidth=1636&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=85981&status=done&style=none&taskId=ue649a5ff-d028-4d8a-a7b5-675126e7d0f&title=)



#### Phase
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687768203090-eb90377e-2875-4c6c-8d75-b97696a64148.png#averageHue=%23f8f7f7&clientId=u03d087a8-da6e-4&from=paste&height=514&id=a5anZ&originHeight=771&originWidth=1616&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=130716&status=done&style=none&taskId=u57c1b050-a817-49a0-b657-7cf180b6bec&title=&width=1077.3333333333333)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687768018037-ba899ebb-fe08-4280-b916-a00520cf092e.png#averageHue=%23f9f9f9&clientId=u03d087a8-da6e-4&from=paste&id=nbg5l&originHeight=766&originWidth=1605&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=82470&status=done&style=none&taskId=u7c2b6a69-f4f8-43bf-9368-fb5f3866ed4&title=)


## High Pass Filter
### Definition
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687505104709-cb8efe5b-dac9-45cf-aeb2-8be1d7c6da56.png#averageHue=%23fbfbfb&clientId=ubb32db90-495a-4&from=paste&height=328&id=ufc2096f4&originHeight=492&originWidth=1971&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=58540&status=done&style=none&taskId=u526abbb2-2294-4d01-af16-afe3f722155&title=&width=1314)
> $H_{\mathrm{HP}}(\mathrm{j} \omega)=\frac{\mathrm{j} \omega L}{R+\mathrm{j} \omega L}=\frac{\mathrm{j} \omega \frac{L}{R}}{1+\mathrm{j} \omega \frac{L}{R}}=\frac{\frac{\mathrm{j} \omega}{\omega_c}}{1+\frac{\mathrm{j} \omega}{\omega_c}}$
> 令$w_c=\frac{R}{L}$, 因为$\frac{L}{R}$的单位是时间，所以$\frac{R}{L}$的单位是频率$Hz$。
> 本质上这个`Filter`就是上面的`Low Pass Filter`的对立面，因为$1-\frac{1}{1+j\frac{w}{w_c}}=\frac{\frac{\mathrm{j} \omega}{\omega_c}}{1+\frac{\mathrm{j} \omega}{\omega_c}}$.
> 除了使用`R-L Circuit(测量L两端的电压)`, 我们还可以使用`C-R Circuit(测量R两端的电压)`
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688263825110-4a2cabe4-6d0f-4d07-b1d5-92fb46378d35.png#averageHue=%23fefefe&clientId=u9bc11cbb-5973-4&from=paste&id=u559f980d&originHeight=369&originWidth=1208&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=37195&status=done&style=none&taskId=u52dac409-2865-4976-a2f0-bce62c1017a&title=)
> $H_{\text{HP}}(jw)=\frac{R}{R+\frac{1}{jwC}}=\frac{jwCR}{1+jwCR}=\frac{j\frac{w}{w_c}}{1+j\frac{w}{w_c}}$，其中$w_c=\frac{1}{CR}$。



### Asymptotic Analysis
> 1. 当$w\to 0$($w\ll w_c$)时，$\frac{\mathrm{j} \frac{\omega}{\omega_c} }{1+\mathrm{j}\frac{\omega}{\omega_c}}\approx \frac{\mathrm{j}\frac{\omega}{\omega_c}}{1}=0+\mathrm{j}\frac{\omega}{\omega_c}$,$\lim_{w\to 0}H_{\mathrm{HP}}(\mathrm{j} \omega)=\lim_{w\to 0}\frac{\mathrm{j} \frac{\omega}{\omega_c} }{1+\mathrm{j} \frac{\omega}{\omega_c}}=\frac{\lim_{w\to 0}j\frac{\omega}{\omega_c}}{\lim_{w\to 0}1+j\frac{\omega}{\omega_c}}=\frac{0}{1}=0$	
> 
$\lim_{w\to 0}|H_{\mathrm{HP}}(jw)|=\lim_{w\to 0}\frac{\frac{w}{w_c}}{\sqrt{1+\frac{w^2}{w_c^2}}}=\lim_{w\to 0}\frac{1}{\sqrt{\frac{w_c^2}{w^2}+1}}\to 0$
> $\angle H_{\text{HP}}(jw)\approx arctan(\frac{\frac{w}{w_c}}{0})\approx arctan(\infty)\approx 90^{\degree}$
> 2. 当$w\to \infty$($w\gg w_c$)时,  $\frac{\mathrm{j} \frac{\omega}{\omega_c} }{1+\mathrm{j}\frac{\omega}{\omega_c}}\approx \frac{\mathrm{j}\frac{\omega}{\omega_c}}{\mathrm{j}\frac{\omega}{\omega_c}}=1+0j$
> 
$\lim_{w\to \infty}H_{\mathrm{HP}}(\mathrm{j} \omega)=\lim_{w\to \infty}\frac{\mathrm{j} \frac{\omega}{\omega_c} }{1+\mathrm{j} \frac{\omega}{\omega_c}}=\lim_{w\to \infty}\frac{1}{\frac{w_c}{jw}+1}=1$
> $\lim_{w\to \infty}|H_{\mathrm{HP}}(jw)|=\frac{1}{\sqrt{\frac{w_c^2}{w^2}+1}}\to 1$, 
> $\angle H_{\text{HP}}(jw)\approx arctan(\frac{0}{1})\approx arctan(0)\approx 0^{\degree}$
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687566478998-35cf3dc1-9a35-4910-9c17-94be2205cf40.png#averageHue=%23faf9f7&clientId=ubed7ee59-ef23-4&from=paste&id=wjNW4&originHeight=135&originWidth=1347&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=41330&status=done&style=none&taskId=ue394c41c-decc-4a05-9444-f6fc139e405&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687566483705-5ae34b2e-5c74-4778-8347-cd68e6c41c05.png#averageHue=%23fcfbfa&clientId=ubed7ee59-ef23-4&from=paste&id=Gasy3&originHeight=218&originWidth=1334&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=47086&status=done&style=none&taskId=u36ebd3d4-34c0-46b7-b26b-87b724251c8&title=)



### Transfer Function Plot
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687566371765-23955c04-b95f-46d7-a095-f1861287ca96.png#averageHue=%23f9f9f8&clientId=ubed7ee59-ef23-4&from=paste&id=Q74Dy&originHeight=463&originWidth=1377&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=54388&status=done&style=none&taskId=ud2cf2430-5858-40ab-91b2-993948730ed&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687566384299-4e54f4ca-8122-4af3-a751-2066542d4dc8.png#averageHue=%23f9f9f8&clientId=ubed7ee59-ef23-4&from=paste&id=VRE9Z&originHeight=450&originWidth=1350&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=53136&status=done&style=none&taskId=ub05235b5-5dfd-458f-bae0-b35e10215d0&title=)
> 所以这样的电路被称为`High-Pass Filter`, 使得高频信号得以通过，低频信号被拦截。



### Bode Plots
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687768076452-86502825-2880-4e6b-bb0e-8e09dc82f45c.png#averageHue=%23f9f9f9&clientId=u03d087a8-da6e-4&from=paste&id=uef05164f&originHeight=767&originWidth=1605&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=82377&status=done&style=none&taskId=u87f54b9f-2835-4065-a25f-65eb3f0043a&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687768081337-a1de1583-a6a8-4446-bd0d-bf934d978a63.png#averageHue=%23faf9f9&clientId=u03d087a8-da6e-4&from=paste&id=u54a943fe&originHeight=795&originWidth=1718&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=85586&status=done&style=none&taskId=u235f2ae6-84c3-4dbd-84b5-c3dca1c54a1&title=)



## More Filters
### LC Tank
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687505809958-3cdbc8b5-a63a-4fc4-bcc4-db4c489be9de.png#averageHue=%23fdfdfd&clientId=ubb32db90-495a-4&from=paste&id=u7776ab55&originHeight=312&originWidth=1531&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=15022&status=done&style=none&taskId=ud470eff0-da28-4a4a-90bc-f8b413da2e9&title=)
> $H(\mathrm{j} \omega)=\frac{\frac{1}{\mathrm{j} \omega C}}{\frac{1}{\mathrm{j} \omega C}+\mathrm{j} \omega L}=\frac{1}{1-\omega^2 L C}$
> 1. **At low frequency, frequencies are preserved:**$\lim_{w\to 0}\frac{1}{1-\omega^2 L C}=1$
> 2. **At high frequency, frequencies are filtered out: **$\lim_{w\to \infty}\frac{1}{1-\omega^2 L C}=0$
> 
所以这是一个`Low-Pass Filter`。





## Cutoff Frequency
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687571164933-f2dac12d-01b3-44c2-8a1a-92ec904552fc.png#averageHue=%23fcfbfb&clientId=ubed7ee59-ef23-4&from=paste&id=ub0cf5ca0&originHeight=171&originWidth=1438&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=30965&status=done&style=none&taskId=ud7eb646e-15a2-458e-b0e5-48a6353fd9f&title=)
> 1. 对于`RC-Low Pass Filter`来说，我们有$H(jw)=\frac{1}{1+jwCR}$, 我们计算$|H(jw)|=\frac{1}{\sqrt{1+w^2(CR)^2}}$, 然后求解$max_w|H(jw)|=1(w=0)$, 所以$\frac{1}{\sqrt{1+(w_cCR)^2}}=\frac{1}{\sqrt{2}}$, 所以$w_cCR=1$, 即$w_c=\frac{1}{CR}$。
> 2. 对于`RL-Low Pass Filter`来说，我们有$H(jw)=\frac{\mathrm{j} \omega \frac{L}{R}}{1+\mathrm{j} \omega \frac{L}{R}}$, 我们计算$|H(jw)|=\frac{w\frac{L}{R}}{\sqrt{1+\frac{w^2L^2}{R^2}}}=\frac{1}{\sqrt{\frac{R^2}{w^2L^2}+1}}$, 然后求解$max_w|H(jw)|=1(w\to \infty)$, 所以$\frac{1}{\sqrt{\frac{R^2}{w_c^2L^2}+1}}=\frac{1}{\sqrt{2}}$, 所以$\frac{R^2}{w_c^2L^2}=1$, 即$w_c=\frac{R}{L}$。
> 3. `Cutoff Frequency`所代表的频率实际上是一种分界线，远低于这个频率的输入信号和远高于这个频率的输入信号在通过$H(jw)$这个`Filter`之后的`Amplitude`的变化差异十分明显。
>    1. 对于`Low-Pass Filter`来说，如果$w\ll w_c$, 则信号几乎完全通过，如果$w\gg w_c$, 则信号几乎被拦截。
>    2. 对于`High-Pass Filter`来说，如果$w\ll w_c$, 则信号几乎被拦截，如果$w\gg w_c$, 则信号几乎完全通过。



# Higher Order Filters
## Band-Pass Filter
### Definition
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687742421544-2abd451d-db18-4bb6-969c-8de683f7130b.png#averageHue=%23f9eae9&clientId=u592420b9-35bd-4&from=paste&id=u566fadd9&originHeight=189&originWidth=1398&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=48523&status=done&style=none&taskId=u00ab3f26-667d-4f59-a27e-3fb5169b0ae&title=)



### OpAmp Model
> It is quite common to need to design a filter which selects only a narrow range of frequencies. One example is in **WiFi radios**, it is desirable to select only the 2.4GHz frequency containing your data, and reject information from other nearby cellular or bluetooth frequencies(用于选取特定频段的信号)。
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687570948402-31960294-1c6c-4f22-9699-7c5b815770db.png#averageHue=%23faf9f9&clientId=ubed7ee59-ef23-4&from=paste&id=u59a2cc3e&originHeight=384&originWidth=1366&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=57501&status=done&style=none&taskId=u6c1d6d1a-a0dd-4c5b-be01-1d79cfdb3c5&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687592846710-4f777604-8300-4795-aaa5-9e41757bb435.png#averageHue=%23faf9f8&clientId=u649ab3c2-cd35-4&from=paste&id=uf022ca8a&originHeight=756&originWidth=1383&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=202079&status=done&style=none&taskId=ubbb2d16e-567f-49a0-a20e-2e6f79b76b5&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687608675411-71a6e511-bd28-421e-8ef6-25c1527f049e.png#averageHue=%23f7f7f7&clientId=uf7f00b19-e712-4&from=paste&id=uad73e86e&originHeight=850&originWidth=2010&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=153399&status=done&style=none&taskId=u7c6feb05-3f1b-4809-8d4d-7edaf6f7685&title=)
> `Band Pass`实际实际上就是两个`Cutoff Frequency`直接的差值，也就是上图中平坦区域的频率范围。
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687614778458-c0fa1770-36b7-4406-9f24-bbdaa67389b9.png#averageHue=%23f3f1ef&clientId=ud36d34b1-f58f-4&from=paste&id=u5f00cceb&originHeight=465&originWidth=1943&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=223921&status=done&style=none&taskId=udf358e9e-e5eb-49fe-9abb-0b5ad3fa97e&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687767635286-09a34237-e420-4035-b825-d872cc75502d.png#averageHue=%23fafafa&clientId=u03d087a8-da6e-4&from=paste&id=uc59b6ce9&originHeight=1328&originWidth=1391&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=159925&status=done&style=none&taskId=u96dcebd6-4395-4c90-8bf4-993035cc969&title=)



### RLC Model(Codes)⭐⭐⭐⭐⭐
> **HW05 Fa21 P8/HW05 Sp22 P6/Disc05A Fa21 P2**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687612470457-02f57b72-5bc6-407f-918c-33402ce115cd.png#averageHue=%23f9f9f8&clientId=ud36d34b1-f58f-4&from=paste&id=ufe6e8286&originHeight=372&originWidth=1464&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=56574&status=done&style=none&taskId=uf52c3faa-6f22-4cc5-994f-421935b5ff5&title=)
> 1. $Z_{RLC} =Z_L+Z_C+Z_R=jwL+\frac{1}{jwC}+R=R+j\cdot (wL-\frac{1}{wC})=A(w)+jX(w)$, 其中$A(w)$和$X(w)$是两个`Real-Valued Functions`。
> 2. `Asymptotic Analysis`渐进分析:$H(jw)=\frac{\tilde{V}_{out}}{\tilde{V}_{in}}=\frac{Z_{R}}{Z_{RLC}}=\frac{R}{R+j\cdot(wL-\frac{1}{wC})}=\frac{1}{1+j(w\frac{L}{R}-\frac{1}{wRC})}$
>    1. 当$w\to 0$时， $\frac{R}{R+j\cdot(wL-\frac{1}{wC})}\approx \frac{R}{R+j(-\frac{1}{wC})}\approx0$
>    2. 当$w\to \infty$时，$\frac{R}{R+j\cdot(wL-\frac{1}{wC})}\approx \frac{R}{R+jwL}\approx 0$
>    3. 当$wL=\frac{1}{wC}$, 即$w=\sqrt{\frac{1}{LC}}$时，$H(jw)=\frac{R}{R+j\cdot(wL-\frac{1}{wC})}=\frac{R}{R}=1$，这个频率称为`Resonant Frequency`，此时电容和电导导致的虚数部分完全消除。在`Resonant Circuits`一章节中详细介绍这类电路。所以`Resonant Frequency`取决于$L,C$的取值。
> 3. `Magnitude&Phase`:
> 
`Magnitude`相对容易，我们只需要求模即可。
> $\begin{aligned}
|H(\mathrm{j} \omega)| & =\left|\frac{1}{1+\mathrm{j}\left(\omega \frac{L}{R}-\frac{1}{\omega R C}\right)}\right| \\
& =\frac{|1|}{\left|1+\mathrm{j}\left(\omega \frac{L}{R}-\frac{1}{\omega R C}\right)\right|} \\
& =\frac{1}{\sqrt{\left(1+\mathrm{j}\left(\omega \frac{L}{R}-\frac{1}{\omega R C}\right)\right)\left(1-\mathrm{j}\left(\omega \frac{L}{R}-\frac{1}{\omega R C}\right)\right)}} \\
& =\frac{1}{\sqrt{1+\left(\omega \frac{L}{R}-\frac{1}{\omega R C}\right)^2}}
\end{aligned}$
> `Phase`的求法由两种，一种是将$H(jw)$写成$H(jw)=X(w)+jY(w)$, 然后$\angle H(jw)=atan2(Y(w),X(w))$(或者$atan2(\frac{Y(w)}{X(w)},1)$)。另一种是将$H(jw)$看成$\frac{A(jw)}{B(jw)}$, 分别求出$\angle B(jw)$和$\angle B(jw)$, 然后$\angle H(jw)=\angle A(jw)-\angle B(jw)$
> **方法一:**
> $\begin{aligned}H(\mathrm{j} \omega) & =\frac{1}{1+\mathrm{j}\left(\omega \frac{L}{R}-\frac{1}{\omega R C}\right)} \\& =\frac{1}{1+\mathrm{j}\left(\omega \frac{L}{R}-\frac{1}{\omega R C}\right)} \times \frac{1-\mathrm{j}\left(\omega \frac{L}{R}-\frac{1}{\omega R C}\right)}{1-\mathrm{j}\left(\omega \frac{L}{R}-\frac{1}{\omega R C}\right)} \\& =\frac{1-\mathrm{j}\left(\omega \frac{L}{R}-\frac{1}{\omega R C}\right)}{1+\left(\omega \frac{L}{R}-\frac{1}{\omega R C}\right)^2} \\& =\frac{1}{1+\left(\omega \frac{L}{R}-\frac{1}{\omega R C}\right)^2}+\mathrm{j} \frac{-\left(\omega \frac{L}{R}-\frac{1}{\omega R C}\right)}{1+\left(\omega \frac{L}{R}-\frac{1}{\omega R C}\right)^2}\end{aligned}$
> $\begin{aligned}\angle H(\mathrm{j} \omega) & =\operatorname{atan} 2\left(\frac{Y(\omega)}{X(\omega)}, 1\right) \\& =\operatorname{atan} 2\left(\frac{-\frac{-\left(\omega \frac{L}{R}-\frac{1}{\omega R C}\right)}{1+\left(\omega \frac{L}{R}-\frac{1}{\omega R C}\right)^2}}{\frac{1}{1+\left(\omega \frac{L}{R}-\frac{1}{\omega R C}\right)^2}}, 1\right)\\&\begin{aligned}
& =\operatorname{atan} 2\left(\frac{-\left(\omega \frac{L}{R}-\frac{1}{\omega R C}\right)}{1}, 1\right) \\
& =-\operatorname{atan} 2\left(\omega \frac{L}{R}-\frac{1}{\omega R C}, 1\right)
\end{aligned}\end{aligned}$
> **方法二:**
> $\begin{aligned}\angle H(\mathrm{j} \omega) & =\angle 1-\angle\left(1+\mathrm{j}\left(\omega \frac{L}{R}-\frac{1}{\omega R C}\right)\right) \\& =0-\operatorname{atan} 2\left(\omega \frac{L}{R}-\frac{1}{\omega R C}, 1\right) \\& =-\operatorname{atan} 2\left(\omega \frac{L}{R}-\frac{1}{\omega R C}, 1\right)\end{aligned}$
> 4. **在**[**RLC Circuit Analysis**](https://www.yuque.com/alexman/edfboy/phq4yp791xcc8if9#HKhkx)**中我们已经分析过，根据**$R,L,C$**的相对大小关系电路会有四种状态:**
> 
特征值是: $\lambda=-\frac{1}{2} \frac{R}{L} \pm \frac{1}{2} \sqrt{\left(\frac{R}{L}\right)^2-\frac{4}{L C}}$, 则:
>       1. `Overdamped`: 此时对应特征值为不相等的实数，即$(\frac{R}{L})^2-\frac{4}{LC}>0$, 即$R>2 \sqrt{\frac{L}{C}}$。
>       2. `Undamped`: 此时对应特征值只有虚数部分，即$R=0$, 且$(\frac{R}{L})^2-\frac{4}{LC}<0$。
>       3. `Underdamped`: 此时对应特征值实部和虚部均不是零，即$R\neq 0$, 且$(\frac{R}{L})^2-\frac{4}{LC}<0$
>       4. `Critically Damped`: 此时对应$(\frac{R}{L})^2-\frac{4}{LC}=0$, 即$R=2\sqrt{\frac{L}{C}}$。

```python
import numpy as np
import matplotlib.pyplot as plt

# This function will generate the magnitude (and optionally the phase) 
# of the inputed transfer function. 
# Inputs: 
#     H (function) - The transfer function of interest
#     w_range (length 2 tuple) - The function will plot w in [10 ** w_range[0], 10 ** w_range[1]]
#     phase (boolean) - Default is false, optionally plots the phase response
# Outputs:
#     None, just plots the function.
def plot_tf(H, w_range, phase=False):
    w = np.logspace(w_range[0], w_range[1], num=1000)
    
    plt.grid()
    plt.title('Magnitude Plot: $|H(j\omega)|$')
    plt.xlabel('$\omega$')
    plt.ylabel('$|H(j\omega)|$')
    plt.loglog(w, np.abs(H(w)))
    
    if phase:
        plt.figure()
        plt.grid()
        plt.title('Phase Plot: Phase of $H(j\omega)$')
        plt.xlabel('$\omega$')
        plt.ylabel('$\measuredangle H(j\omega)$')
        plt.semilogx(w, np.angle(H(w)) * 180 / np.pi)
```
```python
# Define your transfer function
# Our own H(jw)
def H_example(R, L, C):
    # For plotting
    def H(w):
        return 1 / (1 + 1j * ( w * L / R - 1 / (w * R * C)))
    return H

R = 1e3 
L = 25e-6
C = 10e-9

#Pass in your transfer function and the log range to plot_tf
plot_tf(H_example(R, L, C), (-2, 15), phase=True)
```
**Overdamped Output**$R=1 \mathrm{k} \Omega, C=10 \mathrm{nF}, L=25 \mu \mathrm{H}$
![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688266288286-d390b376-d4f0-481e-9bf9-248338b09d4f.png#averageHue=%23f9f9f9&clientId=u2cf541a2-6d1f-4&from=paste&id=ua448b59f&originHeight=1821&originWidth=1291&originalType=binary&ratio=1.6500000953674316&rotation=0&showTitle=false&size=201304&status=done&style=none&taskId=uaf255345-2a90-4a44-977b-94d577b90c0&title=)
**Underdamped Output**$R=1 \Omega, C=10 \mathrm{nF}, L=25 \mu \mathrm{H}$
![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688266389691-88f314ef-4553-4916-989b-0976022ff9e4.png#averageHue=%23fafafa&clientId=u2cf541a2-6d1f-4&from=paste&id=u3b3e60ac&originHeight=1819&originWidth=1199&originalType=binary&ratio=1.6500000953674316&rotation=0&showTitle=false&size=167557&status=done&style=none&taskId=ue697f0a2-de84-44a9-86d7-55ee1f07a80&title=)
**Critically Damped Output**$R=100 \Omega, C=10 \mathrm{nF}, L=25 \mu \mathrm{H}$
![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688266626877-b5f73fe7-321c-4aa1-aa1e-d77133382cc4.png#averageHue=%23fafafa&clientId=u2cf541a2-6d1f-4&from=paste&id=u55caf3d9&originHeight=1812&originWidth=1279&originalType=binary&ratio=1.6500000953674316&rotation=0&showTitle=false&size=178402&status=done&style=none&taskId=u5b8a8213-8f17-4c01-9834-48eb852936f&title=)
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688266735251-1c9b72b0-db73-4570-8386-558e647b95f2.png#averageHue=%23f1f1f1&clientId=u2cf541a2-6d1f-4&from=paste&id=uc7cb63ec&originHeight=857&originWidth=1758&originalType=binary&ratio=1.6500000953674316&rotation=0&showTitle=false&size=188015&status=done&style=none&taskId=u4ef458f7-fdd0-4bca-ac2a-a250c8b37bf&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688266758652-54168638-cee8-466e-b693-42165017fee9.png#averageHue=%23f7f7f7&clientId=u2cf541a2-6d1f-4&from=paste&id=uc4f80762&originHeight=1873&originWidth=3381&originalType=binary&ratio=1.6500000953674316&rotation=0&showTitle=false&size=936251&status=done&style=none&taskId=u81520d1a-da7b-4213-b407-4b03a26c51c&title=)



## Notch Filter
### Definition
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687758097269-f8c311a8-98e9-41ce-99d1-bc6ead7c70d9.png#averageHue=%23fcf8f8&clientId=u68721659-3a92-4&from=paste&id=oIt1w&originHeight=831&originWidth=1447&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=104929&status=done&style=none&taskId=u11cdb3f8-306e-412a-8e32-778634940ed&title=)


### Transfer Function
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687758229788-fb96a5c9-6f01-415f-a3d7-0d77e83d2078.png#averageHue=%23fcfcfb&clientId=u68721659-3a92-4&from=paste&id=fh4RK&originHeight=190&originWidth=1449&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=30416&status=done&style=none&taskId=u23ef6874-36a0-44ed-b6bb-d61f28ffd0f&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687758250847-de587731-3041-4179-b783-ff0ff8ac8bf3.png#averageHue=%23fbfaf9&clientId=u68721659-3a92-4&from=paste&id=aTDaV&originHeight=954&originWidth=1428&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=197420&status=done&style=none&taskId=u41cada7f-4652-4e97-aa40-49f5380b048&title=)
> 当$w\to 0$时，$\lim_{w\to 0}|H(jw)|=\frac{\lim_{w\to 0} 1}{\lim_{w\to 0}\sqrt{1+(\frac{wRC}{1-w^2LC})^2}}=\frac{1}{1}=1$
> 当$w\to \infty$时，$\lim_{w\to \infty}|H(jw)|=\frac{\lim_{w\to \infty} 1}{\lim_{w\to \infty}\sqrt{1+(\frac{wRC}{1-w^2LC})^2}}=\frac{1}{1}=1$



### Graph
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687758486875-b1586012-1f35-4290-946e-6fc9475f095b.png#averageHue=%23fefefe&clientId=u68721659-3a92-4&from=paste&height=280&id=kVuSq&originHeight=420&originWidth=1135&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=72202&status=done&style=none&taskId=u460e83a9-f03c-4e8e-a006-cbd3b261518&title=&width=756.6666666666666)




## Higher Order Low Pass Filter
### Notations
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687742460579-cd76505c-6a23-40ab-b854-13c506d7cf17.png#averageHue=%23fbeceb&clientId=u592420b9-35bd-4&from=paste&id=u8ad4fda0&originHeight=314&originWidth=1414&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=64030&status=done&style=none&taskId=u9abb748f-aa7e-4624-a3a3-242e6641849&title=)



### Second Order
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687613627900-deee37de-abfe-4e18-956a-c4ebf2b231cf.png#averageHue=%23f7f6f5&clientId=ud36d34b1-f58f-4&from=paste&id=ue28567d8&originHeight=1284&originWidth=2015&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=330679&status=done&style=none&taskId=u5c60e1a7-35b8-4efc-beab-9719b48bb73&title=)
> 假设`Cutoff Frequency`是$w_c=\frac{1}{RC}$, 则当$w\gg w_c$时，$H(jw)=\frac{1}{(1+jwRC)^2}=\frac{1}{(1+j\frac{w}{w_c})^2}\approx\frac{1}{(j\frac{w}{w_c})^2}=-\frac{w_c^2}{w^2}$, 所以$|H(jw)|=\frac{w_c^2}{w^2}$, 此时$log(|H(jw)|)=log(w_c^2)-log(w^2)=log(w_c)-2log(w)$, 可以看到这里的斜率是$-2$，比之前的`First Order Low Pass Filter`对于高频信号的过滤效果更好。



### Higher Order
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687614761046-12c71f79-8ab2-43ff-9202-952dce7b6032.png#averageHue=%23f6f5f4&clientId=ud36d34b1-f58f-4&from=paste&id=u53566022&originHeight=1101&originWidth=1846&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=345839&status=done&style=none&taskId=u4c1e27e1-9e99-4880-b3f3-99a64136e12&title=)

## 

## More Filters
### RCR Circuit
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687610677467-ad7ddd6c-b1df-456d-b4c6-aa601e1f9cc7.png#averageHue=%23faf9f9&clientId=ud36d34b1-f58f-4&from=paste&id=X2qyJ&originHeight=712&originWidth=1822&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=87308&status=done&style=none&taskId=u382e7461-24fc-4e05-ac6e-4601144e089&title=)
> $H(jw)=\frac{Z_C+Z_{R_2}}{Z_C+Z_{R_1}+Z_{R_2}}=\frac{\frac{1}{jwC}+R_2}{\frac{1}{jwC}+R_1+R_2}=\frac{1+jwCR_2}{1+jwC(R_1+R_2)}$
> 1. **At low frequency, frequencies are preserved:**$\lim_{w\to 0}\frac{\frac{1}{jwC}+R_2}{\frac{1}{jwC}+R_1+R_2}=\frac{1+jwCR_2}{1+jwC(R_1+R_2)}=\frac{\lim_{w\to 0}1+jwCR_2}{\lim_{w\to 0}1+jwC(R_1+R_2)}=1$
> 2. **At high frequency, frequencies are diminished: **$\lim_{w\to \infty} \frac{1+jwCR_2}{1+jwC(R_1+R_2)}=\lim_{w\to \infty}\frac{1}{1+\frac{jwCR_1}{1+jwCR_2}}=\lim_{w\to \infty}\frac{1}{1+\frac{1}{\frac{1}{jwCR_1}+\frac{R_2}{R_1}}}=\frac{R_2}{R_1+R_2}$
> 
This circuit is like **a combination of a low-pass filter and a voltage divider**: low frequency inputs are preserved, and high-frequency signals are diminished.  




# Composition of Transfer Function
## Basic Properties
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687615095246-3423a37e-cbf9-47eb-9cf4-9a15bd010d76.png#averageHue=%23faf9f9&clientId=ud36d34b1-f58f-4&from=paste&id=u90ac0528&originHeight=512&originWidth=1898&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=124993&status=done&style=none&taskId=u32bffb44-cae3-4e8b-ba3b-2083962c231&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687615098742-da092d9a-e6e9-437b-9b79-2146e680b5d5.png#averageHue=%23fdfdfc&clientId=ud36d34b1-f58f-4&from=paste&id=u4151b8a8&originHeight=254&originWidth=1845&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=31789&status=done&style=none&taskId=u6d7e6161-9db8-4050-8f02-f209b1fc9bd&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687766850585-5b1e0d27-8683-43e0-9cc4-1692783abf14.png#averageHue=%23f7f7f7&clientId=u03d087a8-da6e-4&from=paste&id=ud4252077&originHeight=439&originWidth=1548&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=89084&status=done&style=none&taskId=ud62f7ed8-4b9a-41c9-b877-5e7607b494d&title=)



## Choice of Scale for Plots
### Log-Log Scale - Magnitude
> 上文中的`Transfer Function Plot`旨在探究$|H(jw)|$和$w$之间的关系，一般我们会选取`log-scale`进行绘制，即横轴选取$log(w)$, 纵轴选取$log|H(jw)|$。
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687566249799-8ba72827-675a-4c7f-b350-e1a9a1d69931.png#averageHue=%23f9f8f8&clientId=ubed7ee59-ef23-4&from=paste&id=I4aBu&originHeight=475&originWidth=1299&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=54589&status=done&style=none&taskId=ue49d90bf-9179-41e7-b34f-98f6b51ee54&title=)
> 所以尽管横轴上的数值是$10^1, 10^2,\cdots, 10^6$的非等间距数值，但是`log`之后就是等间距排布。
> 选取`log-log scale`的好处就是，我们再进行`Filters`的组合时:
> 如果已经得到了`Filter`各自的`|H(jw)|-w`图，则因为$|H(jw)|=|H_1(jw)|\times|H_2(jw)|$在`log-scale`下就变成了$log|H(jw)|=log|H_1(jw)|+log|H_2(jw)|$，所以纵轴可以直接相加方便作图。



### Semi-Log Scale - Phase
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687566393989-e4f330a5-d47d-492f-b9ec-6152b28adf0d.png#averageHue=%23f9f8f8&clientId=ubed7ee59-ef23-4&from=paste&id=xq8qY&originHeight=462&originWidth=1282&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=53082&status=done&style=none&taskId=ub2256afb-1972-4dcc-adf3-3995f00039a&title=)
> 横轴上是`log-scale`, 纵轴上是`linear scale`。



### Decibel Scale - Semi-Log
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687742967461-e49397c7-8bce-4e67-9791-36d15ce8c361.png#averageHue=%23f7f6f5&clientId=u592420b9-35bd-4&from=paste&id=s2gM3&originHeight=746&originWidth=2113&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=211657&status=done&style=none&taskId=u52dfd522-016b-476d-b36c-234fa61df2f&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687753195803-6422695d-a2f6-417f-b7bb-5f5a020f4da6.png#averageHue=%23f5f5f4&clientId=u2aca958e-af87-4&from=paste&id=Bkxtk&originHeight=1122&originWidth=2138&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=302126&status=done&style=none&taskId=u33f2fa50-3d13-47bb-b89f-3b8fcbd57c8&title=)
> 🔔: 为什么我们需要使用`Decibel Scale`呢? 好处是什么呢?
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687768537013-452dd230-b7f9-47d9-84de-1b1998bb5e23.png#averageHue=%23eeebe9&clientId=u03d087a8-da6e-4&from=paste&id=udc39b1b4&originHeight=176&originWidth=1928&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=94112&status=done&style=none&taskId=ub23d94c4-b0ae-41dd-a29b-7c40c9d947e&title=)







# 


# Resources
> Note 6/7/8 Fa21
> Note 5/6 Sp23

