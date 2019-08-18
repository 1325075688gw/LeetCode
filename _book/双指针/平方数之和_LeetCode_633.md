### [平方数之和](https://leetcode-cn.com/problems/sum-of-square-numbers/)(LeetCode_633)

#### 1.题目

给定一个非负整数 `c` ，你要判断是否存在两个整数 `a` 和 `b`，使得 a2 + b2 = c。

**示例1:**

```
输入: 5
输出: True
解释: 1 * 1 + 2 * 2 = 5
```

**示例2:**

```
输入: 3
输出: False
```

#### 2.分析

...

#### 3.代码

```python
from math import *
class Solution:
    def judgeSquareSum(self, c: int) -> bool:
        left,right = 0,int(sqrt(c))+1
        
        while left<=right:
            tmp = left**2+right**2
            if tmp > c:
                right -= 1
            elif tmp < c:
                left += 1
            else:
                return True
        return False
```

