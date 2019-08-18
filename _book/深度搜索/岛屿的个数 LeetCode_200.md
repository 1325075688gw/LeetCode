### [岛屿的个数](https://leetcode-cn.com/problems/number-of-islands/) LeetCode_200

#### 1.题目

给定一个由 `'1'`（陆地）和 `'0'`（水）组成的的二维网格，计算岛屿的数量。一个岛被水包围，并且它是通过水平方向或垂直方向上相邻的陆地连接而成的。==你可以假设网格的四个边均被水包围。==

**示例 1:**

```
输入:
11110
11010
11000
00000

输出: 1
```

**示例 2:**

```
输入:
11000
11000
00100
00011

输出: 3
```

#### 2.分析

- 原文：你可以假设网格的四个边均被水包围。 说明边界的1也算岛屿
- 深度搜索

```python
深度优先遍历, 到达边界外或访问到为0的位置则返回0,否则先把该位置的1置为0(作为访问过的标记,相当于visited数组),随后递归的访问四个方向.
```



#### 3.代码

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        if not grid or not grid[0]:
            return 0
        res = 0
        for idx,i in enumerate(grid):
            for jdx,j in enumerate(grid[0]):
                if grid[idx][jdx] == '1':
                    res += 1
                    self.func(idx,jdx,grid)
        return res
    
    def func(self,i,j,grid):
        if i<0 or i>=len(grid) or j <0 or j>=len(grid[0]) or grid[i][j]=='0':
            return 
        grid[i][j] = '0'
        # map(self.func,(i+1, i-1, i, i),(j, j, j+1, j-1),(grid,grid,grid,grid))
        self.func(i+1,j,grid)
        self.func(i-1,j,grid)
        self.func(i,j+1,grid)
        self.func(i,j-1,grid)
```



