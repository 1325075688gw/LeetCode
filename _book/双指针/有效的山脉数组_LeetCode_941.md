### [有效的山脉数组](https://leetcode-cn.com/problems/valid-mountain-array/)(LeetCode_941)

#### 1.题目

给定一个整数数组 A，如果它是有效的山脉数组就返回 true，否则返回 false。

让我们回顾一下，如果 A 满足下述条件，那么它是一个山脉数组：

- A.length >= 3


- 在 0 < i < A.length - 1 条件下，存在 i 使得：
- A[0] < A[1] < ... A[i-1] < A[i]
- A[i] > A[i+1] > ... > A[B.length - 1]



**示例 1：**

```
输入：[2,1]
输出：false
```

**示例 2：**

```
输入：[3,5,5]
输出：false
```

**示例 3：**

```
输入：[0,3,2,1]
输出：true
```

#### 2.分析

双指针，从左到右寻找第一个山峰，从右到左寻找第一个山峰，看两个山峰是否重复，且不为边界。

#### 3.代码



```Python
class Solution:
    def validMountainArray(self, A: List[int]) -> bool:
        l, r = 0, len(A)-1
        r_copy = r
        while l<r and A[l]<A[l+1]:
            l += 1
        while l<r and A[r]<A[r-1]:
            r -= 1
        return l==r and r!=r_copy and l!=0
```





```java
class Solution {
    public boolean validMountainArray(int[] A) {
        int l=0, r=A.length-1;
        while (l<r && A[l]<A[l+1]) {
            l++;
        }
        if(l== r || l==0)
            return false;
        while (l<r && A[l]>A[l+1]) {
            l++;
        }
        // 只有正常退出才会  l== r
        return l == r;
    }
}
```

