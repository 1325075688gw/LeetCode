#### [不同路径](https://leetcode-cn.com/problems/unique-paths/)(LeetCode 62)

#### 1.题目

一个机器人位于一个 *m x n* 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

问总共有多少条不同的路径？

![img](不同路径 LeetCode 62.assets/robot_maze.png)

例如，上图是一个7 x 3 的网格。有多少可能的路径？

**说明：***m* 和 *n* 的值均不超过 100。

**示例 1:**

```
输入: m = 3, n = 2
输出: 3
解释:
从左上角开始，总共有 3 条路径可以到达右下角。
1. 向右 -> 向右 -> 向下
2. 向右 -> 向下 -> 向右
3. 向下 -> 向右 -> 向右
```

**示例 2:**

```
输入: m = 7, n = 3
输出: 28
```

#### 2.分析

- 动态规划
- 起始点颠倒

#### 3.代码

**动态规划**

```python
    # 注意：这是n行m列
    def uniquePaths(self, m: int, n: int) -> int:
        mat = [[None]*m for _ in range(n)]
        for i in range(m):
            mat[-1][i] = 1
        for i in range(n):
            mat[i][-1] = 1
        # for _ in mat:
        #     print(_)
        for i in range(n-2,-1,-1):
            for j in range(m-2,-1,-1):
                mat[i][j] = mat[i][j+1] + mat[i+1][j]
        # print(mat[0][0])
        return mat[0][0]
```

##### 起始点颠倒

```python
    def uniquePaths(self, m, n):
        mat = [[0]*m for _ in range(n)]
        for i in range(n):
            mat[i][0] = 1
        for j in range(m):
            mat[0][j] = 1
        print(mat)
        for i in range(1,n):
            for j in range(1,m):
                mat[i][j] = mat[i-1][j] + mat[i][j-1]
        # print(mat[-1][-1])
        return mat[-1][-1]
```
**空间复杂度优化为2m**

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        up = [1] * m    # 上面一行
        now = [1] * m    # 下面一行 （当前行）
        for i in range(1,n):
            for j in range(1,m):
                now[j] = up[j] + now[j-1]
            up = now[:] # 将计算好的值，赋给上一行
        return now[-1]
```

**优化空间复杂度 O(n)**

```python
def uniquePaths(self, m: int, n: int) -> int:
    up = [1] * m
    for i in range(1,n):
        tmp = up[0] # tmp始终不变，
        # 在这给up【0】赋值
        # up[0] = tmp
        for j in range(1,m):
            tmp = up[j] + tmp
            # 在这给其他up赋值
            up[j] = tmp
    return up[-1]
```

**排列组合**

因为机器到底右下角，向下几步，向右几步都是固定的，

比如，m=3, n=2，我们只要向下 1 步，向右 2 步就一定能到达终点。

所以有 $C_{m+n-2}^{m-1}$

```python
阶层函数 math.factorial(n)

def uniquePaths(self, m: int, n: int) -> int:
        return int(math.factorial(m+n-2)/math.factorial(m-1)/math.factorial(n-1))
阶层计算函数
from functools import reduce
def func(n):
    return reduce(lambda x,y:x*y, range(1,n+1))

阶层递归计算函数
def func(n):
    if n==1:
        return 1:
    else:
        return n*func(n-1)
```

