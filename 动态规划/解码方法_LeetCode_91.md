### [解码方法](https://leetcode-cn.com/problems/decode-ways/)(LeetCode_91)

#### 1.题目

一条包含字母 `A-Z` 的消息通过以下方式进行了编码：

```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```

给定一个只包含数字的**非空**字符串，请计算解码方法的总数。

**示例 1:**

```
输入: "12"
输出: 2
解释: 它可以解码为 "AB"（1 2）或者 "L"（12）。
```

**示例 2:**

```
输入: "226"
输出: 3
解释: 它可以解码为 "BZ" (2 26), "VF" (22 6), 或者 "BBF" (2 2 6) 。
```



#### 2.分析

**动态规划：**

1. dp【n】表示n个字符可编码数，
2. 如果s【n-1】!= '0' , 则dp 【n】= dp【n-1】
3. 如果s【n-2】,s【n-1】 组合成的数字是10~26，则dp【n】 = dp【n-1】+dp【n-2】

#### 3.代码



```python
    def numDecodings(self, s: str) -> int:        
    	if s == '' or s[0] == '0':
            return 0
        s_len = len(s)
        dp = [0] *(s_len+1)
        dp[0] = dp[1] = 1
        for i in range(2, s_len+1):
            if s[i-1] != '0':
                dp[i] += dp[i-1]
            if s[i-2] == '1' or (s[i-2] =='2'and s[i-1]<='6'):
                dp[i] += dp[i-2]
        return dp[s_len]
```



