[cs61b 2019 ds5 lec19 hashing.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1676200887582-01689eb9-ff90-430c-b3f6-44d5dbaf794d.pdf)
[cs61b 2018 ds4 lec23 hashing.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1676775744779-3ce9e424-b533-4325-abf7-69d9ccc9a10d.pdf)
> Prereq: [L2107__BSTMap](../8_Balanced_Search_Trees/L2107__BSTMap.md)


# Recap⭐⭐⭐⭐⭐
> ![image.png](Data_Indexed_Set.assets/20230302_0956088226.png)![image.png](Data_Indexed_Set.assets/20230302_0956087892.png)


# Data Indexed Integer Set
## Goal
> ![image.png](Data_Indexed_Set.assets/20230302_0956098606.png)


## Implementation
> ![image.png](Data_Indexed_Set.assets/20230302_0956094687.png)



## Summary
> ![image.png](Data_Indexed_Set.assets/20230302_0956092598.png)



# Data Indexed English Words Set
## Goal
> ![image.png](Data_Indexed_Set.assets/20230302_0956097747.png)



## Choice of Key
### Initial Character
> ![image.png](Data_Indexed_Set.assets/20230302_0956104371.png)![image.png](Data_Indexed_Set.assets/20230302_0956105085.png)



### Decmial and Strings
> ![image.png](Data_Indexed_Set.assets/20230302_0956101819.png)

**Exercise**![image.png](Data_Indexed_Set.assets/20230302_0956104710.png)![image.png](Data_Indexed_Set.assets/20230302_0956104281.png)

### Uniqueness - Large Base
> ![image.png](Data_Indexed_Set.assets/20230302_0956108184.png)


## StringToInt⭐⭐⭐⭐⭐
> ![image.png](Data_Indexed_Set.assets/20230302_0956107404.png)![image.png](Data_Indexed_Set.assets/20230302_0956108394.png)

**Implemetation**![image.png](Data_Indexed_Set.assets/20230302_0956108508.png)![image.png](Data_Indexed_Set.assets/20230302_0956118467.png)



# Binary Representation
## Decimal Number System
> ![image.png](Data_Indexed_Set.assets/20230302_0956119836.png)




## Binary Number System
> ![image.png](Data_Indexed_Set.assets/20230302_0956116333.png)![image.png](Data_Indexed_Set.assets/20230302_0956116823.png)





# Data Indexed String Sets
## Goal
> ![image.png](Data_Indexed_Set.assets/20230302_0956114543.png)


## Using ASCII
> ![image.png](Data_Indexed_Set.assets/20230302_0956111851.png)![image.png](Data_Indexed_Set.assets/20230302_0956117623.png)


## ASCII To Int
> ![image.png](Data_Indexed_Set.assets/20230302_0956115135.png)
> 注意`s.charAt(i)`返回的是`char`类型，但是`intRep`是`int`类型，所以做运算的时候会默认将`char`转成`ASCII`表示下的`int`类型。



## Unicode - Beyong ASCII
> ![image.png](Data_Indexed_Set.assets/20230302_0956123086.png)![image.png](Data_Indexed_Set.assets/20230302_0956124758.png)



# Integer Overflow
## Collision Problem by Overflow
> ![image.png](Data_Indexed_Set.assets/20230302_0956124425.png)![image.png](Data_Indexed_Set.assets/20230302_0956122634.png)



## HashCode and Pigeonhole Principle
> ![image.png](Data_Indexed_Set.assets/20230302_0956125497.png)



## Challenges of Collision
> ![image.png](Data_Indexed_Set.assets/20230302_0956122363.png)


