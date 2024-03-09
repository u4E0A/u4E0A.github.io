# 力扣 2386 找出数组的第K大和


# 找出数组的第K大和

## 题目

> 给你一个整数数组 `nums` 和一个 **正** 整数 `k` 。你可以选择数组的任一 **子序列** 并且对其全部元素求和。
>
> 数组的 **第 k 大和** 定义为：可以获得的第 `k` 个 **最大** 子序列和（子序列和允许出现重复）
>
> 返回数组的 **第 k 大和** 。
>
> 子序列是一个可以由其他数组删除某些或不删除元素排生而来的数组，且派生过程不改变剩余元素的顺序。
>
> **注意：**空子序列的和视作 `0` 。
>
>  
>
> **示例 1：**
>
> ```
> 输入：nums = [2,4,-2], k = 5
> 输出：2
> 解释：所有可能获得的子序列和列出如下，按递减顺序排列：
> - 6、4、4、2、2、0、0、-2
> 数组的第 5 大和是 2 。
> ```
>
> **示例 2：**
>
> ```
> 输入：nums = [1,-2,3,4,-10,12], k = 16
> 输出：10
> 解释：数组的第 16 大和是 10 。
> ```
>
>  
>
> **提示：**
>
> - `n == nums.length`
> - `1 <= n <= 105`
> - `-109 <= nums[i] <= 109`
> - `1 <= k <= min(2000, 2n)`

## 题解

### 方法一：优先队列

首先，考虑该问题的简化版：给定 $n$ 个非递减的非负数序列 $a_0, a_1, \cdots, a_{n-1}$ ，找出第 k$$ 个最小的子序列和。

当 $k = 1$ 时，空序列即为答案。

当$k \gt 1$，令 $(t, i)$ 表示以 $a_i$ 为最后一个元素且和为 ttt 的子序列，则问题转化为求解第 $k$ 个最小的 $(t, i)$。我们使用一个小根堆来保存 $(t, i)$，初始时堆中只有一个元素 $(a_0, 0)$。为了能按从小到大的顺序依次获得子序列，当我们从小根堆取出堆顶元素 $(t, i)$ 时，我们需要进行以下操作：

- 将 $a_{i + 1}$ 拼接到子序列 $(t, i)$ 后，得到新的子序列 $(t + a_{i + 1}, i + 1)$，并将它加入堆中。

- 将子序列 $(t, i)$ 中的 $a_i$ 替换成 $a_{i+1}$，得到新的子序列 $(t + a_{i + 1} - a_i, i + 1)$，并将它加入堆中。

那么第 $k - 1$ 次取出的堆顶元素对应第 $k$ 个最小的子序列。

> 这种做法可以保证：
>
> 1. 不重复地取出所有的非空子序列
> 2. 依次取出的非空子序列和是非递减的。

根据以上讨论，我们可以求解出非递减的非负数序列的第 $k$ 个最小的子序列和，而原问题给出的条件中，允许序列中有负数。记原序列的非负数和与负数和分别为 $\textit{total}$ 与 $\textit{total}_\textit{neg}$，我们先将原序列中的负数替换成它的绝对值，然后从小到大进行排序，最后求解第 $k$ 个最小的子序列和 $t_k$ 。

$t_k$  对应一个子序列 $s_k$，我们将 $t_k$ 加上 $\textit{total}_\textit{neg}$，那么 $t_k + \textit{total}_\textit{neg}$ 也对应原序列的一个子序列 $s_k'$，该子序列 $s_k'$  的正数元素与 $s_k$ 相同，负数部分由绝对值不存在于 $s_k$ 的负数元素组成。因为 $t_k + \textit{total}_\textit{neg}$ 是非递减的，所以 $s_k'$ 是原序列的第 $k$ 个最小的子序列，$t_k + \textit{total}_\textit{neg}$ 是原序列的第 $k$ 个最小的子序列和。

同时，如果第 $k$ 个最小的子序列和为 $t_k + \textit{total}_\textit{neg}$ ，并且所有序列元素和为 $\textit{total} + \textit{total}_\textit{neg}$，那么 $\textit{total} + \textit{total}_\textit{neg} - (t_k + \textit{total}_\textit{neg}) = \textit{total} - t_k$ 即为第 kkk 个最大的子序列和。

> $\textit{total} - t_k$ 对应没有出现在第 $k$ 个最小的子序列中的元素和，也对应一个子序列，因为 $t_k$ 是非递减的，所以 $\textit{total} - t_k$ 是非递增的，因此 $\textit{total} - t_k$ 即为第 $k$ 个最大的子序列和。

### 方法二：二分

对于问题：给定 $n$ 个非递减的非负数序列 $a_0, a_1, \cdots, a_{n-1}$，找出第 $k$ 个最小的子序列和。除了使用堆，我们还可以使用二分算法来解决。记 $\textit{total}_2$ 为非负数序列的和，令 $\textit{left} = 0, \textit{right} = \textit{total}_2$，那么在区间 $[\textit{left}, \textit{right}]$ 进行二分搜索。

令当前搜索的值为 $\textit{mid} = \lfloor \frac{(\textit{left} + \textit{right})}{2} \rfloor$，令 $\textit{cnt}$ 为和小于等于 $\textit{mid}$ 的非空子序列的个数，求解 $\textit{cnt}$ 可以使用深度优先搜索，假设当前搜索到第 $i$ 个元素，前面已选中的元素和为 $t$：

- 如果 $\textit{cnt} \ge k - 1$ 或 $t + a_i \gt \textit{mid}$，那么说明后续的搜索不必要，直接返回。

- 否则， $t + a_i$ 即对应以 $a_i$ 为最后一个元素的子序列和，将 $\textit{cnt}$ 加一，然后同时对 $(i + 1, t + a_i)$ 和 $(i + 1, t)$ 进行搜索。

最后，如果 $\textit{cnt} \ge k - 1$，令 $\textit{right} = \textit{mid} - 1$，否则令 $\textit{left} = \textit{mid} + 1$。当 $\textit{left} \gt \textit{right}$ 时，$\textit{left}$ 即为第 $k$ 个最小的子序列和。后续问题的求解同方法一。

## 代码

**方法一：优先队列**

```python
class Solution:
    def kSum(self, nums: List[int], k: int) -> int:
        n = len(nums)
        total = 0
        for i in range(n):
            if nums[i] >= 0:
                total += nums[i]
            else:
                nums[i] = -nums[i]
        nums.sort()

        ret = 0
        pq = [(nums[0], 0)]
        for j in range(2, k + 1):
            t, i = heappop(pq)
            ret = t
            if i == n - 1:
                continue
            heappush(pq, (t + nums[i + 1], i + 1))
            heappush(pq, (t - nums[i] + nums[i + 1], i + 1))
        return total - ret
```

**方法二：二分**

```python
class Solution:
    def kSum(self, nums: List[int], k: int) -> int:
        n = len(nums)
        total, total2 = 0, 0
        for i in range(n):
            if nums[i] >= 0:
                total += nums[i]
            else:
                nums[i] = -nums[i]
            total2 += nums[i]
        nums.sort()

        cnt = 0
        def dfs(i: int, t: int, limit: int) -> int:
            nonlocal cnt
            if i == n or cnt >= k - 1 or t + nums[i] > limit:
                return
            cnt += 1
            dfs(i + 1, t + nums[i], limit)
            dfs(i + 1, t, limit)
        
        left, right = 0, total2
        while left <= right:
            mid = (left + right) // 2
            cnt = 0
            dfs(0, 0, mid)
            if cnt >= k - 1:
                right = mid - 1
            else:
                left = mid + 1
        return total - left
```


