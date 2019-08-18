## 有序矩阵中第K小的元素

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

**说明:** 
你可以假设 k 的值永远是有效的, 1 ≤ k ≤ n2 。

#### 2.分析

- 我们使用一个最大堆，然后遍历数组每一个元素，将其加入堆，根据最大堆的性质，大的元素会排到最前面，然后我们看当前堆中的元素个数 是否大于k，大于的话就将首元素去掉，循环结束后我们返回堆中的首元素即为所求:

#### 3.代码

- ```python
  class Solution:
      def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
          # 我们使用一个最大堆，然后遍历数组每一个元素，将其加入堆，根据最大堆的性质，大的元素会排到最前面，然后我们看当前堆中的元素个数         # 是否大于k，大于的话就将首元素去掉，循环结束后我们返回堆中的首元素即为所求:
          import heapq
          tmp = []
          edge = len(matrix)
          for i in range(edge):
              for j in range(edge): 
                  heapq.heappush(tmp,-matrix[i][j])
                  if len(tmp) > k:
                      heapq.heappop(tmp)
          print(-tmp[0])
          return -tmp[0]

  ```

  ​