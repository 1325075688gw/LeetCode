### [最大数](https://leetcode-cn.com/problems/largest-number/)(LeetCode 179)-(数字拼接后最大)

#### 1.题目

给定一组非负整数，重新排列它们的顺序使之组成一个最大的整数。

**示例 1:**

```
输入: [10,2]
输出: 210
```

**示例 2:**

```
输入: [3,30,34,5,9]
输出: 9534330
```

**说明:** 输出结果可能非常大，所以你需要返回一个字符串而不是整数。

#### 2.分析

```
首先现将数字转化为字符
判断x+y 和 y+x谁大

1. if x+y>y+x: 则不交换   比如2，1 ：    21>12 (字符串拼接比较哦)

1..if x+y<y+x: 则交换                1，2：     12<21(交换为2，1)

3.每种语言应该都有内置排序算法，看看能不能指定排序函数（也就是自定义排序方式）
，如果不能，我写了一种冒泡排序，大家可以套模板
```

python：(内置排序方法)

```python
class Solution:
    
    # 自定义排序算法
    def largestNumber(self, nums: List[int]) -> str:
        if sum(nums) == 0:
            return '0'
        from functools import cmp_to_key
        def func(x,y):
            if x+y<y+x:
                return 1
            elif x+y>y+x:
                return -1
            else:
                return 0
        
        arr = map(str, nums)
        res = sorted(arr, key=cmp_to_key(func))
        # print(res)
        return ''.join(res)
        
```

python：自定义排序方法——》冒泡排序

```python
原始数据：1，2，4，3

转化为char后再排序：

第一趟冒泡：2，4，3，1
第二趟冒泡：4，3，2，1
第三趟冒泡：4，3，2，1 没有发生交换，排序结束

将排序好的数据，拼接成字符串
    def largestNumber(self, nums: List[int]) -> str:
        if sum(nums) == 0:
            return '0'
        nums = list(map(str,nums))
        for i in range(len(nums)-1):
            #如果某一趟不冒泡了没有发生交换过程），就代表排好序了，
            exchange = False
            for j in range(len(nums)-i-1):
                if nums[j+1]+nums[j]>nums[j]+nums[j+1]:
                    nums[j+1],nums[j] = nums[j],nums[j+1]
                    exchange = True
            if not exchange:
                break
        return ''.join(nums)
```

#### 3.代码

如2