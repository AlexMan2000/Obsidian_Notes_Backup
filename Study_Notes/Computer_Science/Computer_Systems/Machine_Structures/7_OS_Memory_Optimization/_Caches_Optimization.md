# Basic Concepts
## Memory Hierarchy
> ![image.png](./_Caches_Optimization.assets/20231024_0931079457.png)



## Principle of Locality
> ![image.png](./_Caches_Optimization.assets/20231024_0931081183.png)![image.png](./_Caches_Optimization.assets/20231024_0931106994.png)![image.png](./_Caches_Optimization.assets/20231024_0931126599.png)



## Cache Concepts
> ![image.png](./_Caches_Optimization.assets/20231024_0931125759.png)![image.png](./_Caches_Optimization.assets/20231024_0931122114.png)



## Cache Hierarchy
> ![image.png](./_Caches_Optimization.assets/20231024_0931132885.png)![image.png](./_Caches_Optimization.assets/20231024_0931163978.png)![image.png](./_Caches_Optimization.assets/20231024_0931177674.png)


## TIO Breakdown
> ![image.png](./_Caches_Optimization.assets/20231024_0931206051.png)



## Cache Parameters
> ![image.png](./_Caches_Optimization.assets/20231024_0931209953.png)![image.png](./_Caches_Optimization.assets/20231024_0931219487.png)![image.png](./_Caches_Optimization.assets/20231024_0931222204.png)



# Cache Read/Writes/LRU
## Cache Read Procedure
> ![image.png](./_Caches_Optimization.assets/20231024_0931231800.png)



## Cache Read
### Read Hits
> 就是根据上面的流程读取到了数据。


### Read Misses - Three Types
> ![image.png](./_Caches_Optimization.assets/20231024_0931266493.png)![image.png](./_Caches_Optimization.assets/20231024_0931271449.png)![image.png](./_Caches_Optimization.assets/20231024_0931294333.png)


### Example -  P6.12 ~ P6.15 
> ![image.png](./_Caches_Optimization.assets/20231024_0931327007.png)


#### P6.12 - TIO Breakdown
> ![image.png](./_Caches_Optimization.assets/20231024_0931337903.png)![image.png](./_Caches_Optimization.assets/20231024_0931352874.png)![image.png](./_Caches_Optimization.assets/20231024_0931369097.png)




#### P6.13 - Cache Read 
> ![image.png](./_Caches_Optimization.assets/20231024_0931371280.png)![image.png](./_Caches_Optimization.assets/20231024_0931393390.png)![image.png](./_Caches_Optimization.assets/20231024_0931397101.png)



#### P6.14 - Cache Read
> ![image.png](./_Caches_Optimization.assets/20231024_0931403596.png)![image.png](./_Caches_Optimization.assets/20231024_0931415610.png)




#### P6.15 - Cache Read
> ![image.png](./_Caches_Optimization.assets/20231024_0931429561.png)![image.png](./_Caches_Optimization.assets/20231024_0931434898.png)![image.png](./_Caches_Optimization.assets/20231024_0931446130.png)![image.png](./_Caches_Optimization.assets/20231024_0931459215.png)




## Cache Writes
### Write Hits
> 就是根据上面的流程读取到了数据。


#### Write-Through
> ![image.png](./_Caches_Optimization.assets/20231024_0931465284.png)



#### Write-Back Policy
> ![image.png](./_Caches_Optimization.assets/20231024_0931477251.png)



### Write Misses
> ![image.png](./_Caches_Optimization.assets/20231024_0931496260.png)


#### (No)Write Allocate
> ![image.png](./_Caches_Optimization.assets/20231024_0931516246.png)


### Replacement Policy
> ![image.png](./_Caches_Optimization.assets/20231024_0931525026.png)![image.png](./_Caches_Optimization.assets/20231024_0931534347.png)
> 一般而言我们可以将`LRU Bits`简单的理解为一个`Priority`, 最近访问的(`Read/Write`)的数值小，越不常访问的数值越大。

 


## AWAT Analysis
> ![image.png](./_Caches_Optimization.assets/20231024_0931552013.png)![image.png](./_Caches_Optimization.assets/20231024_0931573170.png)![image.png](./_Caches_Optimization.assets/20231024_0931588328.png)![image.png](./_Caches_Optimization.assets/20231024_0931598475.png)



# Three Types of Cache
## Type 1: Fully-Associative Cache
### Memory Address Breakdown
> ![image.png](./_Caches_Optimization.assets/20231024_0932004639.png)


### Structure
> ![image.png](./_Caches_Optimization.assets/20231024_0932033804.png)



### Bits to Construct
> ![image.png](./_Caches_Optimization.assets/20231024_0932041566.png)![image.png](./_Caches_Optimization.assets/20231024_0932097507.png)




## Type 2: Direct-Mapped Cache
### Memory Address Breakdown
> ![image.png](./_Caches_Optimization.assets/20231024_0932108568.png)**为什么要用**`**Middle Bits**`**作为**`**Index Bits**`**呢?**
> ![image.png](./_Caches_Optimization.assets/20231024_0932127002.png)



### Structure
> ![image.png](./_Caches_Optimization.assets/20231024_0932131122.png)



### Bits to Construct
> ![image.png](./_Caches_Optimization.assets/20231024_0932154398.png)


## Type 3: Set Associative Cache
### Memory Address Breakdown
> ![image.png](./_Caches_Optimization.assets/20231024_0932179122.png)![image.png](./_Caches_Optimization.assets/20231024_0932193857.png)



### Structure
> ![image.png](./_Caches_Optimization.assets/20231024_0932209239.png)



### Bits to Construct
> ![image.png](./_Caches_Optimization.assets/20231024_0932221828.png)



## How to Understand - HashTable
> ![image.png](./_Caches_Optimization.assets/20231024_0932242477.png)![image.png](./_Caches_Optimization.assets/20231024_0932255252.png)



## Associativity Analysis
> ![image.png](./_Caches_Optimization.assets/20231024_0932275145.png)![image.png](./_Caches_Optimization.assets/20231024_0932296415.png)



## Cache Miss Analysis - Disc09 Su20
> ![image.png](./_Caches_Optimization.assets/20231024_0932308307.png)![image.png](./_Caches_Optimization.assets/20231024_0932315546.png)![image.png](./_Caches_Optimization.assets/20231024_0932333510.png)![image.png](./_Caches_Optimization.assets/20231024_0932341519.png)




## Concept Check
> ![image.png](./_Caches_Optimization.assets/20231024_0932357308.png)



# Multi-Level Caches
## Multilevel Cache Diagram
> ![image.png](./_Caches_Optimization.assets/20231024_0932379034.png)![image.png](./_Caches_Optimization.assets/20231024_0932392474.png)



## Multi-Level AWAT Analysis
> ![image.png](./_Caches_Optimization.assets/20231024_0932415864.png)![image.png](./_Caches_Optimization.assets/20231024_0932436428.png)



## Local vs Global Miss Rate
> ![image.png](./_Caches_Optimization.assets/20231024_0932457296.png)
> `Global Miss Rate`就是将括号打开的过程，将所有`Level`的`Miss Rate`相乘得到。
> ![image.png](./_Caches_Optimization.assets/20231024_0932463323.png)![image.png](./_Caches_Optimization.assets/20231024_0932468541.png)




## Rewriting Performance
> ![image.png](./_Caches_Optimization.assets/20231024_0932488570.png)




# Writing Cache-Friendly Codes
## Repeated Reference/Stride-k
> ![image.png](./_Caches_Optimization.assets/20231024_0932491180.png)
> 假设我们的`Cache`参数如下:
> 1. Fully Associative Cache
> 2. Cache Size: 16 bytes
> 3. Block Size: 16 bytes
> 
则当我们访问`v[0]`时, `v[0],v[1],v[2],v[3]`会被加载到缓存中。如果我们的`Stride`是`1`的话，则第一个`miss`过后，后三次访问都是`Hit`，最终我们会达到如下所示的状态:
> ![image.png](./_Caches_Optimization.assets/20231024_0932509582.png)![image.png](./_Caches_Optimization.assets/20231024_0932519231.png)
> 总的来说，`Strike`越小，`Block Size`越大，`Hit Rate`就会越高。
> ![image.png](./_Caches_Optimization.assets/20231024_0932528153.png)




## Matrix Access Order
### Row Major Order
> ![image.png](./_Caches_Optimization.assets/20231024_0932537343.png)



### Column Major Order
> ![image.png](./_Caches_Optimization.assets/20231024_0932542598.png)




## Matrix Transpose
### P6.17 - 2 x 2 - 16 bytes cache
> ![image.png](./_Caches_Optimization.assets/20231024_0932554065.png)![image.png](./_Caches_Optimization.assets/20231024_0932565707.png)![image.png](./_Caches_Optimization.assets/20231024_0932587988.png)
> 本题根据内存地址和缓存的结构可以判断出，`src`和`dst`的相同行会映射到相同的`Cache Set`中。



### P6.34 - 4 x 4 - 32 bytes cache
> ![image.png](./_Caches_Optimization.assets/20231024_0932582934.png)![image.png](./_Caches_Optimization.assets/20231024_0933009533.png)
> 本题根据内存地址和缓存的结构可以判断出，`src`和`dst`的相同行会映射到相同的`Cache Set`中。
> ![image.png](./_Caches_Optimization.assets/20231024_0933026915.png)

```c

初始状态
0:
1:

i = 0, j = 0
读取src[0][0](m)
0: src[0][0], src[0][1], src[0][2], src[0][3]
1:

赋值dst[0][0](m)
0: dst[0][0], dst[0][1], dst[0][2], dst[0][3]
1:

i = 0, j = 1
读取src[0][1](m)
0: src[0][0], src[0][1], src[0][2], src[0][3]
1:

赋值dst[1][0](m)
0: src[0][0], src[0][1], src[0][2], src[0][3]
1: dst[1][0], dst[1][1], dst[1][2], dst[1][3]

i = 0, j = 2
读取src[0][2](h)
0: src[0][0], src[0][1], src[0][2], src[0][3]
1: dst[1][0], dst[1][1], dst[1][2], dst[1][3]

赋值dst[2][0](m)
0: dst[2][0], dst[2][1], dst[2][2], dst[2][3]
1: dst[1][0], dst[1][1], dst[1][2], dst[1][3]

i = 0, j = 3
读取src[0][3](m)
0: src[0][0], src[0][1], src[0][2], src[0][3]
1: dst[2][0], dst[2][1], dst[2][2], dst[2][3]

赋值dst[3][0](m)
0: src[0][0], src[0][1], src[0][2], src[0][3]
1: dst[3][0], dst[3][1], dst[3][2], dst[3][3]
```
```c
初始状态
0: src[0][0], src[0][1], src[0][2], src[0][3]
1: dst[3][0], dst[3][1], dst[3][2], dst[3][3]

i = 1, j = 0
读取src[1][0](m)
0: src[0][0], src[0][1], src[0][2], src[0][3]
1: src[1][0], src[1][1], src[1][2], src[1][3]

赋值dst[0][1](m)
0: dst[0][0], dst[0][1], dst[0][2], dst[0][3]
1: src[1][0], src[1][1], src[1][2], src[1][3]

i = 1, j = 1
读取src[1][1](h)
0: dst[0][0], dst[0][1], dst[0][2], dst[0][3]
1: src[1][0], src[1][1], src[1][2], src[1][3]

赋值dst[1][1](m)
0: dst[0][0], dst[0][1], dst[0][2], dst[0][3]
1: dst[1][0], dst[1][1], dst[1][2], dst[1][3]

i = 1, j = 2
读取src[1][2](m)
0: dst[0][0], dst[0][1], dst[0][2], dst[0][3]
1: src[1][0], src[1][1], src[1][2], src[1][3]

赋值dst[2][1](m)
0: dst[2][0], dst[2][1], dst[2][2], dst[2][3]
1: src[1][0], src[1][1], src[1][2], src[1][3]

i = 1, j = 3
读取src[1][3](h)
0: dst[2][0], dst[2][1], dst[2][2], dst[2][3]
1: src[1][0], src[1][1], src[1][2], src[1][3]

赋值dst[3][1](m)
0: dst[2][0], dst[2][1], dst[2][2], dst[2][3]
1: dst[3][0], dst[3][1], dst[3][2], dst[3][3]
```



### P6.35 - 4 x 4 - 128 bytes cache
> ![image.png](./_Caches_Optimization.assets/20231024_0933032487.png)![image.png](./_Caches_Optimization.assets/20231024_0933056949.png)




## MM Spatial Locality
> ![image.png](./_Caches_Optimization.assets/20231024_0933069964.png)![image.png](./_Caches_Optimization.assets/20231024_0933077329.png)



### ijk Implementation
> ![image.png](./_Caches_Optimization.assets/20231024_0933087221.png)



### jik Implementation
> ![image.png](./_Caches_Optimization.assets/20231024_0933111477.png)




### kij Implementation
> ![image.png](./_Caches_Optimization.assets/20231024_0933129369.png)



### ikj Implementation
> ![image.png](./_Caches_Optimization.assets/20231024_0933131178.png)


### jki Implementation
> ![image.png](./_Caches_Optimization.assets/20231024_0933131950.png)


### kji Implementation
> ![image.png](./_Caches_Optimization.assets/20231024_0933141752.png)


### Summary
> ![image.png](./_Caches_Optimization.assets/20231024_0933156635.png)



## MM Temporal Locality
### Without Blocking
> ![image.png](./_Caches_Optimization.assets/20231024_0933154021.png)
> 这里我们将矩阵使用`1-dimensional array`来表示。
> ![image.png](./_Caches_Optimization.assets/20231024_0933168941.png)![image.png](./_Caches_Optimization.assets/20231024_0933174708.png)


### With Blocking
> ![image.png](./_Caches_Optimization.assets/20231024_0933196544.png)![image.png](./_Caches_Optimization.assets/20231024_0933204046.png)![image.png](./_Caches_Optimization.assets/20231024_0933224850.png)



### Summary
> ![image.png](./_Caches_Optimization.assets/20231024_0933231040.png)



# Code Analysis
## Cache Parameter Analysis
### Example 1: High-Order DMC - P6.11
> ![image.png](./_Caches_Optimization.assets/20231024_0933427677.png)![image.png](./_Caches_Optimization.assets/20231024_0933457001.png)



## Hit/Miss Rate Analysis
### Ex1: Dot Product - P 6.10
> ![image.png](./_Caches_Optimization.assets/20231024_0933459477.png)![image.png](./_Caches_Optimization.assets/20231024_0933461417.png)
> 下面是解析:
> 首先对于`x[0]`和`y[0]`, 因为此时`Cache`还是空的，所以一定会造成`Compulsory Miss`。然后对于`x[5]`和`y[5]`来说，此时会发生`Conflict Miss`, 其余的都是`Cache Hit`, 所以总共`16`次读取操作，其中`12`次`Hit`, 所以`Hit Rate`是$\frac{12}{16}=\frac{3}{4}$。
> ![image.png](./_Caches_Optimization.assets/20231024_0933479218.png)



### Ex2: Loop Analysis - Disc09 Su20
> ![image.png](./_Caches_Optimization.assets/20231024_0933503432.png)



### Ex3: Cache Parameters on Performance
> ![image.png](./_Caches_Optimization.assets/20231024_0933517912.png)![image.png](./_Caches_Optimization.assets/20231024_0933536317.png)![image.png](./_Caches_Optimization.assets/20231024_0933548150.png)



### Ex4: Complicated - P6.37
> ![image.png](./_Caches_Optimization.assets/20231024_0933542928.png)![image.png](./_Caches_Optimization.assets/20231024_0933567085.png)![image.png](./_Caches_Optimization.assets/20231024_0933585455.png)


#### N = 64(Medium)
> ![image.png](./_Caches_Optimization.assets/20231024_0934019183.png)
> `sumC`中的改变在于，`a[i][j]`和`a[i][j+1]`，`a[i+1][j]`和`a[i+1][j+1]`读取的是同一个`Block`中的数据，所以一定是一个`Miss`和一个`Hit`。也就是四个`Miss`里面有两次`Hit`。



#### *N = 60(Hard)
##### sumA
> 



##### sumB
> 



##### sumC
> 



### *Ex5: Loop+ MultiLevel MT2 Su20
> ![image.png](./_Caches_Optimization.assets/20231024_0934022938.png)
> 我们可以画出下面的流程图:
> ![image.png](./_Caches_Optimization.assets/20231024_0934046012.png)
> 所以我们可以很容易得到$\frac{62}{63\times 3}=\frac{62}{189}$。
> ![image.png](./_Caches_Optimization.assets/20231024_0934055149.png)
> 其实我们发现，当`Set-Associativity`大于等于`2`的时候，至少在每次循环内我们都能顺利的读取`A`和`B`的数据进入`Cache`。但是如果`Set-Associativity = 1`，则每次循环中:
> 1. `A[i+16]`永远是`Compulsory Miss`
> 2. `B[i]`就会变成`Conflict Miss`
> 3. `A[i]`也会变成`Conflict Miss`
> 
这直接导致了`Hit Rate = 0`。
> ![image.png](./_Caches_Optimization.assets/20231024_0934067367.png)![image.png](./_Caches_Optimization.assets/20231024_0934074143.png)




### Ex6: Struct - P6.38 ~ P6.40
> ![image.png](./_Caches_Optimization.assets/20231024_0934082142.png)![image.png](./_Caches_Optimization.assets/20231024_0934097023.png)



#### Row Major Access
> ![image.png](./_Caches_Optimization.assets/20231024_0934107506.png)![image.png](./_Caches_Optimization.assets/20231024_0934122148.png)



#### Column Major Access
> ![image.png](./_Caches_Optimization.assets/20231024_0934126510.png)![image.png](./_Caches_Optimization.assets/20231024_0934153211.png)![image.png](./_Caches_Optimization.assets/20231024_0934168539.png)




#### Splitwise Access
> ![image.png](./_Caches_Optimization.assets/20231024_0934195966.png)![image.png](./_Caches_Optimization.assets/20231024_0934199463.png)B.
> 对于第一个循环，每一次写入都会发生miss的情况，最后cache中保存的是square[0][0] ~ square[3][15]，而第二个循环又从头开始写入，所以每三次写入的第一次都会发生miss。总的miss次数就是16 * 16 * 2 = 512。
> C.
> (1024 - 512) / 1024 = 50%

