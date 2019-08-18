## [子集 II](https://leetcode-cn.com/problems/subsets-ii/)(LeetCode 90)

#### 1.题目

给定一个可能包含重复元素的整数数组 **\*nums***，返回该数组所有可能的子集（幂集）。

**说明：**解集不能包含重复的子集。

**示例:**

```
输入: [1,2,2]
输出:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

#### 2.分析

这个问题是之前问题 Leetcode 78 ：子集（最详细的解法！！！）的扩展。我们用之前的解法会出现这样的问题，[1,2]会出现两次
，因为我们有两个2。最简单的思路就是添加一个判断if tmp not in result，并且我们要对nums排序，为什么？为了避免出现这
种情况
1,4,1
4,1,1
这两种在这个问题中是一种情况，但是在判断[1,4,1]==[4,1,1]，两者是不相同的。

#### 3.代码

```python
def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        X = []
        nums.sort()
        self.func(nums, 0, [], X)
        return X
    def func(self, nums, k, x, X):
        X.append(x)
        for i in range(k,len(nums)):
            # if nums[i] in nums[k:i]:
            #     continue
            if k < i and nums[i] == nums[i - 1]:# add
                continue
            self.func(nums, i+1, x+[nums[i]], X)
```

##### 递归

```python
   def subsetsWithDup(self, nums):
        if not nums:
            return [[]]
        nums.sort()
        result = self.subsetsWithDup(nums[1:])
        return result + [[nums[0]] + s for s in result if [nums[0]] + s not in result]
```

