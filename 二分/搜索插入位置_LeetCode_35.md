### [搜索插入位置](https://leetcode-cn.com/problems/search-insert-position/)(LeetCode_35)

#### 1.题目

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

你可以假设数组中无重复元素。

**示例 1:**

```
输入: [1,3,5,6], 5
输出: 2
```

**示例 2:**

```
输入: [1,3,5,6], 2
输出: 1
```

**示例 3:**

```
输入: [1,3,5,6], 7
输出: 4
```

**示例 4:**

```
输入: [1,3,5,6], 0
输出: 0
```



#### 2.分析



#### 3.代码

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        # 寻找插入点使用二分法，但与寻找某数字不同的是，需要考虑一些边界条件：
        # 当插入数字和nums中某数字相等时，插入到左边还是右边？本题要求插到左边；
        # 插入数字在nums第一个数字左边，或在最后一个数字右边；

        left, right = 0, len(nums) - 1
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] < target: 
                left = mid + 1 # insert left side
            else: 
                right = mid - 1
        return left
```



