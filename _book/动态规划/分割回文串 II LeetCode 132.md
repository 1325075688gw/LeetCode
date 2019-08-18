### [分割回文串 II](https://leetcode-cn.com/problems/palindrome-partitioning-ii/)(LeetCode 132)

#### 1.题目

给定一个字符串 *s*，将 *s* 分割成一些子串，使每个子串都是回文串。

返回符合要求的最少分割次数。

**示例:**

```
输入: "aab"
输出: 1
解释: 进行一次分割就可将 s 分割成 ["aa","b"] 这样两个回文子串。
```

#### 2.分析

- 数组`nums[i]`表示前`i`字符串最小的分割次数，那么在遍历过程中需要知道`j`至`i`的字符串是否为回文串。


- 动态规划   f(i)=min(f(j)+1)  for j in range(i)

- 动态规划题目，好比数学数列题，由前面的结果推导后面的结果

- dp[i]表示前i个字母的最少分割次数,默认为i-1。
  当s[a:b]==s[a:b][ ::-1]时，dp[b]=dp[a]+1

- 一般动态规划元素个数都比数组元素个数多一

- 最前面一个元素一般为-1，因此dp的默认写法：

  - ```python
    # 加入s_len =3
    dp = [i for i in range(-1,s_len)]

    # 输出
    -1, 0 , 1, 2
    ```

  - ```python
    dp = [i for i in range(s_len+1)]
    dp[0] = -1                      
    # 输出

    -1, 0 ,0 ,0 
    ```

    ​

#### 3.代码

```python
    def minCut(self, s: str) -> int:
        if not s: return 0
        
        s_len = len(s)
        dp = [i for i in range(-1,s_len)]
        for i in range(1,s_len+1):
            for j in range(0,i):
                if s[j:i] == s[j:i][::-1]:
                    dp[i] = min(dp[j]+1, dp[i])
                    
        return dp[-1]
```



![1553930053874](D:\gitbook\LeetCode\分割回文串 II(LeetCode 132).assets\1553930053874.png)