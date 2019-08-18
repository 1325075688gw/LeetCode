### [Pow(x, n)](https://leetcode-cn.com/problems/powx-n/)

#### 1.题目

实现 [pow(*x*, *n*)](https://www.cplusplus.com/reference/valarray/pow/) ，即计算 x 的 n 次幂函数。

**示例 1:**

```
输入: 2.00000, 10
输出: 1024.00000
```

**示例 2:**

```
输入: 2.10000, 3
输出: 9.26100
```

**示例 3:**

```
输入: 2.00000, -2
输出: 0.25000
解释: 2-2 = 1/22 = 1/4 = 0.25
```



#### 2.分析

**法一：**递归

**法二：**折半

#### 3.代码

**法一**

```python
class Solution:
    # 面试宝典：P252 递归法
    def Power(self, base, exponent):
        # write code here
        b = base
        e = exponent
        # 本题关键点，判断e是偶数还是奇数，判断e是负数还是正数
        
        if e == 0 : return 1
        if e == 1 : return b
        
        tmp = self.Power(b, abs(e)>>1) + 0.0
        if e > 0:
            if e&1 == 1:
                return tmp*tmp*b
            else:
                return tmp*tmp
        else:
            if e&1 == 1:
                return 1/(tmp*tmp*b)
            else:
                return 1/tmp*tmp
            
```



**法二**

```python
    def myPow(self, x: float, n: int) -> float:
        
        res = 1
        i = abs(n)
        while i:
            
            if i&1==1: # 1次方
                res *= x
            x *= x
            i >>= 1
            
        return res if n>0 else 1/res
```



