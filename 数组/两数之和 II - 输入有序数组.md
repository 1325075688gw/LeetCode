## 两数之和 II - 输入有序数组

#### 1.题目

给定一个已按照**升序排列** 的有序数组，找到两个数使得它们相加之和等于目标数。

函数应该返回这两个下标值 index1 和 index2，其中 index1 必须小于 index2*。*

**说明:**

- 返回的下标值（index1 和 index2）不是从零开始的。
- 你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。

**示例:**

```python
输入: numbers = [2, 7, 11, 15], target = 9
输出: [1,2]
解释: 2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。
```

#### 2.分析

暴力法，

二分法，

指针对撞法

#### 3.代码

##### 暴力法

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        for i in range(len(numbers)-1):
            for j in range(i+1,len(numbers)):
                if numbers[i]+numbers[j] == target:
                    return [i+1,j+1]
        return []
```



##### 二分法

```python
    def binary_search(self, li, left, right, val):
        while left <= right:
            mid = (left + right) // 2
            if val == li[mid]:
                return mid
            elif val > li[mid]:
                left = mid + 1
            else:
                right = mid - 1
        else:
            return None
    def twoSum(self, nums, target):
        for i in range(len(nums)):
            a = nums[i]
            b = target - a
            if b > a:
                j = self.binary_search(nums, i + 1, len(nums) - 1, b)
            else:
                j = self.binary_search(nums, 0, i - 1, b)
            if j and j!=i:
                break
        return [i+1, j+1]
```



**字典法**

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        m={}
        for index,value in enumerate(numbers):
            if target-value in m:
                return[m[target-value]+1,index+1]
            m[value]=index
```





##### 双指针法（指针对撞法）

==if elif else: 只会走一个==

```python
if 3>2:
   print(111)
elif 4>2:
	print(4444)
else:
	print(6666)
    
输出：111


if 3>22:
   print(111)
elif 4>2:
	print(4444)
else:
	print(6666)
    
输出：444
```



```python
def twoSum(self, numbers, target):
    left, right = 0, len(numbers)-1
    sum_all = 0
    while left < right:
        sum_all = numbers[left] + numbers[right]
        if sum_all > target:
            right -= 1
            # continue 可以不加，因为if elif else 只会走一个
        elif sum_all < target:
            left += 1
            # continue 可以不加
        else:
            return [left+1, right+1]
    return []
```



