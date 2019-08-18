#### [最长重复子数组](https://leetcode-cn.com/problems/maximum-length-of-repeated-subarray/)(LeetCode_718)

#### 1.题目

给两个整数数组 `A` 和 `B` ，返回两个数组中公共的、长度最长的子数组的长度。

**示例 1:**

```python
输入:
A: [1,2,3,2,1]
B: [3,2,1,4,7]
输出: 3
解释: 
长度最长的公共子数组是 [3, 2, 1]。
```

```C++
说明:

1 <= len(A), len(B) <= 1000
0 <= A[i], B[i] < 100
```

#### 2.分析

- 动态规划

  - “子数组”需要连续的一段，并不是“子序列”。

  - | A  \   B |  空  |  1   |  2   |  1   |
    | :------: | :--: | :--: | :--: | :--: |
    |    空    |  0   |  0   |  0   |  0   |
    |    1     |  0   |  1   |  0   |  1   |
    |    2     |  0   |  0   |  2   |  0   |
    |    2     |  0   |  0   |  1   |  0   |


  ```
  dp[i][j] 表示A【:i-1】和B【:j-1】的最长公共子串的长度

  初始化：
  	A 为空串时，无论B多少字符，公共连续子序列长度都为0 ：dp[0][j] = 0
  	B 为空串时，无论A多少字符，公共连续子序列长度都为0 : dp[i][0] = 0
  ```

  ​

#### 3.代码

```python
class Solution:
    def findLength(self, A: List[int], B: List[int]) -> int:
        s1_len = len(A)
        s2_len = len(B)
        max_len = 0
        # max_id = 0
        mat = [[0]*(s2_len+1) for _ in range(s1_len+1)]
        for i in range(1,s1_len+1):
            for j in range(1,s2_len+1):
                mat[i][j] = mat[i-1][j-1]+ 1 if A[i-1] == B[j-1] else 0
                if mat[i][j] > max_len:
                    max_len = mat[i][j]
                    # max_id = i
        # max_str = s1[max_id-max_len:max_id]
        return max_len
```



```python
class Solution:
    def findLength(self, A: List[int], B: List[int]) -> int:
        s1_len = len(A)
        s2_len = len(B)
        max_len = 0
        # max_id = 0
        mat = [[0]*(s2_len+1) for _ in range(s1_len+1)]
        for i in range(1,s1_len+1):
            for j in range(1,s2_len+1):
                mat[i][j] = mat[i-1][j-1]+1 if A[i-1] == B[j-1] else 0
                max_len = max(max_len, mat[i][j])
        return max_len
```

