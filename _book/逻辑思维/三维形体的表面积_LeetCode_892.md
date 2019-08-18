### [三维形体的表面积](https://leetcode-cn.com/problems/surface-area-of-3d-shapes/)

#### 1.题目

在 N * N 的网格上，我们放置一些 1 * 1 * 1  的立方体。

每个值 v = grid[i][j] 表示 v 个正方体叠放在对应单元格 (i, j) 上。

请你返回最终形体的表面积。

**示例 1：**

```
输入：[[2]]
输出：10
```

**示例 2：**

```
输入：[[1,2],[3,4]]
输出：34
```

**示例 3：**

```
输入：[[1,0],[0,2]]
输出：16
```



#### 2.分析

和463岛屿周长一模一样

#### 3.代码



```python
class Solution:
    def surfaceArea(self, grid: List[List[int]]) -> int:
        row, col = len(grid), len(grid[0])
        
        res = 0
        for i in range(row):
            for j in range(col):
                if grid[i][j]:
                    # 假设每个v=grid[i][j]都是独立的,每一个坐标都可以提供 4*(个数) + 2 面积.
                    res += grid[i][j]*4 + 2
                    # 减去面贴在一起的情况
                    if i>0 and grid[i-1][j]:
                        res -= min(grid[i][j], grid[i-1][j]) * 2
                    if j>0 and grid[i][j-1]:
                        res -= min(grid[i][j], grid[i][j-1]) * 2
        return res
```

