[MIT6_042JS15_Binary Relations.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674132762878-ea937b7b-de21-4435-8315-6335cc79249f.pdf)

# 1 Functions
## Domains and Images
:::info
![image.png](./Functions_Binary_Relation.assets/20230914_1508473117.png)
:::
**Examples**![image.png](./Functions_Binary_Relation.assets/20230914_1508495361.png)![image.png](./Functions_Binary_Relation.assets/20230914_1508516695.png)
**Partial& Total Function**![image.png](./Functions_Binary_Relation.assets/20230914_1508528374.png)
![image.png](./Functions_Binary_Relation.assets/20230914_1508541407.png)
**Functions applied on a set**![image.png](./Functions_Binary_Relation.assets/20230914_1508565333.png)
**Range and Image**![image.png](./Functions_Binary_Relation.assets/20230914_1508589704.png)


## Function Composition
:::info
![image.png](./Functions_Binary_Relation.assets/20230914_1509005257.png)
:::



# 2 Binary Relations
[MIT6_042JS16_Relations_Slides.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674724735604-e5b5023b-802e-4b70-bf4b-31f47c9fbb7e.pdf)
:::info
![image.png](./Functions_Binary_Relation.assets/20230914_1509024132.png)
:::

## Definition
> ![image.png](./Functions_Binary_Relation.assets/20230914_1509031826.png)
> `Function is a special case of binary relation`。

**Explanations**![image.png](./Functions_Binary_Relation.assets/20230914_1509052604.png)
**Binary Relation vs Function Definition**![image.png](./Functions_Binary_Relation.assets/20230914_1509062745.png)![image.png](./Functions_Binary_Relation.assets/20230914_1509088681.png)
**Staff Example**![image.png](./Functions_Binary_Relation.assets/20230914_1509109507.png)


## Relational Diagrams
**Relation Diagrams - arrow out property**![image.png](./Functions_Binary_Relation.assets/20230914_1509125387.png)![image.png](./Functions_Binary_Relation.assets/20230914_1509149579.png)
:::info
![image.png](./Functions_Binary_Relation.assets/20230914_1509169039.png)
:::
**Example**![image.png](./Functions_Binary_Relation.assets/20230914_1509176145.png)


## Relational Images
:::info
![image.png](./Functions_Binary_Relation.assets/20230914_1509191126.png)
:::
**Example**![image.png](./Functions_Binary_Relation.assets/20230914_1509213116.png)
![image.png](./Functions_Binary_Relation.assets/20230914_1509234286.png)


## Inverse Relations and Images
:::info
![image.png](./Functions_Binary_Relation.assets/20230914_1509254766.png)
:::
**Example**![image.png](./Functions_Binary_Relation.assets/20230914_1509264499.png)
![image.png](./Functions_Binary_Relation.assets/20230914_1509283808.png)


## Inverse Function & Inverse Images
> ![image.png](./Functions_Binary_Relation.assets/20230914_1509305378.png)


### Definition
> **Inverse Image:**
> ![image.png](./Functions_Binary_Relation.assets/20230914_1509328782.png)
> **Inverse Function:**
> ![image.png](./Functions_Binary_Relation.assets/20230914_1509336004.png)



### Properties
> [https://math.stackexchange.com/questions/359693/overview-of-basic-results-about-images-and-preimages](https://math.stackexchange.com/questions/359693/overview-of-basic-results-about-images-and-preimages)
> [https://www.cs.odu.edu/~toida/nerzic/content/function/properties_of_inverse.html](https://www.cs.odu.edu/~toida/nerzic/content/function/properties_of_inverse.html)
> **Remarks:**
> 1. If $f:A\to B$is a bijection, then inverse function $f^{-1}$exists. Otherwise, inverse function doesn't exist, but the inverse image $f^{-1}(X)$ of any set $X\subseteq B$always exists. (A bit of messy notations).
> 2. If $f: A\to B$is a bijection and $f^{-1}$is its inverse function, then $f(f^{-1}(x))=x$and $f^{-1}(f(x))=x$always holds (Note that here $x$is en element). Let $X\subseteq A$, also $f(f^{-1}(X))=X$and $f^{-1}(f(X))=X$always holds(where $f^{-1}$is the inverse image, note that $X$is a set).
> 3. Generally for any function $f: A\to B$. Let $X\subseteq A$,$f(f^{-1}(X))=X$always hold but$f^{-1}(f(X))=X$ doesn't. One can prove it through counterexample. For a counter example,  Take `A= {1,2}`, `B={1}`, `X={1}`, `f:A->B` defined by `f(1)=1` and `f(2) =1`. Then `f(X) =f({1}) = {1}` and $f^{-1}(f(X))=f^{-1}(\{1\})= \{1,2\}$ (**here **$f^{-1}$**is the inverse image, defined on a specific set**), which does not equal x.


### Examples
> ![image.png](./Functions_Binary_Relation.assets/20230914_1509354063.png)




# 3 Finite Cardinality
:::info
![image.png](./Functions_Binary_Relation.assets/20230914_1509371685.png)
:::


## Definition
:::info
![image.png](./Functions_Binary_Relation.assets/20230914_1509387555.png)
:::


## Surj/inj/bij
:::info
![image.png](./Functions_Binary_Relation.assets/20230914_1509406105.png)
:::
**Arrow Proof of 1,2**![image.png](./Functions_Binary_Relation.assets/20230914_1509425636.png)
![image.png](./Functions_Binary_Relation.assets/20230914_1509444199.png)
**Arrow Proof of 3**![image.png](./Functions_Binary_Relation.assets/20230914_1509451024.png)

**Converse of Lemma 4.5.3.1**![image.png](./Functions_Binary_Relation.assets/20230914_1509482534.png)![image.png](./Functions_Binary_Relation.assets/20230914_1509499135.png)
:::info
![image.png](./Functions_Binary_Relation.assets/20230914_1509511591.png)
:::



## Subsets of finite Sets
:::info
![image.png](./Functions_Binary_Relation.assets/20230914_1509529765.png)![image.png](./Functions_Binary_Relation.assets/20230914_1509547396.png)![image.png](./Functions_Binary_Relation.assets/20230914_1509563419.png)
:::
