### [二进制求和](https://leetcode-cn.com/problems/add-binary/)

#### 1.题目

给定两个二进制字符串，返回他们的和（用二进制表示）。

输入为**非空**字符串且只包含数字 `1` 和 `0`。

**示例 1:**

```
输入: a = "11", b = "1"
输出: "100"
```

**示例 2:**

```
输入: a = "1010", b = "1011"
输出: "10101"
```



#### 2.分析

**法一**：将2进制数转为10进制计算，然后转化为二进制

**法二**：模仿10进制，字符串相加，这儿我们同样可以将直接利用字符串，也可以将字符串先转化为列表。



#### 3.代码

**法一**

```python
class Solution:
    def addBinary(self, a: str, b: str) -> str:
        a = int(a, 2)
        b = int(b, 2)
        return bin(a+b)[2:]
    
```



**法二**

```python
    def addBinary(self, a: str, b: str) -> str:
        res = ''
        tmp = 0
        a_len = len(a)
        b_len = len(b)
        while a_len>0 or b_len>0 or tmp:
            a_len -= 1
            b_len -= 1
            i = a[a_len] if a_len>=0 else 0
            j = b[b_len] if b_len>=0 else 0
            
            s,y = divmod(int(i)+int(j)+tmp, 2)
            res = str(y) + res
            tmp = s
        return res
```

