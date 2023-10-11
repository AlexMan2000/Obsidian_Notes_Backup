[cs61b 2019 ds6 lec20 heaps and pq.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1676204870766-91caa95d-d161-4510-a010-2712cde51f13.pdf)
[Heaps and Priority Queues Study Guide _ CS 61B Spring 2019.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1676204901247-a5fd6209-0589-4795-b9bc-7efd47c33743.pdf)


# Priority Queue Intro
## Interface
> ![image.png](./Heap_PQs.assets/20230302_0957333438.png)



## Real-World Problem
> ![image.png](./Heap_PQs.assets/20230302_0957338175.png)
> ![image.png](./Heap_PQs.assets/20230302_0957333883.png)![image.png](./Heap_PQs.assets/20230302_0957341653.png)


## Possible PQ Implementation
> ![image.png](./Heap_PQs.assets/20230302_0957341124.png)



# Heap
## Definition
> ![image.png](./Heap_PQs.assets/20230302_0957344621.png)

**Concept Check**![image.png](./Heap_PQs.assets/20230302_0957343210.png)
![image.png](./Heap_PQs.assets/20230302_0957341712.png)


## Goodness of Heap
> ![image.png](./Heap_PQs.assets/20230302_0957343851.png)


## Heap Operations
> ![image.png](./Heap_PQs.assets/20230302_0957348044.png)

**Solution - Insert 3**![image.png](./Heap_PQs.assets/20230302_0957341577.png)![image.png](./Heap_PQs.assets/20230302_0957357685.png)![image.png](./Heap_PQs.assets/20230302_0957352049.png)![image.png](./Heap_PQs.assets/20230302_0957356412.png)![image.png](./Heap_PQs.assets/20230302_0957354638.png)
**Insert 5**![image.png](./Heap_PQs.assets/20230302_0957352748.png)![image.png](./Heap_PQs.assets/20230302_0957357233.png)![image.png](./Heap_PQs.assets/20230302_0957352750.png)

**Delete Min**![image.png](./Heap_PQs.assets/20230302_0957353348.png)![image.png](./Heap_PQs.assets/20230302_0957353890.png)![image.png](./Heap_PQs.assets/20230302_0957359225.png)![image.png](./Heap_PQs.assets/20230302_0957357529.png)![image.png](./Heap_PQs.assets/20230302_0957353248.png)![image.png](./Heap_PQs.assets/20230302_0957361711.png)

**Delete Another Min**![image.png](./Heap_PQs.assets/20230302_0957366984.png)
![image.png](./Heap_PQs.assets/20230302_0957367102.png)![image.png](./Heap_PQs.assets/20230302_0957362108.png)![image.png](./Heap_PQs.assets/20230302_0957365534.png)![image.png](./Heap_PQs.assets/20230302_0957368805.png)

> `Insertion`: Append, swap then swim up.
> `Deletion`: Swap, cut and dive in.

## 
## Summary
> ![image.png](./Heap_PQs.assets/20230302_0957367518.png)



# Heap - PQ Implementation
## Approach 1 - Tree
### 1a - Fixed-Width Nodes
> ![image.png](./Heap_PQs.assets/20230302_0957368591.png)



### 1b - Variable-Width Nodes
> ![image.png](./Heap_PQs.assets/20230302_0957368750.png)


### 1c - Sibling Tree
> ![image.png](./Heap_PQs.assets/20230302_0957365711.png)



## Approach 2 - Two Arrays
> ![image.png](./Heap_PQs.assets/20230302_0957373769.png)



## Approach 3 - One Array⭐⭐⭐⭐⭐
### Representation
> ![image.png](./Heap_PQs.assets/20230302_0957379833.png)
> **注意: 使用**`**array**`**来表示的**`**trees**`**只能是**`**complete trees**`**.**

### 
### Approach 3A
> ![image.png](./Heap_PQs.assets/20230302_0957373456.png)![image.png](./Heap_PQs.assets/20230302_0957376318.png)



### Approach 3B - One Empty Spot⭐⭐⭐⭐⭐
> ![image.png](./Heap_PQs.assets/20230302_0957373565.png)


## Performance&Summary
> ![image.png](./Heap_PQs.assets/20230302_0957379028.png)![image.png](./Heap_PQs.assets/20230302_0957375301.png)

