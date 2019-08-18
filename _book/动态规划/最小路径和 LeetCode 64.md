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

​	

```
(动态规划1)：时间复杂为o(nm)和空间复杂度为o(nm)。典型的动态规划问题，假设当前已经开始计算si，那么si只可能从si-1+gridi或者si+gridi计算得到，也就是si = min(si-1,si)+gridi。我们需要一个o(nm)额外空间保存已经计算的si的值，我们只需要访问一遍数组即可。因此时间复杂度为o(nm)，空间复杂度为o(n*m)。我们需要特殊处理矩阵中第一行和第一列。因为第一行没有si-1元素，只有si元素。第一列没有si元素，只有si-1元素。
```

#### 3.代码

##### 动态规划1(原地修改)：

```python
    def minPathSum(self, grid):
        if not grid or not grid[0]:return 0
        n, m = len(grid), len(grid[0])
        # 从1开始，不然0位置会重复计算
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



**动态规划2（非原地修改，空间复杂度m*n）**

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



**动态规划3（非原地修改，空间复杂度2*m）**

(动态规划2)：时间复杂度为o(nm)，空间复杂度为o(m)，此方法需要2m额外空间。当我们求si时，s[i-2]行的元素我们就不再需要，我们只需要s[i-1]行中的元素，我们把s[i-1]行中的元素保存在up数组中，数组的大小为m。我们把s[i]保存在now数组中，当s[i]行的元素计算完毕以后，我们交换up和now数组。因为需要up数组和now数组，且数组的大小都为m，所以我们需要2*m大小的额外空间。

```python
        def minPathSum(self, grid):
            if not grid or not grid[0]:return 0
            n, m = len(grid), len(grid[0])
            up = [grid[0][0]]*m
            now = [0] *m
            for j in range(1,m):
                up[j] = grid[0][j] + up[j-1]
                
            for i in range(1,n):
                # 计算now【0】
                now[0] = grid[i][0] + up[0]
                for j in range(1,m):
                    # 在这给其他now赋值
                    now[j] = min(up[j],now[j-1]) + grid[i][j]
                up = now.copy()
            return up[-1]
                
```



**动态规划4（非原地修改，空间复杂度为m）**

(动态规划3)：时间复杂度为o(nm)，空间复杂度为o(m)，需要m大小的额外空间，注意此方法和方法三的区别，方法三需要2m大小的额外空间，此方法只需要m大小的额外空间，在方法三中我们保存当前行s[i]中的元素，假设我们当前计算si，我们只需要知道si的值即可，不需要保存s[i]行中的元素。每次计算si时，我们需要更新up[j]的值。

```python
        def minPathSum(self, grid):
            if not grid or not grid[0]:return 0
            n, m = len(grid), len(grid[0])
            up = [grid[0][0]]*m
            for j in range(1,m):
                up[j] = grid[0][j] + up[j-1]
                
            for i in range(1,n):
                # 后面用到tmp，在这计算好tmp的值
                # 给now【0】赋值
                tmp = grid[i][0] + up[0]
                # 计算up[0] = tmp ,给下次进来时候，tmp = grid[i][0] + up[0]赋值
                up[0] = tmp 
                for j in range(1,m):
                    # 在这给其他up赋值
                    tmp = min(up[j],tmp) + grid[i][j]
                    up[j] = tmp
            return up[-1]
```

##### 

​          

