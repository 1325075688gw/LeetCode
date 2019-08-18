### [被围绕的区域](https://leetcode-cn.com/problems/surrounded-regions/)(LeetCode 130)

#### 1.题目

给定一个二维的矩阵，包含 `'X'` 和 `'O'`（**字母 O**）。

找到所有被 `'X'` 围绕的区域，并将这些区域里所有的 `'O'` 用 `'X'` 填充。

**示例:**

```
X X X X
X O O X
X X O X
X O X X
```

运行你的函数后，矩阵变为：

```
X X X X
X X X X
X X X X
X O X X
```

**解释:**

被围绕的区间不会存在于边界上，换句话说，任何边界上的 `'O'` 都不会被填充为 `'X'`。 任何不在边界上，或不与边界上的 `'O'` 相连的 `'O'` 最终都会被填充为 `'X'`。如果两个元素在水平或垂直方向相邻，则称它们是“相连”的。

#### 2.分析

首先对边界上每一个'O'做深度优先搜索，将与其相连的所有'O'改为'-'。然后遍历矩阵，将矩阵中所有'O'改为'X',将矩阵中所有'-'变为'O' 

#### 3.代码

```python
def solve(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        if not board or not board[0]:return
        
        m,n = len(board),len(board[0])
        for i in range(m):
            self.func(i,0,board)
            self.func(i,n-1,board)
        
        for j in range(n):
            self.func(0,j,board)
            self.func(m-1,j,board)
            
        for i in range(m):
            for j in range(n):
                if board[i][j]=='O':
                    board[i][j]='X'
                if board[i][j]=='-':
                    board[i][j]='O'
        
                
    def func(self, i, j ,board):
        if i<0 or j<0 or i>len(board)-1 or j >len(board[0])-1 or board[i][j]!='O':
            return 
        board[i][j]='-'
            
        self.func(i+1,j,board)
        self.func(i-1,j,board)
        self.func(i,j+1,board)
        self.func(i,j-1,board)
```

