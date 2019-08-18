#### [最长回文子串](https://leetcode-cn.com/problems/longest-palindromic-substring/)(LeetCode_5)

#### 1.题目

给定一个字符串 `s`，找到 `s` 中最长的回文子串。你可以假设 `s` 的最大长度为 1000。

**示例 1：**

```
输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案。
```

**示例 2：**

```
输入: "cbbd"
输出: "bb"
```

#### 2.分析

- 法一：中心扩展法，这里要考虑两种情况，回文串的长度为奇数或者偶数情况。
- 法二：动态规划法，dp[j][i] 表示字符串从 j 到 i 是否是为回文串，即当 s[j] == s[i] 如果 dp[j+1][i-1] 也是回文串，那么字符串从 j 到 i 也是回文串，即 dp[j][i] 为真。
- 法三：把每个字符都当做回文串的结束

#### 3.代码

**法一**

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        if not s :
            return ""
        n = len(s)
        self.res = ''
        self.max_len = float('-inf')
        def func(i,j):
            while i>=0 and j<n and s[i]==s[j]:
                i -= 1
                j += 1
                if self.max_len < j-i+1-2:
                    self.res = s[i+1:j]
               	    self.max_len = j-i+1-2
        for i in range(n):
            func(i,i)
            func(i,i+1)
        return self.res     
```

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        if not s:
            return ''
        self.n = len(s)
        self.res = ''
        for i in range(self.n):
            self.func(i,i,s)
            self.func(i,i+1,s)
        return self.res
    def func(self, i, j, s):
        while i>=0 and j<self.n and s[i]==s[j]:
            i-=1
            j+=1
        if len(self.res) < j-i+1-2:
            self.res = s[i+1:j]
```

**法二**

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        if not s :
            return ""
        n = len(s)
        res = ''
        max_len = float('-inf')
        dp = [[0]*n for _ in range(n)]
        for j in range(n):
            for i in range(j+1):
                if s[i]==s[j] and(dp[i+1][j-1] or j-i<=2):
                    dp[i][j]=1
                if dp[i][j] and max_len < j-i+1:
                    max_len = j-i+1
                    res = s[i:j+1]
        return res
 
```

**法三**

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        if not s:
            return ""
        max_len = 1
        n = len(s)
        start = 0
        for i in range(1,n):
            even = s[i-max_len:i+1]
            odd = s[i - max_len-1:i+1]
            print(even,odd)
            if i - max_len - 1 >= 0 and odd == odd[::-1]:
                start = i - max_len - 1
                max_len += 2
            elif i - max_len >=0 and even == even[::-1]:
                start = i - max_len
                max_len += 1
                
        print(start,max_len)
        return s[start: start+max_len]

```

```python
class Solution:
      def longestPalindrome(self,s):
        n = len(s)
        maxl = 0
        start = 0
        for i in range(n):
            if i - maxl >= 1 and s[i-maxl-1: i+1] == s[i-maxl-1: i+1][::-1]:
                # start = i - maxl - 1
                maxl += 2
                continue
            if i - maxl >= 0 and s[i-maxl: i+1] == s[i-maxl: i+1][::-1]:
                start = i - maxl
                maxl += 1
        return s[start: start + maxl]

```

