# 力扣 1793 好子数组的最大分数


# 好子数组的最大分数

## 题目

> 给你一个整数数组 `nums` **（下标从 0 开始）**和一个整数 `k` 。
>
> 一个子数组 `(i, j)` 的 **分数** 定义为 `min(nums[i], nums[i+1], ..., nums[j]) * (j - i + 1)` 。一个 **好** 子数组的两个端点下标需要满足 `i <= k <= j` 。
>
> 请你返回 **好** 子数组的最大可能 **分数** 。
>
>  
>
> **示例 1：**
>
> ```
> 输入：nums = [1,4,3,7,4,5], k = 3
> 输出：15
> 解释：最优子数组的左右端点下标是 (1, 5) ，分数为 min(4,3,7,4,5) * (5-1+1) = 3 * 5 = 15 。
> ```
>
> **示例 2：**
>
> ```
> 输入：nums = [5,5,4,5,4,1,1,1], k = 0
> 输出：20
> 解释：最优子数组的左右端点下标是 (0, 4) ，分数为 min(5,5,4,5,4) * (4-0+1) = 4 * 5 = 20 。
> ```
>
>  
>
> **提示：**
>
> - `1 <= nums.length <= 105`
> - `1 <= nums[i] <= 2 * 104`
> - `0 <= k < nums.length`

## 题解

### 方法一：双指针

由于好子数组必须要包含 $\textit{nums}[k]$，那么我们可以使用两个指针 $\textit{left}$ 和 $\textit{right}$ 表示选择的子数组为 $(\textit{left}, \textit{right})$ （左开右开），且 $\textit{left}$ 和 $\textit{right}$ 的初始值为 $k-1$ 和 $k+1$。

随后我们可以枚举子数组分数定义中 $\min \{ \cdots \}$ 部分的值。它的最大值为 $\textit{nums}[k]$，最小值为数组 $\textit{nums}$ 中的最小值。随后我们从大到小进行枚举，当枚举到 $i$ 时，我们可以不断向左移动 $\textit{left}$，或者向右移动 $\textit{right}$，直到：

1. 指针超出数组的边界，或者
2. 指针指向的元素小于 $i$，分数定义中的 $\min\{ \cdots \}$ 的值发生了变化。

当移动完成后，$(\textit{left}, \textit{right})$ 就是最小值大于等于 $i$ 的一个子数组，它的分数至少为：

$$
(\textit{right} - \textit{left} - 1) \times i
$$
当 $i$ 恰好是 $(\textit{left}, \textit{right})$ 的最小值时，上式就是它对应的分数。当 $i$ 继续减少但指针没有移动时，上式计算出的分数会比正确的分数要低，但一定不会更高。因此，只要我们在枚举的过程中维护上式的最大值，就可以得到正确的答案。

当两个指针都超出数组的边界时，就可以结束枚举并返回答案。

### 方法二：优化的双指针

我们可以对方法一中的代码进行优化。

方法一效率较低的原因是在 $i$ 比 $(\textit{left}, \textit{right})$ 中的最小值更小，但指针没有移动时，计算出的分数是没有意义的。指针没有移动的原因是 $\textit{nums}[\textit{left}]$ 和 $\textit{nums}[\textit{right}]$ 都小于 $i$，因此我们应当直接把 $i$ 减少至二者的较大值，而不是每次减少 $1$，这样就可以保证每一次循环中都至少会移动一次指针，就可以将 $C$ 从时间复杂度 $O(n+C)$ 中移除。

**细节**

在减少 $i$ 时，需要注意指针已经超出数组边界的情况。

## 代码

**方法一：双指针**

```python
class Solution:
    def maximumScore(self, nums: List[int], k: int) -> int:
        n = len(nums)
        left, right = k - 1, k + 1
        ans = 0
        for i in range(nums[k], 0, -1):
            while left >= 0 and nums[left] >= i:
                left -= 1
            while right < n and nums[right] >= i:
                right += 1
            ans = max(ans, (right - left - 1) * i)
        return ans
```

**方法二：优化的双指针**

```python
class Solution:
    def maximumScore(self, nums: List[int], k: int) -> int:
        n = len(nums)
        left, right, i = k - 1, k + 1, nums[k]
        ans = 0
        while True:
            while left >= 0 and nums[left] >= i:
                left -= 1
            while right < n and nums[right] >= i:
                right += 1
            ans = max(ans, (right - left - 1) * i)
            i = max((-1 if left == -1 else nums[left]), (-1 if right == n else nums[right]))
            if i == -1:
                break
        return ans
```


