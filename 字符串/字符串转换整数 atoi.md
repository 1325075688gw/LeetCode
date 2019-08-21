## [字符串转换整数 (atoi)](https://leetcode-cn.com/problems/string-to-integer-atoi/)

**示例 1:**

```
输入: "42"
输出: 42
```

**示例 2:**

```
输入: "   -42"
输出: -42
解释: 第一个非空白字符为 '-', 它是一个负号。
     我们尽可能将负号与后面所有连续出现的数字组合起来，最后得到 -42 。
```

**示例 3:**

```
输入: "4193 with words"
输出: 4193
解释: 转换截止于数字 '3' ，因为它的下一个字符不为数字。
```

**示例 4:**

```
输入: "words and 987"
输出: 0
解释: 第一个非空字符是 'w', 但它不是数字或正、负号。
     因此无法执行有效的转换。
```

**示例 5:**

```
输入: "-91283472332"
输出: -2147483648
解释: 数字 "-91283472332" 超过 32 位有符号整数范围。 
     因此返回 INT_MIN (−231) 。
```

#### 2.分析

草泥马，LeetCode

#### 3.代码

```python
 def myAtoi(self, s):
        s = s.lstrip().split(" ",1)[0]
        length = len(s)
        if length == 0 or s[0] not in '0123456789+-':
            return 0
        index = 1
        # 跳过第一个字符，因为第一个字符有可能是‘+-’
        # 之所以用s[index].isdigit(),是因为有可能这种情况，‘0012a42’

        while index < length and s[index].isdigit():
            index += 1
        if index == 1 and s[0] in '+-':
            return 0
        result = int(s[:index])
        if result < 0:
            return max(-2147483648, result)
        else:
            return min(2147483647, result)
```





```python
class Solution:
    def StrToInt(self, s):
        # write code here
        if s == '0' or not s:
            return 0
        flag = 1
        if s[0] == '+':
            flag = True
            if not s[1:].isdigit():
                return 0
        elif s[0] == '-':
            flag = False
            if not s[1:].isdigit():
                return 0
        elif not s.isdigit():
            flag = None
            return 0
        
        res = 0
        if flag is 1:
            n = len(s)
            m = n
            while n>0:
                n -= 1
                res += int(s[n])*10**(m-n-1)
            return res
        if flag is True or flag is False:
            n = len(s)
            m = n
            while n>1:
                n -= 1
                res += int(s[n])*10**(m-n-1)
            return res if flag else -res
```

