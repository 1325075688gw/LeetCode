### [寻找旋转排序数组中的最小值](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)(LeetCode_153_中等)

#### 1.题目

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。

请找出其中最小的元素。

你可以假设数组中不存在重复元素。

**示例 1:**

```
输入: [3,4,5,1,2]
输出: 1
```

**示例 2:**

```
输入: [4,5,6,7,0,1,2]
输出: 0
```



**2.分析**

等价于前面一堆0，后面一堆1，寻找第一个1的位置



```python
# 1、nums[mid] > nums[right]：例子：[7, 8, 9, 10, 1, 2]，mid 肯定不是最小；
# 2、否则，nums[mid] < nums[right]：例子：[8, 9, 1, 2, 3, 4, 5, 6]，此时 mid 有可能是最小。     
```



```python
# 二分法：首先要判断这个有序数组是否旋转了，通过比较第一个和最后一个数的大小，如果第一个数小，则没有旋转，直接返回这个数。如果第一个数大，就要进一步搜索。我们定义left和right两个指针分别指向开头和结尾，还要找到中间那个数，然后和left指的数比较，如果中间的数大，则继续二分查找右半段数组，反之查找左半段。终止条件是当左右两个指针相邻，返回小的那个。
```





#### 3.代码

```python
    def findMin(self, nums: List[int]) -> int:
        # 二分法：首先要判断这个有序数组是否旋转了，通过比较第一个和最后一个数的大小，如果第一个数小，则没有旋转，直接返回这个数。如果第一个数大，就要进一步搜索。我们定义left和right两个指针分别指向开头和结尾，还要找到中间那个数，然后和left指的数比较，如果中间的数大，则继续二分查找右半段数组，反之查找左半段。终止条件是当左右两个指针相邻，返回小的那个。
        if not nums:
            return -1
        if len(nums) == 1:
            return nums[0]
        if nums[0] < nums[-1]:
            return nums[0]
        left, right = 0, len(nums)-1
        return self.findMin_1(nums, left, right)
    def findMin_1(self, nums, left, right):
        while left < right:
            mid = (left+right)//2
            if nums[mid-1] > nums[mid]:
                return nums[mid]
            elif nums[mid+1] < nums[mid]:
                return nums[mid+1]
            elif nums[mid] < nums[right]:
                right = mid
            elif nums[mid] > nums[left]:
                left = mid
            else:
                # 分治法
                return min(self.findMin_1(nums, left, mid-1), self.findMin_1(nums, mid+1, right))
```



**递归**

```python
    def findMin(self, nums: List[int]) -> int:
        # 二分法：首先要判断这个有序数组是否旋转了，通过比较第一个和最后一个数的大小，如果第一个数小，则没有旋转，直接返回这个数。如果第一个数大，就要进一步搜索。我们定义left和right两个指针分别指向开头和结尾，还要找到中间那个数，然后和left指的数比较，如果中间的数大，则继续二分查找右半段数组，反之查找左半段。终止条件是当左右两个指针相邻，返回小的那个。
        left, right = 0, len(nums)-1
        return self.findMin_1(nums, left, right)
    def findMin_1(self, nums, left, right):
        if left == right:
            return nums[left]
        if left + 1 == right:
            return min(nums[left], nums[right])
        mid = (left+right)//2
        return min(self.findMin_1(nums, left, mid), self.findMin_1(nums, mid+1, right))
```





```python
    def findMin(self, nums):
        if not nums:
            return -1
        if len(nums) == 1:
            return nums[0]
        if nums[0] < nums[-1]:
            return nums[0]
        left, right = 1, len(nums)-1
        while left < right:
            mid = (left+right)//2
            # mid比right小，去左边查找
            # if nums[mid] < nums[-1]:
            if nums[mid] > nums[right]:
                left = mid+1
            # 否则右边一定是有序的,但是mid这个位置可能会是最小值，所以下次还要继续搜索
            else:
                right = mid
        # print(left, right)
        return nums[left]
```

