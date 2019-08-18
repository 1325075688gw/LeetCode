#### [2的幂](https://leetcode-cn.com/problems/power-of-two/)(LeetCode 231)

#### 1.题目

给定一个整数，编写一个函数来判断它是否是 2 的幂次方。

**示例 1:**

```
输入: 1
输出: true
解释: 20 = 1
```

**示例 2:**

```
输入: 16
输出: true
解释: 24 = 16
```

**示例 3:**

```
输入: 218
输出: false
```

#### 2.分析

从二进制上看，2的幂一定是这样的形式：整个二进制数上只有一位是1，其他位全是0；

如果有两个1，一定不是2的幂）

此时，n-1的二进制数一定会是当前位变为0，其他位全是1，这样n与n-1操作，就会是0；

#### 3.代码

```python
    def isPowerOfTwo(self, n: int) -> bool:
        if(n<=0):
            return False
        if((n&n-1)==0):
            return True
        return False
```



