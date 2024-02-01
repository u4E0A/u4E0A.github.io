# 力扣 LCP 24 数字游戏


# 数字游戏

## 题目

> 小扣在秋日市集入口处发现了一个数字游戏。主办方共有 `N` 个计数器，计数器编号为 `0 ~ N-1`。每个计数器上分别显示了一个数字，小扣按计数器编号升序将所显示的数字记于数组 `nums`。每个计数器上有两个按钮，分别可以实现将显示数字加一或减一。小扣每一次操作可以选择一个计数器，按下加一或减一按钮。
>
> 主办方请小扣回答出一个长度为 `N` 的数组，第 `i` 个元素(0 <= i < N)表示将 `0~i` 号计数器 **初始** 所示数字操作成满足所有条件 `nums[a]+1 == nums[a+1],(0 <= a < i)` 的最小操作数。回答正确方可进入秋日市集。
>
> 由于答案可能很大，请将每个最小操作数对 `1,000,000,007` 取余。
>
> **示例 1：**
>
> > 输入：`nums = [3,4,5,1,6,7]`
> >
> > 输出：`[0,0,0,5,6,7]`
> >
> > 解释： i = 0，[3] 无需操作 i = 1，[3,4] 无需操作； i = 2，[3,4,5] 无需操作； i = 3，将 [3,4,5,1] 操作成 [3,4,5,6], 最少 5 次操作； i = 4，将 [3,4,5,1,6] 操作成 [3,4,5,6,7], 最少 6 次操作； i = 5，将 [3,4,5,1,6,7] 操作成 [3,4,5,6,7,8]，最少 7 次操作； 返回 [0,0,0,5,6,7]。
>
> **示例 2：**
>
> > 输入：`nums = [1,2,3,4,5]`
> >
> > 输出：`[0,0,0,0,0]`
> >
> > 解释：对于任意计数器编号 i 都无需操作。
>
> **示例 3：**
>
> > 输入：`nums = [1,1,1,2,3,4]`
> >
> > 输出：`[0,1,2,3,3,3]`
> >
> > 解释： i = 0，无需操作； i = 1，将 [1,1] 操作成 [1,2] 或 [0,1] 最少 1 次操作； i = 2，将 [1,1,1] 操作成 [1,2,3] 或 [0,1,2]，最少 2 次操作； i = 3，将 [1,1,1,2] 操作成 [1,2,3,4] 或 [0,1,2,3]，最少 3 次操作； i = 4，将 [1,1,1,2,3] 操作成 [-1,0,1,2,3]，最少 3 次操作； i = 5，将 [1,1,1,2,3,4] 操作成 [-1,0,1,2,3,4]，最少 3 次操作； 返回 [0,1,2,3,3,3]。
>
> **提示：**
>
> - `1 <= nums.length <= 10^5`
> - `1 <= nums[i] <= 10^3`

## 题解

**将 $[0, i]$ 范围内的计数器初始所示数字操作成满足所有条件  $\textit{nums}[j] + 1 = \textit{nums}[j + 1], j \in [0, i)$，等价于，将 $\textit{nums}[j] - j, j \in [0, i)$ 操作成相同的数字。**因此，先对数组 $\textit{nums}$ 作预处理，即令 $\textit{nums}[i] = \textit{nums}[i] - i$。

将区间 $[0, i]$ 范围内的数字操作成相同的数字的最小操作数，等于将区间 $[0,i]$ 范围内的数字操作成它们的中位数所需要的操作数。证明过程可以参考[462. 最小操作次数使数组元素相等 II](https://leetcode.cn/problems/minimum-moves-to-equal-array-elements-ii/solutions/1501230/zui-shao-yi-dong-ci-shu-shi-shu-zu-yuan-xt3r2/)。

我们分别使用两个优先队列 $\textit{lower}$ 和 $\textit{upper}$ 来保存 $[0,i]$ 内的数字，同时使用 $\textit{lowerSum}$ 和 $\textit{upperSum}$ 分别保存两个优先队列的元素和，这两个优先队列中的元素满足以下两个条件：

1. 优先队列 $\textit{lower}$ 保存的任一元素都小于等于优先队列 $\textit{upper}$ 保存的任一元素；
2. 优先队列 $\textit{lower}$ 的元素数目 $n_\textit{lower}$  与优先队列 $\textit{upper}$ 的元素数目 $n_\textit{upper}$  满足 $n_\textit{upper} \le n_\textit{lower} \le n_\textit{upper} + 1$

遍历数组 $\textit{nums}$，假设当前遍历到元素 $\textit{nums}[i]$，考虑如何将元素 $\textit{nums}[i]$ 加入优先队列，同时不违反以上条件。首先如果 $\textit{lower}$ 为空或 $\textit{nums}[i]$ 小于 $\textit{lower}$ 的最大元素，那么我们将 $\textit{nums}[i]$ 加入 $\textit{lower}$，更新 $\textit{lowerSum}$，否则将 $\textit{nums}[i]$ 加入 $\textit{upper}$ 中，更新 $\textit{upperSum}$，此时条件 $1$ 依旧满足。然后我们需要调整优先队列的元素数目关系，以满足条件 $2$：

- 如果 $n_\textit{lower} \gt n_\textit{upper}$ ，那么将 $\textit{lower}$ 的最大值移动到 $\textit{upper}$，同时更新  和 $\textit{upperSum}$。
- 如果 $n_\textit{lower} \lt n_\textit{upper}$ ，那么将 $\textit{upper}$ 的最小值移动到 $\textit{lower}$，同时更新 $\textit{lowerSum}$ 和 $\textit{upperSum}$。

那么：

- 当 $i+1$ 为偶数时，令中位数为 $t$，那么有 $\max(\textit{lower}) \le t \le \min(\textit{upper})$，从而 $\textit{res}_i = \sum_{j=0}^{i}|\textit{nums}[j] - t| = \textit{upperSum} - \textit{lowerSum}$。

- 当 $i+1$ 为奇数时，中位数 $t = \max(\textit{lower})$，$\textit{res}_i = \sum_{j=0}^{i}|\textit{nums}[j] - t| = \textit{upperSum} - \textit{lowerSum} + \max(\textit{lower})$。

返回结果数组 $\textit{res}$ 即可。

> 类似的求解中位数的题目有 295. 数据流的中位数

## 代码

```python
class Solution:
    def numsGame(self, nums: List[int]) -> List[int]:
        n = len(nums)
        res = [0] * n
        lower, upper = [], []
        lowerSum, upperSum = 0, 0
        mod = int(1e9 + 7)
        for i in range(n):
            x = nums[i] - i
            if len(lower) == 0 or -lower[0] >= x:
                lowerSum += x
                heappush(lower, -x)
                if len(lower) > len(upper) + 1:
                    upperSum -= lower[0]
                    heappush(upper, -lower[0])
                    lowerSum += heappop(lower)
            else:
                upperSum += x
                heappush(upper, x)
                if len(lower) < len(upper):
                    lowerSum += upper[0]
                    heappush(lower, -upper[0])
                    upperSum -= heappop(upper)
            if (i + 1) % 2 == 0:
                res[i] = (upperSum - lowerSum) % mod
            else:
                res[i] = (upperSum - lowerSum - lower[0]) % mod
        return res
```


