# DP Formulation
> [!important]
> ![](Dynamic_Programming.assets/image-20240214225052055.png)![](Dynamic_Programming.assets/image-20240214225041101.png)![](Dynamic_Programming.assets/image-20240214225102209.png)


# Fibonacci Number and DP
## Naive Algorithm
> [!concept]
> ![](Dynamic_Programming.assets/image-20240201170309701.png)



## Memoized DP Algorithm
> [!concept]
> ![](Dynamic_Programming.assets/image-20240201170333612.png)![](Dynamic_Programming.assets/image-20240201170342846.png)


## Bottom-up DP Algorithm
> [!concept]
> ![](Dynamic_Programming.assets/image-20240201170555933.png)



# Merge Sort





# Shortest Path
## DAG DP
> [!concept]
> ![](Dynamic_Programming.assets/image-20240201171402110.png)![](Dynamic_Programming.assets/image-20240201171409172.png)
> **Note:** Subproblem dependencies should be acyclic in order for memoization to work, otherwise infinite recursion.
> 
> If the subproblem dependencies are acyclic, then the runtime is # subproblems * time/subproblem.
> 
> With memoization, time/subproblem is $\Theta(1)$
> 
> Here, # subproblems = V choice for k and E choice for v(indegree), so $O(VE)$


## How to Design Recurrence
> [!important]
> ![](Dynamic_Programming.assets/image-20240201231020304.png)![](Dynamic_Programming.assets/image-20240201231025023.png)





## Cyclic => Acyclic
> [!important]
> If the graph contains cycles(non-negative ones), traditional DP won't work, so we need to transform the cyclic graph to acyclic one. The cost is that we are making more subproblems for DP.
> ![](Dynamic_Programming.assets/image-20240201230123149.png)![](Dynamic_Programming.assets/image-20240201230130981.png)![](Dynamic_Programming.assets/image-20240201230137089.png)




# Text Justification
> [!algo]
> ![](Dynamic_Programming.assets/image-20240410215701040.png)![](Dynamic_Programming.assets/image-20240410215728529.png)
> `DP[n]` can be thought of as empty line, which doesn't have badness since we have no words to fit that line.




# Parent Pointers

 

# Subsequences



# Parenthesization
> [!algo]
> ![](Dynamic_Programming.assets/image-20240705204919276.png)





# Edit Distance





# Perfect-Information Blackjack
> [!algo]
> ![](Dynamic_Programming.assets/image-20240411132735561.png)![](Dynamic_Programming.assets/image-20240411132742466.png)








# Knapsack





# Chain Matrix Multiplication




# Leetcode Problems
## 双序列DP
### 编辑距离
> [!code]
> ![](Dynamic_Programming.assets/image-20240705221712465.png)
> **Remarks:**
> - 我们假设所有的增删改的开销都是`1`。
```java
class Solution {
    public int minDistance(String word1, String word2) {
        int length1 = word1.length();
        int length2 = word2.length();
        int[][] dp = new int[length1 + 1][length2 + 1];

        // Initialize base cases
        for (int i = 0; i <= length1; i++) {
            dp[i][0] = i; // Cost of deleting characters from word1 to make it empty
        }
        for (int j = 0; j <= length2; j++) {
            dp[0][j] = j; // Cost of inserting characters to make word2 from empty
        }

        // Fill dp array
        for (int i = 1; i <= length1; i++) {
            for (int j = 1; j <= length2; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1]; // No operation needed
                } else {
                    int delete = dp[i - 1][j]; // Delete character from word1
                    int insert = dp[i][j - 1]; // Insert character into word1
                    int replace = dp[i - 1][j - 1]; // Replace character in word1
                    dp[i][j] = Math.min(delete, Math.min(insert, replace)) + 1;
                }
            }
        }

        return dp[length1][length2];
    }

```




### 不相交的线
> [!task]
> ![](Dynamic_Programming.assets/image-20240706170728183.png)
> 大体思路是:
> - `dp[i][j]`表示`nums1[:i]`和`nums2[:j]`的最大连线数量
```java
class Solution {
    public int maxUncrossedLines(int[] nums1, int[] nums2) {

        int length1 = nums1.length;
        int length2 = nums2.length;

        int[][] dp = new int[length1 + 1][length2 + 1];

        for (int i = 1; i <= length1; i++) {
            for (int j = 1; j <= length2; j++) {
                int temp = Integer.MIN_VALUE;
                // If we can connect the current pair, 3 choices
                if (nums1[i - 1] == nums2[j - 1]) {
                    temp = Math.max(temp, dp[i - 1][j -1]) + 1;
                }
                // If we cannot connect the current pair, 2 choices
                temp = Math.max(temp, dp[i][j -1]);
                temp = Math.max(temp, dp[i - 1][j]);
                dp[i][j] = temp;
            }
        }
        return dp[length1][length2];
    }
}
```




## 股票问题
> [!important] 模板
> ![](Dynamic_Programming.assets/image-20240706175720275.png)![](Dynamic_Programming.assets/image-20240706175738996.png)![](Dynamic_Programming.assets/image-20240706175937132.png)


### 买卖股票的最佳时机 I



### 买卖股票的最佳时机 II



### 买卖股票的最佳时机 III


### 买卖股票的最佳时机 IV


### 买卖股票的最佳时机 V


### 买卖股票的最佳时机 VI



## 背包问题




