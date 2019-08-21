### [粉刷房子 II](https://leetcode-cn.com/problems/paint-house-ii/)(LeetCode_265)

#### 1.题目

假如有一排房子，共 n 个，每个房子可以被粉刷成 k 种颜色中的一种，你需要粉刷所有的房子并且使其相邻的两个房子颜色不能相同。

当然，因为市场上不同颜色油漆的价格不同，所以房子粉刷成不同颜色的花费成本也是不同的。每个房子粉刷成不同颜色的花费是以一个 n x k 的矩阵来表示的。

例如，costs[0][0] 表示第 0 号房子粉刷成 0 号颜色的成本花费；costs[1][2] 表示第 1 号房子粉刷成 2 号颜色的成本花费，以此类推。请你计算出粉刷完所有房子最少的花费成本。

**注意：**

所有花费均为正整数。

**示例：**

```python
输入: [[1,5,3],[2,9,4]]
输出: 5
解释: 将 0 号房子粉刷成 0 号颜色，1 号房子粉刷成 2 号颜色。最少花费: 1 + 4 = 5; 
     或者将 0 号房子粉刷成 2 号颜色，1 号房子粉刷成 0 号颜色。最少花费: 3 + 2 = 5. 

```





#### 2.分析

- 动态规划

#### 3.代码

```python
class Solution:
    def minCostII(self, costs: List[List[int]]) -> int:
        if not costs: return 0
        n = len(costs[0])
        for i in range(1, len(costs)):
            for j in range(n):
                tmp = costs[i-1][:j] + costs[i-1][j+1:]
                costs[i][j] += min(tmp)
        return min(costs[-1])
        
        if not costs: return 0
        n, m = len(costs), len(costs[0])
        dp = [[0]*m for _ in range(n)]
        dp[0] = costs[0]
        
        for i in range(1,n):
            for j in range(m):
                # dp[i-1][:j] + dp[i-1][j+1:] 列表拼接,理解这点了,就OK了
                dp[i][j] = min(dp[i-1][:j] + dp[i-1][j+1:]) + costs[i][j]
        return min(dp[-1])
        
```

