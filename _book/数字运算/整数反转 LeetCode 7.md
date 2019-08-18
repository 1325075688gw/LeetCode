#### [整数反转](https://leetcode-cn.com/problems/reverse-integer/)(LeetCode 7)

#### 1.题目

给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。

**示例 1:**

```
输入: 123
输出: 321
```

 **示例 2:**

```
输入: -123
输出: -321
```

**示例 3:**

```
输入: 120
输出: 21
```

**注意:**

假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为 [−231,  231 − 1]。请根据这个假设，如果反转后整数溢出那么就返回 0。

#### 2.分析

#### 3.代码

```python
def reverse(self, x: 'int') -> 'int':
        if x < (-2**31) or x > (2**31-1):
            return 0
        x = str(x)
        if x[0] == '-':
            x = x[1:]
            str_x = ''.join(list(reversed(x)))
            str_x = '-'+str_x
        else:
            str_x = ''.join(list(reversed(x)))
        if int(str_x) < (-2**31) or int(str_x) > (2**31-1):
                return 0
        return int(str_x)
```

