### 机器人的运动范围

#### 题目描述

​	地上有一个m行和n列的方格。一个机器人从坐标0,0的格子开始移动，每一次只能向左，右，上，下四个方向移动一格，但是不能进入行坐标和列坐标的数位之和大于k的格子。 例如，当k为18时，机器人能够进入方格（35,37），因为3+5+3+7 = 18。但是，它不能进入方格（35,38），因为3+5+3+8 = 19。请问该机器人能够达到多少个格子？



```python
# -*- coding:utf-8 -*-
class Solution:
    def __init__(self):
        self.count = 0
         
    def movingCount(self, threshold, rows, cols):
        # write code here
        grid = [[0 for _ in range(cols)] for _ in range(rows)]
        self.dfs(grid, 0, 0, threshold)
        return self.count
     
    def dfs(self, grid, i, j, k):
        if i < 0 or j < 0 or i >= len(grid) or j >= len(grid[0]):
            return
        if sum(map(int, str(i)+str(j))) > k or grid[i][j] == -1:
            return
        grid[i][j] = -1
        self.count += 1
        self.dfs(grid, i-1, j, k)
        self.dfs(grid, i+1, j, k)
        self.dfs(grid, i, j-1, k)
        self.dfs(grid, i, j+1, k)
```

