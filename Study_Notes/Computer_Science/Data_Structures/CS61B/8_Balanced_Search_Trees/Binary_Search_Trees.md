# Lectures&Readings
[cs61b 2018 lec21 ds2 binary search trees.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1675817602116-9eea42ae-324f-4359-bfaa-a36afe2bb82c.pdf)
[cs61b 2019 lec16 ds2 adts, sets, maps, binary search trees.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1675950045660-5239783d-4b7b-42f9-b391-09d04ee4a045.pdf)
## From SLL to BST
### Problem Setting
> ![image.png](./Binary_Search_Trees.assets/20230302_0954227684.png)
> We want to speed up the time to search for an item even if the list is sorted. But what if the item is at the end of the list? That would take linear time! Take a look at the linked list below and convince yourself that this is true.


### Improvement 1: Extra Links
> ![image.png](./Binary_Search_Trees.assets/20230302_0954224457.png)


### Improvement 2: Change the Entry Point
> ![image.png](./Binary_Search_Trees.assets/20230302_0954237944.png)One optimization we can implement is to have a reference to the middle node. This way, we can get to the middle in constant time. Then, if we flip the nodes' pointers, which allows us to traverse to both the left and right halves, we can decrease our runtime by half!



### Improvement 3: Recursive Entry
> But, we can do better than that. We can further optimize by adding pointers to the middle of each recursive half like so.
> ![image.png](./Binary_Search_Trees.assets/20230302_0954238794.png)



## Tree Definition
### Nodes&Edges
> ![image.png](./Binary_Search_Trees.assets/20230302_0954235194.png)


### Rooted Tree
> ![image.png](./Binary_Search_Trees.assets/20230302_0954233417.png)


## BST Definition
> ![image.png](./Binary_Search_Trees.assets/20230302_0954231881.png)![image.png](./Binary_Search_Trees.assets/20230302_0954231940.png)





## BST Operations
### findKey
> ![image.png](./Binary_Search_Trees.assets/20230302_0954236761.png)

**Runtime Analysis Exercise**![image.png](./Binary_Search_Trees.assets/20230302_0954238501.png)![image.png](./Binary_Search_Trees.assets/20230302_0954232483.png)![image.png](./Binary_Search_Trees.assets/20230302_0954247086.png)

### insertKey⭐⭐⭐
> ![image.png](./Binary_Search_Trees.assets/20230302_0954244087.png)![image.png](./Binary_Search_Trees.assets/20230302_0954242298.png)![image.png](./Binary_Search_Trees.assets/20230302_0954241278.png)

**Sample Solution to 10.2.4**如果我们要插入`1,2,3,4,5`:
如果插入的顺序是`3->2->1->4->5`, 那么树的高度将会是`2`
如果插入顺序是`1->2->3->4->5`, 那么树的高度将会是`4`
所以对于`Size-N Tree`来说，树的高度在$\lfloor log_2N\rfloor\leq H\leq N-1$

### deleteKey⭐⭐⭐⭐⭐
> ![image.png](./Binary_Search_Trees.assets/20230302_0954241987.png)



#### Case 1 Key with no children
> ![image.png](./Binary_Search_Trees.assets/20230302_0954246921.png)




#### Case 2 Key with one Child
> ![image.png](./Binary_Search_Trees.assets/20230302_0954245321.png)



#### Case 3 Key with two Children
> ![image.png](./Binary_Search_Trees.assets/20230302_0954247067.png)

**Challenge Problem**![image.png](./Binary_Search_Trees.assets/20230302_0954248453.png)![image.png](./Binary_Search_Trees.assets/20230302_0954252979.png)![image.png](./Binary_Search_Trees.assets/20230302_0954257651.png)


## BST Performance
### Tree Height
> ![image.png](./Binary_Search_Trees.assets/20230302_0954252927.png)

**Exercise**![image.png](./Binary_Search_Trees.assets/20230302_0954259889.png)![image.png](./Binary_Search_Trees.assets/20230302_0954251235.png)


### BST Height
> ![image.png](./Binary_Search_Trees.assets/20230302_0954259008.png)![image.png](./Binary_Search_Trees.assets/20230302_0954253008.png)![image.png](./Binary_Search_Trees.assets/20230302_0954251903.png)![image.png](./Binary_Search_Trees.assets/20230302_0954259040.png)![image.png](./Binary_Search_Trees.assets/20230302_0954257586.png)



### Height&Depth
> ![image.png](./Binary_Search_Trees.assets/20230302_0954263666.png)![image.png](./Binary_Search_Trees.assets/20230302_0954264078.png)![image.png](./Binary_Search_Trees.assets/20230302_0954261992.png)

**Exercise**![image.png](./Binary_Search_Trees.assets/20230302_0954265119.png)![image.png](./Binary_Search_Trees.assets/20230302_0954267400.png)


### Randomized Insertion⭐⭐⭐⭐⭐
> ![image.png](./Binary_Search_Trees.assets/20230302_0954265475.png)![image.png](./Binary_Search_Trees.assets/20230302_0954268659.png)



## BST Implementation Tips
> ![image.png](./Binary_Search_Trees.assets/20230302_0954268011.png)![image.png](./Binary_Search_Trees.assets/20230302_0954278191.png)![image.png](./Binary_Search_Trees.assets/20230302_0954273377.png)![image.png](./Binary_Search_Trees.assets/20230302_0954272184.png)



## Summary
> ![image.png](./Binary_Search_Trees.assets/20230302_0954274940.png)


# Study Guide Exercises
[BST Study Guide _ CS 61B Spring 2018.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1675817602121-1990a96a-751b-4b52-a4e6-163a32b8e8f7.pdf)


