### [编辑距离](https://leetcode-cn.com/problems/edit-distance/)

#### 1.题目

给定两个单词 word1 和 word2，计算出将 word1 转换成 word2 所使用的最少操作数 。

你可以对一个单词进行如下三种操作：

- 插入一个字符


- 删除一个字符
- 替换一个字符

**示例 1:**

```python
输入: word1 = "horse", word2 = "ros"
输出: 3
解释: 
horse -> rorse (将 'h' 替换为 'r')
rorse -> rose (删除 'r')
rose -> ros (删除 'e')
```

**示例 2:**

```python
输入: word1 = "intention", word2 = "execution"
输出: 5
解释: 
intention -> inention (删除 't')
inention -> enention (将 'i' 替换为 'e')
enention -> exention (将 'n' 替换为 'x')
exention -> exection (将 'n' 替换为 'c')
exection -> execution (插入 'u')
```



#### 2.分析

#### 3.代码

```python
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        len1 = len(word1)
        len2 = len(word2)
        
        dp = [[0]*(len2+1) for i in range(len1+1)]
        
        for i in range(1,len1+1):
            dp[i][0] = i
        for j in range(1,len2+1):
            dp[0][j] = j
        # 建立数组dp[][]来存储 以word1[i]为结尾的字符串 转换成 以word2[j]为结尾的字符串 所需的最小操作数
        # 1、替换 word1[i] 把 word1[i] 替换成 word2[j] 需要 dp[i-1][j-1]+1步
        # 2、删除 word1[i] 把 word1[i] 删除成 word1[i-1] 需要 dp[i][j-1]+1步
        # 3、删除 word2[j] 把 word2[j] 删除成 word2[j-1] 需要 dp[i-1][j]+1步(增加word1和删除word2一个效果)
        # print(dp)
        for i in range(1,len1+1):
            for j in range(1,len2+1):
                if word1[i-1]==word2[j-1]:
                    dp[i][j] = dp[i-1][j-1]
                else:
                    dp[i][j] = min(dp[i-1][j]+1,dp[i][j-1]+1,dp[i-1][j-1]+1)
        return dp[-1][-1]
    
        # 我们需要进行插入、删除和修改操作将A串变为B串，定义c0，c1，c2分别为三种操作的代价
        for i in range(1,len1+1):
            for j in range(1,len2+1):
                if word1[i-1]==word2[j-1]:
                    dp[i][j] = dp[i-1][j-1]
                else:
                    
                    dp[i][j] = min(dp[i-1][j]+c0,dp[i][j-1]+c1,dp[i-1][j-1]+c2)
        return dp[-1][-1]
```



