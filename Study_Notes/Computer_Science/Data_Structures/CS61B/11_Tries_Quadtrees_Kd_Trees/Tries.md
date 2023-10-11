[cs61b 2019 lec21 tries.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1676795528965-f46b572a-db5f-4803-ae7d-f8e31546526e.pdf)


# Recap on data-indexed array
## Char-Indexed
> ![image.png](./Tries.assets/20230302_0959453611.png)



# Tries Basics
## Introduction
### String-Indexed Array
> ![image.png](./Tries.assets/20230302_0959453688.png)


### BST&HashTable Representation
> ![image.png](./Tries.assets/20230302_0959461658.png)



## Tries Invention
### Insertion
> ![image.png](./Tries.assets/20230302_0959465893.png)![image.png](./Tries.assets/20230302_0959467625.png)


### Search Hits&Misses
> ![image.png](./Tries.assets/20230302_0959461163.png)



## Tries Map
> ![image.png](./Tries.assets/20230302_0959461805.png)



## Comparison
> ![image.png](./Tries.assets/20230302_0959467049.png)



## Retrieval Tree
> ![image.png](./Tries.assets/20230302_0959462996.png)




## Takeaways⭐⭐⭐⭐⭐
> ![image.png](./Tries.assets/20230302_0959463289.png)


# Tries Implementations
## Basic Trie Implementation
### Class
> ![image.png](./Tries.assets/20230302_0959474504.png)![image.png](./Tries.assets/20230302_0959479535.png)


### Node
> ![image.png](./Tries.assets/20230302_0959473324.png)![image.png](./Tries.assets/20230302_0959472074.png)



### Improvement on redundancy
> ![image.png](./Tries.assets/20230302_0959478944.png)



### Performance
> ![image.png](./Tries.assets/20230302_0959472420.png)![image.png](./Tries.assets/20230302_0959475226.png)![image.png](./Tries.assets/20230302_0959484868.png)



## Improved Implementation
> ![image.png](./Tries.assets/20230302_0959489900.png)



### Approach 1: HashTable
> ![image.png](./Tries.assets/20230302_0959487300.png)



### Approach 2: BSTMap
> ![image.png](./Tries.assets/20230302_0959487683.png)



## Summary on Implementations
> ![image.png](./Tries.assets/20230302_0959484327.png)![image.png](./Tries.assets/20230302_0959488487.png)![image.png](./Tries.assets/20230302_0959491872.png)



# Tries String Operations
> Recall all of the comparisons that we've made between Tries and other data structures. 
> We can see that Tries offer us constant time lookup and insertion, but do they actually perform better than BSTs or Hash Tables? Possibly not. 
> For every string we have to traverse through every character, whereas in BSTs we have access to the entire string immediately. So what are Tries good for then?

## Prefix Matching
> ![image.png](./Tries.assets/20230302_0959492892.png)![image.png](./Tries.assets/20230302_0959496492.png)



## Collect All Keys
> ![image.png](./Tries.assets/20230302_0959491397.png)![image.png](./Tries.assets/20230302_0959499517.png)![image.png](./Tries.assets/20230302_0959492237.png)



## KeysWithPrefix
> ![image.png](./Tries.assets/20230302_0959495486.png)![image.png](./Tries.assets/20230302_0959497979.png)



## Autocomplete
### Problem Setting
> ![image.png](./Tries.assets/20230302_0959502622.png)


### Example
> ![image.png](./Tries.assets/20230302_0959502273.png)


### Flaw
> ![image.png](./Tries.assets/20230302_0959503589.png)




## Efficient Autocomplete
> ![image.png](./Tries.assets/20230302_0959504018.png)![image.png](./Tries.assets/20230302_0959502834.png)![image.png](./Tries.assets/20230302_0959503466.png)



# Tries Summary
> ![image.png](./Tries.assets/20230302_0959518179.png)![image.png](./Tries.assets/20230302_0959514877.png)


# Study Guide Exercises
[Tries Guide _ CS 61B Spring 2019.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1676795513574-8b2dfc82-244f-4d5f-8be6-9ac008c61dba.pdf)
