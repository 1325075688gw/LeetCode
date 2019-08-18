#### [不同路径 II](https://leetcode-cn.com/problems/unique-paths-ii/)(LeetCode_63)

#### 1.题目

一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

![img](不同路径2_LeetCode_63.assets/robot_maze.png)

网格中的障碍物和空位置分别用 `1` 和 `0` 来表示。

**说明：***m* 和 *n* 的值均不超过 100。

**示例 1:**

```python
输入:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
输出: 2
解释:
3x3 网格的正中间有一个障碍物。
从左上角到右下角一共有 2 条不同的路径：
1. 向右 -> 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右 -> 向右
```

#### 2.分析

- 对第一行第一列特殊处理
- 在左边和上边各加一条边界

#### 3.代码

**特殊处理**

```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:    
        if not obstacleGrid or not obstacleGrid[0]: return 0
        row = len(obstacleGrid)
        col = len(obstacleGrid[0])
        if obstacleGrid[0][0] == 1:return 0
        dp = [[0]*col for _ in range(row)]
        dp[0][0] = 1
        for i in range(1,row):
            if obstacleGrid[i][0] == 0:
            	dp[i][0] = dp[i-1][0]
        for j in range(1,col):
            if obstacleGrid[0][j] == 0:
                dp[0][j] = dp[0][j-1]
        for i in range(1,row):
            for j in range(1,col):
                if obstacleGrid[i][j] == 0:
                    dp[i][j] = dp[i-1][j] + dp[i][j-1]
        return dp[-1][-1]
  
```

**在左边和上边各加一条边界**

```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        if not obstacleGrid or not obstacleGrid[0]: return 0
        if obstacleGrid[0][0]==1: return 0
        row = len(obstacleGrid)+1
        col = len(obstacleGrid[0])+1
        if obstacleGrid[row-2][-1] == 1 or obstacleGrid[-1][col-2]:return 0
        
        dp = [[0]*(col) for _ in range(row)]
        for i in range(1,row):
            for j in range(1,col):
                if i==1 and j==1:
                    if obstacleGrid[i-1][j-1] == 1:
                        return 0
                    else:
                        dp[1][1] = 1
                else:
                    if obstacleGrid[i-1][j-1] == 1:
                        pass
                    else:
                        dp[i][j] = dp[i-1][j]+ dp[i][j-1]
       
        return dp[-1][-1]
```

**在左边和上边各加一条边界（简写）**

```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        if not obstacleGrid or not obstacleGrid[0]: return 0
        if obstacleGrid[0][0]==1: return 0
        row = len(obstacleGrid)+1
        col = len(obstacleGrid[0])+1
        if obstacleGrid[row-2][-1] == 1 or obstacleGrid[-1][col-2]:return 0
        
        dp = [[0]*(col) for _ in range(row)]
        for i in range(1,row):
            for j in range(1,col):
                if i==1 and j==1:
                    dp[1][1] = 1
                else:
                    if obstacleGrid[i-1][j-1] == 0:
                        dp[i][j] = dp[i-1][j]+ dp[i][j-1]
       
        return dp[-1][-1]
```

