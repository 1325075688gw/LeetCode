## 找出数组中第K大的数

####  1.题目

在未排序的数组中找到第 **k** 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

**示例 1:**

```
输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
```

**示例 2:**

```
输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
```

**说明:**

你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度。

#### 2.分析

- 可以用类似快速排序，也可以用类似冒泡排序

#### 3.代码

```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        
        if len(nums) == 1:
            return nums[0]
        mid = nums[0]
        right = [i for i in nums[1:] if i >= mid]
        left = [i for i in nums[1:] if i< mid]
        if len(right) == k-1:
            return mid
        elif k > len(right):
            return self.findKthLargest(left, k-len(right)-1)
        else:
            return self.findKthLargest(right, k)
```

##### 冒泡排序有错

```python
        def findKthLargest(self, nums, k):
            nums_len = len(nums)
            if nums_len == 1: return nums[0]
            res = 0
            for i in range(k):
                # print(i)
                for j in range(nums_len-1-i):
                    if nums[j] >= nums[j+1]:
                        nums[j],nums[j+1] = nums[j+1],nums[j]
                    if i==k-2 and j == nums_len-2-i:
                        # print(nums[j])
                        return nums[j-1]
```



```
> [!NOTE]
> 这是一个简单的Note类型的使用，所有的属性都是默认值。
```

> [!NOTE]
>
> 这是一个简单的Note类型的使用，所有的属性都是默认值。\



```python
> [!NOTE]
> 这是一个简单的Note类型的使用，所有的属性都是默认值。
```
