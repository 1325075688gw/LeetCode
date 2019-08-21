### [栅栏涂色](https://leetcode-cn.com/problems/paint-fence/)(LeetCode_276)

#### 1.题目

有 k 种颜色的涂料和一个包含 n 个栅栏柱的栅栏，每个栅栏柱可以用其中一种颜色进行上色。

你需要给所有栅栏柱上色，并且保证其中相邻的栅栏柱 最多连续两个 颜色相同。然后，返回所有有效涂色的方案数。

**注意:**
n 和 k 均为非负的整数。

**示例:**

```python
输入: n = 3，k = 2
输出: 6
解析: 用 c1 表示颜色 1，c2 表示颜色 2，所有可能的涂色方案有:

            柱 1    柱 2   柱 3     
 -----      -----  -----  -----       
   1         c1     c1     c2 
   2         c1     c2     c1 
   3         c1     c2     c2 
   4         c2     c1     c1  
   5         c2     c1     c2
   6         c2     c2     c1
```



#### 2.分析

        # 超过3根栏杆动态规划才有意义：
        # 如果超过3根栏杆,才有可能出现,
        # 1.第三根栏杆刷第二根栏杆颜色(这时候就需要考虑第二根栏杆是不是和第一根栏杆一样颜色) : dp[i] = dp[i-2]*(k-1)
        # 2.第三根栏杆不刷第二根栏杆颜色 ：dp[i] = dp[i-1]*(k-1)


#### 3.代码



```python
class Solution:
    def numWays(self, n: int, k: int) -> int:
        if n == 0:
            return 0
        if n == 1:
            return k
        if n == 2: # 如果只有2根栏杆,则可以刷 K*K种方法
            return k*k
        
        dp = [0]*n
        dp[0] = k
        dp[1] = k*k

        for i in range(2, n):
            dp[i] = dp[i-2]*(k-1) + dp[i-1]*(k-1)
        return dp[-1]
            
```

