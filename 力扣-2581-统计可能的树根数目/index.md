# 力扣 2581 统计可能的树根数目


# 统计可能的树根数目

## 题目

> Alice 有一棵 `n` 个节点的树，节点编号为 `0` 到 `n - 1` 。树用一个长度为 `n - 1` 的二维整数数组 `edges` 表示，其中 `edges[i] = [ai, bi]` ，表示树中节点 `ai` 和 `bi` 之间有一条边。
>
> Alice 想要 Bob 找到这棵树的根。她允许 Bob 对这棵树进行若干次 **猜测** 。每一次猜测，Bob 做如下事情：
>
> - 选择两个 **不相等** 的整数 `u` 和 `v` ，且树中必须存在边 `[u, v]` 。
> - Bob 猜测树中 `u` 是 `v` 的 **父节点** 。
>
> Bob 的猜测用二维整数数组 `guesses` 表示，其中 `guesses[j] = [uj, vj]` 表示 Bob 猜 `uj` 是 `vj` 的父节点。
>
> Alice 非常懒，她不想逐个回答 Bob 的猜测，只告诉 Bob 这些猜测里面 **至少** 有 `k` 个猜测的结果为 `true` 。
>
> 给你二维整数数组 `edges` ，Bob 的所有猜测和整数 `k` ，请你返回可能成为树根的 **节点数目** 。如果没有这样的树，则返回 `0`。
>
>  
>
> **示例 1：**
>
> ![img](https://assets.leetcode.com/uploads/2022/12/19/ex-1.png)
>
> ```
> 输入：edges = [[0,1],[1,2],[1,3],[4,2]], guesses = [[1,3],[0,1],[1,0],[2,4]], k = 3
> 输出：3
> 解释：
> 根为节点 0 ，正确的猜测为 [1,3], [0,1], [2,4]
> 根为节点 1 ，正确的猜测为 [1,3], [1,0], [2,4]
> 根为节点 2 ，正确的猜测为 [1,3], [1,0], [2,4]
> 根为节点 3 ，正确的猜测为 [1,0], [2,4]
> 根为节点 4 ，正确的猜测为 [1,3], [1,0]
> 节点 0 ，1 或 2 为根时，可以得到 3 个正确的猜测。
> ```
>
> **示例 2：**
>
> ![img](https://assets.leetcode.com/uploads/2022/12/19/ex-2.png)
>
> ```
> 输入：edges = [[0,1],[1,2],[2,3],[3,4]], guesses = [[1,0],[3,4],[2,1],[3,2]], k = 1
> 输出：5
> 解释：
> 根为节点 0 ，正确的猜测为 [3,4]
> 根为节点 1 ，正确的猜测为 [1,0], [3,4]
> 根为节点 2 ，正确的猜测为 [1,0], [2,1], [3,4]
> 根为节点 3 ，正确的猜测为 [1,0], [2,1], [3,2], [3,4]
> 根为节点 4 ，正确的猜测为 [1,0], [2,1], [3,2]
> 任何节点为根，都至少有 1 个正确的猜测。
> ```
>
>  
>
> **提示：**
>
> - `edges.length == n - 1`
> - `2 <= n <= 105`
> - `1 <= guesses.length <= 105`
> - `0 <= ai, bi, uj, vj <= n - 1`
> - `ai != bi`
> - `uj != vj`
> - `edges` 表示一棵有效的树。
> - `guesses[j]` 是树中的一条边。
> - `guesses` 是唯一的。
> - `0 <= k <= guesses.length`

## 题解

首先计算固定树根时猜对的次数，假设以 $0$ 号节点为树根，从它开始执行深度优先搜索，使用哈希表统计所有树边 $(x, y)$ 在 $\textit{guesses}$ 中出现的个数，其中 $x$ 是 $y$ 的父节点。

然后考虑树根从 $0$ 移动到 $0$ 的子节点后，所有 $\textit{guesses}$ 的状态变化。如下图所示，树根从 $x$ 变成 $y$ 之后，只有 $(x, y)$ 和 $(y, x)$ 这两个猜测的正确性发生变化。

![pic1](https://assets.leetcode-cn.com/solution-static/2581/2581.png)

因此基于已经计算出以 $x$ 为树根时猜对的次数，很容易就可以计算出以 $y$ 为树根时猜对的次数：

- 如果 $(x, y)$ 存在 $\textit{guesses}$，猜对次数减一；
- 如果 $(y, x)$ 存在于 $\textit{guesses}$，猜对次数加一。
  最终答案就是所有猜对次数大于等于 $k$ 的节点个数。

需要注意的是，某些语言可能需要手写树边 $(x, y)$ 的哈希函数，由于树上节点编号不超过 $10^5$ ，而且 $2^{20} > 10^5$ ，因此我们可以用 $x \times 2^{20} + y$ 作为哈希函数。

## 代码

```python
class Solution:
    def rootCount(self, edges: List[List[int]], guesses: List[List[int]], k: int) -> int:
        n = len(edges) + 1
        g = [[] for _ in range(n)]
        st = set()
        
        def h(x, y):
            return x << 20 | y
        for x, y in edges:
            g[x].append(y)
            g[y].append(x)
        for u, v in guesses:
            st.add(h(u, v))

        res, cnt = 0, 0
        def dfs(x, fat):
            nonlocal cnt
            for y in g[x]:
                if y == fat:
                    continue
                cnt += h(x, y) in st
                dfs(y, x)
        dfs(0, -1)

        def redfs(x, fat, cnt):
            nonlocal res
            if cnt >= k:
                res += 1
            for y in g[x]:
                if y == fat:
                    continue
                redfs(y, x, cnt - (h(x, y) in st) + (h(y, x) in st))
        redfs(0, -1, cnt)

        return res
```


