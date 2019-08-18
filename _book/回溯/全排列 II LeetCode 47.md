## 全排列 II（LeetCode 47）

#### 1.题目

给定一个可包含重复数字的序列，返回所有不重复的全排列。

**示例:**

```python
输入: [1,1,2]
输出:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```

#### 2.分析

如baa，b只与第一个a交换，与第二个a不交换。去重复。

#### 3.代码

##### 最正确的代码

```python
class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        self.X = []
        self.func(nums,0,len(nums))
        return self.X
    def func(self, li, k, length):
        if k==length:
            self.X.append(li[:])                    
        else:
            for i in range(k,length):
                # 左包右不包
                if li[i] in li[k:i]:
                    continue
                li[k], li[i] = li[i], li[k]
                self.func(li, k+1, length)
                li[i], li[k] = li[k], li[i]

```



##### 去重代码1

```python
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        X = []
        def tree(li, k, length):
            if k==length:
                X.append(li[:])                    
            else:
                for i in range(k,length):
                    if nums[i] in nums[k:i]:
                        continue
                    li[k], li[i] = li[i], li[k]
                    tree(li, k+1, length)
                    li[i], li[k] = li[k], li[i]
        tree(nums, 0, len(nums))
        # print(X)
        return X

```

##### 去重代码2

```python
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        X = []
        def tree(li, k, length):
            mark = set()
            if k==length:
                X.append(li[:])                    
            else:
                for i in range(k,length):
                    if nums[i] in mark:
                        continue
                    li[k], li[i] = li[i], li[k]
                    tree(li, k+1, length)
                    li[i], li[k] = li[k], li[i]
                    mark.add(li[i])
        tree(nums, 0, len(nums))
        # print(X)
        return X
```

##### 去重代码3

```python
    def conflict(self, start, end, nums):
        for i in nums[start: end]:
            if i == nums[end]:
                return False
        return True
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        X = []
        def tree(li, k, length):
            # mark = set()
            if k==length:
                X.append(li[:])                    
            else:
                for i in range(k,length):
                    if not self.conflict(k, i, nums):
                        continue
                    li[k], li[i] = li[i], li[k]
                    tree(li, k+1, length)
                    li[i], li[k] = li[k], li[i]
        tree(nums, 0, len(nums))
        # print(X)
        return X
```

