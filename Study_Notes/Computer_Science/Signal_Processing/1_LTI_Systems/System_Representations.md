# Block Diagram
## Mathematical Properties
> [!property]
> ![](Difference_Equations.assets/image-20240420163629105.png)![](Difference_Equations.assets/image-20240420163247622.png)

> [!example]
> ![](Difference_Equations.assets/image-20240420163701616.png)![](Difference_Equations.assets/image-20240420163708344.png)



# DT Operator Algebra
## Principles
> [!important]
> ![](Difference_Equations.assets/image-20240420163807125.png)



## Accumulator
> [!def]
> ![](Difference_Equations.assets/image-20240420163836091.png)![](Difference_Equations.assets/image-20240420163844850.png)



## Reciprocal Operator
> [!important]
> ![](Difference_Equations.assets/image-20240420164433913.png)![](Difference_Equations.assets/image-20240420164442815.png)


## Feedback Operator
> [!def]
> ![](Difference_Equations.assets/image-20240420164655220.png)



## Cyclic/Acyclic Path
> [!important]
> ![](Difference_Equations.assets/image-20240420164727530.png)





# CT Operator Algebra
## Basic Definitions
> [!def]
> ![](System_Representations.assets/image-20240420174333361.png)![](System_Representations.assets/image-20240420174547850.png)
> Here $\mathcal{A}$ is like making accumulation.
> 
> ![](System_Representations.assets/image-20240420174620532.png)




## Evaluating Operator Expressions
> [!def]
> ![](System_Representations.assets/image-20240420175025976.png)



## Operator Algebra
> [!property]
> ![](System_Representations.assets/image-20240420175046268.png)

> [!example]
> ![](System_Representations.assets/image-20240420175852486.png)![](System_Representations.assets/image-20240420175840348.png)






# Unit Sample Response
## System Functionals and USR
> [!def]
> For a discrete time system, the unit sample response(or unit impulse response) is the output of the system given the input of this form $$x[n]=\begin{cases}1&n\geq 0\\0&\textbf{otherwise} \end{cases}$$.
> 
> Unit sample response is very closely related to the concepts of poles and system functional. 

> [!example]
> This example shows how to use the expression of system functional to find the poles and unit sample resposne of the DT system.
> 
> Suppose we have an LTI system as follows:
> $$y[n]=\frac{3}{4}y[n-1]-\frac{1}{8}y[n-2]+x[n]$$ where $x[n]$ is a unit impulse input.
> 1. We start by finding the system functional $$\frac{\mathcal{Y}}{\mathcal{X}}=\frac{1}{(1-\frac{1}{2}\mathcal{R})(1-\frac{1}{4}\mathcal{R})}$$
> 2. We use partial fraction to get the following: $$\frac{\mathcal{Y}}{\mathcal{X}}=\frac{2}{1-\frac{1}{2}\mathcal{R}}+\frac{-1}{1-\frac{1}{4}\mathcal{R}}$$
> 3. The poles are just the coefficients of the two denominators: $p_{0}=\frac{1}{2}$ and $p_{1}=\frac{1}{4}$
> 4. The expression for unit sample response is just $$h[n]=2\cdot (\frac{1}{2})^{n}+(-1)\cdot (\frac{1}{4})^{n},\forall n\geq 0$$




## From USR to System Functional
> [!example]
> ![](System_Representations.assets/image-20240624124721878.png)


## Finding USR by System Functional
> [!example]
> ![](System_Representations.assets/image-20240704210821234.png)![](System_Representations.assets/image-20240704210842968.png)



# Poles
## Finding Poles from USR
> [!important]
> ![](System_Representations.assets/image-20240704211029565.png)![](System_Representations.assets/image-20240704211048384.png)



## Repeated Poles
> [!example]
> ![](System_Representations.assets/image-20240704211226468.png)![](System_Representations.assets/image-20240704211235503.png)![](System_Representations.assets/image-20240704211241741.png)




# Euler's Approximation Methods
> [!example]
> ![](System_Representations.assets/image-20240704211320553.png)
> The (b) here uses the knowledge from [Second Order Unit Step Response](../../../Mathematics/Differential_Equations/MIT_18.03SC/3.5_Impulse_Response.md#4%20Second%20Order%20Unit%20Step%20Response) which says that for a system if we have unit step input, then the $y(t)$ and $\dot{y}(t)$ are both continuous at 0.
> 
> ![](System_Representations.assets/image-20240704211614619.png)![](System_Representations.assets/image-20240704211625552.png)![](System_Representations.assets/image-20240704211633692.png)![](System_Representations.assets/image-20240704211641766.png)







