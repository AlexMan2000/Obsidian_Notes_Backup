# 1 Discussion
## Hashcode Validity⭐⭐⭐⭐⭐
> **Sp18, disc09**
> **Sp21, disc08 detailed solution**
> **🔔: **`**Hash Function**`**需要满足下面的两个条件:**
> ![image.png](./DE_Hashing.assets/20230324_1528108567.png)
> ![image.png](./DE_Hashing.assets/20230324_1528104137.png)![image.png](./DE_Hashing.assets/20230324_1528102188.png)



## HashMap Modification
### Modify the Key
> ![image.png](./DE_Hashing.assets/20230324_1528105899.png)

**Detailed Solution**![image.png](./DE_Hashing.assets/20230324_1528103519.png)

### Modify the Value
> ![image.png](./DE_Hashing.assets/20230324_1528102988.png)

**Detailed Solution**![image.png](./DE_Hashing.assets/20230324_1528103588.png)


## HashMap Insertion
> ![image.png](./DE_Hashing.assets/20230324_1528114013.png)


### Insertion&Resizing&Problem
> ![image.png](./DE_Hashing.assets/20230324_1528115869.png)

**Solution**![image.png](./DE_Hashing.assets/20230324_1528111800.png)
> ![image.png](./DE_Hashing.assets/20230324_1528112635.png)

**Solution**![image.png](./DE_Hashing.assets/20230324_1528111473.png)


# 2 Exam Preparations
## Hashing Validity
### Problem Group 1
> **Sp21 examprep08**
> ![image.png](./DE_Hashing.assets/20230324_1528118434.png)
> 🔔: 本题也是只要抓住`Hashcode Validity`的两大条件即可:
> 1. 对于`equals()`结果相同的`Object`, 调用其`hashCode()`函数返回的结果也应该相同。
> 2. 对于同一个`object`调用多次`hashCode()`函数返回的结果应该一致。(Deterministic)
> 
我们会看到，上面两个例子中每一个都会违反其中一个条件。

**Bugs for class Timezone - 违反了第二条**![image.png](./DE_Hashing.assets/20230324_1528115075.png)
**Bugs for class Course - 违反了第一条**![image.png](./DE_Hashing.assets/20230324_1528111757.png)

### Problem Group 2
> **Sp18 examprep09**
> ![image.png](./DE_Hashing.assets/20230324_1528113383.png)


#### Example 1
> ![image.png](./DE_Hashing.assets/20230324_1528115897.png)



#### Example 2
> ![image.png](./DE_Hashing.assets/20230324_1528125872.png)
> ❌: 问题很明显，就是对同一个`object`调用`hashCode()`函数时返回的结果不一致(`getCurrentTime()`返回的是当前的时间戳，每秒都在改变, 所以不是`deterministic`)。


#### Example 3
> ![image.png](./DE_Hashing.assets/20230324_1528125363.png)
> ✔️: `hashCode()`没有问题，满足两个条件。
> ❗:  但是这个函数产生的`hashCode`不是`Unique`的，因为他的结果最后都要`%509`, 这就说明只可能是`0~508`中的一种，这样就会造成严重的`Hashing Collision`现象出现。



#### Example 4
> ![image.png](./DE_Hashing.assets/20230324_1528122108.png)
> ❌: 问题很明显，就是对`equals()`返回`true`的两个`objects`，他们的`id`是一样的，但是对他们调用`hashCode()`的结果可能是不同的，因为还有`name`和`age`的`hashCode()`在起作用。


#### Example 5⭐⭐⭐⭐⭐
> ![image.png](./DE_Hashing.assets/20230324_1528123169.png)
> ✔️: `hashCode()`没有问题，满足两个条件。本质上`equals`在比较不同对象中的`seq1`和`seq2`是否一样。`hashCode()`本质上在`31`进制下对`seq 1`和`seq2`进行`encoding`。
> ❗:  但是这个`hashCode()`函数非常不高效，假设`seq1.length() = M`, `seq2.length() = N`。因为它使用了嵌套循环，也就是$\Theta(MN)$的时间来计算哈希码，但其实只需要$\Theta(M+N)$就可以达成相同的目的。比如`for(char c1: seq1)`一次遍历，`for(char c1: seq2)`一次遍历, 可以更高效的在满足两个`Validity`的情况下计算哈希码。



## HashMap Insertions
### Insertion&Resizing
> Sp 18 ExamPrep09 
> ![image.png](./DE_Hashing.assets/20230324_1528122057.png)

**Solution**![image.png](./DE_Hashing.assets/20230324_1528122892.png)

### Instance as Keys
> ![image.png](./DE_Hashing.assets/20230324_1528128878.png)![image.png](./DE_Hashing.assets/20230324_1528128577.png)
> 🔔**: 本题需要明确两点:**
> 1. 决定`bucket index`需要利用`hashCode()`的结果。
> 2. `put(key, value)`时需要利用`equals()`来判断某个`key`是否已经存在，详见`L1809`中的实现。

**Solution**![image.png](./DE_Hashing.assets/20230324_1528128977.png)
**

## HashMap Performance
### Insertion&Resizing
> Sp 18 ExamPrep09 
> ![image.png](./DE_Hashing.assets/20230324_1528122762.png)![image.png](./DE_Hashing.assets/20230324_1528126063.png)



