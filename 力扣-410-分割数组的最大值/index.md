# 力扣 410 分割数组的最大值


# 分割数组的最大值

## 题目

> 给定一个非负整数数组 `nums` 和一个整数 `k` ，你需要将这个数组分成 `k` 个非空的连续子数组。
>
> 设计一个算法使得这 `k` 个子数组各自和的最大值最小。
>
>  
>
> **示例 1：**
>
> ```
> 输入：nums = [7,2,5,10,8], k = 2
> 输出：18
> 解释：
> 一共有四种方法将 nums 分割为 2 个子数组。 
> 其中最好的方式是将其分为 [7,2,5] 和 [10,8] 。
> 因为此时这两个子数组各自的和的最大值为18，在所有情况中最小。
> ```
>
> **示例 2：**
>
> ```
> 输入：nums = [1,2,3,4,5], k = 2
> 输出：9
> ```
>
> **示例 3：**
>
> ```
> 输入：nums = [1,4,4], k = 3
> 输出：4
> ```
>
>  
>
> **提示：**
>
> - `1 <= nums.length <= 1000`
> - `0 <= nums[i] <= 106`
> - `1 <= k <= min(50, nums.length)`

## 题解

### 方法一：动态规划

**思路与算法**

「将数组分割为 $m$ 段，求……」是动态规划题目常见的问法。

本题中，我们可以令 $f[i][j]$ 表示将数组的前 $i$ 个数分割为 $j$ 段所能得到的最大连续子数组和的最小值。在进行状态转移时，我们可以考虑第 $j$ 段的具体范围，即我们可以枚举 $k$，其中前 $k$ 个数被分割为 $j−1$ 段，而第 $k+1$ 到第 $i$ 个数为第 $j$ 段。此时，这 $j$ 段子数组中和的最大值，就等于 $f[k][j−1]$ 与 $\textit{sub}(k+1, i)$ 中的较大值，其中 $\textit{sub}(i,j)$ 表示数组 $\textit{nums}$ 中下标落在区间 $[i,j]$ 内的数的和。

由于我们要使得子数组中和的最大值最小，因此可以列出如下的状态转移方程：

$$
f[i][j] = \min_{k=0}^{i-1} \Big\{ \max(f[k][j-1], \textit{sub}(k+1,i)) \Big\}
$$
对于状态 $f[i][j]$，由于我们不能分出空的子数组，因此合法的状态必须有 $i \geq j$。对于不合法（$i<j$）的状态，由于我们的目标是求出最小值，因此可以将这些状态全部初始化为一个很大的数。在上述的状态转移方程中，一旦我们尝试从不合法的状态 $f[k][j−1]$ 进行转移，那么 $\max(\cdots)$ 将会是一个很大的数，就不会对最外层的 $\min\{\cdots\}$ 产生任何影响。

此外，我们还需要将 $f[0][0]$ 的值初始化为 $0$。在上述的状态转移方程中，当 $j=1$ 时，唯一的可能性就是前 $i$ 个数被分成了一段。如果枚举的 $k=0$，那么就代表着这种情况；如果 $k \neq 0$，对应的状态 $f[k][0]$ 是一个不合法的状态，无法进行转移。因此我们需要令 $f[0][0] = 0$。

最终的答案即为 $f[n][m]$。

### 方法二：二分查找 + 贪心

**思路及算法**

「使……最大值尽可能小」是二分搜索题目常见的问法。

本题中，我们注意到：当我们选定一个值 $x$，我们可以线性地验证是否存在一种分割方案，满足其最大分割子数组和不超过 $x$。策略如下：

> 贪心地模拟分割的过程，从前到后遍历数组，用 $\textit{sum}$ 表示当前分割子数组的和，$\textit{cnt}$ 表示已经分割出的子数组的数量（包括当前子数组），那么每当 $\textit{sum}$ 加上当前值超过了 $x$，我们就把当前取的值作为新的一段分割子数组的开头，并将 $\textit{cnt}$ 加 $1$。遍历结束后验证是否 $\textit{cnt}$ 不超过 $m$。

这样我们可以用二分查找来解决。二分的上界为数组 $\textit{nums}$ 中所有元素的和，下界为数组 $\textit{nums}$ 中所有元素的最大值。通过二分查找，我们可以得到最小的最大分割子数组和，这样就可以得到最终的答案了。

## 代码

**方法一：动态规划**

```java
class Solution {
    public int splitArray(int[] nums, int m) {
        int n = nums.length;
        int[][] f = new int[n + 1][m + 1];
        for (int i = 0; i <= n; i++) {
            Arrays.fill(f[i], Integer.MAX_VALUE);
        }
        int[] sub = new int[n + 1];
        for (int i = 0; i < n; i++) {
            sub[i + 1] = sub[i] + nums[i];
        }
        f[0][0] = 0;
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= Math.min(i, m); j++) {
                for (int k = 0; k < i; k++) {
                    f[i][j] = Math.min(f[i][j], Math.max(f[k][j - 1], sub[i] - sub[k]));
                }
            }
        }
        return f[n][m];
    }
}
```

**方法二：二分查找 + 贪心**

```java
class Solution {
    public int splitArray(int[] nums, int m) {
        int left = 0, right = 0;
        for (int i = 0; i < nums.length; i++) {
            right += nums[i];
            if (left < nums[i]) {
                left = nums[i];
            }
        }
        while (left < right) {
            int mid = (right - left) / 2 + left;
            if (check(nums, mid, m)) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return left;
    }

    public boolean check(int[] nums, int x, int m) {
        int sum = 0;
        int cnt = 1;
        for (int i = 0; i < nums.length; i++) {
            if (sum + nums[i] > x) {
                cnt++;
                sum = nums[i];
            } else {
                sum += nums[i];
            }
        }
        return cnt <= m;
    }
}
```


