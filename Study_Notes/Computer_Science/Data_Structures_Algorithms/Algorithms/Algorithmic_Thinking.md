# Ingredients of Algorithmic Thinking
## Algorithm
> [!def]
> ![](Algorithmic_Thinking.assets/image-20231209173918470.png)


## Correctness
> [!def]
> ![](Algorithmic_Thinking.assets/image-20231209173930707.png)



## Efficiency
> [!def]
> ![](Algorithmic_Thinking.assets/image-20231209173939984.png)![](Algorithmic_Thinking.assets/image-20231209173952906.png)






# Peak Finding 1D - Divide and Conquer
## Problem Settings
> [!example]
> ![](Algorithmic_Thinking.assets/image-20231208210006863.png)
> **Remarks:** Here we only need to find a peek if it exists. We don't need to find all the peaks, so we only need a simple divide and conquer strategy to solve it.


## Naive Algorithm
> [!algo] Search from Left
> The naive algorithm just search the whole list **from the left** for the peak, recall that the peak should satisfy the condition: it is bigger or equal to both its left and right neighbors.
> - Suppose there is only one peak and the position of the peak is discretely uniformly distributed across the whole array(i.e. $p_{I}(i)=\frac{1}{n}$), then we know that on average we have to go $\frac{1+2+\cdots +n}{n}$ elements(i.e. the expectation of random variable $I$), which is $\frac{n+1}{2}$.
> - But the worst case of the input array is that the peak is at the very end, so we could search the entire array.

> [!algo] Search from Middle
> ![](Algorithmic_Thinking.assets/image-20231208211129588.png)


## Divide and Conquer Algorithm
> [!algo] Better Algorithm
> ![](Algorithmic_Thinking.assets/image-20231208211303585.png)








# Peak Finding 2D
## Problem Setting
> [!example]
> ![](Algorithmic_Thinking.assets/image-20231208211400186.png)![](Algorithmic_Thinking.assets/image-20231208211557948.png)


## Attempt 1: Extended 1D Peak Finding
> [!bug] Attempt 1 Failed
> ![](Algorithmic_Thinking.assets/image-20231208211619340.png)


## Attempt 2: 2D Divide and Conquer
> [!success] Attempt 2 Succeeded
> ![](Algorithmic_Thinking.assets/image-20231208211755036.png)![](Algorithmic_Thinking.assets/image-20231208211800263.png)
> **Remarks:**
> The subtlety is where we choose the global maximum on column j. Could we instead choose 1D peak? The answer is no. 
> Suppose we have the following layout:
> $$\begin{array}{|c|c|c|c|}\hline 10 & 8 & 10 & 10 \\\hline 14 & 13 & 12 & 11 \\\hline 15 & 9 & 11 & 21 \\\hline 16 & 17 & 19 & 20 \\\hline\end{array}$$
> 1. We first pick the second column and choose 13 as our peak by 1D peak finding algorithm. Then since 13 < 14, we go left.
> 2. Then we pick 16 to be the peak on column 1, which is not the global peak.
> 3. The reasoning is that global peak implies local peak, while local peaks are not necessarily global peak.
> 4. Picking global peak along the column makes sure that the column direction is optimal so that we don't need to consider row direction any more, that's why we can proceed with using divide and conquer in the direction of columns.




# Peak Finding Codes and Proof - HW1 Fa11 P3
## Algorithm 1 - Recursive 
### Description
> [!code]
> ![](Algorithmic_Thinking.assets/image-20231209175633243.png)
```python
def algorithm1(problem, trace = None):  
    # if it's empty, we're done   
	if problem.numRow <= 0 or problem.numCol <= 0:  
        return None  
  
    # the recursive subproblem will involve half the number of columns  
    mid = problem.numCol // 2  
  
    # information about the two subproblems  
    (subStartR, subNumR) = (0, problem.numRow)  
    (subStartC1, subNumC1) = (0, mid)  
    (subStartC2, subNumC2) = (mid + 1, problem.numCol - (mid + 1))  
  
    subproblems = []  
    subproblems.append((subStartR, subStartC1, subNumR, subNumC1))  
    subproblems.append((subStartR, subStartC2, subNumR, subNumC2))  
  
    # get a list of all locations in the dividing column  
    divider = crossProduct(range(problem.numRow), [mid])  
  
    # find the maximum in the dividing column  
    bestLoc = problem.getMaximum(divider, trace)  
  
    # see if the maximum value we found on the dividing line has a better  
    # neighbor (which cannot be on the dividing line, because we know that    # this location is the best on the dividing line)    neighbor = problem.getBetterNeighbor(bestLoc, trace)  
  
    # this is a peak, so return it  
    if neighbor == bestLoc:  
        if not trace is None: trace.foundPeak(bestLoc)  
        return bestLoc  
     
    # otherwise, figure out which subproblem contains the neighbor, and  
    # recurse in that half    sub = problem.getSubproblemContaining(subproblems, neighbor)  
    if not trace is None: trace.setProblemDimensions(sub)  
    result = algorithm1(sub, trace)  
    return problem.getLocationInSelf(sub, result)
```


### Correctness Analysis
> [!proof] Correctness
> The algorithm one is just what has been mentioned in the lecture, we find the global maximum on the mid column and recurse on the sub matrices that contains the better neighbor of the global maximum.
> ![](Algorithmic_Thinking.assets/image-20231209175438579.png)

> [!proof] Proof for Correctness
> ![](Algorithmic_Thinking.assets/image-20231209191015641.png)![](Algorithmic_Thinking.assets/image-20231209191024057.png)![](Algorithmic_Thinking.assets/image-20231209191030157.png)




### Efficiency Analysis
> [!proof] Efficiency
> ![](Algorithmic_Thinking.assets/image-20231209190416170.png)




## Algorithm 2 - Greedy Ascent Algorithm
### Description
> [!code]
> ![](Algorithmic_Thinking.assets/image-20231209183732206.png)![](Algorithmic_Thinking.assets/image-20231209183739148.png)

```python
def algorithm2(problem, location = (0, 0), trace = None):  
    # if it's empty, we're done   
	if problem.numRow <= 0 or problem.numCol <= 0:  
        return None  
  
    nextLocation = problem.getBetterNeighbor(location, trace)  
  
    if nextLocation == location:  
        # there is no better neighbor, so return this peak  
        if not trace is None: trace.foundPeak(location)  
        return location  
    else:  
        # there is a better neighbor, so move to the neighbor and recurse  
        return algorithm2(problem, nextLocation, trace)
```


### Correctness Analysis
> [!proof] Correctness
> ![](Algorithmic_Thinking.assets/image-20231209175936849.png)


### Efficiency Analysis
> [!proof] Efficiency
> ![](Algorithmic_Thinking.assets/image-20231209190425105.png)![](Algorithmic_Thinking.assets/image-20231209190430046.png)







## Algorithm 3 - Incorrect Attempt
### Description
> [!code]
```python
def algorithm3(problem, bestSeen = None, trace = None):  
    # if it's empty, we're done   
	if problem.numRow <= 0 or problem.numCol <= 0:  
        return None  
  
    midRow = problem.numRow // 2  
    midCol = problem.numCol // 2  
  
    # first, get the list of all subproblems  
    subproblems = []  
  
    (subStartR1, subNumR1) = (0, midRow)  
    (subStartR2, subNumR2) = (midRow + 1, problem.numRow - (midRow + 1))  
    (subStartC1, subNumC1) = (0, midCol)  
    (subStartC2, subNumC2) = (midCol + 1, problem.numCol - (midCol + 1))  
  
    subproblems.append((subStartR1, subStartC1, subNumR1, subNumC1))  
    subproblems.append((subStartR1, subStartC2, subNumR1, subNumC2))  
    subproblems.append((subStartR2, subStartC1, subNumR2, subNumC1))  
    subproblems.append((subStartR2, subStartC2, subNumR2, subNumC2))  
  
    # find the best location on the cross (the middle row combined with the  
    # middle column)    cross = []  
  
    cross.extend(crossProduct([midRow], range(problem.numCol)))  
    cross.extend(crossProduct(range(problem.numRow), [midCol]))  
  
    crossLoc = problem.getMaximum(cross, trace)  
    neighbor = problem.getBetterNeighbor(crossLoc, trace)  
  
    # update the best we've seen so far based on this new maximum  
    if bestSeen is None or problem.get(neighbor) > problem.get(bestSeen):  
        bestSeen = neighbor  
        if not trace is None: trace.setBestSeen(bestSeen)  
  
    # return if we can't see any better neighbors  
    if neighbor == crossLoc:  
        if not trace is None: trace.foundPeak(crossLoc)  
        return crossLoc  
  
    # figure out which subproblem contains the largest number we've seen so  
    # far, and recurse    sub = problem.getSubproblemContaining(subproblems, bestSeen)  
    newBest = sub.getLocationInSelf(problem, bestSeen)  
    if not trace is None: trace.setProblemDimensions(sub)  
    result = algorithm3(sub, newBest, trace)  
    return problem.getLocationInSelf(sub, result)
```

### Counterexample
> [!proof] Incorrectness
> ![](Algorithmic_Thinking.assets/image-20231209193252933.png)





### Efficiency Analysis
> [!proof] Efficiency
> ![](Algorithmic_Thinking.assets/image-20231209190454090.png)



## Algorithm 4  - Kd Tree Algorithm
### Description
> [!code]
> This algorithm did something really smart, it alternates between rowSplit and columnSplit. 
> 
> Although the code structure for algorithm 1 and algorithm looks very alike, there is still some subtleties out there.
> 
> The most outstanding difference between algorithm 4 and algorithm is the newly defined variable `bestSeen`. The reason why we need to define this variable and pass along the recursive path is that if we have done a columnSplit at $c_1$ and we must have found a $(r_1,c_1)$ where $(r_1, c_1) > (r_n,c_1)\forall n=1,2,\cdots, m$ (global maximum of column $c_1$). Suppose then we find that $val(r_1,c_2)>val(r_1,c_1)$, then in algorithm 1 we will recurse on the subset of columns that contain $(r_1,c_2)$, and may still reach $(r_1,c_2)$ later on. In other words, we are not discarding the case where $(r_1,c_2)$ could be the peak. 
> 
> However in algorithm 4, at the next recursion step we switch to rowSplit. Suppose we rowSplit at $r_3$ and we must have found a global maximum on that row, let's say $(r_3,c_3)$ and if we have a better neighbor $(r_5,c_3)$(suppose $r_1<r_3<r_5$), where the subset of rows doesn't contain $(r_1,c_2)$, then at the next recursion step we may discard the probabilty that $(r_1,c_2)$ maybe the peak. So we have to maintain the value at this location to a variable and make it visible to all the subproblems.

```python
def algorithm4(problem, bestSeen = None, rowSplit = True, trace = None):  
    # if it's empty, we're done   
	if problem.numRow <= 0 or problem.numCol <= 0:  
        return None  
  
    subproblems = []  
    divider = []  
  
    if rowSplit:  
        # the recursive subproblem will involve half the number of rows  
        mid = problem.numRow // 2  
  
        # information about the two subproblems  
        (subStartR1, subNumR1) = (0, mid)  
        (subStartR2, subNumR2) = (mid + 1, problem.numRow - (mid + 1))  
        (subStartC, subNumC) = (0, problem.numCol)  
  
        subproblems.append((subStartR1, subStartC, subNumR1, subNumC))  
        subproblems.append((subStartR2, subStartC, subNumR2, subNumC))  
  
        # get a list of all locations in the dividing column  
        divider = crossProduct([mid], range(problem.numCol))  
    else:  
        # the recursive subproblem will involve half the number of columns  
        mid = problem.numCol // 2  
  
        # information about the two subproblems  
        (subStartR, subNumR) = (0, problem.numRow)  
        (subStartC1, subNumC1) = (0, mid)  
        (subStartC2, subNumC2) = (mid + 1, problem.numCol - (mid + 1))  
  
        subproblems.append((subStartR, subStartC1, subNumR, subNumC1))  
        subproblems.append((subStartR, subStartC2, subNumR, subNumC2))  
  
        # get a list of all locations in the dividing column  
        divider = crossProduct(range(problem.numRow), [mid])  
  
    # find the maximum in the dividing row or column  
    bestLoc = problem.getMaximum(divider, trace)  
    neighbor = problem.getBetterNeighbor(bestLoc, trace)  
  
    # update the best we've seen so far based on this new maximum  
    if bestSeen is None or problem.get(neighbor) > problem.get(bestSeen):  
        bestSeen = neighbor  
        if not trace is None: trace.setBestSeen(bestSeen)  
  
    # return when we know we've found a peak  
    if neighbor == bestLoc and problem.get(bestLoc) >= problem.get(bestSeen):  
        if not trace is None: trace.foundPeak(bestLoc)  
        return bestLoc  
  
    # figure out which subproblem contains the largest number we've seen so  
    # far, and recurse, alternating between splitting on rows and splitting    # on columns    sub = problem.getSubproblemContaining(subproblems, bestSeen)  
    newBest = sub.getLocationInSelf(problem, bestSeen)  
    if not trace is None: trace.setProblemDimensions(sub)  
    result = algorithm4(sub, newBest, not rowSplit, trace)  
    return problem.getLocationInSelf(sub, result)
```

### Correctness Analysis
> [!proof] Correctness
> ![](Algorithmic_Thinking.assets/image-20231209193210455.png)![](Algorithmic_Thinking.assets/image-20231209193218503.png)![](Algorithmic_Thinking.assets/image-20231209193224721.png)![](Algorithmic_Thinking.assets/image-20231209193230897.png)
> **Remarks:**
> 1. $val(r_2,c_2)\leq val(r_1,c_1)$ since the algorithm will update the `bestSeen` and finally return the `bestSeen`, so any result that's returned by the function should satisfy this, no matter it is peak or not.
> 2. All the elements that are examined(by checking the neighbors when we are on the dividing rows/columns) should be updated into `bestSeen` variable.



### Efficiency Analysis
> [!proof] Efficiency
> ![](Algorithmic_Thinking.assets/image-20231209190516010.png)


# Models of Computation
## Random Access Machine
> [!concept]
> ![](Algorithmic_Thinking.assets/image-20231208213723912.png)



## Pointer Machine
> [!concept]
> ![](Algorithmic_Thinking.assets/image-20231208213804993.png)![](Algorithmic_Thinking.assets/image-20231208213810383.png)



## Python Model
> [!important]
> ![](Algorithmic_Thinking.assets/image-20231208213827355.png)![](Algorithmic_Thinking.assets/image-20231208213838095.png)




# Asymptotics - Rec1/HW1 Fa11
## Concepts Review
> [!summary] Rec1 Sp20
> ![](Algorithmic_Thinking.assets/image-20231209170255314.png)





## Some Warmup Problems
> [!example] Good Examples
> 1. For $f(x)=x^{1.4}$, $g(x)=(1+sin(x))\cdot x^{1.5}+x^{1.4}$, we know that $sin(x)\in [-1,1]$, thus $g(x)\in [x^{1.4},2\cdot x^{1.5}+x^{1.4}]$. Now suppose $x\to \infty$, we know that $g(x)\geq x^{1.4}=f(x)$ and $g(x)\leq 2\cdot x^{1.5}+x^{1.4}\leq 2\cdot x^{1.5}+x^{1.5}=3\cdot x^{1.5}$, thus we cannot say that $g(x)=\Theta(\cdot)$ (the exponents are not the same). But we can say $g(x)=O(x^{1.5})$ and $g(x)=\Omega(f(x))$。
> 2. If $f(n)=10^{80}$, then $f(n)=\Theta(1)$.
> 3. If $f(n)=(20n)^7$, then $f(n)=\Theta(n^7)$, since we can find $a=1, b>20^7$ such that for $n\to \infty$, we have $a\cdot n^7\leq f(n)\leq b\cdot n^7$ 



## Natural Base
> [!example] Good Examples
> 1. $log(n^{100})=100log(n)=\Theta(logn)$.
> 2. $log_5(n)=\frac{logn}{log5}=\Theta(logn)$, where $logn$ means we can use any bases.
> 3. $log_{ln(5)}((logn)^{100})=100log_{ln(5)}(logn)=\frac{100\cdot log(logn)}{log(ln5)}=\Theta(log(logn))$
> 4. $log_{ln(5)}(log(n^{100}))=\frac{log(100log(n))}{log(ln(5))}=\frac{log(100)+log(log(n))}{log(ln(5))}=\Theta(log(logn))$
> 


## Factorial Log
> [!example] Good Examples
> **Some prelimiaries:** 
> 1. Let $g(N)$=$N\choose \frac{N}{2}$=$\frac{N!}{\frac{N}{2}! \frac{N}{2}!}$
> 2. Sterling Approximation: $N!\approx \sqrt{2\pi N}(\frac{N}{e})^N$
> 3. $log(g(n))=log(\frac{\sqrt{2\pi n}(\frac{n}{e})^n}{\sqrt{\pi n}(\frac{n}{2e})^{\frac{n}{2}}\cdot\sqrt{\pi n}(\frac{n}{2e})^\frac{n}{2}})=log(\sqrt{\frac{2}{\pi n}}2^n)=log(\frac{2^n}{\sqrt{n}})$


## Sort the Asymptotics
> [!example] PS1 Fa11
> ![](Algorithmic_Thinking.assets/image-20231209121057389.png)![](Algorithmic_Thinking.assets/image-20231209170554513.png)



## More Exercises - Sp20 Rec1
> [!example]
> ![](Algorithmic_Thinking.assets/image-20231209171326901.png)


# Recurrence Relation
> [!example] Fa11 HW1
> ![](Algorithmic_Thinking.assets/image-20231209172659449.png)![](Algorithmic_Thinking.assets/image-20231209172704493.png)![](Algorithmic_Thinking.assets/image-20231209172740415.png)![](Algorithmic_Thinking.assets/image-20231209173042975.png)



# Document Distance
## Problem Setting
> [!concept]
> ![](Algorithmic_Thinking.assets/image-20231208215529894.png)![](Algorithmic_Thinking.assets/image-20231208215541102.png)



## Document Distance Algorithm
> [!algo] List-Tuple Approach
> ![](Algorithmic_Thinking.assets/image-20231208215656429.png)![](Algorithmic_Thinking.assets/image-20231208215703215.png)



> [!algo] Dictionary Approach
> ![](Algorithmic_Thinking.assets/image-20231208220315567.png)


> [!summary]
> For each input file, a word-frequency vector is computed as follows:  
> 1. The specified file is read in 
> 2. It is converted into a list of alphanumeric "words". Here a "word" is a sequence of consecutive alphanumeric  characters.  Non-alphanumeric characters are treated as blanks. Case is not significant.  
> 3. For each word, its frequency of occurrence is determined  
> 4. The word/frequency lists are sorted into order alphabetically

# Document Finding Code Experiments - Rec2 Fa11
> [!code]
> ![](Algorithmic_Thinking.assets/image-20231208220350081.png)


## Concept Review
> [!example] 
> **Suppose we have two documents:**
> D1: The fox is in the hat.
> D2: The fox is outside.
> We first get the document dictionary for both documents:
> - The document dictionary for D1 should be [(The, 2), (fox, 1), (is, 1), (in, 1), (hat, 1)]
> - The document dictionary for D1 should be [(The, 1), (fox, 1), (is, 1), (outside, 1)]
> 
> Based on the word dictionary, we then compute the inner product of the document, where we only have to go through these entries with the same key.(i.e. The, fox, is, they appear in both documents). So the inner product should be $2\times 1+1\times 1+1\times 1=4$


## docdist1 - benchmark
### main function
> [!code]
> ![](Algorithmic_Thinking.assets/image-20231209093634382.png)![](Algorithmic_Thinking.assets/image-20231209093648130.png)

> [!example] Analysis
> We first look at the `main()` function, in order to figure out the runtime we have to know the asymtotics of `word_frequencies_for_file()` and `vector_angle()`.


### word_frequencies_for_file()
> [!example]
> ![](Algorithmic_Thinking.assets/image-20231209100232407.png)


#### get_words_from_string()
> [!code]
> ![](Algorithmic_Thinking.assets/image-20231209100349772.png)

> [!example] Line by Line Analysis
> We assume here that:
> 1. The length of a single line is $N$
> 2. The average length of a valid alphabatic word is $l$
> 3. The length of the word list of a single line(number of words per line) is $\frac{N}{l+1}$, since we append a word only when we encounter a non-alphabetic character, where we have already consume $w+1$ characters of a line(w is the word length, in characters, and 1 is the non-alpha, which acts as the delimiter).

| Line Number | Time for single run | How many times the line is run | Total Time|
| ----------- | ------------------- | -------------------------------- | ---|
| 9           | 1                   | 1                                | 1 |
| 10          | 1                   | 1                              | 1|
| 11          | 1                   | N                              | N|
| 12          | 1                   | N, need to check every loop  | N|
| 13          | 1                   | $N - \frac{1}{l+1}N=\frac{l}{l+1}N$               | $\Theta(N)$|
| 14          | 1                   | $\frac{1}{l+1}N$,  don't need to check every loop | $\Theta(N)$|
| 15          | $l$                   | $\frac{1}{l+1}N$                                  | $\Theta(N)$|
| 16          | 1                   | $\frac{1}{l+1}N$                                  |$\Theta(N)$|
| 17          | 1                   | $\frac{1}{l+1}N$                                  |$\Theta(N)$|
| 18          | 1                   | $\frac{1}{l+1}N$                                  |$\Theta(N)$|
| 19          | 1                    | 1                     |1|
| 20          |  $l$                   | 1           |$l$|
| 21          |  $l$                   |   1            |$l$|
| 22          | 1                    |   1           |1|
| 23            |   1                  |  1            |1|

> [!example] Summary
> In all, we have $O(N)$ times, where N is the length(number of characters) of a single line.



#### get_words_from_line_list()
> [!code]
> ![](Algorithmic_Thinking.assets/image-20231209102753583.png)

> [!example] Line by Line Analysis
> Here we assume that:
> 1. The length of a single line is $N$
> 2. The length of a valid alphabatic word is $l$
> 2. We have $W$ words in the document file.
> 3. We have $k=\frac{N}{l}$ words in a line.
> 4. We have $z=\frac{W}{k}$ lines in the document file.
> 5. In python, performing L1 + L2 is $\Theta(|L_1|+|L_2|+1)$, which si really time consuming. So use extend instead of $+$ operator.

| Line Number | Time for single run | How many times the line is run | Total Time|
| ----------- | ------------------- | -------------------------------- | ---|
| 2           | 1                   | 1                                | 1 |
| 3          | 1                   |  z                             | z|
| 4          | $O(N)$                   | z                              | $O(N)$|
| 5          | Depends on # words in a line                   | z  | $k + 2k+\cdots+zk=\frac{z(z+1)}{2}k=O(z^2k)=O(\frac{W^2}{k})$|
| 6          | 1                   | 1              | 1|

#### count_frequency()
> [!code]
> ![](Algorithmic_Thinking.assets/image-20231209104347582.png)

> [!example] Line by Line Analysis
> Here we assume:
> 1. We have $W$ words in total in the document file.
> 2. Each word on average has length $l$.
> 3. $L$ is the total number of unique words.
> 
> ![](Algorithmic_Thinking.assets/image-20231209105837610.png)

| Line Number | Time for single run | How many times the line is run | Total Time                                                    |
| ----------- | ------------------- | ------------------------------ | ------------------------------------------------------------- |
| 2           | 1                   | 1                              | 1                                                              |
| 3           | 1                   | W                              | W                                                             |
| 4           | 1                   | $O(WL)$        | $O(WL)$                                                        |
| 5           | $l$                   | $O(WL)$                              | $O(WL\times l)$ |
| 6           | 1                   | It depends on the document structure.     | Overall it should not exceed $O(WL\times l)$                                                            |
| 7           | 1                    | It depends on the document structure.   |  Overall it should not exceed $O(WL\times l)$     |
| 8           | 1                    | It depends on the document structure.     |  Overall it should not exceed $O(WL\times l)$  |
| 9           | 1                    | It depends on the document structure.                                |       Overall it should not exceed $O(WL\times l)$   |
| 10            |    1                 |     1                           |   1                                                            |

### vector_angle()
> [!code]
> ![](Algorithmic_Thinking.assets/image-20231209105958251.png)

> [!example] Line By Line Analysis - Inner Product
> Here we assume that the length of list L1 and L2 are respectively $L1$ and $L2$.

| Line Number | Time for single run | How many times the line is run        | Total Time                                    |
| ----------- | ------------------- | ------------------------------------- | --------------------------------------------- |
| 2           | 1                   | 1                                   | 1                                            |
| 3           | 1                   | L1                        | L1                                |
| 4           | 1                   | $L1\times L2$               | $L1\times L2$             |
| 5           | 1                | $L1\times L2$            | $L1\times L2$                 |
| 6           | 1         | It depends on the document structure. | Overall it should not exceed $\Theta(L1\times L2)$ |
| 7           | 1                   | 1 | 1|


### Summary
> [!summary]
> ![](Algorithmic_Thinking.assets/image-20231209110132695.png)


Profiling Test
> [!test]
> ![](Algorithmic_Thinking.assets/image-20231209113228198.png)
> We see that we can improve on the word_frequency_for_file() later.




## docdist2 - Improve Concatenation
> [!algo] Improvements on List Concatenation
> ![](Algorithmic_Thinking.assets/image-20231209112220078.png)![](Algorithmic_Thinking.assets/image-20231209112225869.png)

> [!example] Line by Line Analysis for get_words_from_line_list()
> Here we assume that:
> 1. The length of a single line is $N$ on average.
> 2. The length of a valid alphabatic word is $l$
> 2. We have $W$ words in the document file.
> 3. We have $k=\frac{N}{l}$ words in a line.
> 4. We have $z=\frac{W}{k}$ lines in the document file.
> 5. In python, performing L1 + L2 is $\Theta(|L_1|+|L_2|+1)$, which si really time consuming. So use extend instead of $+$ operator.

| Line Number | Time for single run | How many times the line is run | Total Time|
| ----------- | ------------------- | -------------------------------- | ---|
| 2           | 1                   | 1                                | 1 |
| 3          | 1                   |  z                             | z|
| 4          | $O(N)$                   | z                              | $O(N)$|
| 5          | Depends on # words in a line               | z  | $O(z{k})=O(\frac{W}{k}\times k)=O(W)$|
| 6          | 1                   | 1              | 1|

> [!test] Profiling
> ![](Algorithmic_Thinking.assets/image-20231209113136459.png)
> We see that we can further improve the code at inner_product() and count_frequency(), which take a little more time than other function calls.



## docdist3 - Utilizing Sorting Algorithms
> [!algo]
> ![](Algorithmic_Thinking.assets/image-20231209113442577.png)![](Algorithmic_Thinking.assets/image-20231209113508905.png)



## docdist4 - Python Dictionary
> [!algo]
> ![](Algorithmic_Thinking.assets/image-20231209114118794.png)![](Algorithmic_Thinking.assets/image-20231209114123978.png)

> [!example] Line by Line Analysis - count_frequency()
> 
> [!example] Line by Line Analysis
> Here we assume:
> 1. We have $W$ words in total in the document file.
> 2. Each word on average has length $l$.
> 3. $L$ is the total number of unique words.

| Line Number | Time for single run | How many times the line is run | Total Time                                                    |
| ----------- | ------------------- | ------------------------------ | ------------------------------------------------------------- |
| 2           | 1                   | 1                              | 1                                                              |
| 3           | 1                   | W                              | W                                                             |
| 4           | 1                   | $W$        | $O(W)$                                                        |
| 5           | $1$                   | $O(W)$               | $O(W)$ |
| 6           | 1                   | It depends on the document structure.     | Overall it should not exceed $O(W)$                                                            |
| 7           | 1                    | It depends on the document structure.   |  Overall it should not exceed $O(W)$     |
| 8           | 1                    | 1   |  1 |

## docdist5 - Speed up line split(Python 2)
> [!algo]
> ![](Algorithmic_Thinking.assets/image-20231209115803465.png)


## docdist6 - Improve Insertion Sort
> [!algo]
> ![](Algorithmic_Thinking.assets/image-20231209115847276.png)![](Algorithmic_Thinking.assets/image-20231209115854547.png)


## docdist7 - Fully Utilize Dictionary
> [!algo]
> ![](Algorithmic_Thinking.assets/image-20231209120219723.png)![](Algorithmic_Thinking.assets/image-20231209120225185.png)




## docdist8 - Optimal Program
> [!algo]
> ![](Algorithmic_Thinking.assets/image-20231209120235819.png)![](Algorithmic_Thinking.assets/image-20231209120239751.png)



# Fractal Rendering - HW2 P1
## Background
> [!motiv] Background
> ![](Algorithmic_Thinking.assets/image-20231231175008665.png)


## Algorithm
> [!algo]
> ![](Algorithmic_Thinking.assets/image-20231231175114009.png)![](Algorithmic_Thinking.assets/image-20231231175118946.png)![](Algorithmic_Thinking.assets/image-20231231175149832.png)


## P1: 3D Hardware Accelerated Rendering
> [!example] Problem
> ![](Algorithmic_Thinking.assets/image-20231231175354039.png)![](Algorithmic_Thinking.assets/image-20231231175436096.png)![](Algorithmic_Thinking.assets/image-20231231175422604.png)![](Algorithmic_Thinking.assets/image-20231231175449829.png)![](Algorithmic_Thinking.assets/image-20231231175457553.png)![](Algorithmic_Thinking.assets/image-20231231175606154.png)![](Algorithmic_Thinking.assets/image-20231231175612257.png)



## P2: 2D Hardware Accelerated Rendering
> [!example] Problem
> ![](Algorithmic_Thinking.assets/image-20231231175933546.png)![](Algorithmic_Thinking.assets/image-20231231175942284.png)![](Algorithmic_Thinking.assets/image-20231231175947343.png)![](Algorithmic_Thinking.assets/image-20231231180301010.png)![](Algorithmic_Thinking.assets/image-20231231180347163.png)![](Algorithmic_Thinking.assets/image-20231231180402269.png)![](Algorithmic_Thinking.assets/image-20231231180410809.png)![](Algorithmic_Thinking.assets/image-20231231180419355.png)![](Algorithmic_Thinking.assets/image-20231231180438593.png)



## P3: 2D Software Rendering
> [!example] Problem
> ![](Algorithmic_Thinking.assets/image-20231231180516131.png)![](Algorithmic_Thinking.assets/image-20231231180644520.png)![](Algorithmic_Thinking.assets/image-20231231180649281.png)![](Algorithmic_Thinking.assets/image-20231231180720220.png)![](Algorithmic_Thinking.assets/image-20231231180736812.png)![](Algorithmic_Thinking.assets/image-20231231180746126.png)![](Algorithmic_Thinking.assets/image-20231231180804666.png)![](Algorithmic_Thinking.assets/image-20231231180810803.png)![](Algorithmic_Thinking.assets/image-20231231180906508.png)![](Algorithmic_Thinking.assets/image-20231231180925232.png)



## P4: 3D Software Rendering
> [!example] Problem
> ![](Algorithmic_Thinking.assets/image-20231231181008941.png)![](Algorithmic_Thinking.assets/image-20231231195815969.png)![](Algorithmic_Thinking.assets/image-20231231200013577.png)![](Algorithmic_Thinking.assets/image-20231231200017965.png)


## Summary
> [!summary]
> To compute the asymptotics of a recursion tree, we will always follow the following guides:
> 1. Determine the structure of the recursion tree, i.e. determine the number of branches of each node, height of the recursion tree etc.
> 2. Compute the asymptotic of a single node of layer i.
> 3. Compute the asymptotic of a single layer i.
> 4. Summing up the asymptotics of all the layers in teh recursion tree.
> 5. Simplify it with asymptotic notations.



# Digital Circuit Simulation - HW2 P2
> [!example] Problem 











































