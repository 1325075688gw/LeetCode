### [岛屿的最大面积](https://leetcode-cn.com/problems/max-area-of-island/)(LeetCode_695)

#### 1.题目

给定一个包含了一些 0 和 1的非空二维数组 grid , 一个 岛屿 是由四个方向 (水平或垂直) 的 1 (代表土地) 构成的组合。你可以假设二维矩阵的四个边缘都被水包围着。

找到给定的二维数组中最大的岛屿面积。(如果没有岛屿，则返回面积为0。)

**示例 1:**

```python
[[0,0,1,0,0,0,0,1,0,0,0,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,1,1,0,1,0,0,0,0,0,0,0,0],
 [0,1,0,0,1,1,0,0,1,0,1,0,0],
 [0,1,0,0,1,1,0,0,1,1,1,0,0],
 [0,0,0,0,0,0,0,0,0,0,1,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,0,0,0,0,0,0,1,1,0,0,0,0]]

```

对于上面这个给定矩阵应返回 `6`。注意答案不应该是11，因为岛屿只能包含水平或垂直的四个方向的‘1’。

**示例 2:**

```
[[0,0,0,0,0,0,0,0]]
```

对于上面这个给定的矩阵, 返回 `0`。

**注意:** 给定的矩阵`grid` 的长度和宽度都不超过 50。

#### 2.分析

- 深度搜索

- ```
  深度优先遍历, 到达边界外或访问到为0的位置则返回0,否则先把该位置的1置为0(作为访问过的标记,相当于visited数组),随后递归访问四个方向, 
  ```



#### 3.代码

```python
lass Solution(object):
    def maxAreaOfIsland(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        self.k = 0
        res = 0
        n, m = len(grid), len(grid[0])
        for i in range(n):
            for j in range(m):
                if grid[i][j] == 1:
                    self.func(n, m, i, j, grid)
                    res = max(res, self.k)
                    self.k = 0
        return res
        
    def func(self, n, m , i, j, grid):
        if i<0 or i>=n or j<0 or j>=m or grid[i][j]!=1:
            return
        grid[i][j] = 2
        self.k += 1
        
        map(self.func,(n,n,n,n),(m,m,m,m),(i-1,i+1,i,i),(j,j,j-1,j+1),(grid,grid,grid,grid))
        
        # self.func(m, n, i+1, j, grid)
        # self.func(m, n, i-1, j, grid)
        # self.func(m, n, i, j+1, grid)
        # self.func(m, n, i, j-1, grid)
```

