## [格雷编码](https://leetcode-cn.com/problems/gray-code/)(LeetCode 89)

#### 1.题目

格雷编码是一个二进制数字系统，在该系统中，两个连续的数值仅有一个位数的差异。

给定一个代表编码总位数的非负整数 *n*，打印其格雷编码序列。格雷编码序列必须以 0 开头。

**示例 1:**

```
输入: 2
输出: [0,1,3,2]
解释:
00 - 0
01 - 1
11 - 3
10 - 2

对于给定的 n，其格雷编码序列并不唯一。
例如，[0,2,3,1] 也是一个有效的格雷编码序列。

00 - 0
10 - 2
11 - 3
01 - 1
```

**示例 2:**

```
输入: 0
输出: [0]
解释: 我们定义格雷编码序列必须以 0 开头。
     给定编码总位数为 n 的格雷编码序列，其长度为 2n。当 n = 0 时，长度为 20 = 1。
     因此，当 n = 0 时，其格雷编码序列为 [0]。
```

#### 2.分析

![img](D:\gitbook\LeetCode\格雷编码(LeetCode 89).assets\20180703120635594.png)

![img](D:\gitbook\LeetCode\格雷编码(LeetCode 89).assets\2018070312065295.png)

#### 3.代码

```python
    def grayCode(self, n: int) -> List[int]:
        res = []
        for i in range(2**n):
            res.append(i^(i>>1))
        # print(res)
        return res
```

