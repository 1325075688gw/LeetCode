#### [斐波那契数](https://leetcode-cn.com/problems/fibonacci-number/)(LeetCode_509)

#### 1.题目

**斐波那契数**，通常用 `F(n)` 表示，形成的序列称为**斐波那契数列**。该数列由 `0` 和 `1` 开始，后面的每一项数字都是前面两项数字的和。也就是：

```
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
```

给定 `N`，计算 `F(N)`。

**提示：**

- 0 ≤ `N` ≤ 30

#### 2.分析

#### 3.代码

```python
def func(n):
    if N<2:return N
    dp = [0] * (n+1)
    dp[1] = dp[2] = 1
    for i in range(3,n+1):
        dp[i] = dp[i-1]+dp[i-2]
    return dp[n]
```

