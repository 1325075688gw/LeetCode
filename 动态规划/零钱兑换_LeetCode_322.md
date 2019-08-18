#### [零钱兑换](https://leetcode-cn.com/problems/coin-change/)(LeetCode_322)

#### 1.题目

给定不同面额的硬币 coins 和一个总金额 amount。编写一个函数来计算可以凑成总金额所需的最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回 -1。

**示例 1:**

```
输入: coins = [1, 2, 5], amount = 11
输出: 3 
解释: 11 = 5 + 5 + 1
```

**示例 2:**

```
输入: coins = [2], amount = 3
输出: -1
```

**说明**:
你可以认为每种硬币的数量是无限的。

#### 2.分析

完全背包问题

#### 3.代码

```python
# class Solution:
#     # 递归
#     def coinChange(self, coins: List[int], amount: int) -> int:
#         if amount == 0:return 0
#         res = float('inf')
#         for i in range(len(coins)):
#             if coins[i]>amount:
#                 continue
#             tmp = self.coinChange(coins, amount-coins[i])
#             if tmp == -1:
#                 continue
#             res = min(res, tmp+1)
#         return res if res != float('inf') else -1
        
# 从上到下
# class Solution:
#     def coinChange(self, coins: List[int], amount: int) -> int:
#         memo = [-2]*(amount+1)
#         return self.func(coins, amount, memo)
        
#     def func(self, coins, amount, memo):
#         if amount == 0:return 0
#         res = float('inf')
#         if memo[amount] != -2:
#             return memo[amount]
#         for i in range(len(coins)):
#             # 金额不可达
#             if coins[i]>amount:
#                 continue
#             tmp = self.func(coins, amount-coins[i], memo)
#             # 子问题无解
#             if tmp==-1:
#                 continue
#             res = min(res,tmp+1)
#         # 记录本轮答案
#         memo[amount] = res if res != float('inf') else -1
#         return memo[amount]
    
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [amount+1] *(amount+1)
        dp[0] = 0
        for i in range(1,amount+1):
            for j in coins:
                if j<=i:
                    dp[i] = min(dp[i], dp[i-j]+1)
        return -1 if dp[amount] > amount else dp[amount]
        
```

