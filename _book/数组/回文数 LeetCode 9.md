#### [回文数](https://leetcode-cn.com/problems/palindrome-number/)(LeetCode 9)

#### 1.题目

判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

**示例 1:**

```
输入: 121
输出: true
```

**示例 2:**

```
输入: -121
输出: false
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
```

**示例 3:**

```
输入: 10
输出: false
解释: 从右向左读, 为 01 。因此它不是一个回文数。
```

**进阶:**

你能不将整数转为字符串来解决这个问题吗？

#### 2.分析

整数逆置

#### 3.代码

##### 不用自己写反转

```python
    def isPalindrome(self, x: 'int') -> 'bool':
        x = str(x)
        new_x = x[::-1]
        if new_x == x: 
                return True
        return False
```

##### 自己写反转判断

```python
    def isPalindrome(self, x: 'int') -> 'bool':
        x = str(x)
        return self.func(x)
    def func(self, x):
        l, r =0, len(x)-1
        while l<r:
            if x[l] != x[r]:
                return False
            l += 1
            r -= 1
        return True
```

##### 整数逆置

```python
    def isPalindrome(self, x: 'int') -> 'bool':
        # 如果负数，不是回文数；如果个位数是0（除0这种特殊情况），不是回文数
        if x<0 or (x!=0 and x%10==0):
            return False
        y = x
        n = 0
        # 逆置 整数
        while x:
            n = n * 10 + x % 10
            x = x//10
        return n==y
```

##### 反转一半数

```python
   # 反转一半数
    def isPalindrome(self, x: 'int') -> 'bool':
        if x<0 or (x!=0 and x%10==0):
            return False
        right_rev = 0
        while x > right_rev:
            right_rev = right_rev*10 + x%10
            x = x//10
       #    奇偶情况都考虑
        return x==right_rev or x==right_rev//10
```

