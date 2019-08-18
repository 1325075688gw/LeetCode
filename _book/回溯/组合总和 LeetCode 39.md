#### [组合总和](https://leetcode-cn.com/problems/combination-sum/)(LeetCode 39)

#### 1.题目

给定一个**无重复元素**的数组 `candidates` 和一个目标数 `target` ，找出 `candidates` 中所有可以使数字和为 `target` 的组合。

`candidates` 中的数字可以无限制重复被选取。

**说明：**

- 所有数字（包括 `target`）都是正整数。
- 解集不能包含重复的组合。 

**示例 1:**

```
输入: candidates = [2,3,6,7], target = 7,
所求解集为:
[
  [7],
  [2,2,3]
]
```

**示例 2:**

```
输入: candidates = [2,3,5], target = 8,
所求解集为:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```

#### 2.分析

#### 3.代码

##### python先排序，后回溯，可以使用重复元素

```python
def combinationSum(self, candidates, target):
    # 可以不排序，答案也正确
    candidates.sort()
    self.res = []
    self.func(0,target, candidates,[])
    return self.res
    
def func(self,index, target,nums,x):
    if 0 == target:
        self.res.append(x[:])
        return 
    for i in range(index,len(nums)):
        k = target-nums[i]
        if k >= 0:
            # 注意这儿func（i）而不是func(i+1)
            self.func(i,target-nums[i],nums,x+[nums[i]])
```
##### 不使用重复元素

```python
def combinationSum(self, candidates, target):
    candidates.sort()
    self.res = []
    self.func(0,target, candidates,[])
    return self.res
    
def func(self,index, target,nums,x):
    if 0 == target:
        self.res.append(x[:])
        return 
    for i in range(index,len(nums)):
        k = target-nums[i]
        if k >= 0:
            self.func(i+1,target-nums[i],nums,x+[nums[i]])
```

**如 n = 3**

**输出 【1,1,1】【1，2】【3】**

**我们只需修改candidates为【i for i in range(n+1)】**

```python
    def combinationSum(self, target):
        candidates = [i for i in range(1,target+1)]
        self.res = []
        self.func(0,target, candidates,[])
        return self.res
        
    def func(self,index, target,nums,x):
        if 0 == target:
            self.res.append(x[:])
            return 
        for i in range(index,len(nums)):
            k = target-nums[i]
            if k >= 0:
                self.func(i,target-nums[i],nums,x+[nums[i]])
```





