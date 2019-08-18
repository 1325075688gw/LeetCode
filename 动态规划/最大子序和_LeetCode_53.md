## [最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)(LeetCode 53)

#### 1.题目

给定一个整数数组 `nums` ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

**示例:**

```
输入: [-2,1,-3,4,-1,2,1,-5,4],
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```

**进阶:**

如果你已经实现复杂度为 O(*n*) 的解法，尝试使用更为精妙的分治法求解。

#### 2.分析



#### 3.代码



**动态规划**

```python
    def FindGreatestSumOfSubArray(self, array):
        # write code here
        # 动态规划
        a_len = len(array)
        res = array[0]
        dp = [0]*a_len
        for i in range(a_len):
            dp[i] = max(dp[i-1]+array[i], array[i])
            res = max(res, dp[i])
        return res
```



**正常解法**

```c
class Solution(object):
    def maxSubArray(self, nums):
        sum = 0
        max_sub_sum = nums[0]
        for num in nums:
            sum += num
            if sum > max_sub_sum:
                max_sub_sum = sum
            if sum < 0:
                sum = 0
        return max_sub_sum
```

**动态规划**

遍历数组，记录max(nums[i-1] + nums[i], nums[i])（含义为保留前面累加和与以当前元素为开始，哪种更优），即判断后面subarray是否舍去前面的累计加和，并继续遍历下一元素。
最后return加和中最大值。

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        for i in range(1,len(nums)):
            nums[i] = max(nums[i],nums[i-1]+nums[i])
        return max(nums)
```

**分治法**

- 最大连续子序列是所有连续子序中元素和最大的一个，例如给定序列{ -2, 11, -4, 13, -5, -2 }，其最大连续子序列为{11,-4,13}，最大连续子序列和即为20。

- 问题解决思路：

  现将序列等分为左右两份，则最大子列只可能出现在三个地方：

  1整个子序列出现在左半部分

  2整个子序列出现在右半部分

  3整个子序列跨越中间边界

  前两种情况可以用递归求解，而第三种情况则可以将前半部分的最大子序列和（此处的子序列必须包含前半部分的最后一个元素）与后半部分的最大子序列和（此处的子序列必须包含后半部分的第一个元素）相加得到

  **注1：**因为第三种情况跨越了中间边界，且要求的序列为连续的，因此第三种情况得到的子序列必定包含左子序列的最后一个元素以及右子序列的第一个元素。

  **注2：**若要求的序列可以为不连续的，则第三种情况可以直接用前半部分最大子序列和与后半部分最大子序列和相加得到

##### 1.分治法解决   连续   子序列    和最大问题

```python
# 注1：因为第三种情况跨越了中间边界，且要求的序列为连续的，因此第三种情况得到的子序列必定包含左子序列
# 的最后一个元素以及右子序列的第一个元素。
def findMaxSum(li):
    # 如果问题规模小于等于1，直接解决
    if len(li) <= 1:
        return li[0]
    
    # 分解
    mid = len(li) // 2
    left = li[:mid]
    right = li[mid:]
    
    # 递归求解即分治
    leftMaxSum = findMaxSum(left)
    rightMaxSum = findMaxSum(right)
    
    # 最大和由左右连续序列组合而成
    # 用于包含左边最后一个数的累加求和
    leftAndMid = 0
    # 考虑到存在序列全为负数的情况，因为初始化为负无穷而非0
    leftAndMidMax = float('-inf')#包含左边最后一个数的最大序列和
    for i in left[::-1]:
        leftAndMid += i
        if leftAndMid > leftAndMidMax:
            leftAndMidMax = leftAndMid
            
    # 用于包含右边第一个数的累加求和
    rightAndMid = 0
    # 考虑到存在序列全为负数的情况，因为初始化为负无穷而非0
    rightAndMidMax = float('-inf')#包含右边最后一个数的最大序列和
    for i in right:
        rightAndMid += i
        if rightAndMid > rightAndMidMax:
            rightAndMidMax = rightAndMid        
            
    # 计算跨越了中间的序列 的最大和
    midMaxSum = leftAndMidMax + rightAndMidMax
    
    # 合并
    return max(leftMaxSum, midMaxSum, rightMaxSum)

A=[2,3,4,1,-1,-7,-3,-7,-6]
 
print(findMaxSum(A))



```

##### 2.动态规划解决   连续   子序列   和最大：

```python
def findMaxSum(li):
    # initMax 用于累加求和开始
    initMax = 0
    MaxSum = float("-inf")
    for i in li:
        initMax += i
        if i > initMax:
            initMax = i
        if initMax > MaxSum:
            MaxSum = initMax
    return MaxSum

A=[1,-2,-2,4]
 
print(findMaxSum(A))   



法2
def maxSubArray(self, nums):
    sum = 0
    max_sub_sum = nums[0]
    for num in nums:
        sum += num
        if sum > max_sub_sum:
            max_sub_sum = sum
        if sum < 0:
            sum = 0
    return max_sub_sum
```

##### 3.分治法解决非连续   子序列    和最大问题

```python
def findMaxSum(li):
    # 如果问题规模小于等于1，直接解决
    if len(li) <= 1:
        return li[0]
    
    # 分解
    mid = len(li) // 2
    left = li[:mid]
    right = li[mid:]
    
    # 递归求解即分治
    leftMaxSum = findMaxSum(left)
    rightMaxSum = findMaxSum(right)
    
    # 合并
    midMaxSum = leftMaxSum + rightMaxSum
    return max(leftMaxSum, midMaxSum, rightMaxSum)

A=[-2,-3,-4,-1,-1,-7,-3,-7,-6]
 
print(findMaxSum(A))
```

##### 4.动态规划解决非连续  子序列 和最大问题

```python
def maxSubArray(nums):
    sum = 0
    max_sub_sum = nums[0]
    for num in nums:
        sum += num
        if sum >= max_sub_sum:
            max_sub_sum = sum
        else:
            sum -= num
    print(max_sub_sum)


A = [-1, 2, -2,-3,-5,9]

print(findMaxSum(A))
```

```python
 def maxSubArray(nums):
    max_sub_sum = nums[0]
    for i in nums[1:]:
        if i > 0:
            if max_sub_sum < 0:
                max_sub_sum = 0
            max_sub_sum += i
    print(max_sub_sum)
```





## [最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)(LeetCode 53)

#### (子数组)

#### 1.题目

给定一个整数数组 `nums` ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

**示例:**

```
输入: [-2,1,-3,4,-1,2,1,-5,4],
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```

**进阶:**

如果你已经实现复杂度为 O(*n*) 的解法，尝试使用更为精妙的分治法求解。

#### 2.分析

```python
使用动态规划
F（i）：以array[i]为末尾元素的子数组的和的最大值，子数组的元素的相对位置不变
F（i）=max（F（i-1）+array[i] ， array[i]）
res：所有子数组的和的最大值
res=max（res，F（i））

如数组[6, -3, -2, 7, -15, 1, 2, 2]
初始状态：
    F（0）=6
    res=6
i=1：
    F（1）=max（F（0）-3，-3）=max（6-3，3）=3
    res=max（F（1），res）=max（3，6）=6
i=2：
    F（2）=max（F（1）-2，-2）=max（3-2，-2）=1
    res=max（F（2），res）=max（1，6）=6
i=3：
    F（3）=max（F（2）+7，7）=max（1+7，7）=8
    res=max（F（2），res）=max（8，6）=8
i=4：
    F（4）=max（F（3）-15，-15）=max（8-15，-15）=-7
    res=max（F（4），res）=max（-7，8）=8
以此类推
最终res的值为8
```





#### 3.代码

```c
class Solution(object):
    def maxSubArray(self, nums):
        sum = 0
        max_sub_sum = nums[0]
        for num in nums:
            sum += num
            if sum > max_sub_sum:
                max_sub_sum = sum
            if sum < 0:
                sum = 0
        return max_sub_sum
```



**动态规划**

```python
    def FindGreatestSumOfSubArray(self, array):
        # write code here
        # 动态规划
        a_len = len(array)
        res = array[0]
        dp = [0]*a_len
        for i in range(a_len):
            dp[i] = max(dp[i-1]+array[i], array[i])
            res = max(res, dp[i])
        return res
```

