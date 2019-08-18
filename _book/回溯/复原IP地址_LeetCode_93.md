### [复原IP地址](https://leetcode-cn.com/problems/restore-ip-addresses/)

#### 1.题目

给定一个只包含数字的字符串，复原它并返回所有可能的 IP 地址格式。

**示例:**

```python
输入: "25525511135"

输出: ["255.255.11.135", "255.255.111.35"]

```



#### 2.分析



#### 3.代码



```python
    class Solution:
    def restoreIpAddresses(self, s: str) -> List[str]:
        self.res = []
        tmpList = []
        self.dfs(s, tmpList)
        return self.res

    #dfs遍历，s为待处理字段，tmp存储所有ip小段
    def dfs(self, s, tmpList):  
        if len(tmpList) == 4:   #递归出口，凑够4段
            if len(s) == 0:     #s没有剩余，说明找到一个合法ip，否则返回
                self.res.append('.'.join(tmpList))
            return      
        for i in range(1, 4):   #遍历取s的头，长度从1到3
            if i <= len(s):     #防止越界
                if int(s[:i]) > 255:    #数字超出范围
                    return
                elif i > 1 and s[0] == '0':    #除去0开头，且长度大于1情况
                    return
                self.dfs(s[i:], tmpList + [s[:i]])  #截断s，并将本次截取内容写入tmp
```





```python
class Solution:
    def restoreIpAddresses(self, s: str) -> List[str]:
        X = []
        x = []
        
        def func(s, X, x):
            if len(x) == 4:
                if len(s) == 0:
                    X.append('.'.join(x))
                    return 
                return
            
            for i in range(1,4):
                if i <= len(s):
                    if int(s[:i])>255:
                        return
                    elif i>1 and s[0] == '0':
                        return
                    func(s[i:], X, x+[s[:i]])
                    
        func(s, X, x)
        return X
```

