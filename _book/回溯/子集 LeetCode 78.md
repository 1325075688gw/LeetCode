## [子集](https://leetcode-cn.com/problems/subsets/)(LeetCode 78)

#### 1.题目

给定一组**不含重复元素**的整数数组 *nums*，返回该数组所有可能的子集（幂集）。

**说明：**解集不能包含重复的子集。

**示例:**

```
输入: nums = [1,2,3]
输出:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

#### 2.分析

- 这个问题通过递归可以很快的解决，我们只要知道了subsets(nums[1:])，那么我们只要将nums[0]添加到每个子集的前面形成新的子集，然后将新的子集添加到result中即可。
- 我们也可以通过回溯法来解决。

#### 3.代码

##### 递归

```python
    def subsets(self, nums):
        if len(nums) == 0:return [[]]
        res = self.subsets(nums[1:])
        return res+[[nums[0]] + i for i in res]
```

##### 回溯

````python
    def subsets(self, nums):
        X = []
        self.func(nums, 0, [], X)
        return X
    def func(self, nums, k, x, X):
        X.append(x)
        for i in range(k, len(nums)):
            self.func(nums, i+1, x+[nums[i]], X )
            
            
            
         很多人很难理解为什么上面这种写法是回溯法，其实我们将push和pop的过程合到了一块，我在之前的一些问题中也没说明，所以在此解释一下。   
        #self._subsets(nums, i + 1, path + [nums[i]], result)
        # 可以将它分开写成
        # path.append(nums[i])
        # self._subsets(nums, i + 1, path, result)
        # path.pop()
````

##### 全局变量可以这么设置

```python
    def subsets(self, nums):
        self.X = []
        self.func(nums, 0, [])
        return self.X
    def func(self, nums, k, x):
        self.X.append(x)
        for i in range(k, len(nums)):
            self.func(nums, i+1, x+[nums[i]])
```

