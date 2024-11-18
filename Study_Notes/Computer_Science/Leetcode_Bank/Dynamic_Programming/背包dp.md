# 0-1 背包（容量不超过）
## 经典问法
> [!def]
> 0-1背包指的是每个物品只能选择或者不选择，选择的话至多选择一次。

> [!task]
> ![](%E8%83%8C%E5%8C%85dp.assets/6a23c461b9103cc9e7f9b4eea94659fd_MD5.jpeg)
```java
public class Bag01Solver {  
  
    private int[] weights;  
    private int[] values;  
    private int budget;  
  
    private int n;  
  
    /**  
     *     * @param weights  
     * @param values  
     * @param budget  
     */  
    public Bag01Solver(int[] weights, int[] values, int budget) {  
        this.weights = weights;  
        this.values = values;  
        this.budget = budget;  
        this.n = this.weights.length;  
    }  
  
    public int solve2D() {  
        int m = n;  // Number of items to choose from  
        int n = this.budget + 1;  // Maximum budgets  
        int[][] dp = new int[m][n];  
  
  
        // dp[i][j] 表示：考虑物品区间 [0..i] 里，不超过背包容量 j，能够获得的最大价值，由于包含价值为 0 的计算，所以 + 1        // 初始化：先写第 1 行  
        for (int j = 1; j < n; j++) {  
            // 第 1 个物品的体积要小于等于背包容量  
            if (weights[0] <= j) {  
                dp[0][j] = values[0];  
            }        }  
        for (int i = 1; i < m; i++) {  
            for (int j = 0; j < n; j++) {  
                dp[i][j] = dp[i - 1][j];  
                if (j >= this.weights[i]) {  
                    dp[i][j] = Math.max(  
                            dp[i][j]  // 不选择  
                            , dp[i - 1][j - this.weights[i]] + this.values[i]  // 选择  
                    );  
                }            }        }  
        return dp[m - 1][n - 1];  
    }  
  
    public int solve1D() {  
        int m = n;  // Number of items to choose from  
        int n = this.budget + 1;  // Maximum budgets  
        int[] dp = new int[n];  
  
  
        // 因为dp[i][j] 依赖于  dp[i - 1][j] 和 dp[i - 1][j - this.weights[i]], 所以后填的  
        // 格子所依赖的状态不能在填之前就被更新，所以使用逆序填表最合适。  
        for (int i = 0; i < m; i++) {  
           for (int j = n - 1; j >= this.weights[i] ; j--){  
               dp[j] = Math.max(dp[j], dp[j - this.weights[i]] + this.values[i]);  
           }       }  
  
        return dp[n - 1];  
    }  
    public static void main(String[] args) {  
        int[] weights = new int[] {4, 3, 1, 1};  
        int[] values = new int[] {300, 200, 150, 200};  
  
  
        Bag01Solver bag01Solver = new Bag01Solver(weights, values, 5);  
  
        System.out.println(bag01Solver.solve1D());  
    }}
```


 

## 夏季特惠
> [!task]
> ![](%E8%83%8C%E5%8C%85dp.assets/c2b967a014849d616e4dc2a7fab5a5e1_MD5.jpeg)

> [!example]
> ![](%E8%83%8C%E5%8C%85dp.assets/955d6eb10098d90273ca6ec301fe9ce6_MD5.jpeg)

```java
public int problemSolver(int[] origins, int[] nows, int[] happy, int budget) {  
    int n = origins.length;  
  
    int res = 0;  
  
    List<Integer> constraints = new ArrayList<>();  
  
  
    // 先把那些必选的商品选出来，因为这些商品会增加预算  
    for (int i = 0; i < n; i++) {  
        if (origins[i] - nows[i] > nows[i]) {  
            budget += origins[i] - nows[i] - nows[i];  
            res += happy[i];  
  
        } else {  
            constraints.add(i);  
  
        }    }  
  
    // 然后在剩余的商品上做一个0-1背包  
    int[] weights = new int[constraints.size()];  
    int[] vals = new int[constraints.size()];  
    for (int i = 0; i < weights.length; i++) {  
        int constraintIndex = constraints.get(i);  
        int constraintBudget = nows[constraintIndex] - (origins[constraintIndex] - nows[constraintIndex]);  
  
        weights[i] = constraintBudget;  
        vals[i] = happy[constraintIndex];  
    }  
  
    Bag01Solver bag01Solver = new Bag01Solver(weights, vals, budget);  
    res += bag01Solver.solve2D();  
    return res;  
}
```



## 目标和
> [!task]
> ![](%E8%83%8C%E5%8C%85dp.assets/db35f78d38bcc41c3ab86ee0bca2a0fe_MD5.jpeg)




# 0-1 背包 (恰好装满)
## 等和子集
> [!task]
> ![](%E8%83%8C%E5%8C%85dp.assets/128cbcd3334b790f8e05aabb3fec79bd_MD5.jpeg)
```java
public class EqualSubset {  
  
    private int[] nums;  
  
    private int N;  
  
    public EqualSubset(int[] nums) {  
        this.nums = nums;  
        this.N = this.nums.length;  
    }  
    // Time: O(N * target)  
    // Space: O(N * target)    public boolean solve2D() {  
  
        int sum =  Arrays.stream(this.nums).sum();  
  
        if (sum % 2 != 0 || this.nums.length % 2 != 0) {  
            return false;  
        }  
        int target = sum / 2 + 1;  
  
        boolean[][] dp = new boolean[N][target];  
  
        // Initialize  
        for (int j = this.nums[0]; j < target; j++) {  
            dp[0][j] = true;  
        }  
        for (int  i = 1; i < N; i++) {  
            for (int j = 0; j < target; j++) {  
                dp[i][j] = dp[i - 1][j];  
                if (j >= this.nums[i]) {  
                    dp[i][j] = dp[i][j] || dp[i - 1][j - this.nums[i]];  
                }            }        }  
        return dp[N - 1][target - 1];  
  
    }  
  
    // Time: O(N * target)  
    // Space: O(target)    public boolean solve1D() {  
        int sum =  Arrays.stream(this.nums).sum();  
  
        if (sum % 2 != 0 || this.nums.length % 2 != 0) {  
            return false;  
        }  
        int target = sum / 2 + 1;  
  
        boolean[] dp = new boolean[target];  
  
        // Initialize  
        for (int j = this.nums[0]; j < target; j++) {  
            dp[j] = true;  
        }  
        for (int  i = 1; i < N; i++) {  
            for (int j = target - 1; j >= this.nums[i]; j--) {  
                dp[j] = dp[j] || dp[j - this.nums[i]];  
            }        }  
        return dp[target - 1];  
    }}
```







## 目标和
> [!task]
> ![](%E8%83%8C%E5%8C%85dp.assets/98265e402e38b312456de086a9252685_MD5.jpeg)




### 动态规划解法
> [!code]
```java
public int solve2D() {  
  
    // 因为数组中的数字的和最大是sum(arr), 最小是-1 * sum(arr)  
    // 而如果我们需要使用dp[i][j]来表示[0...i]中和为 j 的符号添加方式的数量  
    // 则需要对 j 重新定义，因为 j 作为数组下标不能小于零  
    int sum = Arrays.stream(this.numList).sum();  
  
    // 不可能求出在 [-sum, sum] 以外的和  
    if (this.target > sum || this.target < -sum) {  
        return 0;  
    }  
    // 偏移  
    int W = 2 * sum + 1;  
    int[][] dp = new int[N][W];  
  
  
    // 初始化, 对于第一个数字的两种可能  
    dp[0][this.numList[0] + sum] = 1;  
    dp[0][-this.numList[0] + sum] += 1;  
  
  
    // 填表  
    for (int i = 1; i < N; i++) {  
        for (int j = 0; j < W; j++) {  
  
            if (j - this.numList[i] >= 0) {  
                dp[i][j] += dp[i - 1][j - this.numList[i]];  
            }            if (j + this.numList[i] < W) {  
                dp[i][j] += dp[i - 1][j + this.numList[i]];  
            }  
        }    }  
    return dp[N - 1][target + sum];  
}
```




### 0-1背包解法
> [!code]
> ![](%E8%83%8C%E5%8C%85dp.assets/b70766fc923ba0108b60bac63e3d0abd_MD5.jpeg)
```java
public int solveThrough01Bag() {  
    // sum(添加+的数字) + sum(添加-的数字) = sum  
    // sum(添加+的数字) - sum(添加-的数字) = target  
  
    // sum(添加+的数字) = (sum + target) / 2  
  
    int sum = Arrays.stream(this.numList).sum();  
    int target = this.target;  
  
    if ((sum + target) % 2 != 0 ) {  
        return 0;  
    }  
    // 问题化为从数组中选出一些数，使得和为 (sum + target) / 2    int W = (sum + target) / 2 + 1;  
    int[][] dp = new int[N][W];  
  
    // 初始化  
    dp[0][0] = 1; // 不选第一个数, 1种方法  
    dp[0][this.numList[0]] += 1; // 第一个数为零的情况  
  
    for (int i = 1; i < N; i++) {  
        for (int j = 0; j < W; j++) {  
            dp[i][j] = dp[i - 1][j];  
  
            if (j - this.numList[i] >= 0) {  
                dp[i][j] += dp[i - 1][j - this.numList[i]];  
            }        }    }  
    return dp[N - 1][W - 1];  
}
```



## 最后一块石头的重量
> [!task]
> ![](%E8%83%8C%E5%8C%85dp.assets/f71f4fca6b7a4132d6f30c349127d79f_MD5.jpeg)

> [!code]
> ![](%E8%83%8C%E5%8C%85dp.assets/3f2d5a572ac7a5dead1f76d77187c177_MD5.jpeg)![](%E8%83%8C%E5%8C%85dp.assets/9b79840d2e6d2ab5eec40f7c9f1cf708_MD5.jpeg)
```java


```


# 0-1 背包 (多个约束)
## 一和零
> [!task]
> 



## 盈利计划
> [!task]
> ![](%E8%83%8C%E5%8C%85dp.assets/aad5b61a6fee5460158e29dda5d2c631_MD5.jpeg)

> [!code]
> ![](%E8%83%8C%E5%8C%85dp.assets/f7faf1a53d269018eedbffcf9f112b8c_MD5.jpeg)
```java
class Solution {  
    int mod = (int)1e9+7;  
    public int profitableSchemes(int n, int min, int[] gs, int[] ps) {  
        int m = gs.length;  
        long[][][] f = new long[m + 1][n + 1][min + 1];  
        for (int i = 0; i <= n; i++) f[0][i][0] = 1;  
        for (int i = 1; i <= m; i++) {  
            int a = gs[i - 1], b = ps[i - 1];  
            for (int j = 0; j <= n; j++) {  
                for (int k = 0; k <= min; k++) {  
                    f[i][j][k] = f[i - 1][j][k];  
                    if (j >= a) {  
                        int u = Math.max(k - b, 0);  
                        f[i][j][k] += f[i - 1][j - a][u];  
                        if (f[i][j][k] >= mod) f[i][j][k] -= mod;  
                    }                }            }        }        return (int)f[m][n][min];  
    }}
```

# 分组背包
## 模板
> [!important]
> ![](%E8%83%8C%E5%8C%85dp.assets/0675eef8e3b0e6dd8c9445b13d4c2708_MD5.jpeg)![](%E8%83%8C%E5%8C%85dp.assets/fd062329ce5dc3c473d784ba7067da74_MD5.jpeg)






# 完全背包
## 经典框架
> [!important]
> ![](%E8%83%8C%E5%8C%85dp.assets/f8572a5c6781c7ec54ce3c39f9482561_MD5.jpeg)![](%E8%83%8C%E5%8C%85dp.assets/509646f7958fcbed113c8b83a44b0031_MD5.jpeg)

```java
public class Solution {  
  
    public int backpackComplete(int W, int[] weights, int[] values) {  
        int N = weights.length;  
        if (N == 0) {  
            return 0;  
        }        // dp[i][j] 表示：考虑物品区间 [0..i] 里，不超过背包容量 j，能够获得的最大价值总和，由于包含价值为 0 的计算，所以 + 1        int[][] dp = new int[N][W + 1];  
        // 初始化：先写第 1 行  
        for (int k = 0; k * weights[0] <= W; k++) {  
            dp[0][k * weights[0]] = k * values[0];  
        }        // 递推开始  
        for (int i = 1; i < N; i++) {  
            for (int j = 0; j <= W; j++) {  
                // 多一个 for 循环，枚举下标为 i 的物品可以选择的个数  
                for (int k = 0; k * weights[i] <= j; k++) {  
                    dp[i][j] = Math.max(dp[i][j], dp[i - 1][j - k * weights[i]] + k * values[i]);  
                }            }        }        return dp[N - 1][W];  
    }
```


### 状态转移方程
> [!important]
> ![](%E8%83%8C%E5%8C%85dp.assets/df5ef80850bad0fe7dd661f096273a00_MD5.jpeg)![](%E8%83%8C%E5%8C%85dp.assets/b0b5f5c22d22282587e5a5433230c785_MD5.jpeg)



### 与0 - 1背包比较
> [!important]
> ![](%E8%83%8C%E5%8C%85dp.assets/821a04f0661a68d438061ea46d6218ba_MD5.jpeg)




## 完全平方数
> [!task]
> ![](%E8%83%8C%E5%8C%85dp.assets/b991fd7d88232b7a67ecdcae018057a6_MD5.jpeg)

> [!code]
> ![](%E8%83%8C%E5%8C%85dp.assets/c8a193966bfbbb2ca47b70dfcef47646_MD5.jpeg)![](%E8%83%8C%E5%8C%85dp.assets/0a88b31afe51cf1a93995b475b1c3e6a_MD5.jpeg)![](%E8%83%8C%E5%8C%85dp.assets/665715bc8d4380338efa225a46d5067b_MD5.jpeg)
```java
import java.util.Arrays;

public class Solution {

    public int numSquares(int n) {
        // 先计算出可能的最大的完全平方数
        int upBound = (int) Math.sqrt(n);
        int[][] dp = new int[upBound + 1][n + 1];
        // 根据四平方和定理，可以将每一个状态值设置成为 4
        for (int i = 0; i < upBound; i++) {
            Arrays.fill(dp[i], 4);
        }
        dp[0][0] = 0;
        for (int i = 1; i <= upBound; i++) {
            for (int j = 0; j <= n; j++) {
              	// 先把上一行的值抄下来
                dp[i][j] = dp[i - 1][j];
              	// 如果在当前容量 j 下可以包含一个完全平方数，就发生状态转移
                if (i * i <= j && dp[i][j - i * i] != 4) {
                    dp[i][j] = Math.min(dp[i][j], dp[i][j - i * i] + 1);
                }
            }
        }
        return dp[upBound][n];
    }
}
```







## 零钱兑换
### 零钱兑换 I
> [!task]
> ![](%E8%83%8C%E5%8C%85dp.assets/fe9b2f3b85514a39b789f35ea63f4b8d_MD5.jpeg)

> [!code] 二维模板
> ![](%E8%83%8C%E5%8C%85dp.assets/a3f1c6bcee1b806cdf834664c5c9c74e_MD5.jpeg)![](%E8%83%8C%E5%8C%85dp.assets/4c74b09c5e9aa024f16c8ea54588f446_MD5.jpeg)
```java
import java.util.Arrays;

public class Solution {

    public int coinChange(int[] coins, int amount) {
        int len = coins.length;
        // 定义：使用区间 [0..i] 中的硬币，可以凑出总容量恰好为 j 的最少方案数
        int[][] dp = new int[len][amount + 1];
        for (int i = 0; i < len; i++) {
            // 要找最小值，所以初始化的时候全部设置为最大值
            Arrays.fill(dp[i], amount + 1);
        }

        // 初始化
        dp[0][0] = 0;
        for (int j = coins[0]; j <= amount; j++) {
            if (dp[0][j - coins[0]] != amount + 1) {
                dp[0][j] = dp[0][j - coins[0]] + 1;
            }
        }

        // 递推开始
        for (int i = 1; i < len; i++) {
            for (int j = 0; j <= amount; j++) {
                dp[i][j] = dp[i - 1][j];
                if (coins[i] <= j && dp[i][j - coins[i]] != amount + 1) {
                    dp[i][j] = Math.min(dp[i][j], dp[i][j - coins[i]] + 1);
                } 
            }
        }

        if (dp[len - 1][amount] == amount + 1) {
            dp[len - 1][amount] = -1;
        }
        return dp[len - 1][amount];
    }
}
```
> [!important]
> ![](%E8%83%8C%E5%8C%85dp.assets/cbc95970a70ea7105dcb2029ebdf4db4_MD5.jpeg)

> [!code] 状态压缩
> ![](%E8%83%8C%E5%8C%85dp.assets/db52a40542cffa0d134c7be8c0021d0f_MD5.jpeg)
```java
import java.util.Arrays;

public class Solution {

    public int coinChange(int[] coins, int amount) {
        int[] dp = new int[amount + 1];
        Arrays.fill(dp, amount + 1);
        dp[0] = 0;

        for (int coin : coins) {
            for (int i = coin; i <= amount; i++) {
                // dp[i - coin] + 1 可能会发生整型溢出
                if (dp[i - coin] != amount + 1) {
                    dp[i] = Math.min(dp[i], dp[i - coin] + 1);
                }
            }
        }

        if (dp[amount] == amount + 1) {
            dp[amount] = -1;
        }
        return dp[amount];
    }
}
```


### 零钱兑换 II
> [!task]
> ![](%E8%83%8C%E5%8C%85dp.assets/242c14bacf3721734d2aa60ae2dd5e07_MD5.jpeg)


> [!code]
> ![](%E8%83%8C%E5%8C%85dp.assets/41290ae200647451556c18be039b7641_MD5.jpeg)![](%E8%83%8C%E5%8C%85dp.assets/a45b0474a14dc7b86b9a6e77bd6ffe86_MD5.jpeg)


```java
public class Solution {

    public int change(int amount, int[] coins) {
        int len = coins.length;
        if (len == 0) {
            if (amount == 0) {
                return 1;
            }
            return 0;
        }

        // 定义：使用区间 [0..i] 里的硬币，恰好可以凑出面值为 j 的方案总数
        int[][] dp = new int[len][amount + 1];
        dp[0][0] = 1;

        // 初始化
        for (int i = coins[0]; i <= amount; i += coins[0]) {
            dp[0][i] = 1;
        }

        // 递推开始
        for (int i = 1; i < len; i++) {
            for (int j = 0; j <= amount; j++) {
                dp[i][j] = dp[i - 1][j];
                if (j - coins[i] >= 0) {
                    dp[i][j] += dp[i][j - coins[i]];
                }
            }
        }
        return dp[len - 1][amount];
    }
}

```

> [!code] 状态压缩
> ![](%E8%83%8C%E5%8C%85dp.assets/6f33ea8b7ece429ef77bc18480959019_MD5.jpeg)


```java
public class Solution {

    public int change(int amount, int[] coins) {
        int len = coins.length;
        if (len == 0) {
            if (amount == 0) {
                return 1;
            }
            return 0;
        }

        int[] dp = new int[amount + 1];
        // 初始化
        dp[0] = 1;
        for (int i = coins[0]; i <= amount; i += coins[0]) {
            dp[i] = 1;
        }

        // 递推开始
        for (int i = 1; i < len; i++) {
            // 从 coins[i] 开始即可
            for (int j = coins[i] ; j <= amount; j++) {
                if (j - coins[i] >= 0) {
                    dp[j] += dp[j - coins[i]];
                }
            }
        }
        return dp[amount];
    }
}
```




## 数位成本
> [!task]
> ![](%E8%83%8C%E5%8C%85dp.assets/e0e68dfa36d65654a31c07429719784c_MD5.jpeg)![](%E8%83%8C%E5%8C%85dp.assets/b2d7917a48bc7d1cbbf350cf5d32f2dd_MD5.jpeg)

> [!code]
> ![](%E8%83%8C%E5%8C%85dp.assets/42cc622cc843d38fc72b40927ab3b43e_MD5.jpeg)
```java
import java.util.Arrays;

public class Solution {

    public String largestNumber(int[] cost, int target) {
        // 第 1 步：使用动态规划计算最大位数
        // dp[i][j] 表示：使用 cost 前缀区间 [0..i] 里的元素能够刚好凑成和为 j 的时候的数字的最大位数
        int[][] dp = new int[9][target + 1];
        for (int i = 0; i < 9; i++) {
            Arrays.fill(dp[i], -1);
        }
        // 初始化
        dp[0][0] = 0;
        for (int j = cost[0]; j <= target; j++) {
            if (dp[0][j - cost[0]] != -1) {
                dp[0][j] = dp[0][j - cost[0]] + 1;
            }
        }
        // 一个数一个数考虑，因此外层循环是 cost
        for (int i = 1; i < 9; i++) {
            for (int j = 0; j <= target; j++) {
                dp[i][j] = dp[i - 1][j];
                if (cost[i] <= j && dp[i][j - cost[i]] != -1) {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - cost[i]] + 1);
                }
            }
        }
        // 判断是否有结果
        if (dp[8][target] == -1) {
            return "0";
        }

        // 第 2 步：根据第 1 步计算的结果，优先考虑数值大的放在高位，还原最大整数
        int t = target;
        // 最大整数的位数
        int len = dp[8][target];
        StringBuilder res = new StringBuilder();
        int i = 8;
        while (t > 0) {
            // 这一步选谁
            int num = -1;
            // 倒着选，如果正着选会选出最小值
            for (int j = 9; j >= 1; j--) {
                if (t >= cost[j - 1] && dp[i][t - cost[j - 1]] == len - 1) {
                    num = j;
                    break;
                }
            }
            res.append(num);
            t -= cost[num - 1];
            len--;
        }
        return res.toString();
    }
}
```







# 多重背包






# 混合背包



