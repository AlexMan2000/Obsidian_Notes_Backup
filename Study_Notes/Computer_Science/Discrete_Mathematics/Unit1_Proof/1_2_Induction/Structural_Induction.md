# 1 Structural Induction
> [!overview]
> ![](./Structural_Induction.assets/20230914_1502227153.png)



## Recursive Data Types
> [!important]
> ![](./Structural_Induction.assets/20230914_1502248246.png)



## Strings of brackets
### Definition
> [!def]
> ![](Structural_Induction.assets/image-20231213101139443.png)![](./Structural_Induction.assets/20230914_1502272480.png)



### RecMatch - Set of matched brackets
> [!def]
> ![](./Structural_Induction.assets/20230914_1502311023.png)![](./Structural_Induction.assets/20230914_1502321533.png)![](./Structural_Induction.assets/20230914_1502341407.png)


## Arithmetic Expression
> [!overview]
> ![](./Structural_Induction.assets/20230914_1502389700.png)


### Defintion
> [!def]
> ![](Structural_Induction.assets/image-20231213101456291.png)![](Structural_Induction.assets/image-20231213101503372.png)![](Structural_Induction.assets/image-20231213101555916.png)



### Expression Parsing
> [!example]
> ![](./Structural_Induction.assets/20230914_1502466262.png)
> 具体的`Parsing`过程可以参考[CS61A Project4](https://www.yuque.com/alexman/ac5oth/uwldsn8kedec0mt5)




## Sturctural Induction on RDT
> [!example]
> ![](./Structural_Induction.assets/20230914_1502482654.png)![](./Structural_Induction.assets/20230914_1502492299.png)![](./Structural_Induction.assets/20230914_1502515670.png)


# 2 Functions on RDT
## Quick Review of Functions
> [!overview]
> ![](./Structural_Induction.assets/20230914_1502536593.png)



## Recursively-Defined Functions
### Evaluation Function for Arithmetic Expression
> [!def]
> ![](./Structural_Induction.assets/20230914_1502569031.png)![](./Structural_Induction.assets/20230914_1502587681.png)




### Depth Function for RecMatch
> [!def]
> ![](./Structural_Induction.assets/20230914_1503001952.png)



# 3 Ambiguous RDT Definition
### What is it?
> [!def]
> **When a recursive deﬁnition of a data type allows the same element to be constructed in more than one way, the deﬁnition is said to be ambiguous.** 
> 
> A function deﬁned recursively from an ambiguous deﬁnition of a data type will not be well-deﬁned unless the values speciﬁed for the different ways of constructing the element agree.
> 
> We were careful to choose an unambiguous deﬁnition of RecMatch to ensure that functions deﬁned recursively on the deﬁnition would always be well-deﬁned. 



### Ambiguous Definition of RecMatch
> [!example]
> As an example of the trouble an ambiguous deﬁnition can cause, let's consider another deﬁnition of the matched strings.
> ![](./Structural_Induction.assets/20230914_1503022118.png)![](./Structural_Induction.assets/20230914_1503047256.png)



## Recursive Functions on N - 3.5.8
:::info
![image.png](./Structural_Induction.assets/20230914_1503064680.png)![image.png](./Structural_Induction.assets/20230914_1503081791.png)
:::


### The Factorial Function
:::info
![image.png](./Structural_Induction.assets/20230914_1503114854.png)
:::


### The Fibonacci Numbers
:::info
![image.png](./Structural_Induction.assets/20230914_1503134190.png)
:::


### Sum-Notation
:::info
![image.png](./Structural_Induction.assets/20230914_1503152195.png)
:::


## Ill-formed Recursive Functions
:::info
![image.png](./Structural_Induction.assets/20230914_1503179401.png)
:::


### Definition 3.5.9
:::info
![image.png](./Structural_Induction.assets/20230914_1503191905.png)
:::


### Definition 3.5.10
:::info
![image.png](./Structural_Induction.assets/20230914_1503219835.png)
:::


### Definition 3.5.11
:::info
![image.png](./Structural_Induction.assets/20230914_1503231944.png)
:::


### Hailstone Function
:::info
![image.png](./Structural_Induction.assets/20230914_1503251501.png)![image.png](./Structural_Induction.assets/20230914_1503275577.png)
:::


