# 力扣 2589 完成所有任务的最少时间


# 完成所有任务的最少时间

## 题目

> 你有一台电脑，它可以 **同时** 运行无数个任务。给你一个二维整数数组 `tasks` ，其中 `tasks[i] = [starti, endi, durationi]` 表示第 `i` 个任务需要在 **闭区间** 时间段 `[starti, endi]` 内运行 `durationi` 个整数时间点（但不需要连续）。
>
> 当电脑需要运行任务时，你可以打开电脑，如果空闲时，你可以将电脑关闭。
>
> 请你返回完成所有任务的情况下，电脑最少需要运行多少秒。
>
>  
>
> **示例 1：**
>
> ```
> 输入：tasks = [[2,3,1],[4,5,1],[1,5,2]]
> 输出：2
> 解释：
> - 第一个任务在闭区间 [2, 2] 运行。
> - 第二个任务在闭区间 [5, 5] 运行。
> - 第三个任务在闭区间 [2, 2] 和 [5, 5] 运行。
> 电脑总共运行 2 个整数时间点。
> ```
>
> **示例 2：**
>
> ```
> 输入：tasks = [[1,3,2],[2,5,3],[5,6,2]]
> 输出：4
> 解释：
> - 第一个任务在闭区间 [2, 3] 运行
> - 第二个任务在闭区间 [2, 3] 和 [5, 5] 运行。
> - 第三个任务在闭区间 [5, 6] 运行。
> 电脑总共运行 4 个整数时间点。
> ```
>
>  
>
> **提示：**
>
> - `1 <= tasks.length <= 2000`
> - `tasks[i].length == 3`
> - `1 <= starti, endi <= 2000`
> - `1 <= durationi <= endi - starti + 1 `

## 题解

### 方法一：贪心+暴力

**提示 1**

按照区间右端点从小到大排序。

**提示 2**

排序后，对于区间 $\textit{tasks}[i]$ 来说，它右侧的任务区间要么和它没有交集，要么包含它的一部分后缀。

例如排序后的区间为 $[1,5],[3,7],[6,8]$，对于 $[1,5]$ 来说，它右边的区间要么和它没有交集，例如 $[6,8]$；要么交集是 $[1,5]$ 的后缀，例如 $[1,5]$ 和 $[3,7]$ 的交集是 $[3,5]$，这是 $[1,5]$ 的后缀（$3,4,5$ 是 $1,2,3,4,5$ 的后缀）。

**提示 3**

遍历排序后的任务，先统计区间内的已运行的电脑运行时间点，如果个数小于 $\textit{duration}$，则需要新增时间点。根据**提示 2**，尽量把新增的时间点安排在区间 $[\textit{start},\textit{end}]$ 的后缀上，这样下一个区间就能统计到更多已运行的时间点。

### 方法二：线段树优化

前置知识：线段树。

在**方法一**的暴力更新上优化。

由于有区间更新操作，需要用 lazy 线段树。

对于本题，在更新的时候需要优先递归右子树，从而保证是从右往左更新。其余细节见代码注释。

### 方法三：栈+二分查找

由于每次都是从右到左新增时间点，如果把连续的时间点看成闭区间，那么从右到左新增时间点，会把若干右侧的区间合并成一个大区间，也就是从 $\textit{end}$ 倒着开始，先合并右边，再合并左边，因此可以用栈来优化。

栈中维护闭区间的左右端点，以及从栈底到栈顶的区间长度之和（类似前缀和）。

由于一旦发现区间相交就立即合并，所以栈中保存的都是不相交的区间。

合并前，先尝试在栈中二分查找包含左端点 start\textit{start}start 的区间。由于栈中还保存了区间长度之和，所以可以快速得到 $[\textit{start},\textit{end}]$ 范围内的运行中的时间点个数。

如果还需要新增时间点，那么就从右到左合并，具体细节见代码。

## 代码

**方法一：贪心+暴力**

```python
class Solution:
    def findMinimumTime(self, tasks: List[List[int]]) -> int:
        tasks.sort(key=lambda t: t[1])
        run = [False] * (tasks[-1][1] + 1)
        for start, end, d in tasks:
            d -= sum(run[start: end + 1])  # 去掉运行中的时间点
            if d <= 0:  # 该任务已完成
                continue
            # 该任务尚未完成，从后往前找没有运行的时间点
            for i in range(end, start - 1, -1):
                if run[i]:  # 已运行
                    continue
                run[i] = True  # 运行
                d -= 1
                if d == 0:
                    break
        return sum(run)
```

**方法二：线段树优化**

```python
class Solution:
    def findMinimumTime(self, tasks: List[List[int]]) -> int:
        tasks.sort(key=lambda t: t[1])
        u = tasks[-1][1]
        m = 2 << u.bit_length()
        cnt = [0] * m
        todo = [False] * m

        def do(o: int, l: int, r: int) -> None:
            cnt[o] = r - l + 1
            todo[o] = True

        def spread(o: int, l: int, m: int, r: int) -> None:
            if todo[o]:
                todo[o] = False
                do(o * 2, l, m)
                do(o * 2 + 1, m + 1, r)

        # 查询区间正在运行的时间点 [L,R]   o,l,r=1,1,u
        def query(o: int, l: int, r: int, L: int, R: int) -> int:
            if L <= l and r <= R: return cnt[o]
            m = (l + r) // 2
            spread(o, l, m, r)
            if m >= R: return query(o * 2, l, m, L, R)
            if m < L: return query(o * 2 + 1, m + 1, r, L, R)
            return query(o * 2, l, m, L, R) + query(o * 2 + 1, m + 1, r, L, R)

        # 在区间 [L,R] 的后缀上新增 suffix 个时间点    o,l,r=1,1,u
        # 相当于把线段树二分和线段树更新合并成了一个函数，时间复杂度为 O(log u)
        def update(o: int, l: int, r: int, L: int, R: int) -> None:
            size = r - l + 1
            if cnt[o] == size: return  # 全部为运行中
            nonlocal suffix
            if L <= l and r <= R and size - cnt[o] <= suffix:  # 整个区间全部改为运行中
                suffix -= size - cnt[o]
                do(o, l, r)
                return
            m = (l + r) // 2
            spread(o, l, m, r)
            if m < R: update(o * 2 + 1, m + 1, r, L, R)  # 先更新右子树
            if suffix: update(o * 2, l, m, L, R)  # 再更新左子树（如果还有需要新增的时间点）
            cnt[o] = cnt[o * 2] + cnt[o * 2 + 1]

        for start, end, d in tasks:
            suffix = d - query(1, 1, u, start, end)  # 去掉运行中的时间点
            if suffix > 0: update(1, 1, u, start, end)  # 新增时间点
        return cnt[1]
```

**方法三：栈+二分查找**

```python
class Solution:
    def findMinimumTime(self, tasks: List[List[int]]) -> int:
        tasks.sort(key=lambda t: t[1])
        # 栈中保存闭区间左右端点，栈底到栈顶的区间长度的和
        st = [(-2, -2, 0)]  # 哨兵，保证不和任何区间相交
        for start, end, d in tasks:
            _, r, s = st[bisect_left(st, (start,)) - 1]
            d -= st[-1][2] - s  # 去掉运行中的时间点
            if start <= r:  # start 在区间 st[i] 内
                d -= r - start + 1  # 去掉运行中的时间点
            if d <= 0:
                continue
            while end - st[-1][1] <= d:  # 剩余的 d 填充区间后缀
                l, r, _ = st.pop()
                d += r - l + 1  # 合并区间
            st.append((end - d + 1, end, st[-1][2] + d))
        return st[-1][2]
```


