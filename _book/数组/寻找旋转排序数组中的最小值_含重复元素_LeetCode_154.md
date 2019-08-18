### [寻找旋转排序数组中的最小值 II](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/)(LeetCode_154)

#### 1.题目

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。

请找出其中最小的元素。

注意数组中可能存在重复的元素。

**示例 1：**

```
输入: [1,3,5]
输出: 1
```

**示例 2：**

```
输入: [2,2,2,0,1]
输出: 0
```



#### 2.分析

#### 3.代码

**暴力法**

```python
    def findMin(self, nums):
        for i in range(1,len(nums)):
            if nums[i]<nums[i-1]:
                return nums[i]
        return nums[0]
```



```python
    def findMin(self, nums):
        if not nums:
            return -1
        if len(nums) == 1:
            return nums[0]
        if nums[0] < nums[-1]:
            return nums[0]
        left, right = 0, len(nums)-1
        return self.find_binary(nums, left, right)
    def find_binary(self, nums, left, right):
        while left < right:
            mid = (left+right)//2
            if nums[mid] < nums[right]:
                right = mid
            elif nums[mid] > nums[right]:
                left = mid+1
            else:
              # 数组中存在重复元素，所以每次只缩小一个查找范围
                right -= 1
            
        return nums[left]
```



