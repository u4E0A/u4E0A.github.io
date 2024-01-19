# 力扣 2809 使数组和小于等于x的最少时间


# 使数组和小于等于x的最少时间

## 题目

> 给你两个长度相等下标从 **0** 开始的整数数组 `nums1` 和 `nums2` 。每一秒，对于所有下标 `0 <= i < nums1.length` ，`nums1[i]` 的值都增加 `nums2[i]` 。操作 **完成后** ，你可以进行如下操作：
>
> - 选择任一满足 `0 <= i < nums1.length` 的下标 `i` ，并使 `nums1[i] = 0` 。
>
> 同时给你一个整数 `x` 。
>
> 请你返回使 `nums1` 中所有元素之和 **小于等于** `x` 所需要的 **最少** 时间，如果无法实现，那么返回 `-1` 。
>
>  
>
> **示例 1：**
>
> ```
> 输入：nums1 = [1,2,3], nums2 = [1,2,3], x = 4
> 输出：3
> 解释：
> 第 1 秒，我们对 i = 0 进行操作，得到 nums1 = [0,2+2,3+3] = [0,4,6] 。
> 第 2 秒，我们对 i = 1 进行操作，得到 nums1 = [0+1,0,6+3] = [1,0,9] 。
> 第 3 秒，我们对 i = 2 进行操作，得到 nums1 = [1+1,0+2,0] = [2,2,0] 。
> 现在 nums1 的和为 4 。不存在更少次数的操作，所以我们返回 3 。
> ```
>
> **示例 2：**
>
> ```
> 输入：nums1 = [1,2,3], nums2 = [3,3,3], x = 4
> 输出：-1
> 解释：不管如何操作，nums1 的和总是会超过 x 。
> ```
>
>  
>
> **提示：**
>
> - `1 <= nums1.length <= 103`
> - `1 <= nums1[i] <= 103`
> - `0 <= nums2[i] <= 103`
> - `nums1.length == nums2.length`
> - `0 <= x <= 106`

## 题解

首先，我们可以发现，每一次操作使得 $nums_1[i]=0$，对于每一个 $nums_1[i]$ 我们最多需要进行一次这样的操作。如果我们需要设置两次，我们可以简单地移除前一次设置。

观察重置为零的数，会按照 $nums_2$ 的速度增长，所以对于所有操作的数，我们应该优先操作增长速度慢的数。

如果我们选择多个索引 $i_1,i_2,\cdots, i_k$ ，那么按照 $\textit{nums}_2[i_1] \le \textit{nums}_2[i_2] \le \cdots \le \textit{nums}_2[i_k]$ 的顺序进行设置是最优的。

让我们按照 $nums_2$  的大小对所有数值对进行排序（非递减顺序）。用 $dp[j][i]$ 表示如果对前 $j$ 个元素进行 $i$ 次操作，可以减少的最大总值，初始值为零。对于第 $j$ 个元素，我们可以选择对其进行操作或者不操作，由此可以得到状态转移方程：
$$
\textit{dp}[j][i] = \max(\textit{dp}[j - 1][i], \textit{dp}[j - 1][i - 1] + \textit{nums}_2[j - 1] \times i + \textit{nums}_1[j - 1])
$$
其中有 $1 \le i \le j \le n$。

最后我们返回最小的 $t$，使满足 $\textit{sum}(\textit{nums}_1) + \textit{sum}(\textit{nums}_2) \times t - \textit{dp}[n][t] \le x$，如果不存在返回 $-1$。

## 代码

```java
class Solution {
    public int minimumTime(List<Integer> nums1, List<Integer> nums2, int x) {
        int n = nums1.size(), s1 = 0, s2 = 0;
        int[][] dp = new int[n + 1][n + 1];
        int[][] nums = new int[n][2];
        for (int i = 0; i < n; i++) {
            int a = nums1.get(i), b = nums2.get(i);
            nums[i][0] = b;
            nums[i][1] = a;
            s1 += a;
            s2 += b;
        }
        Arrays.sort(nums, Comparator.comparingInt(o -> o[0]));

        for (int j = 1; j <= n; ++j) {
            int b = nums[j - 1][0], a = nums[j - 1][1];
            for (int i = j; i > 0; --i) {
                dp[j][i] = Math.max(dp[j - 1][i], dp[j - 1][i - 1] + i * b + a);
            }
        }
        for (int i = 0; i <= n; i++) {
            if (s2 * i + s1 - dp[n][i] <= x) {
                return i;
            }
        }
        return -1;
    }
}
```

在上面的方法中，$dp[i]$ 的状态只和 $dp[i−1]$ 有关。

所以我们可以省去第一个维度，从而优化空间，从 $O(n^2)$ 优化到 $O(n)$，其中 $n$ 是输入数组的长度。

```java
class Solution {
    public int minimumTime(List<Integer> nums1, List<Integer> nums2, int x) {
        int n = nums1.size(), s1 = 0, s2 = 0;
        int[] dp = new int[n + 1];
        List<List<Integer>> nums = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            int a = nums1.get(i), b = nums2.get(i);
            nums.add(Arrays.asList(b, a));
            s1 += a;
            s2 += b;
        }
        Collections.sort(nums, (o1, o2) -> Integer.compare(o1.get(0), o2.get(0)));

        for (int j = 1; j <= n; ++j) {
            int b = nums.get(j - 1).get(0), a = nums.get(j - 1).get(1);
            for (int i = j; i > 0; --i) {
                dp[i] = Math.max(dp[i], dp[i - 1] + i * b + a);
            }
        }
        for (int i = 0; i <= n; i++) {
            if (s2 * i + s1 - dp[i] <= x) {
                return i;
            }
        }
        return -1;
    }
}
```


