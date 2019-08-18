#### [螺旋矩阵 II](https://leetcode-cn.com/problems/spiral-matrix-ii/)(LeetCode 53)

#### 1.题目

给定一个正整数 *n*，生成一个包含 1 到 *n*2 所有元素，且元素按顺时针顺序螺旋排列的正方形矩阵。

**示例:**

```
输入: 3
输出:
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
```

#### 2.分析

```python
实现思路：给定四个边界，left = 0,right = n-1,  top = 0,bottom = n-1,
然后每次进行四遍循环，
(top)left->right  循环结束后top+1
(right)top->bottom  循环结束后right-1
(bottom)right->left  循环结束后bottom-1
(left)bottom->top  循环结束后left+1
循环结束条件为index = n*n
```

#### 3.代码

```python
def generateMatrix(self, n):
        u, d, l, r = 0, n-1, 0, n-1
        matrix = [[0]*n for _ in range(n)]
        index = 0
        while index < n*n:
            for i in range(l,r+1):
                index +=1
                matrix[u][i] += index
            u += 1
            
            for i in range(u,d+1):
                index += 1
                matrix[i][r] += index
            r -= 1
        
            for i in range(r,l-1,-1):
                index += 1
                matrix[d][i] += index
            d -= 1
                
            for i in range(d,u-1,-1):
                index += 1
                matrix[i][l] += index
            l += 1
        # print(res)
        return  matrix
            
```



