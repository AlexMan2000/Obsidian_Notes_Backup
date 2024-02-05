[cs61b 2019 lec17 ds3 2-3 trees, 2-3-4 trees.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1675950646308-155cdca5-f98d-4be5-a5e6-c4082b633da2.pdf)
# Avoid Imbalance
## Juicy Leaves
> ![image.png](B-Trees.assets/20230302_0954167230.png)![image.png](B-Trees.assets/20230302_0954172449.png)![image.png](B-Trees.assets/20230302_0954174468.png)![image.png](B-Trees.assets/20230302_0954176687.png)



## Splitting Nodes - B-Trees
> ![image.png](B-Trees.assets/20230302_0954174914.png)![image.png](B-Trees.assets/20230302_0954172162.png)


## Maintain Search Trees
> ![image.png](B-Trees.assets/20230302_0954176508.png)![image.png](B-Trees.assets/20230302_0954173075.png)![image.png](B-Trees.assets/20230302_0954176065.png)



## Perfect Balance
> ![image.png](B-Trees.assets/20230302_0954182365.png)


# B-Tree Terminology
## Definition(2-3/2-3-4)
> ![image.png](B-Trees.assets/20230302_0954186491.png)


## Terminology
> ![image.png](B-Trees.assets/20230302_0954182087.png)
> 如果`L=2`, 则所有的`Node`都要么没有子节点，要么有`2~L+1`个子节点。


# B-Tree Insertion Operation
## add
> ![image.png](B-Trees.assets/20230302_0954188059.png)![image.png](B-Trees.assets/20230302_0954185180.png)



## add Chain reaction⭐⭐⭐⭐⭐
> ![image.png](B-Trees.assets/20230302_0954181209.png)![image.png](B-Trees.assets/20230302_0954183062.png)

**Root is too full**![image.png](B-Trees.assets/20230302_0954186171.png)![image.png](B-Trees.assets/20230302_0954196655.png)


## Summary
> ![image.png](B-Trees.assets/20230302_0954198158.png)


# B-Tree Invariants
## Warmup Exercises
### Exercise 1: Comparing with BST
> ![image.png](B-Trees.assets/20230302_0954195159.png)

**Solution**![image.png](B-Trees.assets/20230302_0954199719.png)[https://www.cs.usfca.edu/~galles/visualization/BTree.html](https://www.cs.usfca.edu/~galles/visualization/BTree.html)



### Exercise 2: Minimize the Height
> ![image.png](B-Trees.assets/20230302_0954198295.png)

**Solution**![image.png](B-Trees.assets/20230302_0954199631.png)
另解为: $4,5,6,3,7,1,2$

## Bushiness
> ![image.png](B-Trees.assets/20230302_0954195467.png)![image.png](B-Trees.assets/20230302_0954192628.png)



# B-Tree Runtime Analysis
## Height
> ![image.png](B-Trees.assets/20230302_0954206801.png)
> 注意是$\Theta(\cdot)$



## contains
> ![image.png](B-Trees.assets/20230302_0954207186.png)
> 注意是$O(\cdot)$


## add
> ![image.png](B-Trees.assets/20230302_0954205179.png)
> 注意是$O(\cdot)$



## Summary
> ![image.png](B-Trees.assets/20230302_0954203495.png)



# B-Tree Deletion(Extra)
## BST Deletion Recap
> ![image.png](B-Trees.assets/20230302_0954201913.png)![image.png](B-Trees.assets/20230302_0954201821.png)


## Delete MultiKey Leaves
> ![image.png](B-Trees.assets/20230302_0954206518.png)![image.png](B-Trees.assets/20230302_0954202323.png)



## Delete SingleKey Leaves⭐⭐
> ![image.png](B-Trees.assets/20230302_0954215727.png)



## Filling Empty Nodes⭐⭐⭐⭐⭐
> ![image.png](B-Trees.assets/20230302_0954213278.png)


### MultiKey Siblings
#### Inner Node
> ![image.png](B-Trees.assets/20230302_0954216446.png)



#### Leaf Node
> ![image.png](B-Trees.assets/20230302_0954218829.png)![image.png](B-Trees.assets/20230302_0954214277.png)



### Multi-Key Parent
> ![image.png](B-Trees.assets/20230302_0954215194.png)![image.png](B-Trees.assets/20230302_0954216401.png)

**Exercise**![image.png](B-Trees.assets/20230302_0954217266.png)![image.png](B-Trees.assets/20230302_0954227564.png)


### Single-Key Parent and Siblings
> ![image.png](B-Trees.assets/20230302_0954221396.png)

**Exercise 1**⭐⭐⭐⭐⭐![image.png](B-Trees.assets/20230302_0954228062.png)![image.png](B-Trees.assets/20230302_0954224917.png)
**Exercise 2**⭐⭐⭐![image.png](B-Trees.assets/20230302_0954229064.png)![image.png](B-Trees.assets/20230302_0954225771.png)


# Study Guide Exercises
[B-Trees Study Guide _ CS 61B Spring 2019.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1676002692982-fd76caeb-926b-4844-b93d-3926b6d11825.pdf)
> 

