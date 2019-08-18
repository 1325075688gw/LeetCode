### [反转字符串中的元音字母](https://leetcode-cn.com/problems/reverse-vowels-of-a-string/)(LeetCode_345)

#### 1.题目

编写一个函数，以字符串作为输入，反转该字符串中的元音字母。交换左右两边的元音字母

**示例 1:**

```
输入: "hello"
输出: "holle"
```

**示例 2:**

```
输入: "leetcode"
输出: "leotcede"
```

**说明:**
元音字母不包含字母"y"。

#### 2.分析

...

#### 3.代码

```python
class Solution:
    def reverseVowels(self, s: str) -> str:
        if not s:return ''
        left, right = 0, len(s)-1
        # print(right)
        s = list(s)
        tmp = ['a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U']
        while left<right:
            while left < right and s[right] not in tmp:
                right -= 1
            while left < right and s[left] not in tmp:
                left += 1
            s[left], s[right] = s[right], s[left]
            left += 1
            right -= 1
        return ''.join(s)
```

