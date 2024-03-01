# 力扣 2369 检查数组是否存在有效划分


# 检查数组是否存在有效划分

## 题目

> 给你一个下标从 **0** 开始的整数数组 `nums` ，你必须将数组划分为一个或多个 **连续** 子数组。
>
> 如果获得的这些子数组中每个都能满足下述条件 **之一** ，则可以称其为数组的一种 **有效** 划分：
>
> 1. 子数组 **恰** 由 `2` 个相等元素组成，例如，子数组 `[2,2]` 。
> 2. 子数组 **恰** 由 `3` 个相等元素组成，例如，子数组 `[4,4,4]` 。
> 3. 子数组 **恰** 由 `3` 个连续递增元素组成，并且相邻元素之间的差值为 `1` 。例如，子数组 `[3,4,5]` ，但是子数组 `[1,3,5]` 不符合要求。
>
> 如果数组 **至少** 存在一种有效划分，返回 `true` ，否则，返回 `false` 。
>
>  
>
> **示例 1：**
>
> ```
> 输入：nums = [4,4,4,5,6]
> 输出：true
> 解释：数组可以划分成子数组 [4,4] 和 [4,5,6] 。
> 这是一种有效划分，所以返回 true 。
> ```
>
> **示例 2：**
>
> ```
> 输入：nums = [1,1,1,2]
> 输出：false
> 解释：该数组不存在有效划分。
> ```
>
>  
>
> **提示：**
>
> - `2 <= nums.length <= 105`
> - `1 <= nums[i] <= 106`

## 题解

设数组 $\textit{nums}$ 的长度为 $n$，它至少存在一个有效划分的充要条件为：

- 前 $(n-2)$ 个元素组成的数组至少存在一个有效划分，且后两个元素相等。或

- 前 $(n-3)$ 个元素组成的数组至少存在一个有效划分，且
  - 后三个元素相等。或

  - 后三个元素连续递增，且差值为 $1$。


这样的判断可以用动态规划来解决，用一个长度为 $(n+1)$ 的数组来记录 $\textit{nums}$ 是否存在有效划分，$\textit{dp}[i]$ 表示前 iii 个元素组成的数组是否至少存在一个有效划分。边界情况 dp[0]dp[0]dp[0] 恒为 $\texttt{true}$，而 $dp[n]$ 即为结果。

同时，定义两个辅助函数，$\textit{validTwo}(\textit{num}_1, \textit{nums}_2)$ 用来判断长度为 $2$ 的子数组是否满足题目的条件 $1$。$\textit{validThree}(\textit{num}_1, \textit{nums}_2, \textit{nums}_3)$ 用来判断长度为 333 的子数组是否满足题目的条件 $2$ 或 $3$。

这样，动态规划的公式即为

$$
\begin{aligned} \textit{dp}[i] = & (\textit{dp}[i - 2]\wedge\textit{validTwo}(\textit{nums}[i - 2], \textit{nums}[i - 1])) \vee\\&(\textit{dp}[i - 3]\wedge\textit{validThree}(\textit{nums}[i - 3], \textit{nums}[i - 2], \textit{nums}[i - 1])) \end{aligned}
$$
。推导的时候需要注意下标是否越界。

## 代码

```python
class Solution:
    def validPartition(self, nums: List[int]) -> bool:
        n = len(nums)
        dp = [False] * (n + 1)
        dp[0] = True
        for i in range(1, n + 1):
            if i >= 2:
                dp[i] = dp[i - 2] and self.validTwo(nums[i - 2], nums[i - 1])
            if i >= 3:
                dp[i] = dp[i] or (dp[i - 3] and self.validThree(nums[i - 3], nums[i - 2], nums[i - 1]))
        return dp[-1]
    
    def validTwo(self, num1: int, num2: int) -> bool:
        return num1 == num2
    
    def validThree(self, num1: int, num2: int, num3: int) -> bool:
        return (num1 == num2 == num3) or (num1 + 2 == num2 + 1 == num3)
```


