#### 1.题目

给定一个未经排序的整数数组，找到最长且**连续**的的递增序列。

**示例 1:**

```python
输入: [1,3,5,4,7]
输出: 3
解释: 最长连续递增序列是 [1,3,5], 长度为3。
尽管 [1,3,5,7] 也是升序的子序列, 但它不是连续的，因为5和7在原数组里被4隔开。 
```

**示例 2:**

```
输入: [2,2,2,2,2]
输出: 1
解释: 最长连续递增序列是 [2], 长度为1。
```

**注意：**数组长度不会超过10000。



#### 2.分析

**要求时间复杂度为O（n）**

#### 3.代码

**动态规划**

```python
class Solution:
    def findLengthOfLCIS(self, nums: List[int]) -> int:
        n = len(nums)
        if n<2:
            return n
        
        dp = [1]*n
        res = 0
        for i in range(1,n):
            if nums[i]>nums[i-1]:
                dp[i] = dp[i-1]+1
                
        return max(dp)

```





```python
class Solution:
    def findLengthOfLCIS(self, nums: List[int]) -> int:
        nums_len = len(nums)
        if len(nums)<2:
            return nums_len
        
        count = 1
        res = 1
        for i in range(1,nums_len):
            if nums[i]>nums[i-1]:
                count += 1
                res = max(res, count)
            else:
                count = 1
        return res

```









