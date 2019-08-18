#### [搜索旋转排序数组 II](https://leetcode-cn.com/problems/search-in-rotated-sorted-array-ii/)(LeetCode 81)

#### 1.题目

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 `[0,0,1,2,2,5,6]` 可能变为 `[2,5,6,0,0,1,2]` )。

编写一个函数来判断给定的目标值是否存在于数组中。若存在返回 `true`，否则返回 `false`。

**示例 1:**

```
输入: nums = [2,5,6,0,0,1,2], target = 0
输出: true
```

**示例 2:**

```
输入: nums = [2,5,6,0,0,1,2], target = 3
输出: false
```

**进阶:**

- 这是 [搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/description/) 的延伸题目，本题中的 `nums`  可能包含重复元素。
- 这会影响到程序的时间复杂度吗？会有怎样的影响，为什么？

#### 2.分析

解题思路

这是之前Leetcode 33：搜索旋转排列数组（最详细的解法！！！）问题的延伸。如果使用之前的方法解决这个问题，会出现错误，例如

```
1  3  1  1  1
丨     |

```

我们会在[0:2]这个区间查找对应元素，但是这样是错误的，这个区间并不是递增区间。那要怎么做呢？

一种最简单的思路就是将nums的重复元素去除，然后在使用之前的方法就可以啦。

#### 3.代码

##### 去重代码

```python
def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: bool
        """
        if not nums:
            return False
        nums = list(set(nums))
        low, high = 0, len(nums) - 1

        while low <= high:
            mid = (low + high) // 2
            if target == nums[mid]:
                return True

            if nums[low] <= nums[mid]:
                if nums[low] <= target <= nums[mid]:
                    high = mid
                else:
                    low = mid + 1
            else:
                if nums[mid] <= target <= nums[high]:
                    low = mid
                else:
                    high = mid - 1

        return False
```

##### 不去重代码

```python
    def search(self, nums: List[int], target: int) -> bool:
        if nums == None: return False
        l, r = 0, len(nums)-1
        while l<=r:
            mid = (l+r)//2
            if nums[mid] == target: return True
            if nums[mid] == nums[l]:
                l += 1
            elif nums[l] < nums[mid]:
                if nums[l]<=target<=nums[mid]:
                    r = mid-1
                else:
                    l = mid+1
            else:
                if nums[mid]<=target<=nums[r]:
                    l = mid+1
                else:
                    r = mid-1
        return False
```

##### 优秀的代码

```
class Solution:
    def binary_search(self, left, right, nums, target):
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] == target:
                return True
            elif nums[mid] < target:
                left = mid + 1
            elif nums[mid] > target:
                right = mid - 1
        return False


    def sub_search(self, left, right, nums, target):
        if left <= right:
            mid = (left + right) // 2
            if nums[mid] == target:
                return True

            if nums[left] == nums[right]:
                for i in range(left, right + 1):
                    if nums[i] == target:return True
                return False

            if nums[mid] >= nums[left]:      #左边是有序的
                if target < nums[mid] and target >= nums[left]:      #target在左边
                    return self.binary_search(left, mid - 1, nums, target)
                else:
                    return self.sub_search(mid + 1, right, nums, target)
            elif nums[mid] <= nums[right]:   #右边是有序的
                if target > nums[mid] and target <= nums[right]:
                    return self.binary_search(mid + 1, right, nums, target)
                else:
                    return self.sub_search(left, mid - 1, nums, target)

        return False

    def search(self, nums: 'List[int]', target: 'int') -> 'bool':
        if len(nums) == 0: return False
        return self.sub_search(0, len(nums) - 1, nums, target)
```

