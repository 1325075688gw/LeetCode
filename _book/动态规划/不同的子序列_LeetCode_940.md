### [不同的子序列 II](https://leetcode-cn.com/problems/distinct-subsequences-ii/)(LeetCode_940_困难)

#### 1.题目

给定一个字符串 `S`，计算 `S` 的不同非空子序列的个数。

因为结果可能很大，所以**返回答案模** **10^9 + 7**.

**示例 1：**

```
输入："abc"
输出：7
解释：7 个不同的子序列分别是 "a", "b", "c", "ab", "ac", "bc", 以及 "abc"。
```

**示例 2：**

```
输入："aba"
输出：6
解释：6 个不同的子序列分别是 "a", "b", "ab", "ba", "aa" 以及 "aba"。
```

**示例 3：**

```
输入："aaa"
输出：3
解释：3 个不同的子序列分别是 "a", "aa" 以及 "aaa"。
```

**提示：**

1. `S` 只包含小写字母。
2. `1 <= S.length <= 2000`



#### 2.分析

```python
我们假设子序列可以为空，最后的结果减一就可以得到正确答案，dp[i]表示数组前i项构成的不同子序列个数，
初始值dp[0] ,前0个构成的子序列个数，‘’ == 1. ===>dp[0] =1

如果数列第i项没有在之前出现过，那么dp[i] = dp[i-1]*2+1

如果数列第i项在之前出现过，那么我们需要找到第i项对应的字符在前i-1个字符出现的最近位置。即0<j<i.因为前（j-1）项的末尾添加第j项对应的字符，和前（j-1）项的末尾添加第i项对应的字符。构成的子序列是一样的，我们如果不减去dp[j]，那么就会计算重复。所以dp[j-1]是重复的。此时dp[i]=dp[i-1]*2-dp[j-1]。

最后我们还要-1，因为要去除非空的子序列。
```





#### 3.代码

```python
    def distinctSubseqII(self, S: str) -> int:
        s_len = len(S)
        dp = [0] * (s_len+1)
        dp[0] = 1
        history = {}
        for i,k in enumerate(S, start = 1):
            print(i,k)
            tmp = history.get(S[i-1],None)
            if tmp is None:
                dp[i] = dp[i-1]*2
            else:
                dp[i] = 2*dp[i-1] - dp[tmp-1]
            history[S[i-1]] = i
        # print(dp)
        return dp[-1] -1
```





```python
# 用动态规划先求出包括空序列的所有子序列，再返回答案之前再减去空序列。
class Solution(object):
    def distinctSubseqII(self, S):
        dp = [1]
        last = {}
        for i, x in enumerate(S):
            dp.append(dp[-1] * 2)
            if x in last:
                dp[-1] -= dp[last[x]]
            last[x] = i

        return (dp[-1] - 1) % (10**9 + 7)
    
     def distinctSubseqII(self, S):
        s_len = len(S)
        dp = [1] * (s_len+1)
        history = {}
        for i,k in enumerate(S):
            dp[i+1] = dp[i]*2
            if k in history:
                dp[i+1] -= dp[history[k]]
            history[k] = i
            
        return (dp[-1] - 1) % (10**9 + 7)
```



```python
    实现上，我们需要建立一个26大小的数组以容纳不同字母结尾的字符串个数。每当我们遍历到一个新的字母时，
    此时我们只要将数组中所有结果加起来然后再加1即为以新的字母为结尾的字符串总数。最后我们只要将数组中的结果加起来即可。
    def distinctSubseqII(self, S: str) -> int:
        res = [0]*26
        for i in S:
            res[ord(i)-97] = sum(res) + 1
            
        return sum(res) % (10**9 + 7)
```

