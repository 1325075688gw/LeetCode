### [岛屿的周长](https://leetcode-cn.com/problems/island-perimeter/)

#### 1.题目

给定一个包含 0 和 1 的二维网格地图，其中 1 表示陆地 0 表示水域。

网格中的格子水平和垂直方向相连（对角线方向不相连）。整个网格被水完全包围，但其中恰好有一个岛屿（或者说，一个或多个表示陆地的格子相连组成的岛屿）。

岛屿中没有“湖”（“湖” 指水域在岛屿内部且不和岛屿周围的水相连）。格子是边长为 1 的正方形。网格为长方形，且宽度和高度均不超过 100 。计算这个岛屿的周长。

**示例 :**

```
输入:

[[0,1,0,0],
 [1,1,1,0],
 [0,1,0,0],
 [1,1,0,0]]

输出: 16
解释: 它的周长是下面图片中的 16 个黄色的边：

```

![img](岛屿周长_LeetCode_463.assets/island.png)



#### 2.分析



#### 3.代码



```python
    def islandPerimeter(self, grid: List[List[int]]) -> int:
        res = 0
        row, col = len(grid), len(grid[0])
        
        for i in range(row):
            for j in range(col):
                if grid[i][j] == 1:
                    res += 4
                    if i>0 and grid[i-1][j] == 1:
                        res -= 2
                    if j>0 and grid[i][j-1] == 1:
                        res -= 2
                        
        return res
```



```python
    # 由于岛屿内没有湖,所以只需要求出 北面(或南面) + 西面(或东面)的长度再乘2即可
    
        def islandPerimeter(self, grid: List[List[int]]) -> int:
            res = 0
            row, col = len(grid), len(grid[0])
        
            for i in range(row):
                for j in range(col):
                    if grid[i][j] == 1:
                        if i==0 or grid[i-1][j] == 0:
                            res += 1
                        if j==0 or grid[i][j-1] == 0:
                            res += 1
            return res * 2   
```

