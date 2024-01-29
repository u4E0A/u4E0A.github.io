# 力扣 514 自由之路


# 自由之路

## 题目

> 电子游戏“辐射4”中，任务 **“通向自由”** 要求玩家到达名为 “**Freedom Trail Ring”** 的金属表盘，并使用表盘拼写特定关键词才能开门。
>
> 给定一个字符串 `ring` ，表示刻在外环上的编码；给定另一个字符串 `key` ，表示需要拼写的关键词。您需要算出能够拼写关键词中所有字符的**最少**步数。
>
> 最初，**ring** 的第一个字符与 `12:00` 方向对齐。您需要顺时针或逆时针旋转 `ring` 以使 **key** 的一个字符在 `12:00` 方向对齐，然后按下中心按钮，以此逐个拼写完 **`key`** 中的所有字符。
>
> 旋转 `ring` 拼出 key 字符 `key[i]` 的阶段中：
>
> 1. 您可以将 **ring** 顺时针或逆时针旋转 **一个位置** ，计为1步。旋转的最终目的是将字符串 **`ring`** 的一个字符与 `12:00` 方向对齐，并且这个字符必须等于字符 **`key[i]` 。**
> 2. 如果字符 **`key[i]`** 已经对齐到12:00方向，您需要按下中心按钮进行拼写，这也将算作 **1 步**。按完之后，您可以开始拼写 **key** 的下一个字符（下一阶段）, 直至完成所有拼写。
>
>  
>
> **示例 1：**
>
> ![img](https://assets.leetcode.com/uploads/2018/10/22/ring.jpg)
>
>  
>
> ```
> 输入: ring = "godding", key = "gd"
> 输出: 4
> 解释:
>  对于 key 的第一个字符 'g'，已经在正确的位置, 我们只需要1步来拼写这个字符。 
>  对于 key 的第二个字符 'd'，我们需要逆时针旋转 ring "godding" 2步使它变成 "ddinggo"。
>  当然, 我们还需要1步进行拼写。
>  因此最终的输出是 4。
> ```
>
> **示例 2:**
>
> ```
> 输入: ring = "godding", key = "godding"
> 输出: 13
> ```
>
>  
>
> **提示：**
>
> - `1 <= ring.length, key.length <= 100`
> - `ring` 和 `key` 只包含小写英文字母
> - **保证** 字符串 `key` 一定可以由字符串  `ring` 旋转拼出

## 题解

定义 $\textit{dp}[i][j]$ 表示从前往后拼写出 key\textit{key}key 的第 iii 个字符， $\textit{ring}$ 的第 $j$ 个字符与 12:00 方向对齐的最少步数（下标均从 $0$ 开始）。

显然，只有当字符串 $\textit{ring}$ 的第 $j$ 个字符需要和 $\textit{key}$ 的第 $i$ 个字符相同时才能拼写出 $\textit{key}$ 的第 $i$ 个字符，因此对于 $\textit{key}$ 的第 $i$ 个字符，需要考虑计算的 $\textit{ring}$ 的第 $j$ 个字符只有 $\textit{key}[i]$ 在 $r\textit{ring}$ 中出现的下标集合。我们对每个字符维护一个位置数组 $\textit{pos}[i]$，表示字符 $i$ 在 $\textit{ring}$ 中出现的位置集合，用来加速计算转移的过程。

对于状态 $\textit{dp}[i][j]$，需要枚举上一次与 12:00 方向对齐的位置 $k$，因此可以列出如下的转移方程：

$$
\textit{dp}[i][j]=\min_{k \in pos[key[i-1]]}\{dp[i-1][k]+\min\{\text{abs}(j-k),n-\text{abs}(j-k)\}+1\}
$$

其中 $\min\{\text{abs}(j-k),n-\text{abs}(j-k)\}+1$ 表示在当前第 $k$ 个字符与 12:00 方向对齐时第 $j$ 个字符旋转到 12:00 方向并按下拼写的最少步数。

最后答案即为 $\min_{i=0}^{n-1}\{\textit{dp}[m-1][i]\}$

这样的做法需要开辟 $O(mn)$ 的空间来存放 $\textit{dp}$ 值。考虑到每次转移状态 $\textit{dp}[i][]$ 只会从 $\textit{dp}[i-1][]$ 转移过来，因此我们可以利用滚动数组优化第一维的空间复杂度，有能力的读者可以尝试实现。下面只给出最朴素的 $O(mn)$ 空间复杂度的实现。

## 代码

```python
class Solution:
    def findRotateSteps(self, ring: str, key: str) -> int:
        n, m = len(ring), len(key)
        pos = [[] for _ in range(26)]
        for i in range(n):
            pos[ord(ring[i]) - ord('a')].append(i)
        dp = [[0x3f3f3f3f for _ in range(n)] for _ in range(m)]
        for i in pos[ord(key[0]) - ord('a')]:
            dp[0][i] = min(i, n - i) + 1
        for i in range(1, m):
            for j in pos[ord(key[i]) - ord('a')]:
                for k in pos[ord(key[i - 1]) - ord('a')]:
                    dp[i][j] = min(dp[i][j], dp[i - 1][k] + min(abs(j - k), n - abs(j - k)) + 1)
        return min(dp[m - 1])
```


