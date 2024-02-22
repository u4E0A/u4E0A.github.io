# 力扣 1696 跳跃游戏 VI


# 跳跃游戏 VI

## 题目

> 给你一个下标从 **0** 开始的整数数组 `nums` 和一个整数 `k` 。
>
> 一开始你在下标 `0` 处。每一步，你最多可以往前跳 `k` 步，但你不能跳出数组的边界。也就是说，你可以从下标 `i` 跳到 `[i + 1， min(n - 1, i + k)]` **包含** 两个端点的任意位置。
>
> 你的目标是到达数组最后一个位置（下标为 `n - 1` ），你的 **得分** 为经过的所有数字之和。
>
> 请你返回你能得到的 **最大得分** 。
>
>  
>
> **示例 1：**
>
> ```
> 输入：nums = [1,-1,-2,4,-7,3], k = 2
> 输出：7
> 解释：你可以选择子序列 [1,-1,4,3] （上面加粗的数字），和为 7 。
> ```
>
> **示例 2：**
>
> ```
> 输入：nums = [10,-5,-2,4,0,3], k = 3
> 输出：17
> 解释：你可以选择子序列 [10,4,3] （上面加粗数字），和为 17 。
> ```
>
> **示例 3：**
>
> ```
> 输入：nums = [1,-5,-20,4,-1,3,-6,-3], k = 2
> 输出：0
> ```
>
>  
>
> **提示：**
>
> -  `1 <= nums.length, k <= 105`
> - `-104 <= nums[i] <= 104`

## 题解

每一个位置的最大值取决于前面 $k$ 步的最大得分，再加上当前位置的得分，由此我们想到可以使用动态规划来解决这个问题。

用 $\textit{dp}[i]$ 来表示到达位置 $i$ 的最大得分。初始状态 $\textit{dp}[0] = \textit{nums}[0]$，表示位置 $0$ 的得分是它本身的得分。状态转移方程是

$$
\textit{dp}[i] = \max\{\textit{dp}[j]\}
其中 max⁡(0,i−k)≤j<i\max(0, i - k) \leq j < imax(0,i−k)≤j<i。
$$
其中前 $k$ 步的最大值，使用优先队列可以达到 $O(n\times\log{n})$ 的时间复杂度，使用双端队列可以达到 $O(n)$ 的时间复杂度。具体解释，可以参考下题解[「239. 滑动窗口最大值」](https://leetcode.cn/problems/sliding-window-maximum/solutions/543426/hua-dong-chuang-kou-zui-da-zhi-by-leetco-ki6m/)。

本题解采用双端队列来解决。

## 代码

```python
class Solution:
    def maxResult(self, nums: List[int], k: int) -> int:
        n = len(nums)
        dp = [0] * n
        dp[0] = nums[0]
        queue = deque([0])
        for i in range(1, n):
            while queue and queue[0] < i - k:
                queue.popleft()
            dp[i] = dp[queue[0]] + nums[i]
            while queue and dp[queue[-1]] <= dp[i]:
                queue.pop()
            queue.append(i)
        return dp[n - 1]
```


