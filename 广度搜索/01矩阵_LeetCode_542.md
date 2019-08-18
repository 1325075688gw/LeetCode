### [01 矩阵](https://leetcode-cn.com/problems/01-matrix/)(LeetCode_542)

#### 1.题目

给定一个由 0 和 1 组成的矩阵，找出每个元素到最近的 0 的距离。

两个相邻元素间的距离为 1 。

**示例 1:** 
输入:

```
0 0 0
0 1 0
0 0 0
```

输出:

```
0 0 0
0 1 0
0 0 0
```

**示例 2:** 
输入:

```
0 0 0
0 1 0
1 1 1
```

输出:

```
0 0 0
0 1 0
1 2 1
```

**注意:**

1. 给定矩阵的元素个数不超过 10000。
2. 给定矩阵中至少有一个元素是 0。
3. 矩阵中的元素只在四个方向上相邻: 上、下、左、右。

#### 2.分析

- 在找到一个合法节点后需要去探知其附近的合法节点，直到这一个区域内符合合法节点的节点都被找到。 
- 广度搜索，入队可以将所有0都先入队，作为队头节点

#### 3.代码



**BFS**

```python
class Solution:
    
    def updateMatrix(self, matrix: List[List[int]]) -> List[List[int]]:
        from collections import deque
        n, m = len(matrix), len(matrix[0])
        # queue = []
        queue = deque()
        visited = set()
        # 初始化队列，将所有起始点加入
        for i in range(n):
            for j in range(m):
                if matrix[i][j] == 0:
                    queue.append((i, j))
                    # 添加访问标志
                    visited.add((i, j))
                   
        # 将所有相邻节点加入队列
        while queue:
            i, j = queue.popleft()
            dirs = [(i+1, j), (i-1, j), (i, j+1), (i, j-1)]
            # 寻找出队元素的（符合条件的）最近节点
            for x,y in dirs:
                # 满足目标状态,进行操作
                if 0 <= x <= n-1 and 0 <= y <= m-1 and (x,y) not in visited:         # 不是matrix[x][y] !=0:     
                    matrix[x][y] = matrix[i][j] + 1
                    # 添加到队尾,添加访问标志
                    queue.append((x,y))
                    visited.add((x, y))
        return matrix
```

