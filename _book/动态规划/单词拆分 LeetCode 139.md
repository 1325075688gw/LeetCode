### [单词拆分](https://leetcode-cn.com/problems/word-break/)(LeetCode 139)

#### 1.题目

给定一个**非空**字符串 *s* 和一个包含**非空**单词列表的字典 *wordDict*，判定 *s* 是否可以被空格拆分为一个或多个在字典中出现的单词。

**说明：**

- 拆分时可以重复使用字典中的单词。
- 你可以假设字典中没有重复的单词。

**示例 1：**

```
输入: s = "leetcode", wordDict = ["leet", "code"]
输出: true
解释: 返回 true 因为 "leetcode" 可以被拆分成 "leet code"。
```

**示例 2：**

```
输入: s = "applepenapple", wordDict = ["apple", "pen"]
输出: true
解释: 返回 true 因为 "applepenapple" 可以被拆分成 "apple pen apple"。
     注意你可以重复使用字典中的单词。
```

**示例 3：**

```
输入: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
输出: false
```

#### 2.分析

- 动态规划
- 就像爬楼梯，一样，要爬到10楼，先看能不能爬到1楼，2楼等

#### 3.代码

**动态规划**

```python
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        
        if s =='' or len(wordDict) ==0:
            return False
        
        dp = [0]*(len(s)+1)
        dp[0] = 1
        
        max_stride = max([len(x) for x in wordDict])
        for i in range(1,len(s)+1):
            k = i-max_stride
            if k>0:
                for j in range(k,i):
                    if dp[j]==1 and s[j:i] in wordDict:
                        dp[i] = 1
            else:
                for j in range(0,i):
                    if dp[j]==1 and s[j:i] in wordDict:
                        dp[i] = 1
        return dp[-1] == 1
```

**动态规划2**

```python
    def wordBreak(self, s, wordDict):
        s_len = len(s)
        dp = [False]*(s_len+1)
        dp[0] = True
        
        # 因为单词长度最小是1，所以起点是1
        for i in range(1,s_len+1):
            for word in wordDict:
                if i>=len(word) and dp[i-len(word)] and word == s[i-len(word):i]:
                    dp[i] = True
        return dp[-1]
```

**在上一个动态规划上进行优化**

```python
class Solution:
    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: List[str]
        :rtype: bool
        """
        len_s = len(s)
        mem = [False]*(len_s+1)
        mem[0] = True
        tmpDict = dict((i,len(i)) for i in wordDict)
        for i in range(1, len_s + 1):
            for word in wordDict:
                if i >= tmpDict[word] and mem[i - tmpDict[word]] \
                	and word == s[i-tmpDict[word]:i]:
                    mem[i] = True
                    break

        return mem[-1]
```

**回溯**

```python
class Solution:
    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: List[str]
        :rtype: bool
        """
        return self._wordBreak(s, set(wordDict), 0)
        
    def _wordBreak(self, s, words, start):
        if start == len(s):
            return True

        for i in range(start + 1, len(s) + 1):
            sub = s[start:i]
            if sub in words and self._wordBreak(s, words, i):
                return True

        return False
```

