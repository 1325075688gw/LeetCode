#### [三个数的最大乘积](https://leetcode-cn.com/problems/maximum-product-of-three-numbers/) LeetCode 628

#### 1.题目

给定一个整型数组，在数组中找出由三个数组成的最大乘积，并输出这个乘积。

**示例 1:**

```
输入: [1,2,3]
输出: 6
```

**示例 2:**

```
输入: [1,2,3,4]
输出: 24
```

**注意:**

1. 给定的整型数组长度范围是[3,104]，数组中所有的元素范围是[-1000, 1000]。
2. 输入的数组中任意三个数的乘积不会超出32位有符号整数的范围。

#### 2.分析

- 先排好序
- 然后取最大的3个数相乘，或者最小的两个数（负数）和最大的一个数相乘

#### 3.代码

```python
class Solution:
    def maximumProduct(self, nums: List[int]) -> int:
        nums.sort()
        return max(nums[0]*nums[1]*nums[-1], nums[-1]*nums[-2]*nums[-3])
```

