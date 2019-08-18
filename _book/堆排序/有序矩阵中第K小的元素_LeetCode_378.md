### [有序矩阵中第K小的元素](https://leetcode-cn.com/problems/kth-smallest-element-in-a-sorted-matrix/)

#### 1.题目

给定一个 *n x n* 矩阵，其中每行和每列元素均按升序排序，找到矩阵中第k小的元素。
请注意，它是排序后的第k小元素，而不是第k个元素。

**示例:**

```
matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,

返回 13。
```



#### 2.分析



**大根堆**

#### 3.代码



```python
class Solution:
    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
        import heapq
        tmp = []
        edge = len(matrix)
        for i in range(edge):
            for j in range(edge): 
                heapq.heappush(tmp,-matrix[i][j])
                if len(tmp) > k:
                    heapq.heappop(tmp)
        # print(-tmp[0])
        return -tmp[0]

```

