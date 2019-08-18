## [字符串相乘](https://leetcode-cn.com/problems/multiply-strings/)(LeetCode 43)

#### 1.题目

给定两个以字符串形式表示的非负整数 `num1` 和 `num2`，返回 `num1` 和 `num2` 的乘积，它们的乘积也表示为字符串形式。

**示例 1:**

```
输入: num1 = "2", num2 = "3"
输出: "6"
```

**示例 2:**

```
输入: num1 = "123", num2 = "456"
输出: "56088"
```

**说明：**

1. `num1` 和 `num2` 的长度小于110。
2. `num1` 和 `num2` 只包含数字 `0-9`。
3. `num1` 和 `num2` 均不以零开头，除非是数字 0 本身。
4. **不能使用任何标准库的大数类型（比如 BigInteger）**或**直接将输入转换为整数来处理**。

#### 2.分析

对于这个问题，如果你注意到下面的这个规律话就非常简单。

![img](http://wx2.sinaimg.cn/mw690/af2d2659ly1fy08bafbjnj20hz0fiq3x.jpg)

首先要说明的是 我们是按照从左向右的顺序存储的数字。我们注意到对于index:i和index:j相乘的话，结果在index:i+j和index:i+j+1上。



![image.png](字符串相乘 LeetCode 43.assets/171cad48cd0c14f565f2a0e5aa5ccb130e4562906ee10a84289f12e4460fe164-image.png)

#### 3.代码

##### 代码1

```python
    def multiply(self, num1: str, num2: str) -> str:
        num1_len = len(num1)
        num2_len = len(num2)
        res = [0] * (num1_len + num2_len)
        for i in range(num1_len-1,-1,-1):
            for j in range(num2_len-1,-1,-1):
                # 从右向左，所以res[i+j+1]我们可以获取得到
                tmp = int(num1[i]) * int(num2[j]) + int(res[i+j+1])
                res[i+j+1] = tmp%10
                res[i+j] = res[i+j] + tmp//10
        res = list(map(str, res))
        # print(res)
        for i in range(num1_len+num2_len):
            if res[i]!='0':
                return ''.join(res[i:])
        return '0'
```



```python
    def multiply(self, num1: str, num2: str) -> str:
        
        num1_len = len(num1)
        num2_len = len(num2)
        res = [0] *(num1_len+num2_len)
        
        for i in range(num1_len-1,-1,-1):
            for j in range(num2_len-1,-1,-1):
                tmp = int(num1[i]) * int(num2[j]) + res[i+j+1]
                res[i+j+1] = tmp % 10
                res[i+j] += tmp//10
        
        for i in range(num1_len+num2_len):
            if res[i] != 0:
                return ''.join(map(str,res[i:]))
        return '0'
```



##### 代码2（大神版）

```python
    def multiply(self, num1, num2):
        res = 0
        for i in range(1,len(num1)+1):
            for j in range(1, len(num2)+1):
                res += int(num1[-i]) * int(num2[-j]) *10**(i+j-2)
        return str(res)
```

