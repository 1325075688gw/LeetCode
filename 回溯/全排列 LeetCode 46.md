#### [全排列](https://leetcode-cn.com/problems/permutations/)(LeetCode 46)

#### 1.题目

给定一个**没有重复**数字的序列，返回其所有可能的全排列。

**示例:**

```
输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

#### 2.分析

全排列是交换x[i],x[k] = x[k],x[i]，部分排列组合是append，pop

#### 3.代码

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        self.X = []
        self.func(0, len(nums), nums)
        return self.X
    def func(self, index, length,x):
        if index == length:
            self.X.append(x[:])
            return 
        for i in range(index,length):
            x[i],x[index] = x[index],x[i]
            self.func( index+1, length, x)
            x[index],x[i] = x[i],x[index]
    
```

