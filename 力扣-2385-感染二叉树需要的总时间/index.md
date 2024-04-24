# 力扣 2385 感染二叉树需要的总时间


# 感染二叉树需要的总时间

## 题目

> 给你一棵二叉树的根节点 `root` ，二叉树中节点的值 **互不相同** 。另给你一个整数 `start` 。在第 `0` 分钟，**感染** 将会从值为 `start` 的节点开始爆发。
>
> 每分钟，如果节点满足以下全部条件，就会被感染：
>
> - 节点此前还没有感染。
> - 节点与一个已感染节点相邻。
>
> 返回感染整棵树需要的分钟数*。*
>
>  
>
> **示例 1：**
>
> ![img](https://assets.leetcode.com/uploads/2022/06/25/image-20220625231744-1.png)
>
> ```
> 输入：root = [1,5,3,null,4,10,6,9,2], start = 3
> 输出：4
> 解释：节点按以下过程被感染：
> - 第 0 分钟：节点 3
> - 第 1 分钟：节点 1、10、6
> - 第 2 分钟：节点5
> - 第 3 分钟：节点 4
> - 第 4 分钟：节点 9 和 2
> 感染整棵树需要 4 分钟，所以返回 4 。
> ```
>
> **示例 2：**
>
> ![img](https://assets.leetcode.com/uploads/2022/06/25/image-20220625231812-2.png)
>
> ```
> 输入：root = [1], start = 1
> 输出：0
> 解释：第 0 分钟，树中唯一一个节点处于感染状态，返回 0 。
> ```
>
>  
>
> **提示：**
>
> - 树中节点的数目在范围 `[1, 105]` 内
> - `1 <= Node.val <= 105`
> - 每个节点的值 **互不相同**
> - 树中必定存在值为 `start` 的节点

## 题解

根据题意，需求出值为 $\textit{start}$ 的节点到其他节点最远的距离。树中的最远距离可以用广度优先搜索来求解。但是 $\textit{start}$ 不一定为根节点，我们需要先将树的结构用深度优先搜索解析成无向图，再用广度优先搜索来求最长距离。代码中 $\textit{graph}$ 即为邻接表，用一个哈希表来表示。哈希表的键为节点值，值为其相邻节点的值组成的列表。建完表后用广度优先搜索求最长距离。

## 代码

```python
class Solution:
    def amountOfTime(self, root: Optional[TreeNode], start: int) -> int:
        graph = defaultdict(list)
        def dfs(node: TreeNode) -> None:
            for child in [node.left, node.right]:
                if child:
                    graph[node.val].append(child.val)
                    graph[child.val].append(node.val)
                    dfs(child)
        dfs(root)

        q = deque([[start, 0]])
        visited = set([start])
        time = 0
        while q:
            nodeVal, time = q.popleft()
            for childVal in graph[nodeVal]:
                if childVal not in visited:
                    q.append([childVal, time + 1])
                    visited.add(childVal)
        return time
```


