#### [搜索二维矩阵 II](https://leetcode-cn.com/problems/search-a-2d-matrix-ii/)(LeetCode 240)

#### 1.题目

编写一个高效的算法来搜索 *m* x *n* 矩阵 matrix 中的一个目标值 target。该矩阵具有以下特性：

- 每行的元素从左到右升序排列。
- 每列的元素从上到下升序排列。

**示例:**

现有矩阵 matrix 如下：

```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

给定 target = `5`，返回 `true`。

给定 target = `20`，返回 `false`。

#### 2.分析

因为展开成一维列表后也不是有序的，因此，我们就在原矩阵上进行查找，查找的起始点是左下角和右上角

#### 3.代码

```python
 def searchMatrix(self, matrix, target):
        """每一行都用二分法计算，但是，如果匹配成功啦，不是返回的下标，而是True
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        if len(matrix) == 0 or len(matrix[0]) == 0:
            return False
        m, n = len(matrix)-1,len(matrix[0])-1
        i = m
        j = 0
        while (i>=0 and j<=n):
            if matrix[i][j] == target:
                return True
            elif matrix[i][j] < target:
                j += 1
            else:
                i -= 1
        return False
        
```



##### C++

```c++
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        /        // 不加这个传入为空的判断的话会访问越界
        // 只有一句话，可以不加大括号
        // if (matrix.empty()) 
        //     return 0;
        
        //也可以这么判断，
        int len = matrix.size();
        if (len == 0)
            return 0;
        
        
        int row = matrix.size()-1;
        int col = matrix[0].size()-1;
        int j = 0;
        int i = row;
        while (i>=0 && j<=col){
            if (matrix[i][j] > target){
                i--;
                continue;
            }
            else if (matrix[i][j] < target){
                j++;
                continue;
            }
            else{
                return true;
            }
        }
        return false;
    }
};
```



