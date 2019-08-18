### [合并区间](https://leetcode-cn.com/problems/merge-intervals/)(LeetCode_56)

#### 1.题目

给出一个区间的集合，请合并所有重叠的区间。

**示例 1:**

```python
输入: [[1,3],[2,6],[8,10],[15,18]]
输出: [[1,6],[8,10],[15,18]]
解释: 区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6].
```

**示例 2:**

```
输入: [[1,4],[4,5]]
输出: [[1,5]]
解释: 区间 [1,4] 和 [4,5] 可被视为重叠区间。
```



#### 2.分析

...



#### 3.代码

**简化**

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        if not intervals:return []
        # arr = sorted(intervals, key=lambda x:(x[0],[x[1]]))
        # 只需对每个元素第一个位置排序即可，不需要两个位置都排序
        arr = sorted(intervals, key=lambda x:x[0])
        res = [arr[0]]
        for i in range(1,len(arr)):
            if res[-1][1] >= arr[i][0]:
                res[-1][1] = max(res[-1][1], arr[i][1])
            else:
                res.append([arr[i][0],arr[i][1]])
        return res
```



**略显复杂**

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        if not intervals:return []
        arr = sorted(intervals, key=lambda x:(x[0],[x[1]]))
        # print(arr)
        res = [arr[0]]
        for i in range(1,len(arr)):
            if res[-1][1] >= arr[i][0]:
                tmp = [min(res[-1][0],arr[i][0]),max(res[-1][1],arr[i][1])]
                res.pop()
                res.append(tmp)
            else:
                res.append([arr[i][0],arr[i][1]])
        return res
    
```

