[Bootstrap CMU.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1664945656870-c52da945-fd5b-4381-927e-d59ce7b96b36.pdf)
[Bootstrap NTU.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1664945656722-33392071-1c80-4eb5-b12a-30016d797a58.pdf)
# 0 引言
## 0.1 Some Notations
:::info

- : 样本点(随机变量)
- : realization of ， 常数
- 总体分布CDF函数
- ，的`ECDF`
- ，作为的一个`Consistent Estimator`
- , is samples from 
:::

## 0.2 基本理解
> 我们在`Bootstrap`框架下考虑一个估算`Variability of location estimates`的问题。对于样本均值，我们使用`CLT`就可以为期创建一个`Confidence Interval`，而`Bootstrap`方法可以创建任何统计量的`Confidence Interval`, 只要我们有一台高性能计算机，并且使用`Simulation`算法即可。
> 如果我们观测到了一系列的数据样本作为随机变量序列的一个`Realization`，很自然地我们会想求(写作)的`Variance`或者`Sampling Distribution`。（因为是样本集的函数，所以也是一个随机变量，有自己的方差和样本分布）。而的`Sampling Distribution`是被和决定的。如果我们想要知道这个`Sampling Distribution`, 那么我们需要解决下面两个问题:
> 1. 我们不知道的底层分布。
> 2. 即便我们知道, 可能是一个关于的很复杂的函数表达式。
> 
我们有两种情况需要考虑：
> 1. **假设我们知道**:
> 
那么我们如何找到的概率分布情况且不用计算复杂的函数表达式呢? `Compute Simulation`可以帮助我们完成这个任务。我们可以**从已知的中生成**组大小为的样本数据，然后利用每一组样本计算。这样我们可以计算出来一系列的统计量，, 当很大的时候，他们构成的`**Empirical Distribution**`是对于**的**`**Distribution**`的一个很好的估计。
> 如果我们还想知道的`Standard Deviation`, 我们也可以通过计算的`Standard Deviation`得到一个不错的估计，只要足够大就行。
> 2. **实际情况是，很多情况下我们不知道:**
> 
在我们不知道时，我们可以转而使用来作为对的估计。而从之前的章节我们知道, 是一个离散的概率分布，它给每一个样本点分配了一个大小为的概率值。
> 于是我们可以**从的分布(这是我们从**`**Observed Data**`**中可以知道的)中生成**组大小为的样本数据。此时每份样本数据(大小为)都是通过从中进行**有放回**的抽样得到的。**这个过程被称为**`**Simulation**`**。**
> **然后:**
> 的`Standard Error`可以被: 是从中通过计算得来的。


> 如果我们有无限多的样本点，则是一个随机变量，且根据大数定律会无限接近于。我们找到和使得:
> 
> 但是实际上我们没有那么多样本数据:
> 1. In reality, is not known.
> 2. Even if is known, finding &is tricky.


## 0.3 简单示例
> 假设我们观测到两个样本点,  。我们想知道分布的均值是什么。
> 但是此时我们是不知道的，于是我们假设。同时我们知道, 于是取的概率均为。我们知道, 但是未知，所以我们只能使用`Bootstrap`方法从数据集抽样获得, 然后通过计算出, 我们如此重复次，得到一系列, 我们可以很快计算出他们的分布，称为`Bootstrap Distribution`。
> 但是我们也可以想见，如果过大的话，我们的计算就会变得非常的困难。在很多文献中，我们往往不会像上面那样简单的`Random Sampling with replacement`, 而是可能使用更加复杂高效的抽样方式。
> ![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1667122174053-25205636-a4f9-48b9-84eb-ceace00013fd.png#clientId=ua0818dea-55f6-4&from=paste&id=u852da3bb&originHeight=435&originWidth=1817&originalType=binary&ratio=1&rotation=0&showTitle=false&size=197060&status=done&style=shadow&taskId=u66e724db-ff57-4005-9ef9-4947c2fab57&title=)



# 1 BootStrap Procedure
## 1.1 Simulation
:::info
![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664849109679-c6b9b831-42f2-4fdc-a628-930066f3246a.png#clientId=uf4669c20-f3fd-4&errorMessage=unknown%20error&from=paste&id=ude984dc6&originHeight=1096&originWidth=1266&originalType=binary&ratio=1&rotation=0&showTitle=false&size=283524&status=error&style=none&taskId=u81b5decf-0699-40c3-a66d-e8078816d33&title=)
:::

## 1.2 Bootstrap详细步骤
> **我们假设观测到了的数据样本，且我们不知道这些数据的底层分布是什么。**
> **Step 1: Construct Empirical CDF**
> 我们使用来估计, 为每个数据点分配了一个大小为的概率值，我们可以称之为样本的经验分布函数。
> **Step 2: Resample**
> 从这个经验分布函数中有放回地抽取(可以重复)大小为的样本组。
> **Step 3: Caculate Statistics of Interest**
> 利用`Step 2`中的样本组计算统计量(`Statistic of Interest`, 比如`Mean`或者`Variance`) , 得到。
> **Step 4: Repeat Resample Process**
> 重复`Step 2`和`Step 3`次得到组`Resample`, 同时越大越好。一般而言，。最终我们得到。
> **Step 5: Construct Relative Frequency Histogram**
> 根据创建一个频率直方图，形成的分布就是一个对分布的一个较好的近似。



## 1.3 Algorithm
> 1. Input are given data.
> 2. Choose as batch的数量, 一般大于1000
> 3. Sample uniformly from (等价于从sample uniformly with replacement), 得到组
> 4. 计算
> 5. 找到的和quantile, 其中
> 6. ，最终, 其中的目的是在中找到一个使得




# 2 Bootstrap Estimation
## 2.1 思想
> 1. Real World, we have , , and 
> 2. Bootstrap World, we have , ,每个`Batch`一般来说是一个大小为的样本集。
> 3. **Replace by , by , where and are known.**
> 4. **Draw from , Resample from **
> 
![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1667122062839-1702277b-134d-4ad3-91d1-fa12ed5e76a0.png#clientId=ua0818dea-55f6-4&from=paste&id=u52ae6bf5&originHeight=995&originWidth=1842&originalType=binary&ratio=1&rotation=0&showTitle=false&size=251475&status=done&style=shadow&taskId=ud63175f0-7ee8-49af-ad69-1c36b43276e&title=)



## 2.2 Bootstrap Variance Estimation
:::info
![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664850083189-9943549c-4c8b-497b-b286-8f4ec3020a4f.png#clientId=uf4669c20-f3fd-4&errorMessage=unknown%20error&from=paste&id=uc501ebde&originHeight=1554&originWidth=2834&originalType=binary&ratio=1&rotation=0&showTitle=false&size=375569&status=error&style=shadow&taskId=u14605a2b-bcc6-473f-ac2b-118f0c5408a&title=)
:::


## 2.3 Bootstrap Median Estimation
> ![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664850161018-102f0735-76f0-480e-a2db-9a62e9c25f00.png#clientId=uf4669c20-f3fd-4&errorMessage=unknown%20error&from=paste&id=u63cdb19e&originHeight=1234&originWidth=2688&originalType=binary&ratio=1&rotation=0&showTitle=false&size=254369&status=error&style=shadow&taskId=u72d8affe-f5f3-4f96-9c5d-4eac2560c48&title=)![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664850171742-78273d5d-138a-4ae1-9434-f17ecb566df6.png#clientId=uf4669c20-f3fd-4&errorMessage=unknown%20error&from=paste&id=ufa58f3b0&originHeight=564&originWidth=2780&originalType=binary&ratio=1&rotation=0&showTitle=false&size=161693&status=error&style=shadow&taskId=u945f9de8-0fa2-4107-a0f4-a4effcc883d&title=)


## 2.4 Bootstrap Skewness Estimation
> ![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664850646200-7a505419-894e-4a75-9fd4-ef58fa23c25e.png#clientId=uf4669c20-f3fd-4&errorMessage=unknown%20error&from=paste&id=uc5ce9ce4&originHeight=285&originWidth=2827&originalType=binary&ratio=1&rotation=0&showTitle=false&size=164050&status=error&style=shadow&taskId=u9f400329-87c2-412e-8270-a8771d2e581&title=)![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664850655834-0b29c023-bc13-4c11-b254-490146ffa8bc.png#clientId=uf4669c20-f3fd-4&errorMessage=unknown%20error&from=paste&id=u90fbd4e0&originHeight=1073&originWidth=2829&originalType=binary&ratio=1&rotation=0&showTitle=false&size=471534&status=error&style=shadow&taskId=u904c56db-f5c0-430b-802b-15ea826cb80&title=)



# 3 Bootstrap Confidence Interval
[Bootstrap NTU.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1666942018955-6051a6d9-a5be-410c-8ac1-34afdd240ea3.pdf)
## 3.0 导言
> 本单元开始时中我们已经介绍了三种构建的方法，包括`CLT`法和`Hoeffding's Inequality`。本小节我们在`Bootstrap`的框架下再介绍几种方法。
> **Motivation:** Can you obtain a confidence interval for $\theta$? We can use CLT for mean, since it's easy. But what about CI for variance, quantile, covariance, etc. 



## 3.1 思想
> ![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664854280712-0d8106e0-191f-42e4-8366-f09670f48dd1.png#clientId=uf4669c20-f3fd-4&errorMessage=unknown%20error&from=paste&id=HQAAl&originHeight=1406&originWidth=2943&originalType=binary&ratio=1&rotation=0&showTitle=false&size=479293&status=error&style=shadow&taskId=u36881047-aae2-402d-85d5-82b41f6cf54&title=)![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664854295460-2d188fdc-740f-4d8e-86a6-af52450a4924.png#clientId=uf4669c20-f3fd-4&errorMessage=unknown%20error&from=paste&id=wLSkb&originHeight=1662&originWidth=3021&originalType=binary&ratio=1&rotation=0&showTitle=false&size=617359&status=error&style=shadow&taskId=u3897b23f-ea65-4c71-85ea-39f4255d47f&title=)![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664854305268-6f5ca628-d0c0-4028-bb70-49a8f2fd5c07.png#clientId=uf4669c20-f3fd-4&errorMessage=unknown%20error&from=paste&id=nbYgR&originHeight=477&originWidth=2856&originalType=binary&ratio=1&rotation=0&showTitle=false&size=99250&status=error&style=shadow&taskId=ub3270b20-27a4-459d-861a-54995ea182c&title=)


## 3.2 三种BootStrap构建方法
> 下面三种方法都是`Confidence Interval`的`Consistent Estimators`。 

### The Normal Interval
> 假设我们的统计量是, 用于估计总体均值, 则我们的`Confidence Interval`形如:
> , 其中是对于的`Bootstrap`估计。但是我们假设是服从正太分布的。

 
### Pivotal Intervals
> 假设我们要估计一个参数$\theta=T(F)$, 估计量是, 我们可以定义一个`Pivot`: 。让来表示我们通过次`Bootstrap`抽样获得的的复制。
> **我们令表示的**`**CDF**`**: **![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664851700694-0b3faaa6-ff69-48bc-944b-652430e2f190.png#clientId=uf4669c20-f3fd-4&errorMessage=unknown%20error&from=paste&id=u7d2d5adb&originHeight=232&originWidth=2846&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36285&status=error&style=shadow&taskId=u538906d4-b5af-47ae-8e5b-6749180624a&title=)![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664851694677-1a466834-5abc-4653-813a-02127a05c793.png#clientId=uf4669c20-f3fd-4&errorMessage=unknown%20error&from=paste&id=u1e151c9a&originHeight=410&originWidth=2823&originalType=binary&ratio=1&rotation=0&showTitle=false&size=94097&status=error&style=shadow&taskId=ue91f9617-8d52-47e2-854e-9769a08bfbb&title=)
> **所以我们有:**
> ![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664851712645-9c93554e-e9ec-4be1-95ef-af4c81374361.png#clientId=uf4669c20-f3fd-4&errorMessage=unknown%20error&from=paste&id=u53072e20&originHeight=1128&originWidth=2888&originalType=binary&ratio=1&rotation=0&showTitle=false&size=234153&status=error&style=shadow&taskId=uca8d80aa-2593-4317-9313-5fa117b9028&title=)
> 所以就是的`Confidence Interval`。不幸的是，和都取决于未知的分布函数和，我们考虑使用`Bootstrap`估计:
> ![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664853276115-7225bb0d-8f36-45f6-95f3-855ca0418345.png#clientId=uf4669c20-f3fd-4&errorMessage=unknown%20error&from=paste&id=uab196c3a&originHeight=280&originWidth=2824&originalType=binary&ratio=1&rotation=0&showTitle=false&size=52188&status=error&style=shadow&taskId=u7a041f85-0160-42f0-abc3-12c9e178ba3&title=)
> 其中。让表示的sample quantile，让表示。注意。则的`Confidence Interval`是:
> ![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664853702566-58c059f3-1805-49e6-b1f2-b36a5fd237fc.png#clientId=uf4669c20-f3fd-4&errorMessage=unknown%20error&from=paste&id=ue6561a96&originHeight=408&originWidth=2661&originalType=binary&ratio=1&rotation=0&showTitle=false&size=112056&status=error&style=shadow&taskId=ub672673a-384a-4a16-ad31-7a4c7abd961&title=)![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664853710359-6093c295-278e-4f03-8814-78fcc69aa112.png#clientId=uf4669c20-f3fd-4&errorMessage=unknown%20error&from=paste&id=u62230936&originHeight=411&originWidth=2884&originalType=binary&ratio=1&rotation=0&showTitle=false&size=119034&status=error&style=shadow&taskId=u26604e9f-23b4-4873-8290-65c7506a6ed&title=)
> 这里有几个注意点:
> 1. `Empirical Quantile`, 就是, 这个`Empirical Quantile`在足够大的时候是可以称为一个对`Quantile`准确估计。

> ![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664853749377-d003553c-a64d-4cac-8991-4fbca7da0705.png#clientId=uf4669c20-f3fd-4&errorMessage=unknown%20error&from=paste&id=u56942d4b&originHeight=557&originWidth=2760&originalType=binary&ratio=1&rotation=0&showTitle=false&size=140795&status=error&style=shadow&taskId=u4237f4cb-7dea-4797-9374-e4b10e71191&title=)




### Percentile Interval
> ![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664853806863-e5db9e37-9f5f-4f03-bea8-275c042d3011.png#clientId=uf4669c20-f3fd-4&errorMessage=unknown%20error&from=paste&id=u5be39f2f&originHeight=420&originWidth=2828&originalType=binary&ratio=1&rotation=0&showTitle=false&size=110924&status=error&style=shadow&taskId=u25000b1a-2f8a-45f1-92fa-69643fdf8d9&title=)

**Justification**![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664853834919-8570ff68-0ca4-42d1-a155-b1130fc71819.png#clientId=uf4669c20-f3fd-4&errorMessage=unknown%20error&from=paste&id=u257ed5b1&originHeight=1804&originWidth=2818&originalType=binary&ratio=1&rotation=0&showTitle=false&size=789778&status=error&style=shadow&taskId=ua1417d0c-958d-4d02-9d9e-42648856da9&title=)



## 3.3 Bootstrap应用
### 3.3.1 One-dimensonal Data(Mean)
> ![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664955978794-a2f85d63-99b1-498c-8088-4050250ec3b4.png#clientId=u1a23eaab-5a0c-4&errorMessage=unknown%20error&from=paste&id=uc5478d72&originHeight=458&originWidth=2266&originalType=binary&ratio=1&rotation=0&showTitle=false&size=147313&status=error&style=shadow&taskId=u22adc702-568f-45c2-888a-bc2564e1767&title=)![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664955984915-984588ec-1e8b-4802-8638-945a4a4defbf.png#clientId=u1a23eaab-5a0c-4&errorMessage=unknown%20error&from=paste&id=u79aa940e&originHeight=672&originWidth=2275&originalType=binary&ratio=1&rotation=0&showTitle=false&size=215295&status=error&style=none&taskId=u5bd58d9e-e1bb-44b7-bdd2-c1493959f8b&title=)![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664955998169-f7ef4f77-c0d2-434c-b989-6840125bfc18.png#clientId=u1a23eaab-5a0c-4&errorMessage=unknown%20error&from=paste&id=u46fc0ccc&originHeight=1542&originWidth=2272&originalType=binary&ratio=1&rotation=0&showTitle=false&size=177721&status=error&style=none&taskId=ub6578f3f-2c25-42a1-8b8f-f5bb15dfa44&title=)



### 3.3.2 One-dimensional Difference Data(Median Difference)
> ![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664953815504-85d56777-7007-4067-8c12-9e6eebbf2b7a.png#clientId=u44f8312d-4d87-4&errorMessage=unknown%20error&from=paste&id=ud3e4a00d&originHeight=1390&originWidth=1729&originalType=binary&ratio=1&rotation=0&showTitle=false&size=431804&status=error&style=shadow&taskId=ua4086e1e-b77b-4b7b-90de-ab9d462af6a&title=)



### 3.3.3 One-dimensional Data(Mean Difference)
> 




### 3.3.4 Two-dimensional Data (Correlation)
> ![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664955917770-d5ce9464-6f15-4234-9b11-05bd0226269d.png#clientId=u1a23eaab-5a0c-4&errorMessage=unknown%20error&from=paste&id=uc387b3c1&originHeight=911&originWidth=2315&originalType=binary&ratio=1&rotation=0&showTitle=false&size=357072&status=error&style=shadow&taskId=uf04a7488-93d3-4961-84de-d9c3e4c2d83&title=)![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664955920363-da55005a-34b0-4410-93d9-675187aca1f1.png#clientId=u1a23eaab-5a0c-4&errorMessage=unknown%20error&from=paste&id=u977dbe1f&originHeight=1052&originWidth=2272&originalType=binary&ratio=1&rotation=0&showTitle=false&size=234010&status=error&style=shadow&taskId=u49a4dfd8-1bca-4079-9806-9c7b2e71faf&title=)

**Scatter Plot**![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664955930978-1aeb802c-8012-4ff8-81ab-ada83251c31b.png#clientId=u1a23eaab-5a0c-4&errorMessage=unknown%20error&from=paste&id=u43ea5e9f&originHeight=1189&originWidth=2270&originalType=binary&ratio=1&rotation=0&showTitle=false&size=87911&status=error&style=shadow&taskId=u6934f0d5-14e3-4c74-9a56-87cca8f37aa&title=)
> ![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664955947680-156726f1-9bd9-4b90-9812-682a013bd17b.png#clientId=u1a23eaab-5a0c-4&errorMessage=unknown%20error&from=paste&id=u3a1d6a89&originHeight=426&originWidth=2252&originalType=binary&ratio=1&rotation=0&showTitle=false&size=202947&status=error&style=shadow&taskId=ue3da99b2-946f-45d4-9d15-8e313bb7712&title=)![image.png](https://cdn.nlark.com/yuque/0/2022/png/12393765/1664955963707-1c5e62c1-3ff1-4f7c-8ca6-5559a561de74.png#clientId=u1a23eaab-5a0c-4&errorMessage=unknown%20error&from=paste&id=u2aecdb99&originHeight=1488&originWidth=2272&originalType=binary&ratio=1&rotation=0&showTitle=false&size=448900&status=error&style=shadow&taskId=u043ece89-f231-445e-8c41-bd68a1f0ae6&title=)



# 4 Proof/Remarks for Bootstrap*
[Bootstrap CMU.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1666942018877-6400ca7a-ffc7-4d98-84fe-812369267d98.pdf)


