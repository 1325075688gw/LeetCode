## [搜索二维矩阵](https://leetcode-cn.com/problems/search-a-2d-matrix/)(LeetCode 74)

#### 1.题目

编写一个高效的算法来判断 *m* x *n* 矩阵中，是否存在一个目标值。该矩阵具有如下特性：

- 每行中的整数从左到右按升序排列。
- 每行的第一个整数大于前一行的最后一个整数。

**示例 1:**

```
输入:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 3
输出: true
```

**示例 2:**

```
输入:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 13
输出: false
```

#### 2.分析

- 一是变为一维列表，进行二分查找
- 二是就在愿矩阵上，进行查找，不过起始点，选为左下，或者右上，但是我们不能选择左上角和右下角为起点，假设左上角的数字为1，我们查找数字为7，那么第一次比较7比1大，但是我们无法缩小查询范围（即不能剔除第一行，也不能剔除第一列）

#### 3.代码

##### 二分查找

```python
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        if len(matrix) == 0 or len(matrix[0]) == 0:
            return False
        m = len(matrix)
        n = len(matrix[0])
        left = 0
        right = m*n -1
        res =[]
        for i in matrix:
            # 注意：这儿是将矩阵编程以为列表
            res.extend(i)
        return self.binary_search(res, left, right, target)
    
    def binary_search(self,li, left, right, target):
        
        while left <= right:
            mid = (left+right) // 2
            if li[mid] == target:
                return True
            elif li[mid] < target:
                left = mid + 1
            else:
                right = mid - 1
        return False
```

##### 在原矩阵上进行查找

```python
    def searchMatrix(self, matrix, target):
        if not matrix:return False
        m, n = len(matrix), len(matrix[0])
        i, j = m-1, 0
        # 从左下角开始查找
        while i>=0 and j<=n-1:
            if matrix[i][j] == target:
                return True
            if matrix[i][j] < target:
                j += 1
            else:
                i -= 1
        return False
    
```

