# 力扣 518 零钱兑换II


# 零钱兑换II

## 题目

> 给你一个整数数组 `coins` 表示不同面额的硬币，另给一个整数 `amount` 表示总金额。
>
> 请你计算并返回可以凑成总金额的硬币组合数。如果任何硬币组合都无法凑出总金额，返回 `0` 。
>
> 假设每一种面额的硬币有无限个。 
>
> 题目数据保证结果符合 32 位带符号整数。
>
>  
>
> 
>
> **示例 1：**
>
> ```
> 输入：amount = 5, coins = [1, 2, 5]
> 输出：4
> 解释：有四种方式可以凑成总金额：
> 5=5
> 5=2+2+1
> 5=2+1+1+1
> 5=1+1+1+1+1
> ```
>
> **示例 2：**
>
> ```
> 输入：amount = 3, coins = [2]
> 输出：0
> 解释：只用面额 2 的硬币不能凑成总金额 3 。
> ```
>
> **示例 3：**
>
> ```
> 输入：amount = 10, coins = [10] 
> 输出：1
> ```
>
>  
>
> **提示：**
>
> - `1 <= coins.length <= 300`
> - `1 <= coins[i] <= 5000`
> - `coins` 中的所有值 **互不相同**
> - `0 <= amount <= 5000`

## 题解

1. 思考一：为什么这种循环顺序不会造成重复排列。如果是以下循环顺序，会怎么样。

   ```python
           for k, _ in enumerate(amounts):
               for i in coins:
   ```

   

2. 思考二：如果要求凑出金额的最少硬币个数，该如何修改代码。[322. 零钱兑换](https://leetcode.cn/problems/coin-change/)

## 代码

```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        coins = set(i for i in coins if i <= amount)
        amounts = [0 for _ in range(amount + 1)]
        amounts[0] = 1
        for i in coins:
            for k, _ in enumerate(amounts):
                if k - i >= 0 and amounts[k - i] != 0:
                    amounts[k] += amounts[k - i]
        return amounts[amount]
```

**思考二**

```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        if amount == 0:
            return 0
        coins = [i for i in coins if i <= amount]
        amounts = [-1 for _ in range(amount + 1)]
        for i in coins:
            amounts[i] = 1
        for k, v in enumerate(amounts):
            if v == 1:
                continue
            for i in coins:
                if k - i > 0 and amounts[k - i] != -1:
                    if amounts[k] != -1:
                        amounts[k] = min(amounts[k], amounts[k - i] + 1)
                    else:
                        amounts[k] = amounts[k - i] + 1
        return amounts[amount]
```


