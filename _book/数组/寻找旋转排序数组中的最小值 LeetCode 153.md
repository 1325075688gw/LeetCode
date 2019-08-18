## 寻找旋转排序数组中的最小值（LeetCode 153）

#### 1.题目

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 `[0,1,2,4,5,6,7]` 可能变为 `[4,5,6,7,0,1,2]` )。

请找出其中最小的元素。

你可以假设数组中不存在重复元素。

**示例 1:**

```python
输入: [3,4,5,1,2]
输出: 1
```

**示例 2:**

```python
输入: [4,5,6,7,0,1,2]
输出: 0
```

#### 2.分析

通过选择数组的特性知道，数组元素先是递增，然后突然下降到最小值，然后再递增。

- 数组本身没有旋转，是一个有序数组，例如`[1,2,3,4]`
- 数组中元素全部相等，例如【1，1，1，1】
- 数组中大部分元素相同，如【1，0，1，1，1】

通过分析知道，旋转数组可以划分为两个有序数组，前面的数组的每个元素都大于等于后面数组的每个元素，可以用二分法不断缩小查找范围。

- 如果没有旋转，则第一个元素小于最后个元素，直接返回第一个元素
- 如果`nums[mid] <  nums[mid-1]    `,则`nums[mid]`最小
- 如果`nums[mid+1] < nums[mid]`,则`nums[mid+1]`最小
- 如果`nums[mid]  < nums[right]`,则最小值在数组左边
- 如果`nums[mid]  > nums[left]`,则最小值在数组右边
- 如果`nums[mid]  == nums[right] == nums[left] `,如【2，2，2，1，2】无法区别时，只能求左右最小值，然后返回左右最小值中最小的

#### 3.代码

```python
    def findMin(self, nums: List[int]) -> int:
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
                right = mid-1
            elif nums[mid] > nums[left]:
                left = mid+1
            else:
                return min(self.findMin_1(nums, left, mid-1), self.findMin_1(nums, mid+1, right))
```

#### 3.2代码2

```python
 # 二分法：首先要判断这个有序数组是否旋转了，通过比较第一个和最后一个数的大小，如果第一个数小，则没有旋转，直接返回这个数。如果第一个数大，就要进一步搜索。我们定义left和right两个指针分别指向开头和结尾，还要找到中间那个数，然后和left指的数比较，如果中间的数大，则继续二分查找右半段数组，反之查找左半段。终止条件是当左右两个指针相邻，返回小的那个。
    def findMin(self, nums):
        if not nums:
            return -1
        if len(nums) == 1:
            return nums[0]
        if nums[0] < nums[-1]:
            return nums[0]
        left, right = 0, len(nums)-1
        while left+1 < right:
            mid = (left+right)//2
            # mid比right小，去左边查找
            if nums[mid] < nums[-1]:
                right = mid
            else:
                left = mid
        return min(nums[left] , nums[right])
```

#### 3.3代码3

```python
 # 二分法：首先要判断这个有序数组是否旋转了，通过比较第一个和最后一个数的大小，如果第一个数小，则没有# # 旋转，直接返回这个数。如果第一个数大，就要进一步搜索。我们定义left和right两个指针分别指向开头和结
# 尾，还要找到中间那个数，然后和left指的数比较，如果中间的数大，则继续二分查找右半段数组，反之查找左半# 段。终止条件是当左右两个指针相邻，返回小的那个。   
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
        while left+1 < right:
            mid = (left+right)//2
            if nums[mid] < nums[-1]:
                right = mid
            else:
                left = mid
        return min(nums[left] , nums[right])
```





