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
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1684323956610-6c1331bf-d216-4bc7-bfc4-9895409aea29.png#averageHue=%23728274&clientId=ud3c484e6-5e0d-4&from=paste&id=GziBL&originHeight=485&originWidth=1553&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=102597&status=done&style=none&taskId=uecfeb606-efcf-4d7a-80a0-a72fd8d50b3&title=)
> 电流源恒定时，$V_C(t)-V_C(0)=\frac{I_St}{C}$


## Capacitor I
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686732036581-91eb3264-fc92-4c04-843f-f2e1a52006e6.png#averageHue=%23fcfcfc&clientId=u15bb439c-c178-4&from=paste&id=u924cfdae&originHeight=1101&originWidth=1305&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=89463&status=done&style=none&taskId=uc3f0ddaa-ac2b-4d27-8aa7-9ef775715ce&title=)

**Voltage**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686732515046-dd605aad-05c9-401a-8f40-2ff68b66dc70.png#averageHue=%23ffffff&clientId=u15bb439c-c178-4&from=paste&height=146&id=udfc62d16&originHeight=219&originWidth=1237&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=33923&status=done&style=none&taskId=ua24fce31-de79-4bc9-ad17-ec3202e0aff&title=&width=824.6666666666666)
首先注意这里的$\int_{0}^t i(t')dt'$的单位是$mA\cdot ms$, 所以在将$100$和$-100$带入求积分之后我们需要对得到的值乘以$10^{-3}\times 10^{-3}=10^{-6}$, 所以图像的斜率应该是$\frac{1}{3}\times 10^6\times 100\times 10^{-3}\times 10^{-3}=33.3$。
![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686732845008-56f15ac7-7e9c-4ce3-b38e-fb211f46b65b.png#averageHue=%23fefefe&clientId=u15bb439c-c178-4&from=paste&id=ue55ba62b&originHeight=478&originWidth=1093&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=24853&status=done&style=none&taskId=u27d734cf-3cee-442b-9914-d9329d39dcb&title=)
**Power**$V_C(t)=10+33.3t$, $I_C(t)=\begin{cases} 0.1A&0~s<t<0.001~s\\-0.1A&0.001s<t<0.002s\end{cases}$
所以$W_C(t)=V_C(t)I_C(t)=(10+33.3t)I_C(t)=\begin{cases} 1+3.33t&0~s<t<0.001~s\\-1-3.33t&0.001s<t<0.002s\end{cases}$
![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686733882866-d286e038-6a26-4bfc-930c-940b949dc6f4.png#averageHue=%23fefefe&clientId=u15bb439c-c178-4&from=paste&id=u458125a0&originHeight=472&originWidth=1157&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=35880&status=done&style=none&taskId=u053f4237-0299-4c27-9b48-8fc16c0518f&title=)
**Stored Energy**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686747138480-faa077d4-d388-4a6e-9adc-a4f760b6714d.png#averageHue=%23fefefe&clientId=ud9fd1b67-fd7f-4&from=paste&id=ua9b88cb4&originHeight=535&originWidth=1089&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=41973&status=done&style=none&taskId=u679a404f-0540-4911-9b9f-824908e7987&title=)

## Capacitor II: Circuit Equivalence
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686747230006-0c10c8aa-855d-4136-b42d-95b663ca574d.png#averageHue=%23fcfbfb&clientId=ud9fd1b67-fd7f-4&from=paste&id=u94fe2168&originHeight=1195&originWidth=1271&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=157525&status=done&style=none&taskId=u8176a2ef-9c95-4126-9af8-6a44e6f5007&title=)

**Solution (a)**$\begin{aligned}100V-\frac{dV_C(t)}{dt}\cdot CR&=V_C(t)\\\frac{dV_C(t)}{dt}&=-\frac{1}{CR}V_C(t)+\frac{100}{CR}\end{aligned}$
所以$V_C(t)=100(1-e^{-\frac{t}{10^{-3}}})$
![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686748461369-160bf31c-c5c5-40a4-ab5b-22ed1fcf3bf6.png#averageHue=%23fefefe&clientId=ub0c263de-e223-4&from=paste&id=u2afa82e8&originHeight=506&originWidth=1168&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=24722&status=done&style=none&taskId=uf77df4dc-7373-495c-b786-710ba5bf05a&title=)
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686747248954-5305e258-a6c6-4016-9b76-ffd6a898bfbc.png#averageHue=%23fbf9f8&clientId=ud9fd1b67-fd7f-4&from=paste&id=u11cd8d20&originHeight=45&originWidth=1144&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=13501&status=done&style=none&taskId=u80229a8f-8e47-4696-8034-64238de5487&title=)

**Solution (b)**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686748474832-e3706bef-ee7f-4988-9b90-799b8fd5f094.png#averageHue=%23ffffff&clientId=ub0c263de-e223-4&from=paste&id=u245f0946&originHeight=165&originWidth=1168&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=30674&status=done&style=none&taskId=u61d9a0b5-1c78-40f8-bd7c-60de83183a0&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686748478200-80d5e336-e5c4-4b10-aafb-3ebed0338145.png#averageHue=%23fefefe&clientId=ub0c263de-e223-4&from=paste&id=ub8fe8bf0&originHeight=480&originWidth=1154&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=22639&status=done&style=none&taskId=u490418a6-da70-445c-849e-6a9140459c0&title=)

## Capacitor III
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686748601780-88d66734-5373-4315-8a37-e9347ed88be4.png#averageHue=%23fcfcfc&clientId=ueb7e337d-6e82-4&from=paste&id=WMRqs&originHeight=468&originWidth=1157&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=40061&status=done&style=none&taskId=uc3159847-42c7-49c8-a0ee-96104cffe99&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686749600865-af5f8590-a15c-4715-a0ff-0909782962c6.png#averageHue=%23fbf9f8&clientId=ueb7e337d-6e82-4&from=paste&id=ZyNTc&originHeight=84&originWidth=1176&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=20210&status=done&style=none&taskId=ud30c5142-65ba-47be-9c43-b964e8df17e&title=)

**Solution**根据`KVL`定律我们有$V_C(t)-V_R(t)=0$
电流方向是从电容的正极流向负极，所以$V_R(t)=-I_C(t)R$
因为$I_C(t)=\frac{dV_C(t)}{dt}\cdot C$, 所以$V_C(t)+\frac{dV_C(t)}{dt}\cdot CR=0$。
所以$\frac{dV_C(t)}{dt}=-\frac{1}{CR}V_C(t)$, 这里$CR=0.02\times 10^{-6}\cdot 1\times 10^6=0.02$。
所以$\frac{dV_C(t)}{dt}=-\frac{1}{0.02}V_C(t)$, 得到$V_C(t)=V_C(0)e^{-\frac{1}{0.02}t}=50e^{-\frac{t}{0.02}}$
综合来看，我们有: $V_C(t)=\begin{cases} 50&t\leq0\\ 50e^{-\frac{t}{0.02}}&t>0\end{cases}$, $V_R(t)=\begin{cases} 50&t\leq0\\ 50e^{-\frac{t}{0.02}}&t>0\end{cases}$
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686749613187-913217e7-03bf-4cd3-a80f-b83ea72755c1.png#averageHue=%23f9f8f6&clientId=ueb7e337d-6e82-4&from=paste&id=rxf0g&originHeight=43&originWidth=1152&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=12492&status=done&style=none&taskId=ua795c45a-4cbd-415f-a011-963011041b1&title=)

**Solution**$I_C(t)=\frac{dV_C(t)}{dt}\cdot C=\begin{cases}0&t\leq 0\\-2500e^{-50t}&t>0 \end{cases}\times 0.02\times 10^{-6}=\begin{cases} 0&t\leq 0\\-50e^{-50t}\times 10^{-6}&t>0\end{cases}$
$\begin{aligned}W_R(t)&=V_{R}(t)I_R(t)=V_R(t)\cdot (-I_C(t))\\&=\begin{cases} 50&t\leq0\\ 50e^{-\frac{t}{0.02}}&t>0\end{cases}\times (-\begin{cases} 0&t\leq 0\\-5e^{-50t}\times 10^{-6}&t>0\end{cases})\\&=\begin{cases}0&t\leq 0\\2500e^{-100t}\times 10^{-6}&t>0 \end{cases}=\begin{cases}0&t\leq 0\\2.5e^{-100t}\times 10^{-3}&t>0 \end{cases}\end{aligned}$
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686749630464-24e7eff3-b767-4208-a68e-fca369c44ace.png#averageHue=%23f9f7f5&clientId=ueb7e337d-6e82-4&from=paste&height=29&id=BuRmH&originHeight=44&originWidth=1134&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=14939&status=done&style=none&taskId=uc4646f53-3563-40ba-8d53-32c15475987&title=&width=756)

**Solution**本题主要运用公式即可$\int_0^{\infty}V_R(t)I_R(t)dt$:
$\begin{aligned}\int_0^{\infty}V_R(t)I_R(t)dt&=\int_0^{\infty}50e^{-50t}\times -2500e^{-50t}\times 0.02\times 10^{-6}dt\\&=2.5\times 10^{-3}\times (-\frac{1}{100}e^{-100t}\big|_0^{\infty})\\&=25\times 10^{-6}\\&=25uJ\end{aligned}$
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686749643735-208cec73-6a39-4914-b69d-50e4e3a68b66.png#averageHue=%23fbfaf9&clientId=ueb7e337d-6e82-4&from=paste&id=hAy8g&originHeight=104&originWidth=1147&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=19559&status=done&style=none&taskId=ud91af224-85b2-4f63-ba66-1523d495547&title=)

**Solution**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686913197882-bcaaee7e-79b7-464e-95d2-457886e52488.png#averageHue=%23ffffff&clientId=u151d6151-7883-4&from=paste&id=u9943b4d2&originHeight=317&originWidth=1263&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=32489&status=done&style=none&taskId=u6be68ef0-e00f-4b35-834f-585fb5fa5d3&title=)
可以发现，电容中储存的能量最终都流向了电阻。


## Capacitor IV
> **EECS16B sp23 HW1 P4**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685619761061-6c295b14-1cc4-4cf8-bc13-5c22b1e57273.png#averageHue=%23f9f7f5&clientId=u39443957-13ed-4&from=paste&id=ue4a7011c&originHeight=458&originWidth=1243&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=154830&status=done&style=none&taskId=ub9bc9f28-c59f-4862-9aed-b24bcbd0ef7&title=)

**Solution (a)**假设$v(t)$是电容两端的电压，$V$是电压源的电压则我们根据`RC`电路微分方程可知，$\frac{dv(t)}{dt}+\frac{v(t)}{RC}=\frac{V}{RC}$, 其解为$v(t)=V(1-e^{-\frac{t}{RC}}),t\geq 0$, 所以$\frac{dv(t)}{dt}=(-\frac{1}{RC})\cdot (-e^{-\frac{t}{RC}})=\frac{1}{RC}e^{-\frac{t}{RC}}$
于是根据能量公式: 
$\begin{aligned}w_s&=\int_0^{\infty}v(t)i(t)dt\\&=\int_0^{\infty}v(t)\cdot\frac{dv(t)}{dt}Cdt\\&=C\int_0^{\infty}V(1-e^{-\frac{t}{RC}})\frac{d(V(1-e^{-\frac{t}{RC}}))}{dt}dt\\&=C\int_0^{\infty}V(1-e^{-\frac{t}{RC}})\frac{V}{RC}e^{-\frac{t}{RC}}dt\\&=\frac{CV^2}{RC}\int_0^{\infty}(1-e^{-\frac{t}{RC}})e^{-\frac{t}{RC}}dt\\&=\frac{CV^2}{RC}(-RC)(-1+\frac{1}{2})\\&=\frac{1}{2}CV^2\end{aligned}$
**Solution (b)**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686731890760-4d6fd9ba-ee58-48af-84b3-de964acae77a.png#averageHue=%23ffffff&clientId=u15bb439c-c178-4&from=paste&id=u64196875&originHeight=702&originWidth=1794&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=107953&status=done&style=none&taskId=ufe126274-4e7f-4b0f-83ad-8784a640ef9&title=)
**Solution (c)**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686731901062-8bc54a4d-6801-48ce-874f-70dfbf180e78.png#averageHue=%23ffffff&clientId=u15bb439c-c178-4&from=paste&id=u853b664c&originHeight=126&originWidth=1783&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=34759&status=done&style=none&taskId=u7eb5e29d-0586-4380-b44d-3ea5fad3531&title=)
**Solution (d)**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1686731907827-a32c79b1-8b27-41c7-93cb-5c7539c0af56.png#averageHue=%23ffffff&clientId=u15bb439c-c178-4&from=paste&id=u8f1fbd4a&originHeight=375&originWidth=1763&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=123490&status=done&style=none&taskId=uc05d5a7e-0507-4538-a980-5bc4aed9030&title=)


# Inductors
## Definition
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687960443414-7f8d8ced-72b7-41aa-831c-b639373df1fd.png#averageHue=%23f6f5f4&clientId=u0ead45db-6bec-4&from=paste&id=u5c02dcfc&originHeight=799&originWidth=1840&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=256273&status=done&style=none&taskId=u2ecd73ff-fc99-4d9f-bed8-126e4494e50&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687166563753-da8c5cdf-ecff-45d7-871f-ce218e1f692f.png#averageHue=%23fcfbfb&clientId=ucdc41a13-bb4e-4&from=paste&id=ub0573c43&originHeight=676&originWidth=1391&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=91107&status=done&style=none&taskId=u8d02276f-12ba-413a-94b0-4223c45ecfc&title=)
> 🔔: 这里要注意$I_{L}$不会突变，因为如果$I_L$突变，也就是说$\frac{dI_L(t)}{dt}\to \infty$, 那么$V_L(t)\to \infty$, 这也是不符合实际的。


## Physics Behind
> 电容因为电荷的正负极会产生电场$\vec{E}$, 电场能够储存电容的能量。
> 电导因为有电流流经会产生电磁场$\vec{B}$，磁场能够储存电导的能量。
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687168037430-4f01c150-c532-4b4b-8b03-5c8f537fc3d9.png#averageHue=%23f7f6f4&clientId=ucdc41a13-bb4e-4&from=paste&id=u9d426ada&originHeight=736&originWidth=1386&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=205693&status=done&style=none&taskId=u1f5530c8-8c1c-4e4c-bf46-0af9fc8c383&title=)



## Magnetic Flux
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687960520516-357f814d-85fe-49df-a4ba-86533ae7b66b.png#averageHue=%23f5f3f2&clientId=u0ead45db-6bec-4&from=paste&id=u281f1d41&originHeight=962&originWidth=1853&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=520226&status=done&style=none&taskId=u249fefae-1234-472a-9daa-0b26ccb007c&title=)


## Stored Energy
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687238701507-d38fa745-1068-4a36-aba1-55fd83c8cfe8.png#averageHue=%237795c5&clientId=ude6e3a59-bf7d-4&from=paste&id=u30a4dc00&originHeight=364&originWidth=1647&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=49451&status=done&style=none&taskId=ue0082cb3-c45b-425c-b3bf-4e6055854a6&title=)

**Proof**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687238782158-f89ebd1f-c934-4d2c-ab1c-8733475d6ddc.png#averageHue=%23fdfcfc&clientId=ude6e3a59-bf7d-4&from=paste&id=u5c4e2b74&originHeight=651&originWidth=1662&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=83036&status=done&style=none&taskId=u725a8cb5-8bd4-4998-b593-210ca95fb3b&title=)



# Mutual Inductance
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687239008324-afd07fee-ed51-42c8-a72b-1698026525c9.png#averageHue=%23e8e8fc&clientId=ude6e3a59-bf7d-4&from=paste&id=u5de7c8a0&originHeight=489&originWidth=1476&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=76489&status=done&style=none&taskId=u8603ba1b-f605-48af-9a2c-28aaf65092b&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687239015065-ec1c4426-fd22-4a80-93d1-734a022db394.png#averageHue=%23eaeafd&clientId=ude6e3a59-bf7d-4&from=paste&id=u83e53250&originHeight=865&originWidth=1488&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=106197&status=done&style=none&taskId=uf75a249c-5d9b-469a-9917-0a3f808ee34&title=)
> **总的来说，我们有:**
> $\begin{aligned}& v_1(t)=L_1 \frac{\mathrm{d} i_1}{\mathrm{~d} t} \pm M \frac{\mathrm{d} i_2}{\mathrm{~d} t} \\& v_2(t)= \pm M \frac{\mathrm{d} i_1}{\mathrm{~d} t}+L_2 \frac{\mathrm{d} i_2}{\mathrm{~d} t}\end{aligned}$

**Proof**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687239446925-e4fbcbbe-010b-4383-9f6e-a1e0c50c9ab8.png#averageHue=%23faf9f8&clientId=ude6e3a59-bf7d-4&from=paste&id=oxsqY&originHeight=1067&originWidth=1523&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=257954&status=done&style=none&taskId=ud1aaba8d-cb3e-4891-809b-9768fc2ce62&title=)

# Inductor Equivalence
## Series Equivalence
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687221520051-fa1edf7b-aca0-4efd-8596-67c6311d927c.png#averageHue=%23fcfcfc&clientId=ude6e3a59-bf7d-4&from=paste&id=u5be4689a&originHeight=825&originWidth=1756&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=62050&status=done&style=none&taskId=u39414be6-7d39-4980-8587-d462aa19fe6&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687221524594-c5007933-632e-41e8-a919-2302fa3b644e.png#averageHue=%23fcfbfb&clientId=ude6e3a59-bf7d-4&from=paste&id=ua0553f39&originHeight=634&originWidth=1830&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=104879&status=done&style=none&taskId=u1da71194-2cf2-46ac-b680-b2cd5c9004a&title=)




## Parallel Equivalence
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687221532474-40c3ad19-d838-46d2-84e0-772ab884de87.png#averageHue=%23fbfbfb&clientId=ude6e3a59-bf7d-4&from=paste&id=u2fd2af10&originHeight=817&originWidth=1792&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=62088&status=done&style=none&taskId=u7bc07bcf-3ed5-4a1d-8751-bea550111aa&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687221536152-a72efb9d-e148-4483-a5f7-b41ccd05b7f0.png#averageHue=%23fcfbfb&clientId=ude6e3a59-bf7d-4&from=paste&id=ue02eacca&originHeight=802&originWidth=1751&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=123507&status=done&style=none&taskId=ubbf751a4-a54d-4c3a-aa40-bebd6b710ec&title=)



## RL Circuit
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687486771416-cd8a24a7-fff5-41c5-8a9d-4ff2137d3af3.png#averageHue=%23fcfcfb&clientId=u89c8f2c7-07ec-4&from=paste&id=u3f0c82af&originHeight=413&originWidth=1354&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=37631&status=done&style=none&taskId=uda99947d-110b-4b72-b8db-6cb29f89ab5&title=)
> $\begin{aligned}V_R(t) & =V_S-V_L(t) \\R I_L(t) & =V_S-L \frac{\mathrm{d}}{\mathrm{d} t} I_L(t)\\\frac{\mathrm{d}}{\mathrm{d} t} I_L(t)&=-\frac{R}{L} I_L(t)+\frac{V_S}{L}\\
I_L(t) &=-\frac{V_S}{R} \mathrm{e}^{-\frac{R}{L} t}+\frac{V_S}{R} \\
&=\frac{V_S}{R}\left(1-\mathrm{e}^{-\frac{R}{L} t}\right)\\V_L(t)&=V_S \mathrm{e}^{-\frac{R}{L} t}
\end{aligned}$
> 其中$\frac{L}{R}$的单位是$s$, 决定了时间轴上的`Time Scale`。
> 假设 $R=500 \Omega, L=1 \mathrm{mH}, V_S=5 \mathrm{~V}$, 我们有$\tau=\frac{L}{R}=0.2\times 10^6s=2us$, 于是:
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687487005646-a8232564-0146-415b-b0b7-1cc30e6ed58c.png#averageHue=%23fdfcfb&clientId=u89c8f2c7-07ec-4&from=paste&id=uf6639e29&originHeight=1139&originWidth=1048&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=107494&status=done&style=none&taskId=ucb227648-e6c4-411e-9dbe-552544efcfb&title=)


# Inductor Analysis
## Charging Process
> **Disc 02B Sp23 P1(a)**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687932064146-da90ad4c-06e3-4e9e-a7e3-5af33406937f.png#averageHue=%23fafaf9&clientId=u4d42642c-10ca-4&from=paste&id=u8c2706b1&originHeight=792&originWidth=1802&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=144156&status=done&style=none&taskId=uf2671f12-cb46-43a1-9efc-274e3a17eab&title=)
> 1. 假设$I_L(0)=0A$, 两端有一个恒定电压源$V_S$，则$\frac{dI_L(t)}{dt}\cdot L=V_S$, 两边积分得到$\int_0^{t}dI_L(t)=\int_0^{t}\frac{V_S}{L}$, 于是$I_L(t)-I_L(0)=V_S$, 所以$I_L(t)=\frac{V_S t}{L}$。



## Power Properties
> **HW03 Sp23 P2**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687875987053-54cb5d49-7484-4d65-a93d-b8df88e6d9b6.png#averageHue=%23f5f4f2&clientId=ubff626a2-0f58-4&from=paste&id=u83c0ee61&originHeight=153&originWidth=1517&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=62986&status=done&style=none&taskId=ud9376546-bf68-4885-90d7-bc42d91a506&title=)

**Voltage**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687876015302-716d8b5c-3c8b-4fc8-b49b-b0c75a15d3f3.png#averageHue=%23fefefe&clientId=ubff626a2-0f58-4&from=paste&id=u69965584&originHeight=637&originWidth=1454&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=56981&status=done&style=none&taskId=uc494a8a8-4425-4acc-acfd-ea9007cf29f&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687876036344-42428a05-cc95-4e84-a5db-eab3a6e95174.png#averageHue=%23fefefe&clientId=ubff626a2-0f58-4&from=paste&id=ue9a4caa9&originHeight=638&originWidth=1535&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=66219&status=done&style=none&taskId=ua16371b4-488d-4bc5-86fd-8b96d5d1dcc&title=)
**Power**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687876046205-fee7b414-e203-4003-8ead-3e7c753db14d.png#averageHue=%23ffffff&clientId=ubff626a2-0f58-4&from=paste&id=ufe1b2206&originHeight=88&originWidth=1576&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=24636&status=done&style=none&taskId=u0564f4a6-ebbe-49d3-8a4c-8e6b6165629&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687876050297-fdfb3416-8bb0-4df0-b64d-8fc6bccd41b0.png#averageHue=%23fefefe&clientId=ubff626a2-0f58-4&from=paste&id=udbb140ad&originHeight=576&originWidth=1473&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=47851&status=done&style=none&taskId=u45d6b633-e619-4348-9de1-8326cdf169f&title=)
**Stored Energy**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687876058296-632d35d9-02c1-453b-911c-5d9556fae481.png#averageHue=%23fefefe&clientId=ubff626a2-0f58-4&from=paste&id=u5052f04a&originHeight=725&originWidth=1542&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=71581&status=done&style=none&taskId=ue9267a17-ae13-4f7b-b73e-9fc1ca12ef0&title=)


## Inductance Extremities
> **HW03 Sp23 P3**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687876319689-98b2bbd3-922b-4d22-a731-7a8d42265f18.png#averageHue=%23f8f7f6&clientId=ubff626a2-0f58-4&from=paste&id=ua795ad8c&originHeight=133&originWidth=1595&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=36569&status=done&style=none&taskId=ub1762b90-bbfd-45e3-b82d-abdd068bc16&title=)
> `Open Circuit`对应的条件是$I_L(t)=0$, 因为$V_L(t)=\frac{dI_L(t)}{dt}\times L$, 所以:
> $\frac{V_L(t)}{L}=\frac{dI_L(t)}{dt}$, 两边取积分得到$I_L(t)-I_L(t_0)=\frac{1}{L}\int_{t_0}^tV_L(\tau)d\tau$, 因为$I_L(t)=I_L(t_0)=0$
> 所以$\frac{1}{L}\int_{t_0}^tV_L(\tau)d\tau=0$, 因为$\int_{t_0}^tV_L(\tau)d\tau\neq 0$, 所以$L\to \infty$。
> `Short Circuit`对应的条件是$V_L(t)=0$, 因为$\frac{dI_L(t)}{dt}\neq 0$, 所以$L=0$。



## Mutual Inductance
> **HW03 Sp23 P4**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687911308121-c196e4eb-937e-4cb6-a6ae-112e0bcb466f.png#averageHue=%23f5f4f3&clientId=udb62d68f-91e9-4&from=paste&id=u47637abd&originHeight=195&originWidth=1773&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=77271&status=done&style=none&taskId=ua5e54788-8f20-4f71-9016-4fc6b54c6d7&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687911619148-67352879-26e9-4ef6-9368-a4e0f95c253f.png#averageHue=%23ffffff&clientId=udb62d68f-91e9-4&from=paste&id=uacc2f3e0&originHeight=576&originWidth=1541&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=100720&status=done&style=none&taskId=ucb89e384-3a8e-4258-876c-8fed71bd087&title=)






# OpAmp
## Op-Amp Stability Part 1
> **HW02 Fa21 P5**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687098509063-3ae58aee-147f-4297-ae14-79b18c57c059.png#averageHue=%23fbfafa&clientId=uca3e2ef7-fd71-4&from=paste&id=u34f3ed76&originHeight=1244&originWidth=1162&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=157093&status=done&style=none&taskId=u26f7b70a-0ea2-474f-848d-b2a163df7be&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687098520237-a371c47b-adbb-474c-bec7-59c073ef5c7a.png#averageHue=%23f8f6f4&clientId=uca3e2ef7-fd71-4&from=paste&id=u8a9ea242&originHeight=1335&originWidth=1169&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=414768&status=done&style=none&taskId=ub4526836-c178-4ce2-b84a-10bb778beca&title=)

**(a) OpAmp Circuit in Detail**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687151382162-cb76f681-43ad-44bb-b6f8-502d46d80680.png#averageHue=%23f9f8f8&clientId=u06c9345a-f28c-4&from=paste&id=u3e95932f&originHeight=915&originWidth=1919&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=70362&status=done&style=none&taskId=ua64e26ca-f516-4b31-96f7-ada37d08577&title=)
**(b) OpAmp Differential Equation - Negative Feedback Loop**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687152104427-be0067f9-eac2-4921-9598-501443d0dbb2.png#averageHue=%23ffffff&clientId=u06c9345a-f28c-4&from=paste&id=u0f8321eb&originHeight=235&originWidth=1941&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=30134&status=done&style=none&taskId=u06ba3111-f81c-48ca-b0cb-29d38cf8fdc&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687152114612-994e7a17-8e13-4757-9434-f3fc02e882c9.png#averageHue=%23ffffff&clientId=u06c9345a-f28c-4&from=paste&id=ud748fb8f&originHeight=1217&originWidth=2000&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=144885&status=done&style=none&taskId=u3aff416f-6504-478f-8878-171b2905f16&title=)
**(c) OpAmp Differential Equation - Positive Feedback Loop**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687152908951-d8f10108-860c-435a-9090-702db023290b.png#averageHue=%23ffffff&clientId=u06c9345a-f28c-4&from=paste&id=ud8bc26de&originHeight=835&originWidth=1494&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=90422&status=done&style=none&taskId=u7699c7be-eebb-40ab-b7d1-c126d39230e&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687152916871-bcd3b57c-8d86-4e29-b185-f96f4d8ea7b3.png#averageHue=%23ffffff&clientId=u06c9345a-f28c-4&from=paste&id=u7f0a2908&originHeight=662&originWidth=1446&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=136832&status=done&style=none&taskId=u54a49b98-c55a-4b1d-a7e4-77add7b4c9a&title=)
**(d) Limiting Behaviors**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687153457164-d2fadafd-865d-44d1-8cb8-1677845aee7e.png#averageHue=%23ffffff&clientId=u06c9345a-f28c-4&from=paste&id=ub02c398e&originHeight=320&originWidth=1429&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=38298&status=done&style=none&taskId=u2a3d5136-a0ab-494c-9911-1eb20fe815f&title=)
**(e) Vector Differential Equations**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687154005352-c2c6348b-1496-49b1-9944-76ce7e186ccb.png#averageHue=%23ffffff&clientId=u06c9345a-f28c-4&from=paste&id=ub288a3b3&originHeight=407&originWidth=1476&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=41669&status=done&style=none&taskId=ufa4708fb-412b-415a-9943-ce433f8938e&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687154013178-4743b486-e6d7-4393-9f8b-7a21c74e99ba.png#averageHue=%23ffffff&clientId=u06c9345a-f28c-4&from=paste&id=uce7a2cf3&originHeight=833&originWidth=1490&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=97908&status=done&style=none&taskId=u3469d1d2-79e4-463c-bbf9-1a87127de94&title=)
> **本题要注意:**
> 在画一个`Detailed OpAmp`电路的时候，左侧的`Terminal`和`OpAmp`本体之间永远是`Open Circuit`, 无论有没有`Feedback Loop`, 左侧的$V_+$和$V_-$端都是裸露在电路之外的。如下图中的的绿色端，电流都是零，流经`Feeback Loop`的电流也是零。
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687153395994-447e6965-3f27-431e-97bb-e4b2a58dd42d.png#averageHue=%23fafafa&clientId=u06c9345a-f28c-4&from=paste&height=139&id=uc81c7923&originHeight=209&originWidth=978&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=35932&status=done&style=none&taskId=ueb3a2e67-d63c-4a6c-b380-d0bcf35ea54&title=&width=652)
> 即$(a)$中的输入端是$V_{in}-V_{out}$, $(b)$中的输入端是$V_{out}-V_{in}$。


## Op-Amp Stability Part 2
> **HW03 Fa21 P6**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687309096897-bb539c7d-9bbf-412d-9b01-8cff8efa1ac3.png#averageHue=%23f3f1ef&clientId=u515e199f-53e0-4&from=paste&id=u550b178c&originHeight=1129&originWidth=1648&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=467573&status=done&style=none&taskId=u61e3843b-61f0-4b6b-b4be-c2eeb94ea20&title=)

**(a) Eigenvalues**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687356911721-53bdcaf4-dbc5-4982-8b89-0fa6121ac5e7.png#averageHue=%23ffffff&clientId=u515e199f-53e0-4&from=paste&id=u89d67286&originHeight=930&originWidth=1402&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=120690&status=done&style=none&taskId=u81bf5610-d288-4426-91f8-0692483bc54&title=)
**(b) Approximation**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687393375244-96d395b4-96cb-478e-ae9a-dec9df535cde.png#averageHue=%23ffffff&clientId=u497894ac-0f06-4&from=paste&id=uda3fd1dc&originHeight=1047&originWidth=1349&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=136047&status=done&style=none&taskId=ue19ebcb7-f698-45fc-b689-7480ba0ed94&title=)



# Summary
## Capacitors&Inductors
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687958873762-7ac2e650-fd9f-427a-8962-caf0cd8f6a8b.png#averageHue=%23f7f7f6&clientId=u7aad071b-c851-4&from=paste&id=u7f40bffe&originHeight=948&originWidth=1791&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=182649&status=done&style=none&taskId=u0d6acce0-be1a-46ac-a77f-940360a8cf7&title=)

