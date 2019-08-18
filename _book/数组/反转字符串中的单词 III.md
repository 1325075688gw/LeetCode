## 反转字符串中的单词 III

#### 1.题目

给定一个字符串，你需要反转字符串中每个单词的字符顺序，同时仍保留空格和单词的初始顺序。

**示例 1:**

```
输入: "Let's take LeetCode contest"
输出: "s'teL ekat edoCteeL tsetnoc" 
```

**注意：**在字符串中，每个单词由单个空格分隔，并且字符串中不会有任何额外的空格。

#### 2.分析

#### 3.代码

##### 代码1

```python
    def reverseWords(self, s):
        if s == '':
            return ''
        s = s.split()
        res = []
        res = ' '.join(i[::-1] for i in s)
        # print(res)
        return res
```

##### 代码2

```python
   
    def reverseWords(self, s: str) -> str:
        print(s.split()[::-1])
        s = list(s)
        start = 0
        # self.func(s, 0 , len(s)-1)
        for i in range(len(s)-1):
            if s[i] == ' ':
                self.func(s, start, i-1)
                start = i+1
        self.func(s, start, len(s)-1)
        res = ''.join(s)
        # print(res)
        return res
    def func(self, s, b, e):
        # 需要逆置的子串的头尾序号
        # b:begin e:end
        while b < e:
            tmp = s[b]
            s[b] = s[e]
            s[e] = tmp
            b += 1
            e -= 1
            
```

