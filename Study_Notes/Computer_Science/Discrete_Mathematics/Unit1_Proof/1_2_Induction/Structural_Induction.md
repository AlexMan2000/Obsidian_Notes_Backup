# 1 Structural Induction
:::info
![image.png](./Structural_Induction.assets/20230914_1502227153.png)
:::


## Recursive Data Types
:::info
![image.png](./Structural_Induction.assets/20230914_1502248246.png)
:::


## Strings of brackets
### What are they?
:::info
![image.png](./Structural_Induction.assets/20230914_1502272480.png)
:::

### brkts - Set of Brackets
:::info
![image.png](./Structural_Induction.assets/20230914_1502297979.png)
:::


### RecMatch - Set of matched brackets
:::info
![image.png](./Structural_Induction.assets/20230914_1502311023.png)![image.png](./Structural_Induction.assets/20230914_1502321533.png)![image.png](./Structural_Induction.assets/20230914_1502341407.png)
:::
**Remarks**![image.png](./Structural_Induction.assets/20230914_1502366921.png)


## Arithmetic Expression
:::info
![image.png](./Structural_Induction.assets/20230914_1502389700.png)
:::



### Set of an expression
:::info
![image.png](./Structural_Induction.assets/20230914_1502398637.png)![image.png](./Structural_Induction.assets/20230914_1502411610.png)![image.png](./Structural_Induction.assets/20230914_1502434421.png)
:::



### Expression Parsing
:::info
![image.png](./Structural_Induction.assets/20230914_1502466262.png)
具体的`Parsing`过程可以参考[CS61A Project4](https://www.yuque.com/alexman/ac5oth/uwldsn8kedec0mt5)
:::


## Sturctural Induction on RDT
:::info
![image.png](./Structural_Induction.assets/20230914_1502482654.png)![image.png](./Structural_Induction.assets/20230914_1502492299.png)![image.png](./Structural_Induction.assets/20230914_1502515670.png)
:::




# 2 Functions on RDT
## Quick Review of Functions
:::info
![image.png](./Structural_Induction.assets/20230914_1502536593.png)
:::


## Recursively-Defined Functions
### Evaluation Function for Arithmetic Expression
:::info
![image.png](./Structural_Induction.assets/20230914_1502569031.png)![image.png](./Structural_Induction.assets/20230914_1502587681.png)
:::



### Depth Function for RecMatch
:::info
![image.png](./Structural_Induction.assets/20230914_1503001952.png)
:::



## Ambiguous RDT Definition
### What is it?
:::info
When a recursive deﬁnition of a data type allows the same element to be constructed in more than one way, the deﬁnition is said to be ambiguous. 
A function deﬁned recursively from an ambiguous deﬁnition of a data type will not be well-deﬁned unless the values speciﬁed for the different ways of constructing the element agree.
We were careful to choose an unambiguous deﬁnition of RecMatch to ensure that functions deﬁned recursively on the deﬁnition would always be well-deﬁned. 
:::


### Ambiguous Definition of RecMatch
:::info
As an example of the trouble an ambiguous deﬁnition can cause, let's consider another deﬁnition of the matched strings.
![image.png](./Structural_Induction.assets/20230914_1503022118.png)![image.png](./Structural_Induction.assets/20230914_1503047256.png)
:::


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


