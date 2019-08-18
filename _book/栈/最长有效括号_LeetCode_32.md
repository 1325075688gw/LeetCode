### [最长有效括号](https://leetcode-cn.com/problems/longest-valid-parentheses/)(LeetCode_32)

#### 1.题目

给定一个只包含 `'('` 和 `')'` 的字符串，找出最长的包含有效括号的子串的长度。

**示例 1:**

```
输入: "(()"
输出: 2
解释: 最长有效括号子串为 "()"
```

**示例 2:**

```
输入: ")()())"
输出: 4
解释: 最长有效括号子串为 "()()"
```

#### 2.分析



#### 3.代码

```python
class Solution(object):
    def longestValidParentheses(self, s):
        stack = []
        res = 0
        start = 0
        for i in range(len(s)):
            if not stack:
                if i == ')':
                    # 只有连续))))),既不入栈,同时还要不断更新start
                    start = i +1
                elif i == '(':
                    stack.append(i)
            else:
                if i == ')':
                    tmp = stack.pop()
                    if stack:
                        # res = max(res, i-stack[-1])
                   		res = max(res, i-tmp+1)
                    else:
                         res = max(res, i-start + 1)
                elif i == '(':
                    stack.append(i)
          return res
                    
         
```



```python
class Solution:
    def longestValidParentheses(self, s: str) -> int:
        if len(s) == 0:
            return 0
        stack = []
        max_len, start = 0, 0
        for i in range(len(s)):
            if s[i] == "(":
                stack.append(i)
            if s[i] == ")":
                if not stack:
                    start = i + 1
                # elif s[stack[-1]] == "(":
                else:
                    stack.pop(-1)
                    if not stack:
                        max_len = max(max_len, i-start+1)
                    else:
                        max_len = max(max_len, i-stack[-1])
        return max_len
```



**动态规划**

```python
class Solution(object):
    def longestValidParentheses(self, s):
        n = len(s)
        if n<=1:return 0
        
        dp = [0]*n
        for i in range(1,n):
            if s[i] == ')':
                # pre :若前面匹配好了,0()() ,再来一个),则pre指向0位置,若前面没有匹配好,((,则再来一个),则pre指向没匹配好的最右边一个,即第二个(
                pre = i-dp[i-1]-1
                # 如果是左括号，则更新匹配长度
                if s[pre]=='(' and pre>=0:
                    dp[i] = dp[i-1]+2
                    # 处理独立的括号对的情形 类似()()、()(())
                	if pre>0: # 处理只有一对()情况,不加判断,结果为4，当只有一对括号时，不需要向前扩展了
                        dp[i] += dp[pre-1]
        return max(dp)
 
```

