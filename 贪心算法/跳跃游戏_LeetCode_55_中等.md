### [跳跃游戏](https://leetcode-cn.com/problems/jump-game/)(LeetCode_55_中等)

#### 1.题目

判断你是否能够到达最后一个位置。

**示例 1:**

```
输入: [2,3,1,1,4]
输出: true
解释: 从位置 0 到 1 跳 1 步, 然后跳 3 步到达最后一个位置。
```

**示例 2:**

```python
输入: [3,2,1,0,4]
输出: false
解释: 无论怎样，你总会到达索引为 3 的位置。但该位置的最大跳跃长度是 0 ， 所以你永远不可能到达最后一个位置。

```

#### 2.分析

- 贪心算法：如果不能到达i位置，则i+1位置肯定到不了
- 动态规划

#### 3.代码

**贪心算法**

```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        len_nums = len(nums)
        max_root = 0
        for i in range(0, len_nums-1):
            max_root = max(max_root, i+nums[i])
            # 等于0，表示原地不动
            if max_root<=i:
                return False
        return True
```



**动态规划**

```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        len_nums = len(nums)
        dp = [False]*len_nums
        dp[0] = True
        for i in range(1,len_nums):
            for j in range(i):
                if dp[j] and nums[j]+j>=i:
                    dp[i] = True
                    break
        # print(dp)
        return dp[-1]
                    
```

