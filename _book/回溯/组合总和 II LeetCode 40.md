#### [组合总和 II](https://leetcode-cn.com/problems/combination-sum-ii/)(LeetCode 40)

#### 1.题目

给定一个数组 `candidates` 和一个目标数 `target` ，找出 `candidates` 中所有可以使数字和为 `target` 的组合。

`candidates` 中的每个数字在每个组合中只能使用一次。

**说明：**

- 所有数字（包括目标数）都是正整数。
- 解集不能包含重复的组合。 

**示例 1:**

```
输入: candidates = [10,1,2,7,6,1,5], target = 8,
所求解集为:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```

**示例 2:**

```
输入: candidates = [2,5,2,1,2], target = 5,
所求解集为:
[
  [1,2,2],
  [5]
]
```

#### 2.分析

先排序，后去重

去重,如【1，1，7】--->【1，7】，但是先保证数组有序，所以在这之前先sort

#### 3.代码

```python
    def combinationSum2(self, candidates, target):
        candidates.sort()
        len_nums = len(candidates)
        self.X = []
        self.func(0,target,[],candidates,len_nums)
        return self.X
    def func(self,index,target,x,nums,len_nums):
        if target==0:
            self.X.append(x[:])
        for i in range(index, len_nums):
            # 去重,如【1，1，7】--->【1，7】，但是先保证数组有序，所以在这之前先sort
            if i > index and nums[i]==nums[i-1]:
                    continue
            if target - nums[i]>=0:
                self.func(i+1,target-nums[i],x+[nums[i]],nums,len_nums)
```



