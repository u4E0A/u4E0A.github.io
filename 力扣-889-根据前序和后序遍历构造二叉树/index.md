# 力扣 889 根据前序和后序遍历构造二叉树


# 根据前序和后序遍历构造二叉树

## 题目

> 给定两个整数数组，`preorder` 和 `postorder` ，其中 `preorder` 是一个具有 **无重复** 值的二叉树的前序遍历，`postorder` 是同一棵树的后序遍历，重构并返回二叉树。
>
> 如果存在多个答案，您可以返回其中 **任何** 一个。
>
>  
>
> **示例 1：**
>
> ![img](https://assets.leetcode.com/uploads/2021/07/24/lc-prepost.jpg)
>
> ```
> 输入：preorder = [1,2,4,5,3,6,7], postorder = [4,5,2,6,7,3,1]
> 输出：[1,2,3,4,5,6,7]
> ```
>
> **示例 2:**
>
> ```
> 输入: preorder = [1], postorder = [1]
> 输出: [1]
> ```
>
>  
>
> **提示：**
>
> - `1 <= preorder.length <= 30`
> - `1 <= preorder[i] <= preorder.length`
> - `preorder` 中所有值都 **不同**
> - `postorder.length == preorder.length`
> - `1 <= postorder[i] <= postorder.length`
> - `postorder` 中所有值都 **不同**
> - 保证 `preorder` 和 `postorder` 是同一棵二叉树的前序遍历和后序遍历

## 题解

#### 方法一：递归

前序遍历为：

- （根结点）（前序遍历左分支）（前序遍历右分支）

而后序遍历为：

- （后序遍历左分支）（后序遍历右分支）（根结点）

例如，如果最终的二叉树可以被序列化的表述为 $[1, 2, 3, 4, 5, 6, 7]$，那么其前序遍历为 $[1] + [2, 4, 5] + [3, 6, 7]$，而后序遍历为 $[4, 5, 2] + [6, 7, 3] + [1]$。

如果我们知道左分支有多少个结点，我们就可以对这些数组进行分组，并用递归生成树的每个分支。

我们令左分支有 $L$ 个节点。我们知道左分支的头节点为 $pre[1]$，但它也出现在左分支的后序表示的最后。所以 $pre[1] = post[L-1]$（因为结点的值具有唯一性），因此 $L = post.indexOf(pre[1]) + 1$。

现在在我们的递归步骤中，左分支由 $pre[1 : L+1]$ 和 $post[0:L]$ 重新分支，而右分支将由 $pre[L+1 : N]$ 和 $post[L : N-1]$ 重新分支。

#### 方法二：递归（优化）

令 $n$ 为二叉树的节点数目，那么根据前序遍历与后序遍历的定义，$\textit{preorder}[0]$ 与 $\textit{postorder}[n - 1]$ 都对应二叉树的根节点。获取根节点后，我们需要划分根节点的左子树与右子树，考虑两种情况：

- 原二叉树的根节点的左子树不为空，那么 $\textit{preorder}[1]$ 对应左子树的根节点；

- 原二叉树的根节点的左子树为空，那么 $\textit{preorder}[1]$ 对应右子树的根节点。

对于以上两种情况，我们无法区分 $\textit{preorder}[1]$ 到底是哪种情况。但是对于第二种情况，将原二叉树的右子树移到左子树后得到的二叉树的前序遍历数组与后序遍历数组与原二叉树相同，所以我们只需要考虑第一种情况。因为二叉树的值互不相同，我们可以在 $\textit{postorder}$ 中找到 $\textit{postorder}[k] = \textit{preorder}[1]$，那么左子树的节点数目为 $k + 1$。基于此，我们可以对 $\textit{preorder}$ 和 $\textit{postorder}$ 进行分治处理，即将 $\textit{preorder}$ 划分为根节点、左子树节点和右子树节点三个部分，$\textit{postorder}$ 也划分为左子树节点、右子树节点和根节点三个部分。那么问题划分为：

- 根据左子树节点的前序遍历与后序遍历数组构造二叉树；

- 根据右子树节点的前序遍历与后序遍历数组构造二叉树。

同时当节点数目为 $1$ 时，对应构造的二叉树只有一个节点。我们可以递归地对问题进行求解，就可得到构造的二叉树。

## 代码

**方法一：递归**

```python
class Solution(object):
    def constructFromPrePost(self, pre, post):
        if not pre: return None
        root = TreeNode(pre[0])
        if len(pre) == 1: return root

        L = post.index(pre[1]) + 1
        root.left = self.constructFromPrePost(pre[1:L+1], post[:L])
        root.right = self.constructFromPrePost(pre[L+1:], post[L:-1])
        return root
```

**方法二：递归（优化）**

```python
class Solution:
    def constructFromPrePost(self, preorder: List[int], postorder: List[int]) -> Optional[TreeNode]:
        postMap = {x: i for i, x in enumerate(postorder)}
        def dfs(preLeft, preRight, postLeft, postRight):
            if preLeft > preRight:
                return None
            leftCount = 0
            if preLeft < preRight:
                leftCount = postMap[preorder[preLeft + 1]] - postLeft + 1
            return TreeNode(preorder[preLeft],
                dfs(preLeft + 1, preLeft + leftCount, postLeft, postLeft + leftCount - 1),
                dfs(preLeft + leftCount + 1, preRight, postLeft + leftCount, postRight - 1))
        
        return dfs(0, len(preorder) - 1, 0, len(postorder) - 1)
```


