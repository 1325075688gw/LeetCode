#### [组合](https://leetcode-cn.com/problems/combinations/)(LeetCode 77)

#### 1.题目

给定两个整数 *n* 和 *k*，返回 1 ... *n* 中所有可能的 *k* 个数的组合。

**示例:**

```
输入: n = 4, k = 2
输出:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

#### 2.分析

#### 3.代码

```python
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        nums = [i for i in range(1,n+1)]
        self.X =[]
        self.func(0,k,[],nums)
        return self.X        
    def func(self, index, length, x,nums):
        # 如果现在re的长度加上后面能加上的所有的长度已经小于k了）,那么也剪枝
        if len(x)+len(nums)-index < length:return
        if len(x)==length:
            self.X.append(x[:])
            return # return 剪枝操作，及早返回
        for i in range(index,len(nums)):
            self.func(i+1,length,x+[nums[i]],nums)
            
            # 等价于下下面操作
            # x.append(nums[i])
            # self.func(i+1,length,x,nums)
            # x.pop()
```

