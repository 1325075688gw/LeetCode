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
        
        	# l-1不会被遍历
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



**java**

```java
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] res = new int[n][n];
        int u=0, d=n-1, l=0, r=n-1;
        int num = 1;
        
        while (true) {
            for (int i = l; i <= r; i++) res[u][i] = num++;
            if (++u > d) break;
            
            for (int i = u; i <= d; i++) res[i][r] = num++;
            if (--r < l) break;
            
            for (int i = r; i >= l; i--) res[d][i] = num++;
            if (--d < u) break;
            
            for (int i = d; i >= u; i--) res[i][l] = num++;
            if(++l > r) break;
        }
        
        return res;
    }
}

```



**java**

```java
public int[][] generateMatrix(int n) {

        int l = 0, r = n - 1, t = 0, b = n - 1;
        int[][] mat = new int[n][n];
        int num = 1, tar = n * n;
        while(num <= tar){
            for(int i = l; i <= r; i++) mat[t][i] = num++; // left to right.
            t++;
            for(int i = t; i <= b; i++) mat[i][r] = num++; // top to bottom.
            r--;
            for(int i = r; i >= l; i--) mat[b][i] = num++; // right to left.
            b--;
            for(int i = b; i >= t; i--) mat[i][l] = num++; // bottom to top.
            l++;
        }
        return mat;

    }
```

