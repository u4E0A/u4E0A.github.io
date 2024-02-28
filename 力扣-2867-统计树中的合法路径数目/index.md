# 力扣 2867 统计树中的合法路径数目


# 统计树中的合法路径数目

## 题目

> 给你一棵 `n` 个节点的无向树，节点编号为 `1` 到 `n` 。给你一个整数 `n` 和一个长度为 `n - 1` 的二维整数数组 `edges` ，其中 `edges[i] = [ui, vi]` 表示节点 `ui` 和 `vi` 在树中有一条边。
>
> 请你返回树中的 **合法路径数目** 。
>
> 如果在节点 `a` 到节点 `b` 之间 **恰好有一个** 节点的编号是质数，那么我们称路径 `(a, b)` 是 **合法的** 。
>
> **注意：**
>
> - 路径 `(a, b)` 指的是一条从节点 `a` 开始到节点 `b` 结束的一个节点序列，序列中的节点 **互不相同** ，且相邻节点之间在树上有一条边。
> - 路径 `(a, b)` 和路径 `(b, a)` 视为 **同一条** 路径，且只计入答案 **一次** 。
>
>  
>
> **示例 1：**
>
> ![img](https://assets.leetcode.com/uploads/2023/08/27/example1.png)
>
> ```
> 输入：n = 5, edges = [[1,2],[1,3],[2,4],[2,5]]
> 输出：4
> 解释：恰好有一个质数编号的节点路径有：
> - (1, 2) 因为路径 1 到 2 只包含一个质数 2 。
> - (1, 3) 因为路径 1 到 3 只包含一个质数 3 。
> - (1, 4) 因为路径 1 到 4 只包含一个质数 2 。
> - (2, 4) 因为路径 2 到 4 只包含一个质数 2 。
> 只有 4 条合法路径。
> ```
>
> **示例 2：**
>
> ![img](https://assets.leetcode.com/uploads/2023/08/27/example2.png)
>
> ```
> 输入：n = 6, edges = [[1,2],[1,3],[2,4],[3,5],[3,6]]
> 输出：6
> 解释：恰好有一个质数编号的节点路径有：
> - (1, 2) 因为路径 1 到 2 只包含一个质数 2 。
> - (1, 3) 因为路径 1 到 3 只包含一个质数 3 。
> - (1, 4) 因为路径 1 到 4 只包含一个质数 2 。
> - (1, 6) 因为路径 1 到 6 只包含一个质数 3 。
> - (2, 4) 因为路径 2 到 4 只包含一个质数 2 。
> - (3, 6) 因为路径 3 到 6 只包含一个质数 3 。
> 只有 6 条合法路径。
> ```
>
>  
>
> **提示：**
>
> - `1 <= n <= 105`
> - `edges.length == n - 1`
> - `edges[i].length == 2`
> - `1 <= ui, vi <= n`
> - 输入保证 `edges` 形成一棵合法的树。

## 题解

根据题意，我们需要知道一个数是不是质数，可以采用「埃氏筛」来找出范围内所有的质数。关于质数筛选，可以参考题解[204. 计数质数](https://leetcode.cn/problems/count-primes/solutions/507273/ji-shu-zhi-shu-by-leetcode-solution/)。

然后我们分别以质数节点为根，用「深度优先搜索」的方式，递归搜索所有的非质数的子树，并求出所有子树的大小，搜索过程中只搜索非质数节点。任何两个来自不同子树的节点，其路径都通过质数根节点，路径上恰好只有根节点一个质数节点，根据题意路径是合法的。我们只需要把所子树大小，两两相乘并求和，就可以得到包含根节点的所有合法路径。

遍历所有质数节点，并且重复上述过程，便可以得到所有合法路径的数目，返回为最终结果。

## 代码

```python
# 埃氏筛
N = 10001
is_prime = [True] * N
is_prime[1] = False
for i in range(2, N):
    if is_prime[i]:
        for j in range(i * i, N, i):
            is_prime[j] = False

class Solution:
    def countPaths(self, n: int, edges: List[List[int]]) -> int:
        G = [[] for _ in range(n + 1)]
        for i, j in edges:
            G[i].append(j)
            G[j].append(i)

        def dfs(i, pre):
            seen.append(i)
            for j in G[i]:
                if j != pre and not is_prime[j]:
                    dfs(j, i)

        res = 0
        count = [0] * (n + 1)
        for i in range(1, n + 1):
            if not is_prime[i]:
                continue
            cur = 0
            for j in G[i]:
                if is_prime[j]:
                    continue
                if count[j] == 0:
                    seen = []
                    dfs(j, 0)
                    for k in seen:
                        count[k] = len(seen)
                res += count[j] * cur
                cur += count[j]
            res += cur
        return res
```


