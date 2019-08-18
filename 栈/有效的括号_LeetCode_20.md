### [有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)(LeetCode_20)

#### 1.题目

给定一个只包括 `'('`，`')'`，`'{'`，`'}'`，`'['`，`']'` 的字符串，判断字符串是否有效。

有效字符串需满足：

1. 左括号必须用相同类型的右括号闭合。
2. 左括号必须以正确的顺序闭合。

注意空字符串可被认为是有效字符串。

**示例 1:**

```
输入: "()"
输出: true
```

**示例 2:**

```
输入: "()[]{}"
输出: true
```

**示例 3:**

```
输入: "(]"
输出: false
```

**示例 4:**

```
输入: "([)]"
输出: false
```

**示例 5:**

```
输入: "{[]}"
输出: true
```

#### 2.分析

#### 3.代码

**清楚易懂**

```python
class Solution:
    def isValid(self, s: str) -> bool:
        # 没有括号,也叫做括号匹配
        if not s:return True
        stack = []
        if s[0] in ['}',']',')']:
            return False
        for i in s:
            if not stack:
                stack.append(i)
                continue
            tmp = stack[-1]
            if tmp == '{':
                if i != '}':
                    stack.append(i)
                else:
                    stack.pop()
            elif tmp == '[':
                if i != ']':
                    stack.append(i)
                else:
                    stack.pop()
            elif tmp == '(':
                if i != ')':
                    stack.append(i)
                else:
                    stack.pop()
        if not stack:
            return True
        else:
            return False
```



**优化**

```python
class Solution(object):
    def isValid(self, s):
        stack = []
        judge = {'()','[]','{}'}
        for i in s:
            if not stack: 
                stack.append(i)
            else:
                # stack[-1]+ i字符串拼接  
                if stack[-1]+ i in judge:
                    stack.pop()
                else:
                    stack.append(i)
                    
        return stack == []
```

