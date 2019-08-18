### [最长递增子序列的个数](https://leetcode-cn.com/problems/number-of-longest-increasing-subsequence/)(LeetCode_673)

#### 1.题目

给定一个未排序的整数数组，找到最长递增子序列的个数。

**示例 1:**

```
输入: [1,3,5,4,7]
输出: 2
解释: 有两个最长递增子序列，分别是 [1, 3, 4, 7] 和[1, 3, 5, 7]。
```

**示例 2:**

```
输入: [2,2,2,2,2]
输出: 5
解释: 最长递增子序列的长度是1，并且存在5个子序列的长度为1，因此输出5。
```



#### 2.分析



做这道题目之前，建议先去看看300号问题，本题在300号问题的基础上做了一些改变，需要多使用一个数组来记录LIS的组合数

#### 3.代码



```python
class Solution:
    def findNumberOfLIS(self, nums: List[int]) -> int:
        n = len(nums)
        if n<2:
            return n
        dp = [1]*n
        dp_nums = [1]*n
        
        for i in range(1,n):
            for j in range(i):
                if nums[i]>nums[j]: # 如果j位的数值比i位小，则可加入i位的LIS比较队列
                    # dp[i] = max(dp[i], dp[j]+1)
                    if dp[i]<dp[j]+1: # 如果+1长于当前LIS 则组合数不变
                        dp[i] = dp[j]+1
                        dp_nums[i] = dp_nums[j] # 继承j位的LIS种类
                    elif dp[i] == dp[j]+1: # 如果+1等于当前LIS 则说明找到了新组合
                        dp_nums[i] += dp_nums[j] # 把j位的种类数目加给i位
                    # dp[i]>dp[j]+1:不需要做任何调整
        
        ans = 0
        tmp = max(dp)
        for i in range(n):
            if dp[i] == tmp:
                ans += dp_nums[i]
        
        return ans
```

