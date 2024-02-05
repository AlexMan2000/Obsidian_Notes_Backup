[cs61b 2018 lec32 sorting I.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1681556980278-c8876ac8-849d-4b38-91a0-ced29dfb8354.pdf)
# Sorting Basics
## Sorting Properties
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458007971.png)


## Inversion Properties
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458011069.png)![image.png](Basic_Sorting_Algorithms.assets/20230818_1458015739.png)
> 对于一个长度为$n$的数组来说，`Inversion`最多有$C_n^2=\frac{n(n-1)}{2}$个， 最少为零。


## Space Complexity
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458011166.png)
> 🔔: `Performance`通常包含`Time Complexity`和`Space Complexity`两种。



# Selection Sort
## Demo
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458015186.png)

[cs61b selection sort demo.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1681557721307-0c230af5-e61e-4427-a265-bcef18119d56.pdf)

## Implementations
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458025768.png)


# HeapSort
## Naive Heapsort
### Algorithmic Logic
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458028171.png)

[cs61b naive heap sort demo.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1681557860148-7d49e0ad-884e-45a9-9e0a-380a10b926ea.pdf)

### Implementations
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458026523.png)


### Performance
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458034516.png)
> 🔔: 需要注意`Heap`中所有的`Operation`都是$O$而不是$\Theta$, 原因是`Heap`的结构会影响我们`Heap Operations`的速度。设想一下如果`Heap`中所有的元素都一样，那么`remove largest item`之后我们其实不需要做任何`sink`的操作，所以复杂度是$\Theta(1)$。


## In-place Heapsort⭐⭐
### Algorithmic Logic
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458034952.png)

[cs61b in-place heap sort demo.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1681558323545-998bdf8f-220d-421c-bd05-0c705f6ce6b2.pdf)


#### Phase 1 Bottom-up Heapification⭐⭐⭐⭐⭐
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458035275.png)
> 🔔: `Reverse Level Order`指的是从最深的一层中的元素逆向进行`sink`操作，然后逐层向上如是操作。
> 🔔: `max-heap`中进行`sink`操作时，如果当前节点的子节点数值都比当前节点大，则我们选择那个更大的节点进行交换。就像在`min-heap`中进行`sink`操作时，如果当前节点的子节点数值都比当前节点小，则我们选择那个更小的节点进行交换。

**Graph Explanations**![image.png](Basic_Sorting_Algorithms.assets/20230818_1458031148.png)
**One-Step**![image.png](Basic_Sorting_Algorithms.assets/20230818_1458049268.png)![image.png](Basic_Sorting_Algorithms.assets/20230818_1458046225.png)
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458049935.png)


#### Phase 2 Delete Elements
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458049108.png)

**One-Step**![image.png](Basic_Sorting_Algorithms.assets/20230818_1458047244.png)![image.png](Basic_Sorting_Algorithms.assets/20230818_1458055582.png)

### Implementations
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458054582.png)![image.png](Basic_Sorting_Algorithms.assets/20230818_1458067359.png)


### Performance
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458064754.png)
> 🔔: 对于`Bottom-up Heapification`来说，我们假定所有的叶子节点都已经是`Heap`了，假设有$n$个叶子节点，假设深度为$d$。则:
> 1. 对深度为$d-1$的层来说，有$\frac{n}{2}$个节点，每个节点至多发生一次`swap`, 总共$O(\frac{n}{2})$次`swap`操作。
> 2. 对深度为$d-2$的层来说，有$\frac{n}{4}$个节点，每个节点至多发生两次`swap`，总共$O(\frac{n}{4}\times 2)=O(\frac{n}{2})$次`swap`操作。
> 
所以所有的层加起来是$O(N)$的时间复杂度。
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458069338.png)


# MergeSort
## Demo
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458061509.png)

[cs61b merge sort demo.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1681561927554-22d07848-a661-4022-a0a2-a896f3cbb108.pdf)


## Implementations
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458073820.png)![image.png](Basic_Sorting_Algorithms.assets/20230818_1458076500.png)



## Improved Implementations
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458075366.png)


# Insertion Sort
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458078354.png)


## Naive Approach
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458072827.png)

[cs61b naive insertion sort demo.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1681562048019-54697054-4b5e-4f84-a876-bc61cea95b89.pdf)


## In-place Approach
### Demo⭐⭐
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458079412.png)

[cs61b in-place insertion sort demo.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1681562111689-8dcf60c3-b4e5-4e3f-9a75-f69de8625dd1.pdf)

### Examples⭐⭐⭐⭐⭐
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458083577.png)



### Performance
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458088035.png)


## Inversions Effect
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458088180.png)![image.png](Basic_Sorting_Algorithms.assets/20230818_1458085103.png)
> **总的来说，数组的**`**# Inversions**`**越小，排序速度越快。**
> 1. 当`#Inversion`为零时，即`Already Sorted Array`, 则`Time Complexity`为$\Theta(n)$
> 2. 当数组倒序排列时，即`Already Reversely-Sorted Array`, 则`Time Complexity`为$\Theta(n^2)$



## Implementations
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458094610.png)


# Shell's Sort - Optimizing Insertion Sort
## Idea
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458097507.png)



## Example
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458093347.png)



## Performance
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458097969.png)


# Summary
## Picking the Best Sort
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458107684.png)
> 因为我们只有少于两个`Inversions`。


## Performance
> ![image.png](Basic_Sorting_Algorithms.assets/20230818_1458103201.png)



# Study Guide
[Sorting I (Basic Sorts) _ CS 61B Spring 2021.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1692340992561-711b907b-705f-4e2a-b58d-26eb18d38c8b.pdf)
