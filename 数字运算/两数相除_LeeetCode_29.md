### [两数相除](https://leetcode-cn.com/problems/divide-two-integers/)(LeetCode_29)

#### 1.题目

给定两个整数，被除数 dividend 和除数 divisor。将两数相除，要求不使用乘法、除法和 mod 运算符。

返回被除数 dividend 除以除数 divisor 得到的商。

**示例 1:**

```
输入: dividend = 10, divisor = 3
输出: 3
```

**示例 2:**

```
输入: dividend = 7, divisor = -3
输出: -2
```

**说明:**

```python
- 被除数和除数均为 32 位有符号整数。
- 除数不为 0。
- 假设我们的环境只能存储 32 位有符号整数，其数值范围是 [−231,  231 − 1]。本题中，如果除法结果溢出，则返回 231 − 1。
```



#### 2.分析

```python
明确一点,10进制数扩大两倍,左移一位  
        a = 2
        a <<= 1
        输出: a = 4
        10进制数缩小两倍,右移一位
        b = 8
        b >> = 1
        输出: b = 4
当被除数大于等于除数时(否则的话就为0了),我们设置两个变量tmp_cs和tmp_res,并分别初始化为临时除数(除数后面会变化,过一会就知道了)和1(最小的情况),当被除数大于等于tmp_cs的二倍时bcs>=(tmp_cs<<1) (左移一位就代表除数乘以2,而且我们没有用<<=,也就是表明没有真正赋值,我们这一步做的目的是测试被除数到底是不是除数的两倍,如果不是,我们还可以回退),如果进入循环,就代表被除数是除数的两倍或者更大,将tmp_cs和tmp_res(临时结果也扩大两倍,比如47除以8,现在47>=8*2,所以我们有两个8,所以tmp_res扩大两倍,除数也变为原来两倍16,继续循环,被除数47>=16*2,所以tmp_res = 2*2....后面继续判断,不赘述了)同时扩大二倍(左移)，并将返回值加上tmp_res，除数减去tmp_res。
拿十进制举例:29除以8，8扩大二倍，16小于29，再扩大二倍，超过29，于是29减去之前的16(我们保存了的)，返回值加上2(因为现在我们除的是16,16是8的2倍)。剩余除数为29-16=13，第二次循环时因为此时的13小于8的二倍(tmp_cs<<1)，因此我们只能除以8,不能除以8的2倍,幸好我们这句话执行的是(tmp_cs<<1,而不是tmp_cs<<=1:多了一个等号赋值操作,所以还可以还原回去),往下继续走,我们就加上1,代表只能除以一个8,而不能除以2个8即16,整个循环结束，最终结果为2+1=3，符合要求。此外还要注意判断结果正负号时亦或的作用。 
```



#### 3.代码



**暴力法 (每次减去一个除数，统计可以减去多少个除数)**

```
class Solution:
    def divide(self, dividend: int, divisor: int) -> int:
        res = 0 
        sign = 1 if dividend ^ divisor > 0 else -1
        dividend = abs(dividend)
        divisor = abs(divisor)
        while dividend >= divisor:
            dividend -= divisor
            res += 1
        res = res if sign > 0 else -res
        
        return max(res, -2**31) if res < 0 else min(res, 2**31-1)  
```



**(除数倍增法) 移位法**

```python
class Solution:
    def divide(self, dividend, divisor):
        sign = (dividend > 0) ^ (divisor > 0)
        i, bcs, cs = 0, abs(dividend), abs(divisor)
        if bcs == 0 or bcs < cs:
            return 0
        res = 0
        while bcs >= cs:
            tmp_cs, tmp_res = cs, 1
            while bcs>=(tmp_cs<<1):
                tmp_res <<= 1
                tmp_cs <<= 1
            bcs = bcs - tmp_cs
            res += tmp_res

        res = -res if sign else res

        return max(res, -2**31) if res < 0 else min(res, 2**31-1)
```



**除数倍增法**

```python
class Solution:
    def divide(self, dividend, divisor):
        sign = (dividend > 0) ^ (divisor > 0)
        i, bcs, cs = 0, abs(dividend), abs(divisor)
        if bcs == 0 or bcs < cs:
            return 0
        res = 0
        while bcs >= cs:
            tmp_cs, tmp_res = cs,1
            while bcs>=(tmp_cs+tmp_cs):
                tmp_res += tmp_res
                tmp_cs += tmp_cs
            bcs = bcs-tmp_cs
            res = res + tmp_res
            
        res = -res if sign else res
        return max(res, -2**31) if res < 0 else min(res, 2**31-1)
```

