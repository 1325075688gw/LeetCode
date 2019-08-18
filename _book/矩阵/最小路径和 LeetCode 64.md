### [最小路径和](https://leetcode-cn.com/problems/minimum-path-sum/)(LeetCode 64)

#### 1.题目

给定一个包含非负整数的 *m* x *n* 网格，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

**说明：**每次只能向下或者向右移动一步。

**示例:**

```
输入:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 7
解释: 因为路径 1→3→1→1→1 的总和最小。
```

#### 2.分析

​	(动态规划1)：时间复杂为o(n*m)和空间复杂度为o(n*m)。典型的动态规划问题，假设当前已经开始计算s[i][j]，那么s[i][j]只可能从s[i-1][j]+grid[i][j]或者s[i][j-1]+grid[i][j]计算得到，也就是s[i][j] = min(s[i-1][j],s[i][j-1])+grid[i][j]。我们需要一个o(n*m)额外空间保存已经计算的s[i][j]的值，我们只需要访问一遍数组即可。因此时间复杂度为o(n*m)，空间复杂度为o(n*m)。我们需要特殊处理矩阵中第一行和第一列。因为第一行没有s[i-1][j]元素，只有s[i][j-1]元素。第一列没有s[i][j-1]元素，只有s[i-1][j]元素。



#### 3.代码

##### 动态规划1(原地修改)：

```python
    def minPathSum(self, grid):
        if not grid or not grid[0]:return 0
        n, m = len(grid), len(grid[0])
        for i in range(1,n):
            grid[i][0] = grid[i-1][0] + grid[i][0]
        for j in range(1,m):
            grid[0][j] = grid[0][j-1] + grid[0][j]  
        for i in range(1,n):
            for j in range(1,m):
                grid[i][j] = min(grid[i-1][j], grid[i][j-1])+grid[i][j]
        return grid[-1][-1]
```

```python
    def minPathSum(self, grid):
        if not grid or not grid[0]:return 0
        
        n, m = len(grid), len(grid[0])
        for i in range(n):
            for j in range(m):
                if i==0 and j>0:
                    grid[i][j] = grid[i][j-1] + grid[i][j]
                elif j==0 and i>0:
                    grid[i][j] = grid[i-1][j] + grid[i][j]
                elif i>0 and j>0:
                    grid[i][j] = min(grid[i-1][j], grid[i][j-1])+grid[i][j]
        return grid[-1][-1]
```



(动态规划2)：时间复杂度为o(n*m)，空间复杂度为o(m)，此方法需要2*m额外空间。当我们求s[i][j]时，s[i-2]行的元素我们就不再需要，我们只需要s[i-1]行中的元素，我们把s[i-1]行中的元素保存在up数组中，数组的大小为m。我们把s[i]保存在now数组中，当s[i]行的元素计算完毕以后，我们交换up和now数组。因为需要up数组和now数组，且数组的大小都为m，所以我们需要2*m大小的额外空间。

```python
        def minPathSum(self, grid):
            if not grid or not grid[0]:return 0
            n, m = len(grid), len(grid[0])
            up = [grid[0][0]]*m
            now = [0] *m
            for j in range(1,m):
                up[j] = grid[0][j] + up[j-1]
                
            for i in range(1,n):
                now[0] = grid[i][0] + up[0]
                for j in range(1,m):
                    # pre[j]:上元素  tmp:左元素，求和后，tmp也为左元素
                    now[j] = min(up[j],now[j-1]) + grid[i][j]
                up = now.copy()
            return up[-1]
                
```



(动态规划3)：时间复杂度为o(n*m)，空间复杂度为o(m)，需要m大小的额外空间，注意此方法和方法三的区别，方法三需要2*m大小的额外空间，此方法只需要m大小的额外空间，在方法三中我们保存当前行s[i]中的元素，假设我们当前计算s[i][j]，我们只需要知道s[i][j-1]的值即可，不需要保存s[i]行中的元素。每次计算s[i][j]时，我们需要更新up[j]的值。

```python
        def minPathSum(self, grid):
            if not grid or not grid[0]:return 0
            n, m = len(grid), len(grid[0])
            up = [grid[0][0]]*m
            for j in range(1,m):
                up[j] = grid[0][j] + up[j-1]
                
            for i in range(1,n):
                tmp = grid[i][0] + up[0]
                up[0] = tmp
                for j in range(1,m):
                    # pre[j]:上元素  tmp:左元素，求和后，tmp也为左元素
                    tmp = min(up[j],tmp) + grid[i][j]
                    up[j] = tmp
            return up[-1]
```



##### 非原地修改，动态规划

```python
        def minPathSum(self, grid):
            if not grid or not grid[0]:return 0
            
            n, m = len(grid), len(grid[0])
            mat = [[grid[0][0]]*m]*n
            for i in range(1,n):
                mat[i][0] = mat[i-1][0] + grid[i][0]
    
            for j in range(1,m):
                mat[0][j] = mat[0][j-1] + grid[0][j]
            for i in range(1,n):
                for j in range(1,m):
                    mat[i][j] = min(mat[i][j-1], mat[i-1][j]) + grid[i][j]
            return mat[-1][-1]
                
```

