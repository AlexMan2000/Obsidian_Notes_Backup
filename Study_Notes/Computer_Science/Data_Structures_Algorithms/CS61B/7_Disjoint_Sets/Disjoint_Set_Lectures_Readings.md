[cs61b 2019 lec14 ds1 disjoint sets.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1675587758529-101d5dec-8711-4091-b170-108fced3f265.pdf)
# 1 Basic Operations
## What Use?
> Used for solving the dynamic connectivity problem.


## Disjoint Set Data Structure
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951292892.png)
> **Useful for many purposes, e.g.:**
> ● Percolation theory:
> ○ Computational chemistry.
> ● Implementation of other algorithms:
> ○Kruskal’s algorithm.



## Disjoint Set on Integers
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951296726.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951299705.png)



## DS Interface
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951299254.png)

**Set Implementation**![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951298480.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951305392.png)
```java
public interface DisjointSets {
    /** connects two items P and Q */
    void connect(int p, int q);

    /** checks to see if two items are connected */
    boolean isConnected(int p, int q); 
}
```

## List of Sets Implementation
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951301300.png)


## Performace
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951306532.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951309673.png)
> `connect`是$O(N)$而不是$\Theta(N)$是因为我们可能不需要遍历所有的`Set<Integer>`就能找到目标`p`和`q`, 然后执行一个耗时$\Theta(1)$的`Set Merge`操作。


# 2 Quick Find - better find
> 上一节中的`ListofSets Implementation`效率不是很高，本小节中我们将探讨如何优化`connect`或者`isConnected`过程。

### 
## Array Implementation
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951302161.png)

**Walkthrough**![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951303494.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951304978.png)

## Code Implementation
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951306835.png)
> `isConnected(p,q)`costs constant time，只需要两次`Random Access`即可。
> `connect(p,q)` is $\Theta(N)$, since we have to iterate through all elements in the array no matter the input so as to find all the `id[i] == p`. 注意不是$O(N)$因为无论所有的`input array`, 都需要**完整遍历**确保找到所有满足`id[i]==p`的`i`。

```java
public class QuickFindDS implements DisjointSets {

    private int[] id;

    /* Θ(N) */
    public QuickFindDS(int N){
        id = new int[N];
        for (int i = 0; i < N; i++){
            id[i] = i;
        }
    }

    /* need to iterate through the array => Θ(N) */
    public void connect(int p, int q){
        int pid = id[p];
        int qid = id[q];
        for (int i = 0; i < id.length; i++){
            if (id[i] == pid){
                id[i] = qid;
            }
        }
    }

    /* Θ(1) */
    public boolean isConnected(int p, int q){
        return (id[p] == id[q]);
    }
}
```


## Performance
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951302603.png)


# 3 Quick Union - better union
## Recap
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951317448.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951316615.png)



## Tree Implementation
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951317554.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951318483.png)
> `-1`是根节点，表示当前`Element`没有`Parent`
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951313327.png)
> 简单来说就是找到各自的`root`, 然后将`p`的`root`的`parent`设置成`q`的`root`

```java
public class QuickUnionDS implements DisjointSets {
    private int[] parent;

    public QuickUnionDS(int num) {
        parent = new int[num];
        for (int i = 0; i < num; i++) {
            parent[i] = i;
        }
    }

    private int find(int p) {
        while (parent[p] >= 0) {
            p = parent[p];
        }
        return p;
    }


    /*
    * It relies on find(), so also takes Θ(N)
    */
    @Override
    public void connect(int p, int q) {
        int i = find(p);
        int j= find(q);
        parent[i] = j;
    }

    @Override
    public boolean isConnected(int p, int q) {
        return find(p) == find(q);
    }
}
```


## Performance Analysis
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951311656.png)
> The worst case run time (when the tree is flattened to a linked list structure) is $\Theta(N)$(can reach $N$upper bound) and the run time is thus $O(N)$(less than the upper bound $N$, may not reach)



## Comparison
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951313877.png)
> 重点是要记住, `QU`的时间复杂度是$O(H)$,  其中$H$是树的高度。 


# 4 Weighted Quick Union
## Warmup Exercise
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951314140.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951325923.png)

**Example**![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951323874.png)

## Improvements
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951323692.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951328939.png)
> Weighted Union is better than height-based union.



## Weighted Implementation
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951323442.png)
> Code Implementation explained in Lab1906




## Performance Analysis
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951321838.png)
> 简单来说，就是每次我们`double the size of the nodes`, 我们的最大深度就会增加`1`, 但是`double`的操作只能重复不超过$log_2N$次，也就是$O(log_2N)$次，所以我们的最大高度就是$log_2N$。
> 重点是要记住, `QU`的时间复杂度是$O(H)$,  其中$H$是树的高度。 

**Graphical Walkthrough - Worst Case - Grow as fast as possible**![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951325874.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951327882.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951334819.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951336002.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951334552.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951334386.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951336266.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951334282.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951335156.png)
> 读者可能会想，为什么不是$\Theta(logN)$, 因为在`connect`操作的时候，我们可以选择一种让树的高度增长非常慢的方式，就是将所有新的节点都和`root`相连，这样即便我们有再多的`Node`($N$再大)，高度也只有$1$，这显然小于$logN$，于是用$O(logN)$表示更好。


## Comparison
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951338757.png)


# 5 WQU with Path Compression
## Recap
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951336775.png)
> `M`就是`connect()`或者`isConnect()`操作


## Path Compression
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951337551.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951339803.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951349599.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951342997.png)
> **要注意一点: **`**Path Compression**`**是通过**`**find**`**来实现的，而**`**find**`**会将沿途的而所有节点和当前节点的根节点相连，而不是和新的根节点相连, 这里很容易出错。**

**Exercise**![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951346444.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951342106.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951349798.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951344422.png)


## Performance
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951344167.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951343240.png)



# 6 Summary
> ![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951342645.png)![image.png](Disjoint_Set_Lectures_Readings.assets/20230302_0951354992.png)


# 7 Study Guide Exercises
[Disjoint Sets Study Guide _ CS 61B Spring 2019.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1675587783734-f2720625-835b-43a3-967c-9b561e42f00a.pdf)




