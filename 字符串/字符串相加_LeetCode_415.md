### [字符串相加](https://leetcode-cn.com/problems/add-strings/)(LeetCode_415)

#### 1.题目

给定两个字符串形式的非负整数 num1 和num2 ，计算它们的和。

**注意：**

- num1 和num2 的长度都小于 5100.
- num1 和num2 都只包含数字 0-9.
- num1 和num2 都不包含任何前导零。
- 你不能使用任何內建 BigInteger 库， 也不能直接将输入的字符串转换为整数形式。



#### 2.分析

**法一：转化为列表**

**法二：不转化为列表**



#### 3.代码



**法一**

```python
    def addStrings(self, num1: str, num2: str) -> str:
        res = ''
        tmp = 0
        num1 = list(num1)
        num2 = list(num2)
        while num1 or num2 or tmp:
            i = num1.pop() if num1 else 0
            j = num2.pop() if num2 else 0
            # s:商  y:余数
            s,y = divmod(int(i)+int(j)+tmp,10)
            res = str(y) + res
            tmp = s         
        return res
```



**法二**

```python
        res = ''
        tmp = 0
        num1_len = len(num1)
        num2_len = len(num2)
        while num1_len>0 or num2_len>0 or tmp:
            num1_len -= 1
            num2_len -= 1
            i = num1[num1_len] if num1_len>=0 else 0
            j = num2[num2_len] if num2_len>=0 else 0
            
            s,y = divmod(int(i)+int(j)+tmp, 10)
            res = str(y) + res
            tmp = s
        return res
```



