## 两数之和 II - 输入无须数组

#### 1.题目

#### 2.分析

#### 3.代码

##### 3.1二分法

```python
class Solution:
    def binary_search(self, li, left, right, val):
        while left <= right:
            mid = (left + right) // 2
            if val == li[mid][0]:
                return mid
            elif val > li[mid][0]:
                left = mid + 1
            else:
                right = mid - 1
        else:
            return None
        
    def twoSum(self, nums, target):
        new_list = [[num,i] for i,num in enumerate(nums)]
        new_list.sort()
        for i in range(len(new_list)):
            a = new_list[i][0]
            b = target - a
            if b > a:
                j = self.binary_search(new_list, i + 1, len(new_list) - 1, b)
            else:
                j = self.binary_search(new_list, 0, i - 1, b)
            if j:
                break
        return [new_list[i][1], new_list[j][1]]
ret = Solution()
print(ret.twoSum([-1,-3,-2],-5))
```

##### 3.2字典法

```python
class Solution:
	def twoSum(self, nums, target):
        nums_len = len(nums)
        for i in range(nums_len):
        	dif = target - nums[i]
        	if dif in nums[:i]:
        		return [nums.index(dif), i]
        return []
```

##### 3.3字典法

```python
class Solution:
	def twoSum(self, nums, target):
        bag = {}
        for index, value in enumerate(nums):
        	dif = target - value
        	if dif in bag:
        		return [index, bag[dif]]
        return []
```

##### 3.4切片法

```python
class Solution:
    def twoSum(self, nums, target):
        nums_len = len(nums)
        for i in range(nums_len):
        	dif = target - nums[i]
        	if dif in nums[:i]:
        		return [nums.index(dif), i]
    return []
```



