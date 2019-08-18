## [分割回文串](https://leetcode-cn.com/problems/palindrome-partitioning/)(LeetCode 131)

#### 1.题目

给定一个字符串 *s*，将 *s* 分割成一些子串，使每个子串都是回文串。

返回 *s* 所有可能的分割方案。

**示例:**

```
输入: "aab"
输出:
[
  ["aa","b"],
  ["a","a","b"]
]
```

#### 2.分析

- 回溯法
- 一个字符一个字符累加，这儿是个关键技巧

#### 3.代码

##### 递归、回溯

```python
    def partition(self, s):
        X = []
        self.func(s,0,[],X)
        return X
    def func(self, s, index, x, X):
        if index == len(s):
            X.append(x[:])
        else:
            
            # 还有着而需要注意回溯思想，我们只需要单条线走通，其它的就交给回溯算法本身去工作
            # 一个字符一个字符累加，关键技巧
            for i in range(index+1,len(s)+1):
                if s[index:i] == s[index:i][::-1]:
                    x.append(s[index:i])
                    self.func(s,i,x,X)
                    x.pop()
                    
```

****













