#### [最长上升子序列](https://leetcode-cn.com/problems/longest-increasing-subsequence/)(LeetCode 300)

#### 1.题目

给定一个无序的整数数组，找到其中最长上升子序列的长度。

**示例:**

```
输入: [10,9,2,5,3,7,101,18]
输出: 4 
解释: 最长的上升子序列是 [2,3,7,101]，它的长度是 4。
```

**说明:**

- 可能会有多种最长上升子序列的组合，你只需要输出对应的长度即可。
- 你算法的时间复杂度应该为 O(*n2*) 。

**进阶:** 你能将算法的时间复杂度降低到 O(*n* log *n*) 吗?

#### 2.分析

##### 动态规划思路

1、子序列：不要求连续子序列，只要保证元素前后顺序一致即可；

2、上升：这里的“上升”是“严格上升”，类似于 `[2, 3, 3, 6, 7]` 这样的子序列是不符合要求的；

```
    # 动态规划的思路：将 dp 数组定义为：以 nums[i] 结尾的最长上升子序列的长度
    # 那么题目要求的，就是这个 dp 数组中的最大者
    # 以数组  [10, 9, 2, 5, 3, 7, 101, 18] 为例：
    # dp 的值： 1  1  1  2  2  3  4    4
```



##### 替换思路

dp[i]: 所有长度为i+1的递增子序列中, 最小的那个序列尾数. 由定义知dp数组必然是一个递增数组 依次判断每个数num将其插入dp数组相应的位置: 1. num > dp[-1], ，执行插入尾部操作，表示num比所有已知递增序列的尾数都大, 将num添加入dp 数组尾部 2. num <= dp [-1],则执行替换操作，【1，2，4，5】 现在来了一个3，那么替换为【1，2，3，5】，而不是【1，3， 4，5】

#### 3.代码

##### 动态规划

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        size = len(nums)
        if size <= 1:
            return size
        dp = [1] * size
        for i in range(1, size):
            for j in range(i):
                if nums[i] > nums[j]:
                    dp[i] = max(dp[j] + 1,dp[i])
        # 最后要全部走一遍，看最大值
        return max(dp)
    
    
为什么是
dp[i] = max(dp[j] + 1,dp[i])
而不是
dp[i] = dp[j]+1

如下
# [1,3,6,7,9,4,10,5,6] 对于4，如果不用max(dp[j]+1,dp[i]),那 
# 么dp['4'] 等于3，当求10，dp['10']时候，10>4,则dp['10'] = 
# dp['4']+1=4,所以最后max(dp),答案为5，而不是6
```

##### 动态规划替换

```python
class Solution:
    def lengthOfLIS(self, nums):
        n = len(nums)
        if n <= 1: # 不要忘了空数组
            return n
        stack = [nums[0]]  # 初始时候，只有一个元素，那么它肯定是递增的，所以加入
        for i in range(1,n):
            if nums[i] > stack[-1]:
                stack.append(nums[i])
            else:
                # 不会动递增序列的个数，但是会调整递增序列的值，这儿也可以用二分查找
                for j in range(len(stack)):
                    # dp=【1，2，4】 ,nums[i]=3
                    if nums[i] > stack[j]:
                        continue
                    else:
                        stack[j] = nums[i] # 将数组中的值替换
                        break
        return len(stack) # 返回递增序列的长度，就是最长递增子序列
```

##### 动态规划之二分替换

```python
class Solution:
    def lengthOfLIS(self, nums):
        n = len(nums)
        if n <= 1:
            return n
        dp = [nums[0]]
        for i in range(1,n):
            flag = True
            if nums[i]>dp[-1]:
                dp.append(nums[i])
            if nums[i]<dp[0]:
             	dp[0] = nums[i]
            # 其实还可以分析其他情况，如nums==dp[0],直接continue，但是代码太长了，就不写了
            else:
                # 查找第一个大于等于nums[i]的元素，然后替换之
                low,high = 0,len(dp)-1
                while low<=high:
                    mid = (low+high)//2
                    if dp[mid] < nums[i]:
                        low = mid+1
                    elif dp[mid] > nums[i]:
                        high = mid-1
                    else: # 不用替换,设置一个标志位，跳过外循环的替换操作
                        flag = False
                        break
                if flag == False:
                    flag = True
                    continue
                dp[low] = nums[i]
        return len(dp)
                    
```



