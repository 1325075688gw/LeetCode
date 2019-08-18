### [验证回文字符串 Ⅱ](https://leetcode-cn.com/problems/valid-palindrome-ii/)(LeetCode_680)

#### 1.题目

给定一个非空字符串 `s`，**最多**删除一个字符。判断是否能成为回文字符串。

**示例 1:**

```
输入: "aba"
输出: True
```

**示例 2:**

```
输入: "abca"
输出: True
解释: 你可以删除c字符。
```

**注意:**

```python
字符串只包含从 a-z 的小写字母。字符串的最大长度是50000。
```



#### 2.分析

- 双指针
- 递归
- 原生 判断回文字符串

#### 3.代码



**双指针**

```python
class Solution:
    def validPalindrome(self, s: str) -> bool:
        if len(s) <= 1:return True
        Flag = True
        left,right = 0, len(s)-1
        while left < right:
            if s[left] == s[right]:
                left += 1
                right -= 1
            else:
                if Flag:
                    return s[left:right]==s[left:right:-1] or s[left+1:right+1] == s[left+1:right+1:-1]
                else:
                    return False
```



**递归**

```python
class Solution:
    def validPalindrome(self, s: str) -> bool:   
        if len(s)<=1:return True
        def func(s,left,right,n):
            while left<right:
                if s[left]==s[right]:
                    left += 1
                    right -= 1
                else:
                    if n>0:
                        return func(s,left+1,right,0) or func(s,left,right-1,0)
                    else:
                        return False
                
            return True
        return func(s,0,len(s)-1,1)
```



**原生写法，通过率99.99%，超时，其它语言可通过**

```python
class Solution:
    def validPalindrome(self, s: str) -> bool:
        if not s:return True
        flag =True
        left, right = 0,len(s)-1
        while left < right:
            # print(3)
            if s[left]==s[right]:
                left += 1
                right -= 1
            elif flag == True:
                # print(1)
                i = left+1
                j = right-1
                if s[i] == s[right]:
                    left = i
                    flag=False
                elif s[left] == s[j]:
                    right = j
                    flag=False
                else:
                    return False
            else:
                # elif flag == False:
                return False
        return True
```

