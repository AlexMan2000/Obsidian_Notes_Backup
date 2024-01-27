# Series Resonance Circuits
## Resonant Frequency
> 对于这个电路来说:
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688193704850-efff295a-1ce6-4799-a6af-8378fc9c28ac.png#averageHue=%23f9f9f9&clientId=u5546b544-7fd3-4&from=paste&id=u5e8e209e&originHeight=305&originWidth=1266&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=30289&status=done&style=none&taskId=uec8aeffb-bf3b-4f04-863b-09092d546aa&title=)
> 我们有`Total Impedence`:
> $Z(f)=jwL+R+\frac{1}{jwC}=jwL+R-\frac{j}{wC}=j2\pi fL+R-\frac{j}{2\pi fC}$
> 我们**定义**`**Resonant Frequency**`$f_0$为使得`Total Impendence`$Z(f)$为`Purely Resistive`(只含有实数项，即$R$)时候的频率。换句话说，就是使得`Total Reactance`为零的频率。
> 我们零$jwL=\frac{j}{wC}$得到$w=\frac{1}{\sqrt{LC}}$。因为$2\pi f_0=w$, 所以$f_0=\frac{1}{2\pi \sqrt{LC}}$，就是我们的共振频率。



## Quality Factor
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688194293812-2a60e269-2834-44cb-a233-5f1c44497eb3.png#averageHue=%23f1f1f1&clientId=u5546b544-7fd3-4&from=paste&id=ub39b501d&originHeight=780&originWidth=1239&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=107704&status=done&style=none&taskId=ub9bd8b10-1500-4f90-89c8-14fc3152c93&title=)


## Series Resonant Bandpass Filter
> 还是这个电路:
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688193704850-efff295a-1ce6-4799-a6af-8378fc9c28ac.png#averageHue=%23f9f9f9&clientId=u5546b544-7fd3-4&from=paste&id=eFir8&originHeight=305&originWidth=1266&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=30289&status=done&style=none&taskId=uec8aeffb-bf3b-4f04-863b-09092d546aa&title=)
> 我们有$\widetilde{I}=\frac{\widetilde{V_s}}{Z(f)}=\frac{\widetilde{V_s}}{R\left[1+j Q_s\left(\frac{f}{f_0}-\frac{f_0}{f}\right)\right]}$, $\widetilde{V_{R}}=\widetilde{I}R=\frac{V_s}{1+j Q_s\left(\frac{f}{f_0}-\frac{f_0}{f}\right)}$
> 所以$\frac{\widetilde{V_R}}{\widetilde{V_s}}=\widetilde{I}R=\frac{1}{1+j Q_s\left(\frac{f}{f_0}-\frac{f_0}{f}\right)}$, 我们画$\frac{f}{f_0}-\frac{|\widetilde{V_R}|}{|\widetilde{V_s}|}$图像如下:
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688194487675-abf2c16e-4a47-4db0-8c6e-3a17bf370534.png#averageHue=%23f5f5f5&clientId=u5546b544-7fd3-4&from=paste&height=458&id=uf5084e0d&originHeight=687&originWidth=1191&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=99259&status=done&style=none&taskId=u14cce469-c405-4989-bc7e-b17144f1314&title=&width=794)
> 可以看到，在`Resonant Frequency`的时候输出的电压值最大。




# Parallel Resonance Circuits
## Circuit
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688194748269-b4988323-6fe6-4889-81e8-0605fd7c6041.png#averageHue=%23f7f7f7&clientId=uab85e16e-ad7e-4&from=paste&id=u0ccdb8b0&originHeight=304&originWidth=1149&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=32990&status=done&style=none&taskId=ua41beb5c-7c0e-4c52-b150-df2a730cd01&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688194800138-5aa390ef-a709-45c2-8f18-cade2b4fb664.png#averageHue=%23f1f1f1&clientId=uab85e16e-ad7e-4&from=paste&id=ucecb4903&originHeight=544&originWidth=1318&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=89193&status=done&style=none&taskId=ufc0911ce-5c86-402f-a77b-0e2c6d52acf&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688194809685-ebd6fcad-d6ef-4203-8803-a80e30aaf9b2.png#averageHue=%23f4f4f4&clientId=uab85e16e-ad7e-4&from=paste&id=uf7a0330c&originHeight=1226&originWidth=1639&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=212374&status=done&style=none&taskId=u75963a59-369d-4d31-9e18-70b84c0095a&title=)



## Working Example
### Example 1: Analysis
> **Hw05 Fa21 P7**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688194865162-006d420f-0c30-41ee-8c58-de66db11f123.png#averageHue=%23f9f8f7&clientId=uab85e16e-ad7e-4&from=paste&id=u86ad1a8c&originHeight=1725&originWidth=1926&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=355774&status=done&style=none&taskId=ub0b9fbbb-7a44-4937-b202-839990e9e89&title=)

**(a)**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688194896509-270e814a-de22-43a8-b1d1-8364dd706bae.png#averageHue=%23ffffff&clientId=uab85e16e-ad7e-4&from=paste&id=u74d1470a&originHeight=269&originWidth=1314&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=31128&status=done&style=none&taskId=u77e977fc-e1ec-48bf-8c18-545eab6ee10&title=)
**(b) Figure out Input Phasor**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688194904440-7a462ce8-69f2-4df5-b3f1-f70e64502e44.png#averageHue=%23ffffff&clientId=uab85e16e-ad7e-4&from=paste&id=u0cdd573c&originHeight=341&originWidth=1369&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=27098&status=done&style=none&taskId=ue05b85fe-92f0-4401-ae5c-1ea6355e6e1&title=)
**(c) Resonant Analysis ⭐⭐⭐⭐⭐**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688194961857-4ad30dc7-6b35-414c-ab66-60a3b4cf30b7.png#averageHue=%23fdfdfd&clientId=uab85e16e-ad7e-4&from=paste&id=ud360a582&originHeight=1322&originWidth=1500&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=102925&status=done&style=none&taskId=ucfc7ce7b-697b-4ebb-85b9-0139536f891&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688209413643-32993b62-66cf-4651-ad45-8175a7016513.png#averageHue=%23ffffff&clientId=ue802abbd-2c2f-4&from=paste&id=u64ff6bea&originHeight=625&originWidth=1358&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=139628&status=done&style=none&taskId=u3bc99ee5-af43-478c-b4b9-d5a4510c3e4&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688209427380-abc5a1c2-1396-4773-bb25-39d06cf3cef7.png#averageHue=%23fefefe&clientId=ue802abbd-2c2f-4&from=paste&id=ufa37fcdc&originHeight=200&originWidth=1339&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=53695&status=done&style=none&taskId=u695c0bd3-94fc-47a0-b907-624aa85ff56&title=)
**(d) Convert to time domain**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688209612532-2eaa899c-f568-4b05-a68a-3e635d003dc8.png#averageHue=%23ffffff&clientId=ue802abbd-2c2f-4&from=paste&height=104&id=ua2c63853&originHeight=156&originWidth=1415&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=16328&status=done&style=none&taskId=u97f36706-c16d-431d-92bb-99d9eb67a75&title=&width=943.3333333333334)
> 在`Phasor Domain`进行电路分析时，我们可以使用`Circuit Equivalent`, 但是有时候会得到$\infty$的等效结果，这也正常，因为我们的`Impedence`是复数。



### Example 2: Find resonant frequency
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688219832728-feec7f9a-4097-401e-808a-c995520b8d2c.png#averageHue=%23fbfafa&clientId=u83449d12-016e-4&from=paste&id=u2ddb411c&originHeight=729&originWidth=1732&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=78757&status=done&style=none&taskId=uef062499-76b0-4935-9b92-7bd70a82f45&title=)

**Solution**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688219840835-8ee09854-8cfe-426d-a677-ab2c953c3353.png#averageHue=%23ffffff&clientId=u83449d12-016e-4&from=paste&id=u308655cc&originHeight=705&originWidth=1729&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=83123&status=done&style=none&taskId=u6ec467b4-e5b0-4834-bcd5-de08ea73cc5&title=)

# Resources
> Electrical Engineering Principles 6ed Ch6.6/Ch6.7

