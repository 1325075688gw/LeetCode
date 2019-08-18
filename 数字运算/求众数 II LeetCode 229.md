#### [求众数 II](https://leetcode-cn.com/problems/majority-element-ii/)(LeetCode 229)

#### 1.题目

给定一个大小为 *n* 的数组，找出其中所有出现超过 `⌊ n/3 ⌋` 次的元素。

**说明:** 要求算法的时间复杂度为 O(n)，空间复杂度为 O(1)。

**示例 1:**

```
输入: [3,2,3]
输出: [3]
```

**示例 2:**

```
输入: [1,1,1,3,3,2,2,2]
输出: [1,2]
```

#### 2.分析

摩根投票法

- 如果我们在使用摩尔算法时，同时记录两个大多数，会怎么样呢？直觉告诉我，这会得到一个大多数，和一个出现次数仅次于大多数的数，但是这两个数不一定会比数组长的1/3大
- 所以我们得到它们后，还需要检查它们出现的次数是否符合条件。

#### 3.代码

```python
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        a, b, ca, cb, ans = None, None, 0, 0, []
        for i in nums:
            if   i  == a: ca += 1
            elif i  == b: cb += 1
            elif ca == 0: a, ca = i, 1
            elif cb == 0: b, cb = i, 1
            else:         ca, cb = ca - 1, cb - 1
        # print(a, b)
        ca, cb = 0, 0
        for i in nums:
            if   i == a: ca += 1
            elif i == b: cb += 1
                
        if ca > len(nums)//3:
            ans.append(a)
        if cb > len(nums)//3:
            ans.append(b)
        return ans
```

```python
# print(a, b) 不检验的结果
输入
[3,2,3,2,3,2,3,2,2,1,1,1,1,1,1,1,1,1,1,1,1,1,1]
stdout
1 2
输出
[1]
预期结果
[1]
```

